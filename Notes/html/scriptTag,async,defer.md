# script 태그 삽입 위치

브라우저는 HTML 문서를 해석(Parsing)할 때 DOM 트리를 구성하고 페이지를 렌더링합니다.
만약 파싱 중 `<script>` 태그를 만나면 브라우저는 파싱을 중단하고 스크립트를 로드한 뒤 실행하게 되고 이 과정을 수행하는 동안 렌더링은 지연됩니다. 즉, js 파일의 처리 시간이 길어질수록 사용자에게 HTML 페이지가 화면에 보여지기까지 시간이 지연됩니다.

**스크립트의 삽입 위치에 따라 스크립트 실행 순서와 렌더링에 영향을 준다**

## head에 삽입하는 경우

```
<head>
	<script src='main.js'></script>
<head>
```

![](https://images.velog.io/images/ksh4820/post/821a790a-ca63-4608-a7d9-bd36eb5d2c39/image.png)

- 무거운 스크립트일수록 브라우저 렌더링이 더 지연되어 사용자에게 완성되지 못한 화면을 오랫동안 노출합니다.

- DOM 구조가 필요한 스크립트의 경우 아직 렌더링되지 않은 DOM 요소가 있을 경우 오류가 발생할 수 있습니다.

## `</body>` 앞에 선언

```
...
	<script src='main.js'></script>
</body>
```

![](https://images.velog.io/images/ksh4820/post/eccbb9ef-ba65-4eac-838a-285ea1f392b4/image.png)

- 브라우저가 렌더링이 완료된 상태에서 스크립트가 실행됩니다.

- 대부분의 스크립트의 위치로 추천되는 위치입니다.

- 스크립트에서 DOM 요소에 접근하여도 문제가 발생하지 않습니다.

# async / defer

## async

```
<head>
	<script async src='main.js'></script>
<head>
```

async 속성을 선언하게 되면 브라우저가 HTML를 파싱하는 중 병렬로 js파일을 다운받으면서 파싱을 진행하다가 js가 다운이 완료되면 파싱을 중지하고 js를 실행합니다. 실행이 된 뒤 다시 HTML 파싱을 진행합니다.

- js 파일을 다운받는 시간을 절약할 수 있지만 js에서 DOM 요소에 접근 시 아직 파싱이 완료된 상태가 아니므로 오류가 발생할 수 있습니다.

- 브라우저 렌더링이 지연될 수 있습니다.

- 다운로드가 먼저 된 js 파일을 우선적으로 실행하기 때문에 js 파일의 순서가 중요한 경우 사용을 자제해야한다.

![](https://images.velog.io/images/ksh4820/post/72e5d48d-56a5-467b-8ddf-21a833564acd/image.png)

## defer

```
<head>
	<script defer src='main.js'></script>
<head>
```

defer 속성을 선언하면 브라우저가 HTML 파싱과 js파일 다운로드를 병렬로 실행합니다.
이후 파싱이 끝난 뒤 js파일을 실행합니다.

- js 파일 다운로드 시간을 절약할 수 있고 정의한 js 순서대로 js 파일이 실행됩니다.

- 가장 효율적인 방법입니다.

![](https://images.velog.io/images/ksh4820/post/55f3f581-b385-45b5-8325-ec301982c3c3/image.png)

[이미지 출처](https://www.youtube.com/watch?v=tJieVCgGzhs)
