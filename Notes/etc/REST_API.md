# 🧑🏻‍💻 REST API

REST는 Representational State Transfer의 약자입니다. 핵심은 **Representational State**, 번역하면 대표적인 상태. 이때 이야기하는 상태는 서버가 가지고 있는 리소스의 상태입니다.

즉, REST는 통신을 통해 자원의 표현된 상태를 주고받는 것에 대한 아키텍쳐 가이드라인이라고 할 수 있습니다.

웹은 클라이언트와 서버로 구분됩니다. 클라이언트에서 서버로 요청을 보내고, 서버는 클라이언트에게 응답을 보냅니다. REST API를 사용하는 웹앱은 URI(주소)를 통해 서버에 요청하고. 서버는 html, xml, json 등으로 응답합니다.

## RESTful API

REST는 단지 리소스가 표현된 상태만을 이야기할 뿐, 어떠한 "행위"에 대해서는 이야기하고 있지 않습니다. 하지만 클라이언트가 API를 사용할 때 원하는 것은 소스를 생성하거나 삭제하거나 수정하능 등 명백한 어떠한 행위입니다.

그래서 RESTful API에서는 REST 아키텍쳐를 통해 표현된 리소스와 더불어 어떠한 행위를 명시할 수 있는 HTTP 메서드와 URI까지 활용합니다.

1. 리소스가 어떻게 표현되는지? - REST
2. 어떤 리소스인지? - URI
3. 어떤 행위인지? - HTTP 메서드

즉, **GET /users/3** 과 같은 엔드포인트만 보고도 3번 유저의 정보를 가져오는 API라고 추측할 수 있게 되는 것입니다.

## 장점

- 체계적이라 관리하기가 쉽다.

- 주소만 봐도 무슨 내용인지 이해할 수 있다.

- 서버를 REST API로 만들어 놓으면 언어에 상관없이 HTTP를 사용하는 다양한 플랫폼에서 동시에 사용할 수 있다.

- 캐싱이 가능하다. ( GET 요청의 경우 같은 응답에 대해서 캐싱으로 더 빨리 로딩 )

## 주의점

REST API 하나의 구조이다.

- 잘 이해가 가지 않는 주소는 사용해선 안된다. /users/3 과 같이 주소를 봐서 어떠한 요청인지 추측이 가능해야한다. 주소만 봐도 어떤 동작을 하는 API인지 바로 이해할 수 있을 정도로 명확한 API가 가장 좋은 API다.

- 요청 의도에 맞는 HTTP 메서드를 사용해야한다.

# HTTP 메서드

RESTful API는 HTTP 메소드를 사용하여 API가 수행하는 행위를 표현하도록 권장한다.

대부분의 API들은 CRUD이기 떄문에, 특수한 경우를 제외하곤 5가지의 HTTP 메서드로 정의된다.

- GET - 리소스 조회

- POST - 리소스 생성

- PUT - 리소스 수정(전체)

- PATCH - 리소스 수정(일부)

- DELETE - 리소스 삭제
