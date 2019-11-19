String 문자열 정리
========================

## String 
- 짧은 문자열을 더할 경우
- 제일 느림

## StringBuffer
- **스레드 세이프** 해야 할 경우 사용

## StringBuilder
- 스레드 세이프 하지 않아도 될 때 사용
- 가장 빠름

## JDK 5.0 이상
JDK 5.0 이상부터는 컴파일러가 String으로 문자열을 더할 때 StringBuilder로 변환 한다.

그래도 S
