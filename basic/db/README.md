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

오라클

~~~sql
select 컬럼명
from 테이블명
were 
~~~

MYSQL



