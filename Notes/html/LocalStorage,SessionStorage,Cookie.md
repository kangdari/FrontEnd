# Web Storage

Web Storage의 두가지 방식 = 웹 스토리지 객체(web storage object) = LocalStorage와 SessionStorage

LocalStorage와 SessionStorage는 HTML5에 추가된 저장소입니다. 간단한 키와 값을 저장할 수있는 key-value 형태의 저장소입니다. 두 스토리즈는 모두 window 객체 안에 들어있고 Storage 객체를 상속받기 때문에 메서드가 공통적으로 존재합니다. 도메인 별 용량 제한도 있습니다.

LocalStorage와 SessionStorage의 차이점은 **데이터의 영구성**입니다. LocalStorage의 데이터는 사용자가 지우지 않는 이상 브라우저에 계속 남아 있습니다. 반면에 SessionStorage의 데이터는 윈도우나 브라우저 탭을 닫을 경우 데이터가 제거됩니다. 즉, 지속적으로 필요한 데이터는 LocalStorage, 잠깐 사용하는 데이터는 SessionStorage에 저장하면 됩니다.

두 저장소는 도메인별로 별도로 생성되지만 LocalStorage와 다르게 SessionStorage는 같은 도메인이라도 브라우저가 다를 경우 서로 다른 영역이 됩니다. 브라우저 컨텍스트가 다르기 때문이다.

## LocalStorage

- 유효기간 없이 데이터를 저장하고, 자바스크립틑 사용하거나 브라우저 캐시 또는 LocalStorage의 데이터를 지워야 사라진다.

- 셋 중 가장 큰 저장 공간을 가진다.

- 도메인별로 별도로 생성

## SessionStorage

- 브라우저 또는 탭이 닫힐 때까지만 데이터를 저장한다.

- 데이터를 절대 서버에 전송하지 않는다.

- 저장 공간이 쿠키(4KB)보다 크다(최대 5MB)

- 도메인별로 별도로 생성(도메인이 같아도 브라우저가 다르면 서로 다른 영역)

# Cookie

쿠키는 LocalStorage와 SessionStorage가 나오기 이전부터 사용하던 만료 기한이 있는 key-value 저장소 입니다.

- 매번 서버 요청마다 서버에 전송됨
  HTTP 요청은 상태에 대한 정보를 가지고 있지 않습니다. 때문에 서버는 해당 요청이 누구에게서 오는지 알 수 없습니다. 그래서 쿠키에 나에 대한 정보를 담아 서버로 보내면 서버는 쿠키를 읽고 내가 누군지 파악한 뒤 나에게 응답을 해줍니다. 즉, 쿠키는 처음부터 서버와 클라이언트 간의 지속적인 데이터 교환을 위해 만들어졌기 때문에 서버로 계속 전송됩니다.

- 4kb의 용량 제한
  요청을 할 때마다 4kb의 기본 데이터를 사용하는데 4kb 중에는 서버에 불필요한 데이터들이 포함되어 있습니다. 바로 그런 데이터들을 LocalStorage와 SessionStorage에 저장할 수 있습니다.

[로컬스토리지, 세션스토리지](https://www.zerocho.com/category/HTML&DOM/post/5918515b1ed39f00182d3048)
[Web Storage API](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API)
