## 기술블로그 만들면 이전할 내용들!
### 신입 웹개발자 면접 질문 정리

### 데이터베이스
## 오라클과 mysql의 차이점


오라클은 오라클사에서 만든 데이터베이스

공개 DB MySQL (오픈 소스 DBMS)

-"솔직히 생각도 안 하고 있었다"


### 오라클과 MYSQL의 차이점

### 1. null값 확인 함수가 다르다.

컬럼값에 null이면 다른 값으로 표시해주는 함수 사용법이 다르다.

오라클에서는 NVL 함수

### nvl함수는 null을 0 또는 다른 갑승로 변환하기 위해서 사용하는 함수이다.

오라클 : nvl 함수 사용
~~~sql
select nvl(컬럼명)
from 테이블명;
~~~
MYSQL : ifnull을 사용

~~~sql
select ifnull(컬럼명)
from 테이블명;
~~~

### 2. 현재날짜 시간을 확인하는 방법이 다르다.

오라클 : sysdate
~~~sql
select sysdate
from dual;
~~~
MYSQL : now
~~~sql
select now
from dual;
~~~
### 3. 날짜 포맷 변환 방법이 다르다.

오라클에서는 날짜를 string으로 변경시 to_char() 함수를 사용하지만

mysql 에서는 date_format()함수를 사용한다.

오라클 : to_char
~~~sql
select to_char(reg_date, 'YYYYMMDD HH24MISS')
from dual;
~~~
MYSQL
~~~sql
select date_format(reg_date, '%Y%m%d%H%i%s')
from dual;
~~~

### 4. 요일변환의 숫자 범위가 다르다.

오라클은 일월화수목금토를 1, 2, 3, 4, 5, 6, 7로 인식한다

MYSQL은 일월화수목금토를 0, 1, 2, 3, 4, 5, 6으로 인식한다.

그렇기 때문에 요일 계산하는 경우 조심해야 한다.

오늘이 금요일인 경우 오라클에서는 6을 반환하고
MYSQL에서는 5를 반환하기 때문에 요일변환 사용하는 부분을 생각해서 사용해야 한다.

[보통 JS에서는 일월화수목금토를 0, 1, 2, 3, 4, 5, 6으로 사용하기 때문에 오라클에서는 -1을 넣어준다]

-"비슷한 상황을 겪었어서 이해가 확 된다."

### 5. 문자와 문자 합치는 방법이 다르다.

오라클 ||

MYSQL concat()

### 6. 형변환 방법이 다르다.

오라클 to_char, to_number

~~~sql
  select to_char(632)
  from dual;
~~~

MYSQL cast

~~~sql
  select cast(1234 as char)
  from dual;
~~~

### 7. 페이징 처리가 다르다
오라클 rownum을 사용하여 where절에서 between으로 1~10번째 자료를 나타낸다.

MYSQL limit을 사용하여 1~10번째자료를 나타낸다

