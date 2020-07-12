# 웹팩

웹팩이란 최신 프런트엔드 프레임워크에서 가장 많이 사용되는 모듈 번들러입니다.
모듈 번들러란 웹 애플리케이션을 구성하는 자원(html, css, javascript, image...)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구를 의미합니다.

## 모듈

모듈이란 프로그래밍 관점에서 특정 기능을 갖는 코드 단위를 의미합니다.
ex) 함수, 변수

## 웹팩에서의 모듈

웹팩에서 지칭하는 모듈이라는 개념은 웹 애플리케이션을 구성하는 html, css, javascript, image, font, video 등 많은 파일들을 의미합니다.

## 모듈 번들링

웹 애플리케이션을 구성하는 수많은 자원들을 하나의 파일로 병합 및 압축해주는 동작을 모듈 번들링이라고합니다.
![](https://images.velog.io/images/ksh4820/post/f1b2a572-915d-4bf2-b377-ad42ecc41502/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-07-11%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.34.07.png)

(빌드 = 변환 = 컴파일 = 번들링)

## 웹팩 튜토리얼 링크

[웹팩 튜토리얼](https://joshua1988.github.io/webpack-guide/getting-started.html#%EC%9B%B9%ED%8C%A9-%EB%A7%9B%EB%B3%B4%EA%B8%B0-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC)

### webpack.config.js

웹팩 빌드를 위한 설정 파일. 프로젝트 루트 폴더 아래 생성하여 작성.

```
const path = require("path");

module.exports = {
  mode: "none",
  entry: "./src/index.js", // 대상
  output: {
    filename: "main.js", // 생성하고자 하는 파일 이름
    path: path.resolve(__dirname, "dist"), // 현재 파일 경로 + /dist
  },
};
```

```
// package.json
  "scripts": {
    "build": "webpack"
  },
```

### 웹팩 변환 전후 결과 비교

**변환 전**

변환 전의 경우 브라우저는 html을 파싱하면서 라이브러리와 js파일들에 대해서 서버에 요청을하게 됩니다.지금은 요청한 라이브러리가 1개이기 때문에 요청 수가 적지만 요청한 라이브러리의 수가 많아질 수 록 요청 수가 많아지고 이를 수행하기 위한 실행시간도 길어집니다.

![](https://images.velog.io/images/ksh4820/post/be60d0b0-17d3-47ab-83da-1aea15bba317/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-07-12%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.07.01.png)

**변환 후**

웹팩을 적용한 경우 애플리케이션을 구성하는 모든 자원들을 하나의 파일로 합치고 해당 파일에 대한 요청을 1번만 보내기 때문에 변환 전의 경우와 비교하여 실행 속도가 빨라집니다.

![](https://images.velog.io/images/ksh4820/post/e9062ae7-da44-4b0c-84d1-6f37306fd0e6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-07-12%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.06.49.png)

## 웹팩의 주요 속성 4가지

### entry

웹팩을 실행 할 대상 파일

```
// webpack.config.js
module.exports = {
  entry: './index.js'
}
```

entry 속성에는 애플리케이션의 전제적인 구조와 내용이 담겨야합니다.

### output

웹팩의 결과물에 대한 정보를 입력하는 속성. 보통 `filename`, `path`를 정의

```
// webpack.config.js
var path = require('path');

module.exports = {
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, './dist')
  }
}
```

filename 속성에는 여러가지 옵션을 넣을 수 있습니다.

결과 파일 이름에 entry 속성을 포함하는 옵션
`filename: '[name].bundle.js'`

결과 파일 이름에 웹팩 내부적으로 사용하는 모듈 ID를 포함하는 옵션
`filename: '[id].bundle.js'`

매 빌드시 마다 고유 해시 값을 붙이는 옵션
`filename: '[hash].bundle.js'`

웹팩의 각 모듈 내용을 기준으로 생생된 해시 값을 붙이는 옵션
`filename: '[chunkhash].bundle.js'`

### loader

웹팩이 웹 애플리케이션을 해석할 때 자바스크립트 파일이 아닌 웹 자원(html, css ,img, font)들을 변환할 수 있도록 도와주는 속성. 오른쪽에서 왼쪽 순으로 적용.

- test : 로더를 적용할 파일 유형 (일반적으로 정규 표현식 사용)
- use : 해당 파일에 적용할 로더의 이름

```
module: {
    rules: [
      {
        test: /\.css$/, // 모든 css 파일들에 대해서
        use: ['style-loader', 'css-loader'] // 해당 로더 적용
      }
    ]
  }
```

css-loader는 css 파일들을 읽어주고 style-loader는 읽은 css 파일들을 style 태그로 만들어 head 태그 안에 넣어줍니다.

### plugin

웹팩의 기본적인 동작에 추가적인 기능을 제공하는 속성입니다. 로더랑 비교하면 로더는 파일을 해석하고 변환하는 과정에 관여하는 반면, 플러그인은 **해당 결과물의 형태를 바꾸는 역할**을 한다고 보면 됩니다.

```
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

{
  module: {
    rules: [{
    }, {
      test: /\.css$/,
      use: [MiniCssExtractPlugin.loader, 'css-loader'],
    }],
  },
  plugins: [
    // 기타 플러그인
    new MiniCssExtractPlugin({ filename: 'app.css' });
  ]
}
```

만약 style 태그 대신 css파일로 만들고 싶은 경우에 mini-css-extract-plugin을 사용하면 됩니다.

- HtmlWebpackPlugin : 웹팩으로 빌드한 결과물로 HTML 파일을 생성해주는 플러그인
- ProgressPlugin : 웹팩의 빌드 진행율을 표시해주는 플러그인4
- MiniCssExtractPlugin: css 파일로 변환해주는 플러그인

[참고 사이트](https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html#%EC%9B%B9%ED%8C%A9%EC%9D%B4%EB%9E%80)
