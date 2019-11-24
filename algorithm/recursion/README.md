[Do it! 자료구조와 함께 배우는 알고리즘 입문 - 시바타 보요] {http://www.yes24.com/Product/Goods/60547893?Acode=101}

## 재귀(Recursion)

재귀란?
어떤 사건이 자기 자신을 포함하고 다시 자기 자신을 사용하여 정의 될 때 재귀적(recursive)이라고 한다.

예)
![image](https://user-images.githubusercontent.com/57930450/69475789-dbeb7f00-0e14-11ea-8530-9c225e78534d.png)

재귀의 개념을 그림으로 표현한 예로, 화면 가운데 다시 화면이 나타난다!
그 화면 가운데에도 다시 화면이 반복되어 나타난다.
이러한 재귀의 개념을 사용하면 1부터 시작하여 2, 3, . . .과 같이 무한하게 이어지는 자연수를 아래처럼 정의할 수 있다.

1. 1은 자연수이다.
2. 자연수 n의 바로 다음 수도 자연수이다.

재귀적 정의에 의해 무한으로 존재하는 자연수를 위의 두 문장으로 정의할 수 있다.

재귀를 효과저긍로 사용하면 이런 정의뿐만 아니라 프로그램도 간결하게 할 수 있다.

## 팩토리얼 구하기
재귀의 사용 예로 가장 먼저 살펴볼 문제는 음이 아닌 정수의 팩토리얼을 구하는 프로그램이다.

1. 0! = 10
2. n > 0이면 n! = n x (n - 1)!

예컨데 1-의 팩토리얼인 10!은 10 x 9!로 구할 수 있고 그 우변에서 사용되는 식 9!은 9 x 8!로 구할 수 있다.

### !. 팩토리얼이란?
- 수학 용어 / 한자어인 계승(차례대로 곱한다)보다는 영어 명칭을 소리나는데로 쓴 팩토리얼이라고 부른다.

- 차례곱이라고도 부른다
예) 자연수 n을 이용하여 기호로는 간단하게 n!로 나타내며 1부터 n까지의 자연수를 모두 곱하는 것을 의미한다.

## 하노이의 탑
- 쌓아 놓은 원반을 최소의 횟수로 옮기기 위한 알고리즘인 '하노이의 탑'
- 재귀 알고리즘에서 유명한 문제인가보다..!
- 하노이의 탑이라는 알고리즘 이름은 '64개의 황금 원반을3개의 기둥 사이에서 바꿔 옮기는 작업을 완료하면 세 개의 종말이 찾아온다. 라는 인도 신화에서 유래했다.'

하노이의 탑은 작은 원반이 위에, 큰 원반이 아래에 위치할 수 있도록 원반을 3개의 기둥 사이에서 옮기는 문제이다.

모든 원반은 크기가 다르고 처음에는 모든 원반이 이 규칙에 맞게 첫 번째 기둥이 쌓여있다.

이 상태에서 모든 원반을 세 번째 기둥으로 최소의 횟수로 옮기면 된다.

원반은 1개씩만 옮길 수 있고 큰 원반을 작은 원반 위에 쌓을 수는 없다.

![image](https://user-images.githubusercontent.com/57930450/69488489-2ae4f300-0ead-11ea-9268-e7d7ddc0d381.png)

이해도는 이것..!

처음에 원반@1을 세 번째 기둥이 아니라 두 번째 기둥으로 옮겨도 되지만(나도 이렇게 생각함) 그러면 단계가 오히려 많아진다고 한다..!

최소의 횟수로 이동을 끝마칠 수가 없다고 한다.

그러므로 원반 옮기는 순서를 다시 생각해봐야한다.

원반이 4개일 경우도 마찬가지 요는 그룹으로 묶어서 제일 큰 원반을 시작 기둥에 두고 나머지 원반들을 중간 기둥에 그룹으로

몰아넣은 다음, 가장 큰 원반을 목표 기둥에 넣고 그 후에 나머지 그룹들을 옮기면 된다.
