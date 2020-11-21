# CMake

* 공홈 : [https://cmake.org/](https://cmake.org/)
* 참고 사이트
  * [https://cgold.readthedocs.io/en/latest/](https://cgold.readthedocs.io/en/latest/)
  * [https://gist.github.com/luncliff/6e2d4eb7ca29a0afd5b592f72b80cb5c\#%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%9D%98-%EA%B5%AC%EC%84%B1](https://gist.github.com/luncliff/6e2d4eb7ca29a0afd5b592f72b80cb5c#%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%9D%98-%EA%B5%AC%EC%84%B1)



## Template

### directory 구조

```cpp
[project]
|- CMakeLists.txt
|- [include]
|- [external]
|   |- [bin]      
|   |- [include]
|   |- [lib]
|- [lib]
|   |- CMakeLists.txt
|   |- [include]
|   |- [src]   
|- [src]
|   |- CMakeLists.txt
|   |- [src]
|- [tests]
    |- CMakeLists.txt
    |- [src]
```

### template

#### \[project\]/CMakeLists.txt

```text
# project setting
cmake_minimum_required(version 3.10)

project([project_name] VERSION "0.0.0" LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(${PROJECT_NAME}_DIR ${CMAKE_CURRENT_SOURCE_DIR})

# build option
set(CMAKE_BUILD_TYPE Debug) # <Debug|Release>
if (MSVC)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /O2 /MD") #[/MD|/MT] 주의
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /Zi /Od /MDd")
else()
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -g0 -O3")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Wall -Wextra -Werror -g3 -ggdb -O0")
endif()
set(CMAKE_VERBOSE_MAKEFILE false) # <true|false>

# configure
include(${PROEJCT_NAME}_DIR/configure/xxx.cmake) # devide cmake
include(${PROEJCT_NAME}_DIR/configure/yyy.cmake)

# common include directory (every target in this project share this include path) 
include_directories(${PROJECT_NAME}_DIR/include)
include_directories(${PROEJCT_NAME}_DIR/external/include)

# common link directory (evert target in this project share this link path too)
link_directories(${PROEJCT_NAME}_DIR/external/bin)
link_directories(${PROJECT_NAME}_DIR/external/lib)

# output directory setting
set(CMAKE_INSTALL_PREFIX ${TMF_PROJECT_DIR}/dist/${CMAKE_BUILD_TYPE})
foreach(OUTPUTCONFIG ${CMAKE_CONFIGURATION_TYPES})
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_INSTALL_PREFIX}/bin)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_INSTALL_PREFIX}/lib) # dynamic
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_INSTALL_PREFIX}/lib) # static
endforeach()

# add libary
add_subdirectory(lib)

# add executable
add_subdirectory(src)

# add unit test
add_subdirectory(tests)
```

#### \[project\]/lib/CMakeLists.txt

```text
add_library(${PROJECT_NAME} SHARED project.cpp)

# private header inlcude path
target_include_directories(${PROJECT_NAME} PUBLIC ${PROEJCT_NAME_DIR}/lib/include)

# Symbol export
if(WIN32)
    set_target_properties(${PROEJCT_NAME}
        PROPERTIES
        WINDOWS_EXPORT_ALL_SYMBOLS true
    )
endif()

# cmake splitting
include(aaa/aaa.cmake)
include(bbb/bbb.cmake)

# add target source
target_source(${PROJECT_NAME} PUBLIC
    lib.cpp
    ...
)

# install target
install(TARGETS ${PROJECT_NAME}
        CONFIGURATION ${CMAKE_BUILD_TYPE}
        RUNTIME DESTINATION bin
        LIBRART DESTINATION lib
        ARCHIVE DESTINATION lib
)

# install public header
install(DIRECTORY     ${PROJECT_NAME_DIR}/include
        CONFIGURATION ${CMAKE_BUILD_TYPE}
        DESTINATION   ${CMAKE_INSTALL_PREFIX}
)
```

