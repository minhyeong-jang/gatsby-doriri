---
title: Parcel 30분 마스터하기
date: 2019-5-16 17:27:13
category: 'nomadcoders'
---

> Github : [parcel-experiments](https://github.com/minhyeong-jang/parcel-experiments)  
> Reference : [nomadcoders](https://academy.nomadcoders.co/p/learn-parcel)

### Feature

- React
- ES6 with Babel
- PostCSS ( SCSS, CSS Modules )
- Typography.js
- Build for production

## 1. Parcel 이란?

최근 빠르게 성장중인 번들러다. 빠른 빌드 속도를 자랑하며, 설정 파일 없이 사용이 가능하다.  
Webpack을 사용하면 관리해야하는 플러그인이 늘어나고 설정 파일의 내용이 많아진다.  
Parcel은 zero configuration을 지향하고, 플러그인을 사용하지 않아도 된다.  
따라서 새로운 개발자가 투입되었을 때 학습 시간이 없다.

다음은 빌드 속도에 관한 parcel 자료이다. (참고 : [Parcel Github](https://github.com/parcel-bundler/parcel#benchmarks))

| Bundler                 | Time      |
| ----------------------- | --------- |
| browserify              | 22.98s    |
| webpack                 | 20.71s    |
| **parcel**              | **9.98s** |
| **parcel - with cache** | **2.64s** |

이처럼 빌드 속도에 관하여 압도적인 차이를 보여주고있다.

### 1.1 설치

[Get started](https://parceljs.org/getting_started.html)

```bash
yarn global add parcel
yarn init -y
yarn add react react-dom
yarn add babel-preset-env babel-preset-react --dev
or
npm install -g parcel
npm init -y
npm install react react-dom
npm install babel-preset-env babel-preset-react --dev
```

### 1.2 예제 파일

**index.html**

```html{10,11}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Parcel Experiments</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="./index.js"></script>
  </body>
</html>
```

**index.js**

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import App from './src/App'

ReactDOM.render(<App />, document.getElementById('app'))
```

**src/App.js**

```jsx
import React from 'react'

export default () => <div>Hello World</div>
```

> index.js 에서 src/App 을 가져와 `<div id="app">` 에 렌더링하는 코드

### 1.3 실행

실행 후 **dist 폴더에서 압축된 파일**을 볼 수 있다.

```bash
parcel index.html
```

> 아래와 같이 **package.json 에 scripts를 추가**하는 방식도 있다.
>
> ```js
> {
>   "scripts": {
>     "start": "parcel index.html"
>   }
> }
> ```
>
> ```bash
> yarn start
> or
> npm start
> ```

## 2. PostCSS 추가하기

JS 플러그인을 사용하여 CSS를 변환하는 툴이다.  
[많은 플러그인](https://github.com/postcss/postcss/blob/master/docs/plugins.md)이 있으며, 강의에서는 autoprefixer만을 소개한다.

### 2.1 설치

```bash
yarn add postcss-modules
yarn add autoprefixer
```

### 2.2 셋팅

**src/styles.scss**

```css
.title:fullscreen {
  color: red;
  transform: translateY(-10%);
}
```

**src/App.js**

```jsx
import styles from "./styles.scss";
...
export default () => <div className={styles.title}>Hello World</div>
```

**.postcssrc**

> `> 1%` 글로벌 마켓 쉐어에서 1% 이상의 브라우저  
> `Last 2 versions` 해당 브라우저의 최근 2개 버전  
> `IE 10` IE 10 지원

```json
{
  "modules": true,
  "plugins": {
    "autoprefixer": {
      "browsers": ["> 1%", "Last 2 versions", "IE 10"]
    }
  }
}
```

App.js 에서 scss를 호출하여 class를 적용하는 소스코드이다.  
해당 소스코드를 반영 후 parcel을 실행하면 해당되는 브라우저의 CSS(-webkit-, -ms- 등)를 자동으로 생성해준다.

## 3. Typography

자바스크립트를 활용한 [Typography](https://kyleamathews.github.io/typography.js/) 이다.

> Typography: 글자를 의미하는 Typo에 graphy가 붙은 말로 쉽게 해석하면 글자 디자인이란 뜻이다.

- 많은 테마를 다운받을 수 있다.
- 구글 폰트를 자동으로 불러올 수 있게 되어있다.

### 3.1 설치

```bash
yarn add typography
```

### 3.2 셋팅

**typography.js**

```js
import Typography from 'typography'

const typography = new Typography({
  baseFontSize: '18px',
  baseLineHeight: 1.666,
  googleFonts: [
    {
      name: 'Montserrat',
      styles: ['700'],
    },
    {
      name: 'Open Sans',
      styles: ['400'],
    },
  ],
  headerFontFamily: ['Montserrat', 'Helvetica Neue', 'sans-serif'],
  bodyFontFamily: ['Open Sans', 'sans-serif'],
})

typography.injectStyles() // 상단 js를 css으로 변환하는 함수

export default typography
```

**index.js**

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import App from './src/App'
import typography from './typography'

ReactDOM.render(<App />, document.getElementById('app'))
```

**src/App.js**

```jsx
import React from 'react'
import styles from './styles.scss'

export default () => (
  <div className={styles.title}>
    <h1>Hello!</h1>
    <p>Hello World</p>
  </div>
)
```

### 3.3 확인

h1, p 태그에 headerFontFamily 및 bodyFontFamily 이 적용된 것을 확인할 수 있다.

## 4. 후기

Parcel에 관하여 배우는 강의이지만, 워낙 설정이 쉽다보니 시간이 소요된 부분은 없었다.
오히려 Typography를 사용하여 폰트를 정의하는 부분에 더 흥미가 생겼다.
현재 사용하고 있는 gatsby 블로그에도 Typography가 적용되어 있는데 내부 코드를 확인하면서 강의를 들으니 이해가 더 잘 되었다.
