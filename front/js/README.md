## ECMA5와 ECMA6 차이점

ECMA Script란?
자바스크립트는 여러 개발사에서 많이 사용되어 하나의 표준이 필요하기 때문에 그 표준으로 정의 된 것을
ECMA Script라고 한다.


### ES5 (2009)
1. 배열에 forEach, map, filter, reduce, some, every와 같은 메소드 지원

2. Object에 대한 getter/setter 지원

3. 자바스크립트 strict 모드 지원

=> strict 모드란? 더 깐깐한 문법 검사를 한다.

### strict모드

strict 모드는 ES5에서 추가 된 키워드

strict 모드는 자바스크립트가 묵인했던 에러들의 에러 메시지를 발생시킨다.

엄격하게 문법 검사를 하겠다로 이해하면 된다!!

(1) strict 모드 선언
스크립트의 시작 혹은 함수의 시작 부분에 "use strict" (또는 싱글 쿼테이션으로 감싸도 동일하다.)를 선언하면 strict 모드로 코드를 작성할 수 있다.

### 스크립트에서 strict 선언
![image](https://user-images.githubusercontent.com/57930450/70769045-39874180-1dab-11ea-9ed4-5a25d5b41d86.png)

### 함수에서 strict 선언
![image](https://user-images.githubusercontent.com/57930450/70769204-e6fa5500-1dab-11ea-951f-1ec43979d97f.png)

(2) strict 모드 변화
strict 모드는 문법과 런타임 동작을 모두 검사하여, 실수를 에러로 변화하고, 변수 사용을 단순화(Simplifying) 시켜준다.

실수를 에러로 변환 (Converting mistakes into errors)

자바스크립트는 오류를 어느 정도 무시하고 넘어갈 수 있다.
이것이 편하게 코딩을 할 수 있게 하지만, 때로는 심각한 버그를 만들게 된다. strict 모드는 이러한 실수를 에러로 변화하여 즉시 수정할 수 있게 한다.

4. JSON 지원 (과거에는 XML을 사용하다가, json이 뜨면서 지원하게 됨.)


### ES 2015 (ES6)
1. let, const 키워드 추가
기존의 변수는 함수 scope를 가진 var 키워드를 이용하여 선언하였다.
때문에 block scope를 가진 let과 const 키워드를 추가하였다. 
기존에는 상수형 키워드가 없어 CONST_TEST와 같이 대문자로 상수임을 표시했다면, ES6부터 const 키워드가 추가되어 값의 변경을 통제한다.

2. arrow 문법 지원
arrow 문법은 두 가지의 장점을 제공한다. 첫 번째는 익숙하면 편하고 간결해진 코드를 작성할 수 있다.

### 화살표 함수
기존 함수 선언문은 읽고, 쓰기 쉽게 되어있었다.
하지만 함수 네스팅이 시작되면 선언문 자체가 불필요하게 느껴지고, 햇갈리게 된다.

~~~script
            function sayHello(name) {
                console.log('Hello', name);
            }

            setTimeout(function() {
                console.log('Loaded')
            }, 2000);

            list.forEach(function(item) {
                 console.log(item);
             });

            // 축약기법
 
             sayHello = name => console.log('Hello', name);
             
             setTimeout(() => console.log('Loaded'), 2000);

             list.forEach(item => console.log(item));
~~~

애로우 함수 표기법에서는 thi 가 기존의 함수 선언문과 다르게 받아들여진다.

