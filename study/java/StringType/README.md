String 정리
========================

## String 
- 짧은 문자열을 더할 경우
- 제일 느림

## StringBuffer
- **스레드 세이프** 해야 할 경우 사용
- 동기화(synchronization)를 지원하여 멀티 스레드 환경에서 안전하게 동작함.

## StringBuilder
- 스레드 세이프 하지 않아도 될 때 사용
- 가장 빠름
- 동기화(synchronization)를 지원하지 않음.

## StringBuffer, StringBuilder가 String보다 성능이 좋은 이유와 원리
String 클래스가 StringBuffer, StringBuilder보다 느리고 메모리 관리 측면에서도 큰 차이를 보인다.
따라서 문자열의 더하기 연산을 이용할 때는 StringBuilder의 사용을 고려해봐야 한다.

StringBuffer와 StringBuilder는 기능이 동일하지만 한 가지 차이점이 존재한다.

바로 동기화 처리 문제이다.

## 문자열을 추가하는 연산에서 String가 느린 이유
String 클래스가 StringBuffer와 StringBuilder보다 느린 이유는 뭘까?
String 클래스의 Immutable(불변) 특성 때문이다.
불변이란 말은 String의 Value 값은 한 번 생성되면 변경할 수가 없단 뜻.

문자열을 더하는 코드 예를 들어보자
~~~java
String a = "a";

String b = "b";

a = a + b;
~~~

위 코드가 실행되면 "a"와 "b"의 문자열에 대해 메모리가 할당되고 a, b 변수가 그 값을 각각 참조하게 된다.

a = a + b가 실행 된 후에는?

String은 불변 특성이 있기 때문에 a가 참조하고 있는 공간에 "a" 대신에 "ab"란 값으로 바꾸어 주는 것이 아니라,

"ab"에 대해 새로운 Stirng 인스턴스를 생성하여 a가 참조하도록 한다.

이전에 참조하던 "a"는 쓰레기가 되고 나중에 가비지 컬렉션에 의해 처리된다.

바로 이런 이유 때문에 더 많은 시간과 메모리가 소요되는 것!!

연산을 많이하면 많이 할수록 이런 성능 차이는 더욱 심해진다.

## StringBuffer, StringBuilder와 비교해보았을 경우 String 클래스의 장점은?

물론 String 클래스에도 그만의 장점이 있다.

String 클래스는 불변 속성을 가짐으로써 안전하다. 값이 변경되지 않기 때문에 여러 쓰레드가 데이터를

공유하더라도 동기화를 신경 쓸 필요가 없어 안정성이 유지되는 장점이 있다.

그리고 StringBuffer, StringBuilder 클래스에서도 String 클래스를 이용한다.

toString 메소드의 경우 StringBuffer, StringBuilder의 toString가 호출되면 해당 문자열에 대한 String 객체를

생성해서 반환한다.

**따라서 연산이 적게 사용되고, 문자열 값의 수정없이 읽기가 많은 경우에는 String  클래스의 사용이 적절하다.**
