> [what the heck is the event loop anyway](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
> 이벤트 루프를 설명 하기 위한 유튜브 영상이다. 짧은 영상이지만 정말 좋은 영상같다.

![](https://images.velog.io/images/ksh4820/post/b48942e1-f4c7-4cd7-9e9c-770e285354ec/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.04.29.png)

위 사진 처럼 자바스크립트 개발을 진행하다보면 다양한 용어들을 접한다.
v8, callStack, Web api, Task Queue(Evnet Queue), Event Loop 한번 쯤은 어디서 들어본 적은 있지만 제대로 알지 못했다.

자바스크립트는 **싱글 스레드** 프로그래밍 언어이다.(CallStack이 1개) 즉, **한번에 하나의 작업**만을 수행할 수 있음을 의미한다. 다른 작업이 중간에 끼어들수 도 없고, 기존에 수행하던 작업이 끝나야 다음 작업을 수행할 수 있다.

그러면 대체 자바스크립트는 비동기 처리를 어떻게 수행하는 것일까 ??

하나 하나 정리해보자.

# Javascript Runtime

**런타임**이란 프로그래밍 언어가 구동되는 환경을 말합니다.

자바스크립트 런타임은 Javascript engine, Web API, Task Queue, Event Loop, Render Queue로 구성되어있다.

# Javascript engine

자바스크립트 엔진은 CallStack과 Memory Heap 으로 구성되어 있다. 그 중 가장 유명한 것이 구글의 V8 엔진이다.

- CallStack: 현재 실행중인 코드가 담기는 스택 구조의 메모리 영역 (FILO)
  함수를 실행하면 함수에 대한 기록이 스택에 push된다. 함수의 결과 값이 반환되면 pop된다.
- Memory Heap: 메모리 할당이 일어나는 곳. (변수, 함수 등...)

# Web API

Web API는 브라우저에서 제공하는 API로 DOM, Ajax, TimeOut 등이 있다.
CallStack에서 실행된 비동기 함수는 Web API를 호출하고, Web API는 콜백 함수를 Task Queue에 넣는다.

# Event Loop

Event Loop는 **CallStack과 Task Queue의 상태를 체크하여, CallStack이 비어 있을 때,
Task Queue의 첫번째 콜백을 CallStack으로 밀어넣는다.**

## 이벤트 큐와 이벤트 루프의 동작을 잘 보여주는 setTimeout 예

```
console.log('hello');

setTimeout(() => {
  console.log('kang');
}, 3000);

console.log('bye');

// hello
// bye
// kang
```

1. 우선 `console.log('hello')` 구문이 CallStack에 push되고 실행된 뒤 pop 된다. 그럼 콘솔창에는 hello가 출력된다.
2. 다음은 setTimeout을 호출한다. setTimeout은 브라우저에서 제공하는 API이다. 때문에 Web API로 호출된다. 이 때 CallStack에서는 setTimeout 호출 자체는 완료되었으므로 스택에서 pop한다.
3. 다음은 `console.log('bye');` 구문이 CallStack에 들어오고 실행되고 다시 지워진다. 동시에 WEB API에서는 이전에 호출했던 setTimeou의 타이머가 작동 중이다.
4. 모든 Web API는 작동이 완료되면 콜백을 Task Queue로 넣는다.
5. 이벤트 루프는 CallStack과 Task Queue의 상태를 체크하면서 스택이 비어있을 경우 Task Queue의 첫번째 콜백을 CallStack에 넣는다.

6. 이제야 `console.log('kang')`이 CallStack에 들어와 실행된다.

---

```
setTimeout(() => {
  console.log('first');
}, 0);

console.log('second');
// second
// first
```

1. setTimeout의 지연시간으로 0s를 주었다고 바로 실행되지 않는다. setTimeout은 CallStack에서 실행된 후 Web API의 Timer API를 호출한다. 이후 cb은 Task Queue에 들어간다.

2. `console.log('second');` 가 CallStack에 들어가고 실행된 후 나간다.

3. 이벤트루프는 스택이 비어있음을 확인하고 Task Queue의 첫번째 cb인 `console.log('first')`을 CallStack에 넣는다.

4. `console.log('first')`이 실행된다.

# 정리

**자바스크립트는 싱글 스레드 프로그래밍 언어라 한번에 하나의 작업만 수행한다. 하지만 Web API, TaskQueue, EvnetLoop 덕분에 멀티 스레드처럼 실행하는듯 보여진다.**
