---
layout: post
title: Android Studio 2.3.2 에서 Let's Encrypt 인증서 SSLHandShakeException 발생할때
categories: [dev, android]
tags: [dev, android, ssl, letsencrypt]
description: android studio에서 unit 테스트 중에 let's encrypt 인증서에서 SSLHandShakeException 해결
---

안드로이드 스튜디오에서 Let's Encrypt 인증서를 사용한 사이트에 접근시 SSLHandShakeException이 발생했다.

원인은 Let's Encrypt root인증서가 java의 keystore에 없기때문이라 인증서를 추가해 주면 문제 해결!

참조한 사이트는 [이곳](https://www.lesstif.com/pages/viewpage.action?pageId=12451848#Java의keystore에SSL/TLSServer인증서를import하는방법-let'sencrypt인증서) 이다.


## 고대로 따라하면 겁나게 잘 되야하는데 
그대로 SSLHandShakeException이 발생한다.

원인은 android studio 프로젝트 속성의 SDK Location을 보면 임베디드 jdk를 사용하도록 되어있다.
![Embedded JDK](/assets/images/android_studio_embedded_jdk.png)
> /Applications/Android Studio.app/Contents/jre/jdk/Contents/Home

방법은 저 경로의 JDK에다 다시 인증서를 추가하던가 임베디드 jdk를 사용 안하던가.