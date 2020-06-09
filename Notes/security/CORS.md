# Cross-Origin Resource Sharing

**CORS(교차 출처 리소스 공유)** 는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제입니다. **웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행합니다.** `출처 - MDN`

즉, Same-Origin Policy의 문제점을 해결하기 위한 정책으로 **출처가 다른 도메인에서의 ajax 요청이라도 서버 단에서 데이터 접근 권한을 허용하는 정책**입니다.

![](https://images.velog.io/images/ksh4820/post/332ffc95-8019-4241-8935-5036fb1f8367/image.png)


하지만 동일 출처 정책때문에 CORS 같은 상황이 발생하면 외부 서버에 요청한 데이터를 브라우저에서 보안 목적을 차단합니다. 때문에 서버나 클라이어트 단에서 특정 도메인 혹은 모든 도메인을 허용하도록 설정해주면 해결 가능합니다.

## 서버 단 해결

### Access-Control-Allow-Origin response 헤더 추가

`Access-Control-Allow-Origin` 응답 헤더는 이 응답이 주어진 origin으로부터 요청 코드와 공유될 수 있는지를 나타냅니다. `출처 - mdn `

`response.setHeader("Access-Control-Allow-Origin", "*")` 

`*`는 모든 도메인에 대해서 허용하겠다는 의미로, 어떤 웹사이트에서도 이 서버에 접근하여 ajax 요청하여 결과를 가져갈 수 있도록 허용하는 의미입니다. * 대신 특정 도메인을 지정할 수 있습니다.

예시 

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

저같은 경우 리액트 프로젝트를 진행하면서 클라이언트의 package.json 파일에 
`proxy: host:portNumber`를 작성하여 해결한 적이 있습니다.






