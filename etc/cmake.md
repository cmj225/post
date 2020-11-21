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

## Template

### \[project\]/CMakeLists.txt

```text
# project setting
cmake_minimum_required(version 3.10)

project([project_name] VERSION "0.0.0" LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(PROJECT_DIR ${CMAKE_CURRENT_SOURCE_DIR})

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
include_directories(${PROJECT_DIR}/include)
include_directories(${PROEJCT_DIR|/external/include)

# common link directory (evert target in this project share this link path too)
link_directories(${PROEJCT_DIR|/external/bin)
link_directories(${PROJECT_DIR}/external/lib)

# output directory setting
set(CMAKE_INSTALL_PREFIX ${PROJECT_DIR}/dist/${CMAKE_BUILD_TYPE})
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

#### 

### \[project\]/configure/package.cmake

```text
# pkg-config
INCLUDE(FindPkgConfig REQUIRED)

# find some REQUIRED package

## 1. ffmpeg
pkg_config_modules(AVFORMAT  libavformat   REQUIRED)
pkg_config_modules(AVCODEC   libavcodec    REQUIRED)
pkg_config_modules(AVUTIL    libavutil     REQUIRED)
pkg_config_modules(SWSCALE   libswscale    REQUIRED)
pkg_config_modules(SWREAMPLE libswresample REQUIRED)
pkg_config_modules(AVFILTER  libavfilter   REQUIRED)
set(FFMPEG_FOUND "1")
set(FFMPEG_INCLUDE_DIRS ${AVFORMAT_INCLUDE_DIRS) # other ffmpeg lib share this path
set(FFMPEG_LIBRARY_DIRS ${AVFORMAT_LIBRARY_DIRS}
                        ${AVFORMAT_LIBRARY_DIRS}/../bin
)
set(FFMPEG_LIBRARIES avformat avcodec avutil swscale swresample avfilter) # avdevice

## 2. SDL2
pkg_check_modules(SDL2 sdl2 REQUIRED)

## Googletest
include(${PRJECT_DIR}/configure/googletest.cmake
```

### \[project\]/configure/googletest.cmake

```text
# Download and unpack googletest at configure time
configure_file(${PROJECT_DIR}/configure/googletest.in.txt googletest-download/CMakeLists.txt)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
if(result)
  message(FATAL_ERROR "CMake step for googletest failed: ${result}")
endif()
execute_process(COMMAND ${CMAKE_COMMAND} --build .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
if(result)
  message(FATAL_ERROR "Build step for googletest failed: ${result}")
endif()

# Prevent overriding the parent project's compiler/linker
# settings on Windows
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# Add googletest directly to our build. This defines
# the gtest and gtest_main targets.
add_subdirectory(${CMAKE_CURRENT_BINARY_DIR}/googletest-src
                 ${CMAKE_CURRENT_BINARY_DIR}/googletest-build
                 EXCLUDE_FROM_ALL)

# The gtest/gtest_main targets carry header search path
# dependencies automatically when using CMake 2.8.11 or
# later. Otherwise we have to add them here ourselves.
if (CMAKE_VERSION VERSION_LESS 2.8.11)
  include_directories("${gtest_SOURCE_DIR}/include")
endif()
```

### \[project\]/configure/googletest.in.txt

```text
cmake_minimum_required(VERSION 3.10)

project(googletest-download NONE)

include(ExternalProject)
ExternalProject_Add(googletest
  GIT_REPOSITORY    https://github.com/google/googletest.git
  GIT_TAG           master
  SOURCE_DIR        "${CMAKE_CURRENT_BINARY_DIR}/googletest-src"
  BINARY_DIR        "${CMAKE_CURRENT_BINARY_DIR}/googletest-build"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     ""
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
)
```

### \[project\]/configure/project.cmake

```text
# get info and make header
set(VERSION ${PROJECT_VERSION})
if (UNIX)    
    set(TARGET_OS "LINUX")
elseif(WIN32)
    set(TARGET_OS "WINDOWS")
    set(CMAKE_SHARED_LINKER_FLAGS "/SAFESEH:NO") # in Windows
endif()

set(BUILD_ARCH ${CMAKE_SYSTEM_PROCESSOR})
set(BUILD_TYPE ${CMAKE_BUILD_TYPE})
configure_file(${TMF_PROJECT_DIR}/configure/build_info.h.in.txt
               ${TMF_PROJECT_DIR}/include/build_info.h
)
```

### \[project\]/configure/build\_info.in.h

```text
#ifndef BUILD_INFO_H
#define BUILD_INFO_H

#define VERSION     "@VERSION@"
#define TARGET_OS   "@TARGET_OS@"
#define BUILD_ARCH  "@BUILD_ARCH@"
#define BUILD_TYPE  "@BUILD_TYPE@"

// pkg-config
#define PKG_CONFIG_FOUND "@PKG_CONFIG_FOUND@"
#define PKG_CONFIG_VERSION "@PKG_CONFIG_VERSION@"

// ffmpeg
#define FFMPEG_FOUND "@FFMPEG_FOUND@"
#define AVFORMAT_VERSION "@AVFORMAT_VERSION@"
#define AVCODEC_VERSION "@AVCODEC_VERSION@"
#define AVUTIL_VERSION "@AVCODEC_VERSION@"
#define AVDEVICE_VERSION "@AVDEVICE_VERSION@"
#define SWSCALE_VERSION "@SWSCALE_VERSION@"
#define SWRESAMPLE_VERSION "@SWRESAMPLE_VERSION@"
#define AVFILTER_VERSION "@AVFILTER_VERSION@"
#define FFMPEG_INCLUDE_DIRS "@FFMPEG_INCLUDE_DIRS@"
#define FFMPEG_LIBRARY_DIRS "@FFMPEG_LIBRARY_DIRS@"

// sdl2
#define SDL2_FOUND "@SDL2_FOUND@"
#define SDL2_VERSION "@SDL2_VERSION@"
#define SDL2_INCLUDE_DIRS "@SDL2_INCLUDE_DIRS@"
#define SDL2_LIBRARY_DIRS "@SDL2_LIBRARY_DIRS@"

// test
#define CMAKE_COMMAND "@CMAKE_COMMAND@"
#define CMAKE_GENERATOR "@CMAKE_GENERATOR@"
#define CMAKE_CURRENT_BINARY_DIR "@CMAKE_CURRENT_BINARY_DIR@"
```

### 

### \[project\]/lib/CMakeLists.txt

```text
add_library(${PROJECT_NAME} SHARED project.cpp)

# private header inlcude path
target_include_directories(${PROJECT_NAME} PUBLIC ${PROEJCT_NAME_DIR}/lib/include)

# private link path
target_link_directories( ... )

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
install(DIRECTORY     ${PROJECT_DIR}/include
        CONFIGURATION ${CMAKE_BUILD_TYPE}
        DESTINATION   ${CMAKE_INSTALL_PREFIX}
)
```

