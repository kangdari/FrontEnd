# Ajax와 fetch

## Ajax란 ??

* Ajax(Asynchronous Javascript And Xml)는 **비동기식 자바스크립트 통신을 의미**합니다. 브라우저가 가지고 있는 XMLHttpRequest 객체를 이용해서 전체 페이지를 새로고침 하지않고 페이지의 일부만을 위한 데이터를 로드하는 기법입니다.

* 비동기적 자바스크립트 동작을 하는 기술들을 통틀어 AJAX라고 부릅니다.

* 예전에는 XMLHttpRequest API를 이용하여 구현했지만, 불편함을 느낀 사용자들이 JQuery를 통해 구현하기 시작했고, 그 이후 fetch API가 ES6(ES2015) 표준으로 등장하면서 fetch API를 통해 구현하는 것이 일반적인 방법이 되었습니다.

## fetch API

ES6에서 지원해주는 fetch API는 ES6의 Promise와 함께 AJAX를 쉽게 구현해주고 가독성이 매우 좋은 방식입니다. 
fetch는 반환값으로 Promise를 가집니다. 

아래는 기본적인 fetch의 구조입니다.

```
fetch(resource, init)
    .then( callback )
    .catch( callback )
```

* resource: URL 경로, 요청 주소

* init: 설정 객체

아래는 fetch의 간단한 예시입니다.

```
fetch('URL')
    .then(res => {
        if(res.status === 200){
            return res.json()
        }else{
            console.error(res.statusText)
        }
    })
    .then(jsonData => {
        console.log(jsonData)
    })
    .catch(err => {
        console.log(err)
    })
```

* fetch에 요청할 경로를 작성하고 필요시 설정 객체도 함께 전달합니다.

* 요청 결과 Response 인스턴스가 반환되고, 첫번째 then의 res 값입니다.

* 첫번째 then에서 상태 코드가 200일 경우 res.json()을 반환하고, 다른 상태 코드일 경우 res.statusText를 반환합니다.

* 두번째 then에서 res.json() 값을 출력합니다.

* 첫번째 then에서 res.json() 값을 바로 출력하지 않고 다음 then으로 리턴하여 넘겨준 response.json()은 기대하는 실제 값이 아닌 Promise를 가지고 있습니다.

* 그래서 Response 객체의 body 값을 출력하기 위해 타입에 따른 아래의 메소드를 사용해야합니다.
    * arrayBuffer()
    * blob()
    * json()
    * text()
    * formData()

위 메소드들은 모두 Promise를 반환하며 이 Promise가 resolve되어야 다음 then에서 실제 값(data)를 다룰 수 있습니다.

## 참고

[Ajax_MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX)

[AJAX, XMLHttpRequest와 Fetch 살펴보기](https://junhobaik.github.io/ajax-xhr-fetch/)

