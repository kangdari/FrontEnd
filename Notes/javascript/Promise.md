# Promise

callback 함수로 비동기 처리를 하는 경우 callback hell이 형성되어 가독성이 떨어지거나 디버깅, 유지보수의 어려움이 있다. 이를 보완하기 위한 것이 Promise이다.

Promise는 비동기 작업을 위한 자바스크립트 객체이다. Promise는 State와 Producer, Consumer가 있다.

**State** - Promise의 진행 상태

- pending 비동기 처리 로직이 아직 완료되지 않은 상태
- fulfilled 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- rejected 비동기 처리가 실패하거나 오류가 발생한 상태

**Producer**
Producer는 원하는 기능을 수행하고 해당하는 데이터를 만든다.

- Promise가 정상적으로 수행 시 resolve를 반환한다.

- 오류가 발생하는 경우에는 reject를 반환하고 에러가 발생하는 이유를 적어두는 것이 좋다.

```
// excutor : (resolve, reject)
const promise = new Promise((resolve, reject) => {
  console.log('doing something!!');
  setTimeout(() => {
    resolve('kang');
    // reject(new Error('no network'));
  }, 1000);
});
```

**Consumer**
then, catch, finally으로 값을 처리합니다.

- then은 Promise가 정상적으로 수행했을 경우 resolve 콜백함수를 통해 전달받은 값을 파라미터로 전달받는다.

- catch는 Promise가 에러 발생 시 reject 콜백함수를 통해 전달받은 값을 파라미터로 전달받는다.

- finally는 Promise의 결과와 상관없이 마지막에 무조건 실행된다.

```
promise
  .then((value) => {
    console.log(value); // kang
  })
  .catch((err) => console.log(err))
  .finally(() => console.log('finally'));
```

## Promise chaining && error handling

```
const getHen = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('🐓');
    }, 1000);
  });
const getEgg = (hen) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      // reject(` error ${hen} => 🥚`);
      resolve(`${hen} => 🥚`);
    }, 1000);
  });
const cook = (egg) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${egg} => 🍳`);
    }, 1000);
  });
```

### Promise chaining

Prmomise는 Promise를 반환하기 때문에 then() 메서드를 호출하고 나면 새로운 프로미스 객체가 반환됩니다. 때문에 여러개의 Promise를 연결할 수 있습니다.

```
getHen()
  .then((hen) => getEgg(hen))
  .then((egg) => cook(egg))
  .then((food) => console.log(food))
  .catch((err) => console.log(err));

// 🐓 => 🥚 => 🍳 (3초 후 출력)
```

아래와 같이 간단하게 작성할 수도 있다.

```
getHen() //
  .then(getEgg)
  .then(cook)
  .then(console.log)
  .catch(console.log);

// 🐓 => 🥚 => 🍳 (3초 후 출력)
```

### error handling

catch()를 사용하여 원하는 위치에서 오류 처리가 가능하다.

```
getHen() //
  .then(getEgg)
  .catch((error) => {
    return '🍞';
  })
  .then(cook)
  .then(console.log)
  .catch(console.log);

// 🍞 => 🍳
```
