# Web Worker

> Web Worker는 script 실행을 메인 쓰레드가 아니라 백그라운드 쓰레드에서 실행할 수 있도록 해주는 기술 입니다. 이 기술을 통해 무거운 작업을 분리된 쓰레드에서 처리할 수 있으며, 이를 통해 메인 쓰레드(일반적으로 UI 쓰레드)는 멈춤, 속도저하 없이 동작할 수 있게 됩니다. [Web Workers API](https://developer.mozilla.org/ko/docs/Web/API/Web_Workers_API)

Javascript는 보통 Single Thread로 동작합니다. 하지만 브라우저는 Single Thread로 동작하지 않습니다.

브라우저에서 처리되는 Network 통신이나 I/O들은 서로 다른 스레드에서 동작합니다.

Web Worker는 브라우저의 Main Thread와 별개로 작동되는 Thread를 생성할 수 있습니다.
즉, Web Worker를 사용하면 브라우저에서 멀티 쓰레드를 활용할 수 있습니다.

Web Worker로 생성한, Thread는 브라우저 렌더링 같은 Main Thread의 작업을 방해하지 않고, 새로운 Thread에서 스크립트를 싱행하는 간단한 방법을 제공합니다.

대부분의 웹에서는 워커를 쓸 정도로 복작합 작업을 진행하지 않기 때문에 웹 워커를 사용할 일이 드뭅니다. 하지만 빅데이터 처리나 웹 게임 등의 경우에는 유용합니다. 계산은 워커에게 맡기고 메인 쓰레드는 DOM 업데이트만 담당하면 됩니다.

[Web Worker 간단 정리하기](https://medium.com/@pks2974/web-worker-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-4ec90055aa4d)

[웹 워커](https://www.zerocho.com/category/HTML&DOM/post/5a85672158a199001b42ed9c)
