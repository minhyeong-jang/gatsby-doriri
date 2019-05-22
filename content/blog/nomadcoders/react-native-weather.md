---
title: React Native로 날씨앱 만들기
date: 2019-05-22 16:05:09
category: nomadcoders
---

> Github : [react-native-weather](https://github.com/minhyeong-jang/react-native-weather)  
> Lecture : [nomadcoders](https://academy.nomadcoders.co/p/fucking-react-native-apps?ref=map)

## 1. React Native & Expo 특징

#### React Native

- div, span 등 웹 태그 사용이 불가능하다.
- CSS 사용이 가능하다. ( 100% 동일하지는 않으며, Flexbox 사용이 가능 )
- 리액트 네이티브가 지원하는 태그는 빌드 시 Android / iOS에 맞게 변환해준다.
- 오류를 엄격하게 체크한다.
- CSS shorthand property가 작동하지 않는다.

#### Expo

- Android, IOS 테스트가 가능하다.
- 모바일에서 코드를 스캔하여 앱을 다운받고 실시간으로 수정사항 반영이 가능하다. ( Live Reload )
- 배포 시 앱을 업데이트 하는 것이 아닌 서버에 코드를 업데이트하는 방식이다.
  - 따라서 앱 스토어의 승인 절차가 필요없고, 유저는 서버에서 코드를 다운받는다.

> Online Coding : snack.expo.io

### 1.1 설치

[Expo Learn](https://expo.io/learn)

```bash
npm install expo-cli --global
expo init react-native-weather

? Choose a template: expo-template-blank
? Choose which workflow to use: managed
✔ Please enter a few initial configuration values.
  Read more: https://docs.expo.io/versions/latest/workflow/configuration · 100% completed
? Yarn v1.13.0 found. Use Yarn to install dependencies? Yes
```

### 1.2 Expo 회원가입 및 로그인

[expo 회원가입](https://expo.io/signup)

```bash
expo login
? Username/Email Address:
? Password: [hidden]
```

### 1.2 실행

```bash
cd react-native-weather
yarn start
```

Expo 로컬 홈페이지가 열리면 Run simulator 또는 모바일에서 Expo 앱을 설치하여 QR코드를 인식한다.

> Xcode 업데이트 필수

### 1.3 설정

- Live Reload : 화면 전체 새로고침
- Hot Reloading : 변경 사항 새로고침
- Debug Remote JS : 인터넷 브라우저에서 디버깅

### 학습 한 모듈

```js
import { LinearGradient } from 'expo'
import { MaterialCommunityIcons } from '@expo/vector-icons'
```

### 수강 후기

처음 React Native를 공부했을 때는 React 경험이 없어서 어렵고 이해 안되는 부분이 많았다.  
지금이야 React 개발자가 되어 공부해보니 생각보다 쉽고 재미있었다.  
다만, 기초적인 부분이기도하고 사용했던 LinearGradient, Vector-Icons 모듈처럼 여러 모듈의 존재여부를 모르는 부분이 React Native를 개발하면서 난관일 것이라고 생각한다.
