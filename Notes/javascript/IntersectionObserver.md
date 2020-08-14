# 개요

인스타그램 클론 프로젝트를 진행하다 Infinite-Scroll를 구현하기 위해 알아보던 중 IntersectionObserver에 대해서 정리하게 되었습니다.

# 🧑🏻‍💻 IntersectionObserver API???

> The IntersectionObserver interface of the Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport. [출처 - MDN](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver)

> Intersection Observer API 의 IntersectionObserver 인터페이스는 대상 요소와 상위 요소 또는 최상위 문서의 뷰포트 의 교차점에서 변경 사항을 비동기식으로 관찰하는 방법을 제공합니다.

IntersectionObserver API는 **관측 요소**가 **부모 요소** 또는 **viewport** 관계에서 **가시성**(보이는지 안 보이는지)을 쉽게 알 수 있도록 기능을 제공합니다.
(한참 헷갈리다가 코드보고 이해했습니다...)

대표적인 사용 예시

- Lazy Loading 페이지 스크롤 시 이미지 지연 로딩
- Infinite Scroll 비동기 무한 스크롤 UI(인스타그램, 트위터...)
- 광고의 수익을 계산하기 위해 광고의 가시성을 참고할 때

# 브라우저 지원 현황

![](https://images.velog.io/images/ksh4820/post/7d95524d-a5a1-49ad-a8f7-f06f8aba6617/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.08.09.png)

# Intersection Observer 사용 방법

```
// 콜백함수와 옵션을 받습니다.
const io = new IntersectionObserver(callback[, options])
```

### Parameters

- **callback**
  관측 요소가 타켓 요소와 교차되었을 때 실행할 함수로 두 개의 파라미터를 입력받습니다
  - **entries**: IntersectionObserverEntry 객체의 리스트. 배열 형식으로 반환하기 때문에 forEach를 사용해서 처리를 하거나, 단일 타겟의 경우 배열인 점을 고려해서 코드를 작성해야 합니다.
  - **observer**: 콜백함수가 호출되는 IntersectionObserver
- **options**

  - root: `scrollable Element` 또는 `null`

    - default: null, 브라우저의 viewport
    - `Element`의 경우 관측 요소의 부모 요소를 뜻함.

  - rootMargin

    - default: `0px 0px 0px 0px` \* root 엘리먼트의 마진값. css에서 margin을 사용하는 방법으로 선언할 수 있고, 축약도 가능하다. px과 %로 표현할 수 있습니다. rootMargin 값에 따라 교차 영역이 확장 또는 축소된다.

- threshold
  - default: 0
  - 0.0부터 1.0 사이의 숫자 혹은 이 숫자들도 이루어진 배열로, 타켓 요소에 대한 교차 영역 비율을 의미한다. 0.0일 경우 타켓 요소가 교차영역에 진입했을 시점에 observer를 실행하는 것을 의미하며, 0.5일 때는 절반, 1.0일 때는 타켓 요소가 교차 영역 전체에 들어왔을 때 observer를 실행하는 것을 의미한다.

### 사용 예시

```
// option 설정
const options = {
  // root: null, // viewport
  root: document.querySelector('.container'),
  rootMargin: '10px', // '10px 10px 10px 10px'
  threshold: [0, 1], // 관측 요소가 교차영역에 진입했을 때, 교차 영역에 관측 요소가 100% 있을 때 observer가 반응.
};

// IntersectionObserver 생성
const io = new IntersectionObserver((entries, observer) => {
  // IntersectionObserverEntry 객체 리스트와 observer 본인(self)를 받음
  // 원하는 동작 작성
  entries.forEach((entry) => {
    console.log('entry:', entry);
    console.log('observer:', observer);
  });
}, options);
```

### Methods

**IntersectionObserver.observe(targetElement)**

- 타겟 엘리먼트에 대한 IntersectionObserver를 등록할 때(관찰을 시작할 때) 사용합니다.

**IntersectionObserver.unobserve(targetElement)**

- 타겟 엘리먼트에 대한 관찰을 멈추고 싶을 때 사용하면 됩니다. 예를 들어 Lazy-loading(지연 로딩)을 할 때는 한 번 처리를 한 후에는 관찰을 멈춰도 됩니다. 이 경우에는 처리를 한 후 해당 엘리먼트에 대해 `unobserve(targetElement)`을 실행하면 이 엘리먼트에 대한 관찰만 멈출 수 있습니다.

**IntersectionObserver.disconnect()**

- 다수의 엘리먼트를 관찰하고 있을 때, 이에 대한 모든 관찰을 멈추고 싶을 때 사용하면 됩니다.

**IntersectionObserver.takerecords()**

- IntersectionObserverEntry 객체의 배열을 리턴합니다.

# Lazy Loading

[LazyLoading - gist](https://gist.github.com/kangdari/87e3482ce1d0189057e40f7901fe9512)

# Infinite Scrolling

[Infinite Scrolling - gist](https://gist.github.com/kangdari/686f0a4fcea6ed72683dbf1caf80bfa8)

# 마무리

지금까지 IntersectionObserver API에 대해서 알아봤습니다.
IntersectionObserver를 사용하면 기존의 scroll 이벤트를 사용하여 구현하는 방식보다 간단하게 구현이 가능합니다.

# 참고 블로그

[👀 IntersectionObserver API](http://blog.hyeyoonjung.com/2019/01/09/intersectionobserver-tutorial/)
[Intersection Observer API의 사용법과 활용방법](https://velog.io/@doondoony/IntersectionObserver)
[레진 기술블로그](https://tech.lezhin.com/2017/07/13/intersectionobserver-overview)
