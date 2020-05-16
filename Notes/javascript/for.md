## 기존 for문

기존에 사용하던 for문 입니다.

```
const arr = [1,2,3]

for(let i=0; i<arr.length; i++){
    console.log(arr[i])
}
// 1, 2, 3
```

## forEach

* ES5에서 추가됨.

* **return 혹은 break를 통해 루프 탈출이 불가능합니다.**

```
arr.forEach(item => console.log(item))
// 1, 2, 3
```

## for..in

* ES5에서 추가됨.

* **객체의 프로퍼티를 순회하기 위해 만들어진 문법**

```
const object = { a: 1, b: 2, c: 3 };

for (const property in object) {
  console.log(`${property}: ${object[property]}`);
}
// a: 1
// b: 2
// c: 3
```

## for..of
* ES6에서 추가됨.

* **배열의 data를 순회하기 위한 문법**

* iterable한, 반복 가능한 객체들에서 사용이 가능.(Array, Set, Map, String...)

* **return, break문을 사용하여 루프문 탈출이 가능.**

```
const arr = [10, 20, 30]

for(let item of arr){
    console.log(item)
}
// 10 20 30
```

```
let iterable = new Map([["a", 1], ["b", 2], ["c", 3]]);

for (let entry of iterable) {
  console.log(entry);
}
// [a, 1]
// [b, 2]
// [c, 3]
```

**배열 or iterable객체는 for...of문 // 객체는 for...in문**