# null과 undefined

## null

- null은 비어있거나 존재하지 않는 값을 나타낸다.

- null은 할당되어야 존재할 수 있는 값이다.

```
const a = null;

console.log(a) // null
```

## undefined

- 선언된 변수에 값 할당이 이루어지지 않았음을 나타낸다.

```
let b;
console.log(b); // undefined

let c = undefined;
console.log(c); // undefined
```

- 존재하지 않는 값을 참조시 undefined가 출력된다.

```
let d = {}

console.log(d.value) // undefined
```

## 비교법

이런 차이가 있음에도 불구하고 null과 undefined는 포괄적으로 둘 다 값이 없음을 가리킨다.
동등연산자(==)를 사용하면 두 값은 같다고 간주되기 때문에 엄격한 일치연산자(===)를 사용해야한다.

```
null == undefined // true

null === undefined // false
```
