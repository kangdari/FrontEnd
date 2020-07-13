# async & await

async와 await는 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법입니다. Promise를 좀 더 간결하게 사용하게 해주고 동기적으로 실행되는 것처럼 보이기 때문에 가독성이 좋습니다.

## async & await 기본 문법

```
async function 함수() {
	await 비동기_처리_메서드()
}
```

함수 선언 앞에 `async` 키워드를 붙이고, 함수 내부에서 프로미스 객체를 반환하는 비동기 처리 메서드 앞에 `await`를 붙여야 `await`가 의도한대로 작동합니다.
(보통 await의 대상이 되는 비동기 처리 코드는 Axios, HTTP 통신 코드 등 프로미스를 반환하는 코드입니다.)

`async` 키워드가 붙으면 그 함수는 Promise를 반환합니다. `await` 키워드를 붙이면 해당 비동기 처리 코드가 수행이 완료되기 전까지 대기합니다.

## async & await 예외 처리

async & await를 예외 처리하는 방법은 try-catch문 입니다.

```
async function logTodoTitle() {
    try{
    	await 비동기_처리_메서드();
    }catch(err){
    	console.log(err);
    }
}
```

## 예제

delay 함수와 promise를 반환하는 2개의 함수가 있습니다.

```
function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function getMellon() {
  await delay(1000);
  return '🍈';
}

async function getApple() {
  await delay(500);
  return '🍎';
}
```

---

```
async function pickFruit() {
  const mellon = await getMellon(); // 1s 소요
  const apple = await getApple(); // 0.5 소요
  return `${mellon}  ${apple}`;
}

pickFruit().then(console.log) // 🍈 🍎 // 1.5s 소요
```

위 코드와 같이 작성하면 mellon을 얻는데 1s, apple을 얻는데 0.5s가 소요되기 때문에 매우 비효율적입니다.

---

Promise를 생성하면 바로 실행되는 특성을 사용하면 Promise를 병렬 처리함으로 더 효율적입니다.

```
async function pickFruit() {
  const mellonPromise = getMellon();
  const applePromise = getApple();
  const mellon = await mellonPromise;
  const apple = await applePromise;
  return `${mellon}  ${apple}`;
}
pickFruit().then(console.log) // 🍈 🍎 // 1s 소요
```

**Promise.all**을 사용하면 좀더 간결하게 병렬 처리가 가능합니다.

Promise.all은 Promise 배열을 전달받으면 그 Promise들을 병렬 수행하고 기다렸다가 그 결과를 배열 형태로 반환합니다.

```
function pickAllFruits() {
  return Promise.all([getMellon(), getApple()]).then((fruits) => fruits.join(' '));
}

pickAllFruits().then(console.log); // 🍈 🍎 // 1s 소요
```

---

**Promise.race**
Promise.race는 배열로 전달받은 Promise 중 가장 먼저 수행된 Promise의 결과를 반환합니다.

```
function pickOnlyOne() {
  return Promise.race([getMellon(), getApple()]).then((fruit) => fruit);
}

pickOnlyOne().then(console.log); // 🍈
```

[캡틴 판교](https://joshua1988.github.io/web-development/javascript/js-async-await/)
[엘리 youtube](https://www.youtube.com/watch?v=JB_yU6Oe2eE)
