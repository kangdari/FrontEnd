# 모듈

개발하는 애플리케이션의 크기가 커지면 언젠가 파일을 여러 개로 분리해야 하는 시점이 옵니다. 이때 분리된 파일을 각각 모듈(module)이라고 부릅니다.

## 모듈 시스템의 등장

웹 개발 초기에는 스크립트의 크기도 작고 기능도 단순했기 때문에 모듈을 중요시하지 않았습니다. 하지만 스크립트의 크기가 점점 커지고 기능도 복잡해지면서 특별한 라이브러리를 만들어 필요한 모듈을 언제든지 쉽게 불러올 수 있도록 코드를 모듈 단위로 구성해주는 방법을 시도합니다.
ex) AMD, CommonJS, UMD# 모듈
개발하는 애플리케이션의 크기가 커지면 언젠가 파일을 여러 개로 분리해야 하는 시점이 옵니다. 이때 분리된 파일을 각각 모듈(module)이라고 부릅니다.

## 모듈 시스템의 등장

웹 개발 초기에는 스크립트의 크기도 작고 기능도 단순했기 때문에 모듈을 중요시하지 않았습니다. 하지만 스크립트의 크기가 점점 커지고 기능도 복잡해지면서 특별한 라이브러리를 만들어 필요한 모듈을 언제든지 쉽게 불러올 수 있도록 코드를 모듈 단위로 구성해주는 방법을 시도합니다.
ex) AMD, CommonJS, UMD

이후 ECMA2015(ES6)가 도입되면서 새로운 모듈 시스템이 등장합니다.

# 모듈 활용법

모듈을 내보낼 때는 **export**, 가져올 때는 **import**를 사용합니다.

## named export

모듈을 내보내는 가장 쉬운 방법입니다. 내보내려는 항목 앞에 export 지시자를 배치합니다. 그 항목이 변수, 함수, 클래스 인지는 상관없습니다.

```
// 배열
export const name = ["kang", "kim", "Ryu"];

// 함수
export const sayHello = (name) => console.log(name);

// 클래스
export class User {
  constructor(name) {
    this.name = name;
  }
}
```

위와 같이 하나씩 내보내지 않고 모듈 최하단에서 {}로 묶어 한번에 내보낼 수 있습니다.

```
export { name, sayHello, User };
```

as를 사용하여 원하는 이름으로 변경하여 내보낼 수 있습니다.

```
export { name as name_arr };
```

## named import

named export로 내보내진 모듈은 **import**를 통해 가져올 수 있습니다.
import 뒤 중괄호에 가져올 모듈의 이름을 적고 from 뒤에는 가져올 모듈의 경로를 작성합니다.

**경로 뒤에는 .js 확장자 명을 작성해야합니다.**(IDE에 따라서 작성하지 않아도 되는 경우가 있습니다.)

```
import { name, sayHello, User } from './export.js'

sayHello('kang'); // kang
```

import에서도 as를 사용하여 원하는 이름으로 변경하여 모듈을 가져올 수 있습니다.

\*는 해당 경로의 모든 모듈을 의미합니다.

```
import * as all_module from './export'
```

## default export

보통 단 하나만 export할 경우나, 다른 export보다 중요도가 높은 경우 주로 사용합니다.

이 경우 이름없는 함수나 클래스 등도 보낼 수 있습니다.

```
export default (name) => console.log(name);
```

## default import

default export로 내보내진 모듈은 중괄호 없이 가져올 수 있고 import한 파일에서 원하는 이름으로 설정하여 사용이 가능합니다.

```
import sayHello from "./print.js";

sayHello("kang"); // kang
```

## HTML에서 module 적용하기

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>module</title>
  </head>
  <body>
    <h1>test</h1>
    <script type="module" src="app.js"></script>
  </body>
</html>
```

`<script type="module" src="app.js"></script>` script 태그에 `type="module"`을 설정합니다.

type 속성 값을 설정하지 않는다면
`Uncaught SyntaxError: Cannot use import statement outside a module`
해당 오류가 발생합니다.

[참고 사이트](https://velog.io/@takeknowledge/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%AA%A8%EB%93%88-%ED%95%99%EC%8A%B5-%EB%82%B4%EC%9A%A9-%EC%9A%94%EC%95%BD-lwk4drjnni#-%EB%AA%A8%EB%93%88module%EC%9D%B4%EB%9E%80)

이후 ECMA2015(ES6)가 도입되면서 새로운 모듈 시스템이 등장합니다.

# 모듈 활용법

모듈을 내보낼 때는 **export**, 가져올 때는 **import**를 사용합니다.

## named export

모듈을 내보내는 가장 쉬운 방법입니다. 내보내려는 항목 앞에 export 지시자를 배치합니다. 그 항목이 변수, 함수, 클래스 인지는 상관없습니다.

```
// 배열
export const name = ["kang", "kim", "Ryu"];

// 함수
export const sayHello = (name) => console.log(name);

// 클래스
export class User {
  constructor(name) {
    this.name = name;
  }
}
```

위와 같이 하나씩 내보내지 않고 모듈 최하단에서 {}로 묶어 한번에 내보낼 수 있습니다.

```
export { name, sayHello, User };
```

as를 사용하여 원하는 이름으로 변경하여 내보낼 수 있습니다.

```
export { name as name_arr };
```

## named import

named export로 내보내진 모듈은 **import**를 통해 가져올 수 있습니다.
import 뒤 중괄호에 가져올 모듈의 이름을 적고 from 뒤에는 가져올 모듈의 경로를 작성합니다.

**경로 뒤에는 .js 확장자 명을 작성해야합니다.**(IDE에 따라서 작성하지 않아도 되는 경우가 있습니다.)

```
import { name, sayHello, User } from './export.js'

sayHello('kang'); // kang
```

import에서도 as를 사용하여 원하는 이름으로 변경하여 모듈을 가져올 수 있습니다.

\*는 해당 경로의 모든 모듈을 의미합니다.

```
import * as all_module from './export'
```

## default export

보통 단 하나만 export할 경우나, 다른 export보다 중요도가 높은 경우 주로 사용합니다.

이 경우 이름없는 함수나 클래스 등도 보낼 수 있습니다.

```
export default (name) => console.log(name);
```

## default import

default export로 내보내진 모듈은 중괄호 없이 가져올 수 있고 import한 파일에서 원하는 이름으로 설정하여 사용이 가능합니다.

```
import sayHello from "./print.js";

sayHello("kang"); // kang
```

## HTML에서 module 적용하기

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>module</title>
  </head>
  <body>
    <h1>test</h1>
    <script type="module" src="app.js"></script>
  </body>
</html>
```

`<script type="module" src="app.js"></script>` script 태그에 `type="module"`을 설정합니다.

type 속성 값을 설정하지 않는다면
`Uncaught SyntaxError: Cannot use import statement outside a module`
해당 오류가 발생합니다.

[참고 사이트](https://velog.io/@takeknowledge/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%AA%A8%EB%93%88-%ED%95%99%EC%8A%B5-%EB%82%B4%EC%9A%A9-%EC%9A%94%EC%95%BD-lwk4drjnni#-%EB%AA%A8%EB%93%88module%EC%9D%B4%EB%9E%80)
