---
layout: post
title: Qt Creator 에 yocto poky sdk 빌드 설정하기
categories: [linux, dev]
tags: [linux, dev, qtcreator, qt, yocto, poky]
description: Qt Creator에서 poky sdk 빌드 설정하기
---
## 회사에서 개발하는 시스템 개발 설정 정리

# 준비물
1. poky sdk
2. Qt Creator 설치

# poky sdk 설치
1. 관리자 권한으로 기본 경로에 설정
![poky setup](/assets/images/poky_setup.png)

# Qt Creator 설정
## Device 추가
1. menu - options - devices
![poky setup](/assets/images/options_devices.png)
1. Add - Generic Linux Device
1. 타겟 디바이스 정보 입력
    1. 디바이스 이름
    1. 디바이스 IP address
    1. 디바이스 계정
    1. 인증 방법
![poky setup](/assets/images/device_config.png)

## Compiler 추가
1. menu options - Build & Run - Compilers
1. add - gcc - c++
1. poky sysroot 의 x86용 arm cross compiler 선택
 > /opt/poky/1.7.1/sysroots/x86_64-pokysdk-linux/usr/bin/arm-poky-linux-gnueabi/arm-poky-linux-gnueabi-gcc
![compiler](/assets/images/qtcreator_add_compilers.png)
## 디버거 추가
1. menu options - Build & Run - Debuggers
1. Add
    1. 디버거 이름
    1. 디버거 경로 - poky gdb 사용
    > /opt/poky/1.7.1/sysroots/x86_64-pokysdk-linux/usr/bin/arm-poky-linux-gnueabi/arm-poky-linux-gnueabi-gdb
    ![debugger](/assets/images/qtcreator_add_debugger.png)

## Qt5 추가
1. menu options - Build & Run - Qt Versions
1. Add - poky qmake 경로 설정
    > /opt/poky/1.7.1/sysroots/x86_64-pokysdk-linux/usr/bin/qt5/qmake
    ![qt5](/assets/images/qtcreator_add_qt5.png)


## Kits 추가
1. menu - options - Build & Run - Kits
1. Add
1. 설정
    1. Kit 이름
    1. File system name - 비워둠
    1. 디바이스 타입 - Generic Linux Device
    1. 장치 선택 - 추가한 디바이스 선택
    1. poky sdk의 sysroot 경로 선택 - 내 경우는 poky 기본 경로 
    1. compiler
        1. C: no compiler
        1. C++: 위에서 설정한 poky 용 gcc 선택
    1. Environment : 기본값
    1. 위에서 설정한 poky용 디버거 선택
    1. 위에서 설정한 Qt 선택
    1. 이하 기본값 사용
    ![kit](/assets/images/qtcreator_add_kits.png)
