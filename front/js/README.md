## 호이스팅
함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것을 말한다.

-"스크립트단에서 선언해둔 함수들이 브라우저에서 렌더링 된 후에 해당 함수 유효 범위의 최상단에 선언 되는 것."

- 자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 유효 범위의 최상단에 선언한다.
    => 자바스크립트 Parser가 함수 실행 전에 해당 함수를 한 번 훑는다.
    => 함수 안에 존재하는 변수 / 함수 선언에 대한 정보를 기억하고 있다가 실행시킨다.
    => 유효 범위 : 함수 블록  {} 안에 유효
    
- 즉, 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것이다.
    => 실제로 코드가 끌어올려지는건 아니며, 자바스크립트 Parser가 내부적으로 끌어올려서 처리하는 것.
    => 실제 메모리에서는 변화가 없음.
    
### 호이스팅의 대상
var 변수 선언과 함수 선언문에서만 호이스팅이 일어난다.
    => var 변수 / 함수의 선언만 위로 끌어 올려지며, 할당은 끌어 올려지지 않는다.
    => let / const 변수 선언과 함수 표현식에서는 호이스팅이 발생하지 않는다.
 
~~~script
            console.log("Hello");

            var test = "TestCase";
            
            let test = "TestCase2";
~~~

~~~script
            // JS Parser 내부의 호이스팅의 결과
            var test; // 호이스팅으로 인해서 console.log보다 함수 선언이 최상위로 끌어올려졌다.

            console.log("Hello");

            test = "TestCase"; // 할당
            
            let test = "TestCase2"; // 호이스팅이 발생하지 않는다.
~~~

~~~script
            // 함수선언문 VS 함수표현식

            foo();

            foo2();

            function foo() {
                console.log("TESTCASE");
            }

            var foo2 = function() {
                console.log("TESTCASE2");
            }
~~~

~~~script
            // JS Parser 내부의 호이스팅 결과

            var foo2; // 호이스팅으로 표현식의 변수값 선언만 최상단으로 끌어올려진다.

            function foo() { // 호이스팅 된 함수 선언문
                console.log("TESTCASE");
            }

            foo();
            
            foo2(); // 에러

            foo2 = function() {
                console.log("TESTCASE2");
            }          
~~~

호이스팅은 함수 선언문과 함수 표현식에서 서로 다르게 동작하기 때문에 주의해야 한다.
    => 변수에 할당 된 함수표현식은 끌어 올려지지 않기 때문에 이 때는 변수의 스코프 규칙을 그대로 따른다.


### 함수 선언문과 함수 표현식에서의 호이스팅

함수 선언문에서의 호이스팅 
함수 선언문은 코드를 구현한 위치와 관계없이 자바스크립트의 특징인 호이스팅에 따라 브라우저가 자바스크립트를 해석할 때 맨위로 끌어올려진다.

~~~script
            // 함수 선언문에서의 호이스팅
            function printName(firstname) {
                var result = inner(); // 선언 및 할당
                
                console.log(typeof inner); // function 출력
                console.log("name is " + result); // result는 undefined로 출력됨.

                function inner() {
                    return "inner value";
                }
            }

            printName(); // 함수 호출
~~~

~~~script
            // JS Parser 내부의 호이스팅 결과

            function printName(firstname) {
                var result; // 호이스팅 var 변수 선언

                function inner() { // 호이스팅 함수 선언문
                    return "innser value";

                }

                result = inner(); // 할당
                
                console.log(typeof inner);
                console.log("name is " + result);
            }

            printName();
~~~

즉 해당 예제에서는 함수 선언문이 아래에 있어도 printName 함수 내에서 inner를 function으로 인식하기 때문에 오류가 발생하지 않는다. 

### 함수 표현식에서의 호이스팅

함수표현식은 함수선언문과 달리 선언과 호출 순서에 따라서 정상적으로 함수가 실행되지 않을 수 있다.

=> 함수 표현식에서는 선언과 할당의 분리가 발생한다.

1. 함수표현식의 선언이 호출보다 위에 있는 경우 - 정상 출력
~~~script
            function printName(firstname) { // 함수 선언문
                var inner = function() { // 함수 표현식
                    return "inner value";

                }

                var result = inner(); // 함수 "호출"
                console.log("name is " + result);
            }

            printName();
~~~

