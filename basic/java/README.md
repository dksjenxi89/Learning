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


