
## SPA(Single Page Application)

![](https://images.velog.io/images/ksh4820/post/60a183e5-96ae-4222-865e-09cbe2479a4d/image.png)

* 최초 한번 페이지를 로딩한 이후 JS를 이용해 동적으로 데이터만 변경하여 화면의 컨텐츠를 바꾸는 방식의 웹 어플레케이션이다.

* 웹에서 제공하는 정보량이 많아지고 데스크탑보다 성능이 떨어지는 모바일에 최적화시키기 위해 등장.

* 서버는 단지 JSON 파일만 보내주는 역할을 수행하며 HTML을 그리는 역할은 클라이언트에서 JS로 수행한다. 그리고 이러한 방식이 CSR이다.

---


## 렌더링(Rendering)

요청받은 내용을 브라우저 화면에 표시하는 작업


## CSR(클라이언트사이드 렌더링)


![](https://images.velog.io/images/ksh4820/post/23d1d2f2-169e-47fe-a4f9-7538638925d7/image.png)

[출처](https://medium.com/@adamzerner/client-side-rendering-vs-server-side-rendering-a32d2cf3bfcc)

CSR은 최초에 한 번 서버에서 전체 페이지를 로딩하여 보여주고 이후 사용자의 요청에 따라 JS를 이용하여 필요한 리소스를 서버로 부터 제공받고 클라이언트가 데이터를 해석, 렌더링하는 방식이다. 
=> HTML을 그리는 역할을 클라이언트가 JS로 수행.

### 장점

* 첫 로딩만 기다린다면 이후부터는 좋은 사용자 경험(UX)를 제공한다.

* 연속된 렌더링으로 인한 과부하를 줄일 수 있다.

### 단점

* 초기 렌더링 속도가 느리다.

* 검색 엔진 최적화에 문제가 발생한다.

---

## SSR(Server Side Rendering)

![](https://images.velog.io/images/ksh4820/post/c91eadac-3f4a-4762-81a3-a4a2a54f0982/image.png)

[출처](https://medium.com/@adamzerner/client-side-rendering-vs-server-side-rendering-a32d2cf3bfcc)

SSR은 서버에 페이지에 대한 요청을 하고 서버로부터 HTML, JS, CSS 파일 및 데이터를 전달받아 렌더링하는 방식입니다. => 서버에서 렌더링을 수행하는 방식.

### 장점

* 초기 렌더링 속도가 빠르다.

* JS를 이용한 렌더링이 아니므로 SEO(검색 엔진 최적화)가 가능하다. => HTML에 모든 컨텐츠가 저장되어 있음.


### 단점

* 매번 새로운 페이지를 요청할 때 마다 새고로침이 발생한다.

* 간단한 데이터 수정에도 서버를 거쳐야한다.

* 매번 서버에 요청을 하는 행위는 서버에 과부하의 원인이다.


---

## SSR과 CSR의 렌더링 속도 차이

![](https://images.velog.io/images/ksh4820/post/073ecd83-dc1d-4909-b05e-23e04ef18811/image.png)

---

## SEO(Search Engine Optimization)

* 대부분의 웹 크롤러, 봇들은 JS를 실행시키지 못하고 HTML에서만 컨텐츠를 수집하기 때문에 
CSR 방식으로 개발된 페이지를 빈 페이지로 인식하게 됩니다.

* SSR 방식은 View를 서버에서 전부 렌더링하기 때문에 HTML에 모든 컨텐츠가 저장되어 있어 SEO를 사용하는데 문제가 없습니다.

---

## 주의할 점

* 전통적인 웹 페이지 방식 !== SSR

* SPA !== CSR

* 즉, 전통적인 웹 페이지 방식이 주로 SSR 방식을 사용한 것이고, SPA가 주로 CSR 방식을 사용하는 것.

---

## 참고

* [취준생이라면 반드시 알아야 하는 프론트엔드 관련 지식들](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/frontend/csr-ssr.md)

* [서버 사이드 렌더링 그리고 클라이언트 사이드 렌더링](https://asfirstalways.tistory.com/244)

* [예전 블로그](https://blog.naver.com/ksh44820/221724601476)