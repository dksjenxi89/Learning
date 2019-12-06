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

select nvl(컬럼명)
from 테이블명;

MYSQL : ifnull을 사용

~~~sql
select ifnull(컬럼명)
from 테이블명;
~~~

### 2. 현재날짜 시간을 확인하는 방법이 다르다.

오라클 : sysdate

select sysdate
from dual;

MYSQL : now

select now
from dual;

### 3. 날짜 포맷 변환 방법이 다르다.

오라클에서는 날짜를 string으로 변경시 to_char() 함수를 사용하지만

mysql 에서는 date_format()함수를 사용한다.

오라클 : to_char

select to_char(reg_date, 'YYYYMMDD HH24MISS')
from dual;

MYSQL

S




