# Event Delegation - 이벤트 위임

## 개요

프로그래머스 2020 Dev-Matching: 웹 프론트엔드 개발자(상반기) 챌린지 문제를 풀이하면서 
동적 요소에 이벤트 리스너를 추가 하는 과정에서 Event Delegation 기법을 이용하라는 문제가 있었습니다. 정확하게 이해하기 위해 정리했습니다.


## Event Delegation - 이벤트 위임
---

* 하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트를 제어하는 방식.

동적으로 노드를 생성해보았습니다.
```
wrapper.innerHTML += arr
  .map(
    (url) => `
    <div class="item"><img src="${url}" alt="img"></img></div>
`
  )
  .join("");
```

이벤트 위임을 사용하지 않고 각 요소마다 이벤트 핸들러를 추가했습니다.

```
document
  .querySelectorAll(".item")
  .forEach((item) =>
    item.addEventListener("click", () => console.log("click"))
  );
```

이러한 방식으로 추가한 이벤트 리스너들은 잠재적으로 메모리 누수 및 성능 저하의 원인이 될 수 있습니다.


이번에는 이벤트 위임 기법을 사용해보겠습니다.

```
wrapper.addEventListener('click', (e) => {
    if(e.target.tagName === "IMG"){
        console.log('click')
    }
})
```
이전과는 item 요소에 일일이 이벤트 리스너를 추가하는 대신 상위 요소인 .wrapper에 이벤트 리스너를 추가하고 하위에서 발생한 클릭 이벤트를 감지합니다. 이 부분이 이벤트 버블링입니다.

---

## Event Bubbling - 이벤트 버블링

* 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되어 가는 특성

![](https://images.velog.io/images/ksh4820/post/81989790-757d-41a7-a8fc-031a1d319942/image.png)

```
const divs = document.querySelectorAll('div')

const clickEvent = (e) => {
    console.log(e.currentTarget.className)
}
```

```
divs.forEach(div => {
    div.addEventListener('click' , clickEvent)
})

// 3번 클래스 선택 시
// three
// two
// one
```

브라우저는 특정 화면 요소에 이벤트가 발생했을 때 그 이벤트를 최상위에 있는 화면 요소까지 전파시킵니다. 따라서 클래스명 three => two => one 순서대로 div 태그에 등록된 이벤트들이 실행됩니다. 

여기서 주의해야 할 점은 각 태그마다 이벤트가 등록되어 있기 때문에 상위 요소로 이벤트가 전달되는 것을 확인할 수 있습니다. 만약 이벤트가 특정 div 태그에만 달려있다면 위와 같이 동작 결과를 확인할 수 없습니다. 

---
## Event Capture - 이벤트 캡쳐

* 이벤트 캡쳐는 이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식.

![](https://images.velog.io/images/ksh4820/post/14a2706f-b4b9-43b8-bfa7-36f81cf630a5/image.png)

```
const divs = document.querySelectorAll('div')

const clickEvent = (e) => {
    console.log(e.currentTarget.className)
}

divs.forEach(div => {
    div.addEventListener('click' , clickEvent, {
        capture: true
    })
})

// 3번 클래스 선택 시
// one
// two
// three
```

addEventListener() API 옵션 객체에 capture: true를 설정합니다. 그러면 해당 이벤트를 감지하기 위해 이벤트 버블링과 반대 방향으로 탐색합니다. ( 기본 값: false )

## 참조


[이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)