~~~script
            // JS Parser 내부의 호이스팅의 결과
            function printName(firstname) {
                var inner; // 호이스팅 함수 표현식의 변수값 선언
                var result; // 호이스팅 var 변수값 선언

                inner = function() { // 함수 표현식 할당
                    return "inner value";
                }

                result = inner(); // 함수 호출

                console.log("name is " + result);
            }

            printName();
~~~

2. 함수표현식의 선언이 호출보다 아래에 있는 경우 (var 변수에 할당) - TypeError 중요!!!!

~~~script
            // 함수표현식 에러 선언이 호출보다 아래에 있는 경우

            function printName(firstname) { // 함수 선언문
                console.log(inner); // "undefined" : 선언은 되어 있지만 갑싱 할당되어 있지 않은 경우.

                var result = inner(); // 에러
                
                console.log("name is " + result);
                
                var inner = function() {
                    return "inner value";
                }
            }
~~~
~~~script
            // JS Parser 내부의 호이스팅
            function printName(firstname) {

                var inner; // 호이스팅 함수 표현식의 변수값 선언

                console.log(inner); // undefined

                var result = inner(); // 에러

                console.log("name is " + result);

                inner = function() {
                    return "inner value";
                }
            }

            printName(); // 타입에러
~~~

printName에서 "inner is not defined"이라고 오류가 나오지 않고, "inner is not a function"이라는 TypeError가 나오는 이유?

printName 이 실행되는 순간 (호이스팅에 의해) inner는 undefined으로 지정되기 때문

inner가 undefined라는 것은 즉, 아직은 함수로 인식이 되지 않고 있다는 것을 의미한다.

3. 함수표현식의 선언이 호출보다 아래에 있는 경우 (const / let 변수에 할당) ReferenceError
~~~script
            function printName(firstname) { // 함수 선언문
                console.log(inner); // 에러
                
                let result = inner();

                console.log("name is "  + result);

                let inner = function() { // 함수 표현식
                    return "inner value";
                }
            }
~~~

let / const의 경우, 호이스팅이 일어나지 않기 때문에 위의 예시 그대로 이해하면 된다.

console.log(inner);에서 inner에 대한 선언이 되어있지 않기 때문에 이때는 "inner is not defined" 오류가 발생한다.

함수 표현식보다 함수 선언문을 더 자주 사용하지만, 어떤 코딩 컨벤션에서는 함수 표현식을 권장하기도 한다.

즉, 어떤 컨벤션을 갖던지 한 가지만 정해서 사용하는게 좋다.

### 호이스팅 우선순위
같은 이름의 var 변수 선언과 함수 선언에서의 호이스팅
- 변수 선언이 함수 선언보다 위로 끌어올려진다.

~~~script
            // 2. 호이스팅 함수 선언문
            function testName() {
                console.log("JS");
            }

            function testName2() {
                console.log("front");
            }

            // 3. 변수값 할당            
            testName = "Hi";
            testName2 = "Bye";

            console.log(typeof testName);
            console.log(typeof testName2);
~~~

~~~script
            // JS Parser 내부의 호이스팅
            var testName;
            var testName2;

            // 2. 호이스팅 함수 선언문
            function testName() {
                console.log("JS");
            }

            function testName2() {
                console.log("front");
            }

            // 3. 변수값 할당            
            testName = "Hi";
            testName2 = "Bye";

            console.log(typeof testName);
            console.log(typeof testName2);
~~~

TIP 호이스팅 사용시 주의
- 코드의 가독성과 유지보수를 위해 호이스팅이 일어나지 않도록 한다.
   => 호이스팅을 제대로 모르더라도 함수와 변수를 가급적 코드 상단부에서 선언하면, 호이스팅으로 인한
   스코프 꼬임 현상은 방지할 수 있다.
   
- var를 쓰면 혼란스럽고 쓸모없는 코드가 생길 수 있다. 그럼 왜 var와 호이스팅을 이해해야 할까?
   => ES6를 어디에서든 쓸 수 있으려면 아직 시간이 더 필요하므로 ES5로 트랜스 컴파일을 해야 한다.
   => 따라서 아직은 var가 어떻게 동작하는지 이해하고 있어야 한다.





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

애로우 함수 표기법에서는 this 가 기존의 함수 선언문과 다르게 받아들여진다.

3. iterator / generator 추가


4. module import / export 추가

5. Promise 도입



