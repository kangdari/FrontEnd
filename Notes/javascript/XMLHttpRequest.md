# XMLHttpRequest

XMLHttpRequest를 이용하여 AJAX를 구현해보겠습니다.

JSONPlaceholder의 예제 코드를 불러와 보겠습니다.

예제 코드입니다.

```
(() => {
  const httpRequest = new XMLHttpRequest();

  httpRequest.onreadystatechange = (e) => {
    console.log(
      `state: ${httpRequest.readyState} / status : ${httpRequest.status} / ${responseReady()} `
    );
  };

  const responseReady = () => {
    try {
      if (httpRequest.readyState === XMLHttpRequest.DONE) {
        if (httpRequest.status === 200) {
          // 응답 정상
          console.log(httpRequest.responseText);
          return httpRequest.responseText;
        } else {
          return new Error('request 에러 발생');
        }
      } else {
        return new Error('reqeust 상태 complete(4) 아님');
      }
    } catch (e) {
      return new Error('예외 발생' + e.description);
    }
  };

  httpRequest.open('GET', 'https://jsonplaceholder.typicode.com/todos/');
  httpRequest.send();
})();
```

`const httpRequest = new XMLHttpRequest();` 생성자를 사용하여 XMLHttpRequest 인스턴스를 생성합니다.

`httpRequest.onreadystatechange`
onreadystatechange 내장 함수를 사용하여 서버의 상태를 확인하는 코드를 작성했습니다.

```
  httpRequest.onreadystatechange = (e) => {
    console.log(
      `state: ${httpRequest.readyState} / status : ${httpRequest.status} / ${responseReady()} `
    );
  };
```

readyState는 서버의 응답 상태를 나타내며 아래 값들을 가질 수 있습니다.

- 0 (uninitialized) -(request가 초기화되지 않음)
- 1 (loading) -(서버와의 연결이 성사됨)
- 2 (loaded) -(서버가 request를 받음)
- 3 (interactive) -(request(요청)을 처리하는 중)
- 4 (complete) -(request에 대한 처리가 끝났으며응답할 준비가 완료됨)

responseReady() 까지가 요청에 대한 응답을 처리하는 코드 부분입니다.

아래 코드의 open(), send() 메서드가 응답을 요청하는 부분입니다.

```
  httpRequest.open('GET', 'https://jsonplaceholder.typicode.com/todos/');
  httpRequest.send();
```

open()을 하면 위의 상태 1번 까지 진행되고, send()를 하면 4번까지 작동하여 응답을 받을 수 있습니다.

- open()
  첫번째 파라미터로는 HTTP 요청메서드(GET, POST, HEAD)를 설정합니다.
  두번째 파라미터로는 요청 URL 또는 주소, 경로를 설정합니다.
  세번째 파리미터는 생략이 가능하며 요청이 비동기적으로 실행될지 설정합니다.
  (default : true // false로 설정 시 동기적으로 실행됨. 즉, send() 메서드에서 서버로부터 응답이 오기 전까지 대기)

아래는 콘솔에 출력된 내용이며
state가 4일 때 XMLHttpRequest.DONE이며 complete 상태일 때 응답을 받을 수 있는 상태이며 응답을 전달받은 것을 확인 할 수 있습니다.

```
state: 1 / status : 0 / Error: reqeust 상태 complete(4) 아님
state: 2 / status : 200 / Error: reqeust 상태 complete(4) 아님
state: 3 / status : 200 / Error: reqeust 상태 complete(4) 아님
state: 4 / status : 200 / [
  {
    "userId": 1,
    "id": 1,
    "title": "delectus aut autem",
    "completed": false
  },
  ...
```

[fetch를 이용한 AJAX 구현](https://velog.io/@ksh4820/AJAX)

---

[참고 블로그](https://junhobaik.github.io/ajax-xhr-fetch/)
