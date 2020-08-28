Javascript는 흔히 프로토타입 기반 언어(prototyped-base language)라 불린다. 모든 객체들이 메소드와 속성들을 상속받기 위한 템플릿으로써 **프로토타입 객체(prototype object)** 를 가진다는 의미이다. 프로토타입 객체도 또 다시 상위 프로토 타입 객체로부터 메소드와 속성을 상속 받을 수 있고 그 상위 프로토타입 객체도 마찬가지인다. 이를 **프로토타입 체인(prototype chain)** 이라 부르며 다른 객체에 정의된 메소드와 속성을 한 객체에서 사용할 수 있는 근간이다.

즉, 자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결되어 있다. 그리고 이것은 마치 객체 지향의 상속 개념과 같이 부모의 객체의 속성 또는 메소드를 상속받아 사용할 수 있게 한다.
이러한 부모 객체를 **Prototype Object(프로토타입 객체)** 또는 **Prototype(프로토타입)** 이라 한다.

# 프로토타입 언제 쓰나

```
function Person() {}

Person.prototype.eyes = 2;

var kang  = new Person();

console.log(kang.eyes); // => 2
```

Person.prototype이라는 빈 Object가 어딘가 존재하고, Person 함수로 부터 생성된 객체 kang은 어딘가 존재하는 Object에 들어있는 값을 모두 가져다 쓸 수 있습니다.

```
function Person(){}

var joon = new Person();
var jisoo = new Person();

Person.prototype.getType = function (){
    return "kang";
};

console.log(joon.getType());   // kang
console.log(jisoo.getType());  // kang
```

이 코드도 마찬가지로 Person.prototype을 이용해 getType 이라는 함수를 추가했고 각 joon, jisoo 객체에서 getType()을 사용할 수 있습니다.

# Prototype Link와 Prototype Object

자바스크립트에는 Prototype Link와 Prototype Object가 존재합니다. 이 둘을 통틀어 Prototype이라고 부릅니다.

![](https://images.velog.io/images/ksh4820/post/520b1f81-8753-4947-9489-58eecf770dfa/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.36.55.png)

생성된 함수는 prototype이라는 속성을 통해 Prototype Object에 접근할 수 있습니다. Prototype Object는 일반적인 객체와 같으며 기본적인 속성으로 `constructor`와 `__proto__`를 가지고 있습니다.

![](https://images.velog.io/images/ksh4820/post/85d02c49-a431-4595-8702-9f7b6c1f049d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.10.25.png)

**constructor** 는 Prototype Object와 같이 생성되었던 함수를 가르킵니다.

**`__proto__`** 는 Prototype Link입니다.

![](https://images.velog.io/images/ksh4820/post/9e78fa24-950c-48e9-b367-c457ed2eb3d8/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.12.44.png)

Prototype Object는 일반적인 객체이므로 속성을 마음대로 추가 / 삭제 할 수 있습니다.
kang은 Person 함수를 통해 생성되었으니 Person.prototype을 참조할 수 있게 됩니다.

**Prototype Link**

![](https://images.velog.io/images/ksh4820/post/d57b1174-f9c8-4d4f-9902-9d8720ce8d3d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.14.34.png)

kang에는 eyes라는 속성이 없는데도 kang.eyes는 1이라는 값을 참조합니다. 이는 위에서 설명했듯이 Prototype Object에 있는 eyes 속성 값을 참조한 것입니다. 어떻게 이게 가능할까 ??

바로 kang 객체가 가지고 있는 `__proto__`가 이것을 가능하게 해줍니다.

`__proto__` 속성은 모든 객체가 가지고 있는 속성입니다.

**`__proto__`는 객체가 생성될 때 부모였던 함수의 Prototype Object를 가르킵니다.** 즉, kang 객체는 Person 함수로부터 생성되었으니 Person 함수의 Prototype Object를 가르킵니다.

![](https://images.velog.io/images/ksh4820/post/eee4b48a-03c9-44d7-ae07-99546cb0776c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.19.05.png)

kang 객체는 eyes 속성을 직접 가지고 있지 않기 때문에 eyes 속성을 찾을 때까지 상위 프로토 타입을 탐색합니다. 최상위 Object의 Prototype Object까지 도달했는데도 못찾을 경우 `undefined`를 반환합니다. **이렇게 `__proto__` 속성을 통해 상위 프로토타입과 연결되어 있는 형태를 프로토타입 체인(prototype chain)** 이라고 합니다.

![](https://images.velog.io/images/ksh4820/post/4c1710ac-b827-458d-b2be-9ce5b6421524/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.21.40.png)

이러한 프로토타입 체인 구조 때문에 모든 객체는 Object의 자식이라고 불리고, Object Prototype에 있는 모든 속성을 사용할 수 있습니다.

![](https://images.velog.io/images/ksh4820/post/6369edda-e4b3-4a83-9008-92cb9165d89a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.22.58.png)

[[Javascript ] 프로토타입 이해하기](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67)
