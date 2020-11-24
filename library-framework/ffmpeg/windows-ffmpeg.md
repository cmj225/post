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
  * MSYS2, Cygwin은 사용 시 런타임에 별도의 추가 dll을 필요로 함
    * cygwin.dll, msys-2.0.dll을 필요로 하므로 MSYS를 이용
  * \*\*\*\*[**download**](https://sourceforge.net/projects/mingw/files/MSYS/Base/msys-core/msys-1.0.11/MSYS-1.0.11.exe/download?use_mirror=jaist)\*\*\*\*
  * msys 내부에 /mingw directory에 etc/fstab에 기록된 directory를 mount
    * /가 msys.bat이 있는 위치\(c:/msys/1.0\)로 파일시스템이 분리됨
    * msys 설치과정에서 mingw가 설치된 위치를 잡아주거나, 혹은 설치 후 mingw 위치로 위에서 설치한 mingw를 복사
  * 편의를 위해 [~~**`MSYS developer kit`**~~](https://sourceforge.net/projects/mingw/files/Other/Unsupported/MSYS/msysDTK/msysDTK-1.0.1/msysDTK-1.0.1.exe/download?use_mirror=jaist) , [**`coreutil-bin, coreutil-dev`**](http://gnuwin32.sourceforge.net/packages/coreutils.htm)도 설치

{% hint style="info" %}
제일 편한 방법은 mingw-get을 이용해 mingw 및 개발자 툴킷들이 내장된 msys를 다운받는 것으로 보임

다만, installer에 mingw64\(x86\_64bit gcc\)는 없는 것으로 보여, 이 부분만 따로 설치해서 마운트해주면 될 것 같음
{% endhint %}

* \*\*\*\*[**`Git for Windows`**](https://gitforwindows.org/) 설치
* **`yasm`** 설치
* [**`pkg-config와 glib, gettext-runtime`**](https://download.gnome.org/binaries/win32) 설치
* 위에서 받은 것들에 대한 환경변수 Path setting

## Build

* **`git clone https://git.ffmpeg.org/ffmpeg.git`**
* **`git checkout -t origin/release/4.1`**
* **`./configure`** 
* **`make`**
* **`make install`**

## External Library

* sdl2
  * --enable-sdl2
  * .pc path만 잘 맞춰주면 정상적으로 빌드됨
* openh264
  * --enable-openh264
  * 빌드 시 x86\_64의 경우, x86\_64-w64-mingw32-gcc-ar.exe를 복사하여 x86\_64-w64-mingw32-ar.exe로 바꿔주어야

## issue

* sed
  * 해당 tool을 설치하지 않을 경우, avfilter 등 일부 필터를 빌드하기 위한 스크립트가 정상동작하지 않, 빌드된 dll에서 sound 재생등에 문제가 발생
* make 실행 시, crlf/lf 충돌로 문제가 발생하는 상황이 있을 수 있음
  * git config --global core.autocrlf false

## Reference

* \*\*\*\*[**FFmpeg/CompilationGuide**](https://trac.ffmpeg.org/wiki/CompilationGuide)\*\*\*\*
* \*\*\*\*[**FFmpeg/CompilationGuide/MinGW**](https://trac.ffmpeg.org/wiki/CompilationGuide/MinGW)\*\*\*\*
* \*\*\*\*[**MinGW&MSYS**](http://www.mingw.org/wiki/msys)\*\*\*\*

