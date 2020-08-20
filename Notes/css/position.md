# position

- 해당 태그 요소의 위치를 어디를 기준으로 위치시킬것인지 기준 대상을 정하는 속성

- static, relative, absolute, fixed, sticky(IE 지원 x)

- position은 left, right, top, bottom 속성과 함께 사용하여 위치를 지정할 수 있다.
  단, position: static 경우 적용되지 않는다.

- z-index 속성은 static을 제외한 absolute, relative, fixed, sticky 상태에서 적용된다.

## static

- 기본값

- left, right, top, bottom 속성이 적용 안됨.

- z-index 속성이 적용 안됨.

## relative

- static일 때의 해당 요소 위치를 기준으로 한다.

- 방향 속성을 사용하여 위치를 설정할 수 있다.

## absolute

- 부모 요소의 위치를 기준으로 한다.
  단, 부모 요소는 relative, absolute, fixed 속성 중 하나를 가져야 한다.

- 부모 요소가 position 속성을 가지고 있지 않다면 브라우저 창을 기준으로 한다.

- 방향 속성을 사용하여 위치를 설정할 수 있다.

## fixed

- 브라우저 창을 기준으로 한다.

- 방향 속성을 사용하여 위치를 설정할 수 있다.

## sticky

- relative처럼 작동하다가 스크롤 시 설정해둔 위치에 도달 시 고정된다.

- IE에서는 지원하지 않는다.
