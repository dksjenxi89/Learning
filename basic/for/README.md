## for문 정리

공부를 했었으나. . . 알고리즘 공부를 하며 많이 햇갈려서 다시 정리하고 넘어간다.

- 하나의 변수를 사용할 땐 while보단 for문이 낫다.

### 향상 된 for문

~~~java
  int[] testArray = {1, 2, 3, 4, 5};

  for(int i : testArray) System.out.println(i)

~~~

배열을 짧은 코드로 사용할 때 사용한다.
testArray에서 가져올 값이 있을 때까지 향상 된 for문에 존재하는 실행문을 실행한다.

### 이중 for문

~~~java
  for (int i = 1; i <= 3; i++) {
  
    for (int j = 1; j <= 5; i++) {
    
      System.out.println("i = " + i + "i번째 반복");
      
      System.out.println("j = " + j + "j번째 반복");
    
    }
  }
~~~

이중for문은 상위 for문이 더 큰 조건이고 하위 for문이 작은 조건으로 생각하면 될 듯.

예제 코드에서 인덱스 i가 들어간 코드가 1번 실행 되면

그 하위의 j가 j의 조건까지 실행된다. . .

결과값
![image](https://user-images.githubusercontent.com/57930450/69312204-a0647f80-0c71-11ea-96a1-30e649b6f381.png)

i 1 i 1 i 1 i 1 i 1
j 1 j 2 j 3 j 4 j 5

i 2 i 2 i 2 i 2 i 2
j 1 j 2 j 3 j 4 j 5

i 3 i 3 i 3 i 3 i 3
j 1 j 2 j 3 j 4 j 5

이런 느낌으로 실행된다!



