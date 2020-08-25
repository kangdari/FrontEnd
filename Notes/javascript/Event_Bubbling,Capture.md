# 이벤트 등록

웹 애플리케이션의 이벤트 등록입니다.

```
<button>Button</button>

const button = document.querySelector('button');
button.addEventListener('click', onClick);

function onClick(event) {
  console.log(event);
}
```

button 요소에 클릭 이벤트를 등록했습니다. button을 클릭하면 onClick 함수가 실행되는 코드입니다. event 인자를 출력해보면 이벤트와 관련된 정보를 확인할 수 있습니다.

그렇다면 브라우저는 어떻게 이벤트의 발생을 감지할까? 브라우저가 이벤트를 감지하는 방식은 2가지가 있습니다.

# Event Bubbling

이벤트 버블링은 특정 요소에서 이벤트 발생 시 해당 이벤트가 더 상위 요소들로 전달되어가는 특성입니다.

![](https://images.velog.io/images/ksh4820/post/db5b7214-eabc-4193-b1be-cfd64895679a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-25%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.36.05.png)

# Event Caputre

이벤트 캡쳐는 이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식입니다.
![](https://images.velog.io/images/ksh4820/post/2d75c620-4cc9-4e64-917a-213317b70c07/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-25%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.41.59.png)

```
div.addEventListener('click', onClick, {
	capture: true // default 값은 false입니다.
});
```

addEventListener API에서 옵션 객체에 `capture: true`를 설정해주면 해당 이벤트를 감지하기 위해 이벤트 버블링과 반대 방향으로 탐색하게 됩니다.

# event.stopPropagation()

```
function onClick() {
	event.stopPropagation();
}
```

event.stopPropagation()는 해당 이벤트가 전파되는 것을 막습니다. 즉, 이벤트 버블링의 경우 클릭한 요소의 이벤트를 발생시키고 상위 요소로 이벤트가 전달되는 것을 막고, 캡쳐링의 경우에는 최상위 요소의 이벤트만 발생시키고 하위 요소들로 이벤트를 전달하지 않습니다.

# Event Delegation

바닐라 자바스크립트로 웹 앱을 구현할 때 자주 사용되는 코딩 패턴입니다.

이벤트 위임은 **하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트를 제어하는 방식**입니다.

[이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)
