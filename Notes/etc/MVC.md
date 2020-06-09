# MVC

Model + View + Controller를 합친 용어로 어플리케이션을 개발할 때 구성 요소를 세가지 역할로 구분하는 패턴.

장점: 가장 보편적으로 사용되는 패턴이며 단순

단점: view와 model이 서로 의존적

**model**
어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분

**view**
사용자에게 보여지는 UI 부분

**controller**
사용자의 입력을 받고 처리하는 부분

![](https://images.velog.io/images/ksh4820/post/3aae5462-67a1-4aef-a9ab-a65250f8283b/image.png)

사용자가 controller를 조작하면(입력) controller는 model을 통해서 데이터를 가져와 그 데이터를 바탕으로 시작적인 표현을 담당하는 view를 제어하여 사용자에게 전달한다.

## Web과 MVC

1. 사용자가 웹사이트에 접속.

2. controller는 사용자가 요청한 웹페이지를 서비스하기 위해서 model 호출.

3. model은 DB나 파일과 같은 데이터 소스를 제어한 후 결과를 리턴.

4. controller는 model이 리턴한 결과를 view에 반영.

5. 데이터가 반영된 view는 사용자에게 보여진다.

[출처](https://opentutorials.org/course/697/3828)
