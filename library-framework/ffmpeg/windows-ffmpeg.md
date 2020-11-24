# Windows에서 FFmpeg 빌드하기

## Getting Prerequisite

MinGW, Msys, Git, Yasm

* install [**`MinGW-w64-build`**](http://mingw-w64.org/doku.php/download/mingw-build) 
  * Mingw-w64가 Mingw "mainline"보다 최신 버전으로 관리가 되고 있고, library compatibility가 좋아 ffmpeg 공홈에서 MinGW-w64를 선호한다고 함
  * 설치 시 목적 Architecture 선택 및 Threads를 **`win32`**로 변경
    * i686 : 32bit binary / x86\_64 : 32bit memory map을 가지는 64bit binary
    * posix 선택 시, C++11/C11 multithreading feature 사용 가능, **`libwinpthreads.dll`** 필요
    * win32 선택 시, 향후 C++11/C11 multithreading feature\(std::thread\)에 대한 구현이 불확실하여, 해당 기능을 이용한 코드 컴파일 시 문제가 있을 수 있음 \(To Do: 확인 필요\)
    * 우선 빌드된 ffmpeg을 linking하여 구현할 프로젝트를 MinGW에서 컴파일할 계획이 없으므로, 배포하기 편리한 win32 thread로 선택
* install **`MSYS`**
  * 

