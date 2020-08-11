# 🧑🏻‍💻 CORS

CORS는 Cross-Origin Resource Sharing의 약자로 **도메인** 또는 **프로토콜**, **포트**가 다른 서버의 자원을 요청하는 매커니즘을 말한다.

이때 요청을 할 때는 cross-origin HTTP에 의해 요청됩니다.

하지만 동일 출처 정책(same-origin policy)때문에 CORS 같은 상황이 발생하면 외부 서버에 요청한 데이터를 브라우저에서 보안 목적을 차단합니다. 때문에 서버나 클라이어트 단에서 특정 도메인 혹은 모든 도메인을 허용하도록 설정하여 해결해야 합니다.

[동일 출처 정책](https://velog.io/@ksh4820/Same-Origin-Policy-%EB%8F%99%EC%9D%BC-%EC%B6%9C%EC%B2%98-%EC%A0%95%EC%B1%85)

저는 로컬 환경에서 리액트 프로젝트를 진행하면서 리액트(3000번)와 서버(5000번)의 포트 번호가 달라서 CORS가 발생한적이 있었습니다.

## 🧑🏻‍💻 해결 방법

### Access-Control-Allow-Origin response 헤더 추가

`Access-Control-Allow-Origin` 응답 헤더는 이 응답이 주어진 origin으로부터 요청 코드와 공유될 수 있는지를 나타냅니다. `출처 - mdn`

`response.setHeader("Access-Control-Allow-Origin", "*")`

`*`는 모든 도메인에 대해서 허용하겠다는 의미로, 어떤 웹사이트에서도 이 서버에 접근하여 ajax 요청하여 결과를 가져갈 수 있도록 허용하는 의미입니다. \* 대신 특정 도메인을 지정할 수 있습니다.

```
app.use((req, res) => {
	res.header("Access-Control-Allow-Origin", "*"); // 모든 도메인
    res.header("Access-Control-Allow-Origin", "https://sample.com"); // 특정 도메인
});
```

### Node.js Express CORS 미들웨어

`yarn add cors` or `npm install cors`

CORS 미들웨어 설치 후

```
const express = require('express');
const cors = require('cors');
const app = express();

app.use(cors());
```

위와 같이 아무 옵션 없이 `app.use(cors());`로 설정한다면 모든 cross-origin 요청에 대해 응답한다. 만약 특정 도메인 요청만 받거나, 특정 요청에만 응답하는 경우 그에 따른 옵션을 설정해야한다.

**특정 도메인 접근 허용**

```
const options = {
  origin: 'http://example.com', // 접근 권한을 부여하는 도메인
  credentials: true, // 응답 헤더에 Access-Control-Allow-Credentials 추가
  optionsSuccessStatus: 200 // 응답 상태 200으로 설정
};

app.use(cors(options));
```

**특정 요청 접근 허용**

```
app.get('/path/:id', cors(), (req, res, next) => {
	res.json({msg: '~~~'})
});
```

## 클라이언트 단 해결

### proxy 설정

proxy란 클라이언트가 자신을 통해서 다른 네트워크나 컴퓨터 사이에서 서로 통신할 수 있도록 돕는 것입니다.

![](https://images.velog.io/images/ksh4820/post/38aafeda-a74f-4344-8b08-ea81435779a8/image.png)

proxy 설정 2가지 방법

- 클라이언트의 package.json 파일에 `proxy: host:portNumber`를 작성

- http-proxy-middleware 패키지 사용
  https://create-react-app.dev/docs/proxying-api-requests-in-development

## 🧑🏻‍💻 요약

- cors는 **도메인** 및 **프로토콜**, **포트**가 다른 서버의 자원을 요청하면 발생하는 이슈이다.
- 서버와 클라이언트가 분리되어 있는 애플리케이션에서는 cross-origin HTTP 요청을 서버에서 승인해주거나 proxy 설정을 해줘야한다.
