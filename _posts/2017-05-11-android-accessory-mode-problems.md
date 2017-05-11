---
layout: post
title: Android에서 accessory mode 사용시 문제점 정리
categories: [dev, android, accessory, usb]
tags: [dev, android, accessory]
description: android 에서 accessory mode 사용할때 격은 문제점 정리
---

# Android accessory mode 란?
https://source.android.com/devices/accessories/protocol
https://developer.android.com/guide/topics/connectivity/usb/accessory.html

USB host 모드를 지원 하지 않는 안드로이드 장치에서도 외부 usb 장치를 지원하기 위한 모드
더 자세한건 구글링 참조... ㅋ

# 발생한 문제점

> ## USB 연결을 끊었는데도 detach가 안됨!!

문서상에는 accessory 장치와 통신이 끝났으면 받아온 파일 디스크립터를 닫으면 된다고 되어있고 accessory 장치를 연결 해제 하면 ACTION_USB_ACCESSORY_DETACHED 가 브로드캐스트 된다고 되어있다.

파일 디스크립터를 닫은 경우에는 어차피 accessory 모드가 해제된 것이 아니므로 다시 accessory 를 열면 문제 없이 사용이 가능하다.

문제는 USB 연결을 해제했는데 ACTION_USB_ACCESSORY_DETACHED가 발생을 안한다. file descriptor는 예외가 발생해서 닫았지만 ACTION_USB_ACCESSORY_DETACHED는 몇분을 기다려도 발생을 하지 않는다.

> ## 상황이 발생하면 오직 해결책은 app을 종료하는것뿐이다. OMG

디바이스에서는 accessory 모드가 해제 되었더라도 app에서 무언가 자원 해제가 안되는 느낌.
안드로이드 버전 6.0 이상에서는 정상 동작하는걸 확인했으나 롤리팝 이하에서는 회사에서 보유한 갤럭시탭 노트 10.1 2012, 2014, 갤럭시탭 S2 전부 동일증상.

마쉬멜로우인 레노보 탭에서는 정상동작, 안드로이드 6.0 사용하시는 회사분 삼성폰 빌려다 테스트 해 본 결과도 레노보보단 덜 매끄럽지만 정상적으로 ACTION_USB_ACCESSORY_DETACHED가 발생하는것 확인.

# 다른 사람들의 경우에는?
대부분의 경우 accessory 사용하다가 usb 연결을 끊으면 fd 읽거나 쓸때 예외 발생하고 app을 종료하는 시나리오로 추정된다. github등에서 소스 뒤져보아도 예외 발생하는순간 자원 정리하고 앱 종료하도록 동작한다.

> ## 하지만 우리 앱은 종료되면 안되는데???

# 해결책
* 6.0 이상 기기를 사용한다 - 간단함.
* 5.0 이하에서는 accessory 관련 서비스를 레이어를 분리해서 독립적인 앱으로 만들고 aidl이나 소켓으로 통신, usb연결되면 실행되고 해제되면 종료되게 만들어야됨 - 이건 정말 고객사에서 5.0이하에서 지원되게 해달라고 하기전엔 pass