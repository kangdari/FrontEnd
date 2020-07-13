# Asynchronous(비동기) Synchronous(동기)

둘의 차이는 **결과물을 가져오는 시점**이 다르다.

---

- 자바스크립트는 synchronous입니다.
- 호이스팅이 된 이후 부터 순서대로 코드를 실행합니다.
- 호이스팅은 변수와 함수 선언이 자동적으로 제일 위로 올라가는 것.
  (함수 표현식, 화살표 함수는 호이스팅 되지 않습니다.)

## **Synchronous**

- 요청과 결과가 **동시에 일어난다**. 즉, 요청을 하면 시간이 얼마나 걸리든 요청한 위치에서 결과가 올 때까지 대기해야한다.

![동기](https://images.velog.io/images/ksh4820/post/73f26b7a-9eb4-4d52-ad2c-8a1298a60fde/synchronous.JPG)

[이미지 출처](https://jieun0113.tistory.com/73)

Synchronous는 순서대로 실행되기 때문에 결과가 예측됩니다.

```
console.log('1')
console.log('2')
console.log('3')

// 1 2 3
```

## **Asynchronous**

- 요청과 결과가 **동시에 일어나지 않는다**. 즉, 요청을 보낸 후 응답(결과)과 상관없이 다음 작업이 진행된다.

- 비동기식 처리를 요청할 때는 할 일이 끝난 후 처리 결과를 알려주는 콜백 함수를 함께 알려준다. 이 콜백 함수를 통해 결과물을 가져온다.

![비동기](https://images.velog.io/images/ksh4820/post/20bae4bc-ffb9-49a2-b97c-babe784c1792/asynchronous.JPG)

[이미지 출처](https://jieun0113.tistory.com/73)

Asynchronous는 요청의 처리가 끝난 뒤 콜백 함수가 실행되기 때문에 정확한 실행 시점을 알 수 없습니다.

```
console.log('1'); // sync
setTimeout(() => {
  console.log('2'); // async
}, 1000);
console.log('3'); // sync

1 3 2(1s 후)
```

## Callback

콜백은 다른 코드의 인수로 넘겨진 실행 가능한 코드를 말합니다. 넘겨받은 콜백은 즉시 실행할 수도 있고 나중에 실행할 수도 있습니다.

```
console.log('1'); // sync
setTimeout(() => {
  console.log('2'); // async
}, 1000);
console.log('3'); // sync

// Synchronous Callback, 동기 콜백
function printImmediately(print) {
  // 함수 선언식은 호이스팅에 의해 제일 위로 올라감.
  print();
}

printImmediately(() => console.log('hello')); // sync

// Asynchronous Callback, 비동기 콜백
function printWithDelay(print, timeout) {
  setTimeout(print, timeout);
}

printWithDelay(() => console.log('async Callback'), 1000); // async

// output
// 1
// 3
// hello
// 2
// async Callback
```

## Callback hell

콜백지옥은 비동기 프로그래밍시 발생하는 문제로 함수의 매개 변수로 넘겨지는 콜백 함수가 반복되어 코드의 들여쓰기 수준이 감당하기 힘들 정도로 깊어지는 현상을 말합니다.
가독성이 안좋고 디버깅, 유지보수가 어려워집니다.

```
step1(function (value1) {
    step2(function (value2) {
        step3(function (value3) {
            step4(function (value4) {
                step5(function (value5) {
                    step6(function (value6) {
                        // Do something with value6...
                    });
                });
            });
        });
    });
});
```

### 실행 예제

로그인을 위해 서버에 요청하는 방식과 비슷하게 구현하기 위해서 class를 이용했습니다.

```
class UserStorage {
  loginUser(id, password, onSuccess, onError) {
    setTimeout(() => {
      if ((id === 'kang' && password === '123') || (id === 'dari' && password === '123')) {
        onSuccess(id);
      } else {
        onError(new Error('login failed'));
      }
    }, 1000);
  }

  getRoles(user, onSuccess, onError) {
    setTimeout(() => {
      if (id === 'kang') {
        onSuccess({ name: 'kang', role: 'admin' });
      } else {
        onError(new Error('no access'));
      }
    }, 500);
  }
}
```

브라우저에서 id와 password 값을 입력받고 그 값을 비교하여 로그인 성공 시 해당 유저의 role을 반환해주는 코드입니다. ( 가독성 안좋아... )

```
const userStorage = new UserStorage();
const id = prompt('id');
const password = prompt('password');

userStorage.loginUser(
  id,
  password,
  (userId) => {
    userStorage.getRoles(
      userId,
      (userWithRole) => {
        alert(`hello ${userWithRole.name}, your role is ${userWithRole.role} `);
      },
      (error) => {
        console.log(error);
      }
    );
  },
  (error) => {
    console.log(error);
  }
);
```

promise를 사용하여 callback 지옥 벗어나기

```
class UserStorage {
  loginUser = (id, password) =>
    new Promise((resolve, reject) => {
      setTimeout(() => {
        if ((id === 'kang' && password === '123') || (id === 'dari' && password === '123')) {
          resolve(id);
        } else {
          reject(new Error('login failed'));
        }
      }, 1000);
    });

  getRoles = (user) =>
    new Promise((resolve, reject) => {
      setTimeout(() => {
        if (user === 'kang') {
          resolve({ name: 'kang', role: 'admin' });
        } else {
          reject(new Error('no access'));
        }
      }, 1000);
    });
}

const userStorage = new UserStorage();
const id = prompt('id');
const password = prompt('password');

userStorage
  .loginUser(id, password)
  .then(userStorage.getRoles)
  .then((user) => alert(`hello ${user.name}, your role is ${user.role} `))
  .catch(console.log);

```
