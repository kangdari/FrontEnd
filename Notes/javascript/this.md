# this

자바스크립트 함수는 호출될 때, 매개변수로 전달되는 인자값 이외에도, arguments 객체와 `this`를 암묵적으로 전달 받는다.

자바스크립트의 `this`는 Java와 `this`와 다르다.
Java에서의 `this`는 인스턴스 자신(Self)을 가르키는 참조변수이다. this가 객체 자신에 대한 참조값을 가지고 있다는 뜻이다. 하지만 자바스크립트의 경우 **함수를 호출할 때 함수가 어떻게 호출되었는지에 따라** `this`에 바인딩할 객체가 동적으로 결정된다.

---

브라우저에서 this를 쳐보면 Window가 나온다.

```
this; // Window {}
```

함수 안에서 this를 쳐보면 마찬가지로 Window가 나온다.

```
function foo() {
  console.log(this);
}
foo(); // Window {}
```

기본적으로 this는 Window이다.

---

그럼 this가 Window가 아닌 경우를 알아보자.

객체의 메서드 a의 this는 객체를 가르킨다. 이것은 객체의 메서드를 호출할 때 this를 내부적으로 바꿔주기 때문이다.

```
const obj = {
  a: function () {
       console.dir(this);
  },
};
obj.a(); // Object
```

obj의 a 메서드를 b에 할당해주면 결과는 달라진다.

```
var b = obj.a;
b(); // window
```

호출할 때, 호출하는 함수가 객체의 메서드인지 그냥 함수인지가 중요하다. b는 obj.a를 꺼내왔기 때문에 더 이상 obj의 메서드가 아니므로 window가 나온다

---

명시적으로 this를 바꾸는 함수 bind, call, apply를 사용하면 this가 객체를 가르킨다.

```
const obj2 = { c: 'd' };
function b() {
  console.log(this);
}
b();
b.bind(obj2).call(); // obj2
b.call(obj2); // obj2
b.apply(obj2); // obj2
```

---

생성자 함수도 함수.

```
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.sayHi = function () {
  console.log(this.name, this.age);
};
```

new를 호출하지 않고 그냥 사용할 경우 this는 window를 가르킵니다.

```
Person('kang', '27');
console.log(window.name, window.age); // kang 27
```

이를 막기 위해서는 new 키워드를 사용해야합니다.

```
const man = new Person('kim', '27');
man.sayHi(); // kim 33
```

new를 붙이면 this가 생성자를 통해 생성된 인스턴스 man 자기 자신을 가르킵니다.

---

```
document.body.onclick = function () {
  console.log(this); // body
};
```

그냥 함수인데도 this가 window가 아니라 body를 가르킵니다. 이는 이벤트가 발생할 때 내부적으로 this가 바뀐 것입니다. 외우랍니다.

---

방금적 클릭 이벤트에서 내부적으로 this를 바꾼다고 했으나 내부함수 inner 호출 시 this는 window를 가르킵니다. inner는 함수이기 때문에...

```
document.body.onclick = function () {
  console.log(this); // body
  function inner() {
    console.log(this); // Window
  }
  inner();
};
```

이를 해결하기 위해서는 변수에 this를 저장하여 사용하던가

```
document.body.onclick = function () {
  const that = this;
  function inner() {
    console.log(that);
  }
  inner(); // body
};
```

ES6 화살표 함수를 사용하면 됩니다. 화살표 함수는 this를 window 대신 상위 함수의 this를 가져옵니다.

```
document.body.onclick = function () {
  const inner = () => console.log(this);
  inner(); // body
};
```

## 정리

- 자바스크립트에서 this는 기본적으로 window이다.
- 하지만 객체 메서드, bind, call, apply, new일 때는 this가 바뀐다.
- 이벤트 리스터나 기타 라이브러리는 this를 내부적으로 바꿀 수도 있으니 항상 this를 확인해야한다.
- 화살표 함수의 this는 상위 함수의 this를 가르킨다.

[자바스크립트의 this는 무엇인가?](https://www.zerocho.com/category/JavaScript/post/5b0645cc7e3e36001bf676eb)
