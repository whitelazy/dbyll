---
layout: post
title: 안드로이드 스튜디오에서 로컬 유닛테스팅 수행시에 리소스 파일 사용 방법
categories: [general, dev, android, java, junit]
tags: [dev, android, java, junit]
description: 안드로이드 스튜디오에서 로컬 유닛테스팅 수행시에 리소스 파일 접근하는 방법 기술
---

안드로이드 스튜디오에서 로컬 유닛 테스팅 수행시 자바 리소스에 접근이 안되서 해결방법 찾던중 발견
진즉에 찾아놓고 몇번 헤매다가 다시 적용해서 해결 했다 ... 안될리가 없지 ㅠㅠ

[Android Studio unit testing: read data (input) file](http://stackoverflow.com/a/29488904/7830231)

1. src/test/res 디렉토리 생성
2. 모듈의 build.gradle에 아래 스크립트 추가

```java

android{
   ...
}

task copyResDirectoryToClasses(type: Copy){
    from "${projectDir}/src/test/res"
    into "${buildDir}/intermediates/classes/test/debug/res"
}

// 내 경우는 app 모듈이 아닌 다른 library 모듈에서 수행해서 assembleDebug가 안되더라 build 태스크로 대체
assembleDebug.dependsOn(copyResDirectoryToClasses)

```

3. 코드에서 해당 리소스 읽어올때는 Class.getResource대신 Class.getClassLoader().getResource() 또는 Class.getClassLoader().getResourceAsStream() 사용

```java

ClassLoader classLoader = obj.getClass().getClassLoader();
    URL resource = classLoader.getResource(fileName);
    
```
