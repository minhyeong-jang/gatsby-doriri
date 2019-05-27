---
title: Sourcemap 이란?
date: 2019-05-24 10:05:14
category: development
---

## 1. Sourcemap 이란?

많은 개발 환경은 Webpack 등으로 빌드 과정을 거치고있다. 만일 빌드 후 취합되거나 변환 된 CSS, JavaScript 파일들이 오류가 발생한다면, 개발자 도구에서는 빌드 된 파일에서 오류를 출력하고 있을 것이다. 하지만 우리가 원하는 것은 **빌드 전 오류난 파일 및 라인**을 알고싶은 것이다.

예를 들면, SCSS에 오류가 있고 Webpack으로 빌드를 진행하면 웹페이지에서 오류를 알려주는 부분은 빌드가 완료된 CSS를 출력한다. JavaScript도 마찬가지로 오류가 나면 취합하고 minify된 JS를 출력하고있다.

이럴때 Soucemap을 설정하면, **코드상의 위치를 기억하고 알려주기 때문에 빌드 전 어떤 파일, 라인에서 오류가 났는지 확인할 수 있다.**

## 2. 설정

### 2.1 Webpack

Dev 환경에서만 작동하도록 설정하였다.

```json
{
  "devtool": env.mode === "development" ? "source-map" : ""
}
```

### 2.2 Typescript

```json
{
  "compilerOptions": {
    "sourceMap": true
  }
}
```
