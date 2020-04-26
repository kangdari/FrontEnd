## 퀴크 모드와 스탠다드 모드

웹 브라우저는 두 가지 렌더링 모드를 지니고 있는데 쿼크(호환) 모드(Quirks mode)와 표준 모드(Standard mode)입니다.

브라우저는 HTML 문서가 DOCTYPE을 가지고 있지 않으면 쿼크 모드로 렌더링을 하고, DOCTYPE을 가지고 있다면 스탠다드 모드로 렌더링을 합니다.

쿼크 모드로 렌더링 하게 되면 오랜된 웹 페이지들을 최신 버전의 브라우저에서도 깨지지 않게 하기 위해 각 브라우저 마다 다르게 보일 수 있습니다.

웹 표준이 정립된 현 시점에서는 HTML5에서 권장하는 `<!DOCTYPE html>`을 사용하는 것이 바람직합니다.

## 참고

* [표준 모드와 호환 모드](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/html/standard-quirks.md)

* [html 101 - DOCTYPE 과 Semantic](https://velog.io/@jay/html-101-DOCTYPE)