오라클
~~~sql
  select *
  from (select rownum, A.*
        from(select * from 테이블명) A
   where rownum between 0 and 10
~~~

MYSQL

~~~sql
  select *
  from 테이블명 limit 0, 10
~~~

### 8. 시퀀스 사용시 다음번호 불러오는 방법이 다르다

오라클 시퀀스명.nextval

MYSQL 시퀀스명.currval


-"차이점이 있긴 한줄 알았는데 정말 생각없이 있었던거 같다... 한 번 정리할걸..."


## 서버
## 서버란?

한 컴퓨터가 네트워크로 연결 된 다른 하나, 또는 그 이상의 컴퓨터들에게 뭔가를 해주면

예를 들어 저장 된 글과 사진들을 보여주거나 반대로, 이것들을 업로드 받아서 보관해준다거나

한 컴퓨터에서 톡을 보내면 다른 컴퓨터에 알림을 보내거나

위치와 목적지를 받아서, 가는 길과 소요 시간을 계산해주는 등

그 serve 해주는 컴퓨터가 '서버(server)'이고,

그 service를 받는 컴퓨터가 '클라이언트(client)'가 된다.


또 예를 들어, 한 모바일 앱에서 그 앱에서 서비스하는 정보를

앱 사용자에게 제공하면 서버가 되는 것이고,


그 정보 중에서 다른 클라우드 플랫폼에서 또 정보를 받아서 유저에게 제공하게 되면. . .

그 앱 또한 클라이언트가 되는 것이다.


서버라고 알고 있는 컴퓨터들은 보통 IDC(Internet Data Center)에 있다.

## 기초지식
얄팍한 코딩사전 - https://www.youtube.com/watch?v=iks_Xb9DtTM&t=1s

### 프로세스, 스레드 개념 정리

-"프로세스는 알고리즘에서 처리하는 과정을 프로세스라고 하지 않던가..."


컴퓨터가 무슨 일을 하고 있는 상태를 '프로세스'라고 한다.

과거와 달리 멀티 태스킹이 가능한 이유는 운영체제가 여러개의 프로세스를 운용하고 있기 때문이다.

동시적, 병렬적 구조로 프로세스를 운용하고 있다.

동시성은 프로세스 하나가 한 작업, 한 작업씩 여러 작업을 돌며 일부분씩 수행하는 것이다.(Context Switching)
=> 엄청 빠르기 때문에 동시에 진행되는 것처럼 느껴진다.

병렬성은 프로세스 하나에 코어 여러 개가 달려서 각각 동시에 작업들을 수행하는 것이다.


한 프로세스 내에서도 여러 갈래의 작업들이 동시에 진행 될 필요가 있다.

이 갈래를 **스레드**라고 부른다.

컴퓨터는 프로세스마다 자원을 분할해서 할당한다.

분할 되는 단위는 섹션이라고 부른다.


프로세스들은 컴퓨터의 자원을 분할해서 쓰지만

스레드는 프로세스마다 주어진 전체 자원을 함께 사용한다.


단점도 물론 존재한다.
프로세스 안에서 공유되는 변수에 스레드 두 개가 동시에 손을 댄다. (Error)

시간 문제로 발생하는 이런 상황들을 예상하고 방지해야 하기 때문에 스레드를 사용하는 프로그래밍은 코드를 짜기도, 디버깅을 해서
오류를 찾아내고 원인을 밝히기도 굉장히 까다로운 경우가 많다.

자바

###
## 자바 기초 정리

-"햇갈렸던걸 하나하나 다시 정리하자.."

### 오버 라이딩 (메소드 재정의)

-"자바에서 클래스를 상속받아서 사용할 때 객체를 가져오는걸 오버 라이딩이라고 하는 것 아니였나..??"

### 슈퍼 클래스에 존재하는 필드나 메소드를 서브 클래스에서 재정의하여 사용할 수 있다.

-"작년 9월달에 정리했던 말인데 많이 안 와닿았는데 이제는 좀 와닿네"

슈퍼 클래스(상위 클래스)에 존재하는 메소드나 필드를 서브 클래스에서 재정의하여 사용할 수 있다.

### 오버 로딩

-"배우고 쓴 적이 없어서 뭔지 가물가물..."

같은 이름의 메소드를 여러 개 가지면서 매개 변수를 다르게 정의하는 것

~~~java

static void test(int[] testArray, int[] testArray2nd) {

    . . .
    
}



static void test(int[] changeArray, int[] changeArray2nd) {

    . . .
    
}


~~~

-"이런건가.. 추측"

~~~java
public class OverLodingTest {
	static void test() {
		
		System.out.println("매개변수 없음");
	}
	
	static void test(int a, int b) {
		
		System.out.println("매개 변수 " + a + "와 " + b);
	}
	
	static void test(double d) {
		System.out.println("매개변수 " + d);
	}
 }
~~~

~~~java
public class OverLodingTest {


	
	static int test() {
		
		int ww = 0;
		
		
		return ww;
	}
	
	static int test(int a, int b) {
		
		int ww = 0;
		
		
		return ww;
	}
	
	static int test(double d) {
		
		int ww = 0;
		
		
		return ww;
	}
}

~~~

-"같은 메소드명을 가졌지만 매개변수를 다르게 하면 오버로딩이다!!"


