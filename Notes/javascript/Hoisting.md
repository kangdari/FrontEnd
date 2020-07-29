# 호이스팅(Hoisting)

코드에서 작성한 변수 및 함수 **선언**이 코드의 상단으로 옮겨지는 것으로 자바스크립트는 실행시점에 변수와 함수에 대해서 호이스팅을 수행합니다.

## var

```
console.log(a); // undefined
var a = 10;
```

위 코드를 보면 첫 줄에서 a값에 대해 ReferenceError가 아닌 undefined가 출력됩니다. 왜냐하면 실행시점에 호이스팅에 의해서 var 변수가 아래 코드와 같이 최상단에서 선언되기 때문입니다.

```
var a;
console.log(a);
a = 10;
```

기존의 자바스크립트에서는 호이스팅으로 인해서 변수나 함수가 코드 하단에 선언되어 있어도 코드 상단 부분에서 호출하여도 에러가 발생하지 않았습니다. 이는 에러를 찾아 고치기 힘든 상황이 발생할 수 있습니다. 그래서 ES6에서는 기존의 vard와 함수 선언문에 대해서는 그대로 유지하되 let과 const에서는 위와 같이 동작하지 않도록 하였습니다.

## const와 let

**TDZ(Temporal Dead Zone)(임시 사각지대)**
const, let에 대해서 실제로 변수가 선언된 위치가 오기 전에 해당 변수를 호출할 수 없음.

const와 let도 호이스팅이 되지만 var와는 조금 다르게 실행됩니다.

```
const a = 10; // 전역 변수
{
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 20; // 지역 변수
}
```

a 변수를 전역변수로 선언했지만 ReferenceError가 발생했습니다. 이는 {} 내부에서 let으로 선언된 a 변수가 호이스팅 되었기 때문입니다. 만약 let a 변수가 호이스팅 되었지 않았더라면 console.log의 결과는 10이 출력되었을겁니다. 즉, 호이스팅은 하되 값은 할당하지 않습니다.

const와 let도 호이스팅이 된다는 것을 확인했습니다. 하지만 var와는 다르게 왜 undefined 아닌 ReferenceError를 출력할까요???

이를 이해하기 위해서는 자바스크립트에서 변수가 어떻게 할당되는지 알아야합니다.

## 변수 선언단계

1. 선언단계 : 변수를 실행컨텍스트의 변수객체에 등록한다.
2. 초기화 단계 : 실행 컨텍스트에 등록 된 변수객체에 대한 메모리를 할당한다. 이 단계에서 변수는 undefined로 초기화 된다.
3. 할당단계 : undefined로 초기화 된 변수에 값을 할당한다.

var로 선언된 변수는 선언과 초기화 단계가 동시에 진행됩니다. 그렇기 때문에 undefined를 출력합니다.

반면에 const와 let은 선언과 초기화 단계가 분리되어 진행됩니다. 호이스팅 되었을 때 선언단계가 진행되고 실제 const와 let으로 선언된 위치(**TDZ**)에 와야 초기화 단계가 진행됩니다. 그래서 초기화가 아직 이루어지지 않은 변수에 접근했기 때문에 ReferenceError가 발생합니다.

## 함수 선언식과 함수 표현식

**함수 선언식은 호이스팅에 영향을 받지만, 함수 표현식은 호이스팅에 영향을 받지 않는다.**

```
a1(); // a2
a2(); // TypeError: a is not a function

function a1() {
  console.log('a1');
}

var a2 = function () {
  console.log('a2');
};
```

호이스팅에 의해 자바스크립트 해석기는 아래와 같이 인식한다.

```
function a1() {
  console.log('a1');
}

var a2;

a1(); // a2
a2(); // TypeError: a is not a function

a2 = function () {
  console.log('a2');
};
```

함수 선언식은 호이스팅에 의해 코드 최상단에서 선언되므로 문제가 없다.

하지만 함수 표현식의 경우 var로 선언된 a2는 호이스팅 되었지만 a에 실제 할당될 function() 로직은 호출된 이후에 선언되므로 a는 함수가 아닌 변수로 인식된다. 때문에 TypeError가 발생한다.
