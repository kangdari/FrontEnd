> How do you serve a page with content in multiple languages?

인코딩 방식을 utf-8로 설정한다.

# UTF-8

> **UTF-8**은 유니코드를 인코딩(encoding)하는 방식이다. 전세계에서 사용하는 약속이다.

예전에는 영어 문자만을 위해 ASCII가 쓰였으나 현재는 전 세계 문자와 기호를 인코딩하는데 utf-8을 사용한다. 그래서 html 문서 작성 시 head 태그 안에 `<meta charset="UTF-8">`을 작성하여 utf-8로 인코딩함을 표시한다.

utf-8로 인코딩하지 않으면 html 문서를 브라우저에세 구현할 때 글자가 깨져보이는 현상이 발생 할 수 있다.
