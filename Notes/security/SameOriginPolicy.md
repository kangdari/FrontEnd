# Same-Origin Policy

**동일 출처 정책**은 어떤 출처에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 중요한 보안 방식입니다. 동일 출처 정책은 잠재적으로 해로울 수 있는 문서를 분리함으로써 가능한 공격 경로를 줄이는데 도움을 줍니다. `출처 MDN`

동일한 출처의 의미는 URL의 프로토콜, 포트, 호스트가 모두 같은 것을 의미합니다. 

즉, 동일 출처 정책은 웹 브라우저 보안을 위해 프로토콜, 호스트, 포트가 동일한 서버로만 AJAX 요청을 주고 받을 수 있도록 한 정책. 

## 프로토콜, 호스트, 포트 ??

개발자 도구의 콘솔창에서 `location`을 입력하면 현재 브라우저의 프로토콜, 호스트, 포트와 그 외 정보들을 확인할 수 있습니다. 

![](https://images.velog.io/images/ksh4820/post/27865977-9f87-47f7-85f6-737ee542b991/image.png)

( http는 80번, https는 433번이 기본 포트입니다. )

정리하면 **동일 출처 정책**은 같은 출처의 서버로만 요청을 서로 주고 받을 수 있다는 것이다.

* http://www.sameDomain.com/ ==> http://www.sameDomain.com/dir2 
이 경우 경로만 다를뿐 출처는 동일하기 때문에 서로 요청을 주고 받을 수 있습니다.

* http://www.sameDomain.com/ =/=> https://www.crossDomain.com 
이 경우 프로토콜이 서로 다르기 때문에 동일 출처 정책에 어긋납니다.

* http://www.sameDomain.com/ =/=> http://www.crossDomain.com
이 경우 호스트가 다르기 때문에 동일 출처 정책에 어긋납니다.


예를 들어 클라이언트를 3000번 포트, 서버를 5000번 포트에서 실행한 후에 클라이언트에서 서버로 요청을 보내면 아래와 같은 오류가 발생한다.

>XMLHttpRequest cannot load 'http://localhost:3000'. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:5000' is therefore not allowed access.

클라이언트와 서버가 서로 다른 포트이기때문에 동일 출처 정책에 어긋난 경우입니다.

실제로 개발을 하다보면 외부 API를 사용하거나 클라이언트와 서버를 분리하여 개발하면서 
해당 정책으로 인한 오류가 많이 발생합니다. 

이러한 불편함을 해결하기 위해서 등장한 것이 **Cross-Origin Resource Sharing(CORS)** 정책입니다.

### 참고

[Same-Origin Policy 동일 출처 정책과 CORS 에러](https://velog.io/@yejinh/CORS-4tk536f0db)

[MDN - 동일 출처 정책 ](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy)

