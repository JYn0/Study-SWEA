# SW 문제해결 응용



## [Learn > Course > Programming Advanced > 강의형 > 01 알고리즘 개론]



### START

##### O(big-Oh) - 표기법

* 실행 시간의 점근적 상한을 나타낸다.

  최대한 이만한 시간은 걸릴 수 있다

  |            | 자주 사용하는 O-표기              |
  | :--------: | --------------------------------- |
  |    O(1)    | 상수시간(Constant time)           |
  |  O(log n)  | 로그(대수) 시간(Logarithmic time) |
  |    O(n)    | 선형 시간(Linear time)            |
  | O(n log n) | 로그 선형 시간(Log-linear time)   |
  |   O(n^2)   | 제곱 시간(Quadratic time)         |
  |   O(n^3)   | 세제곱 시간(Cubic time)           |
  |   O(2^n)   | 지수 시간(Exponential time)       |



### 표준입출력

##### java 입출력

* 표준입출력 - System.in, Systm.out

  표준입출력의 대상 변경 - setIn(), setOut()

  표준입력

  * Scanner sc = new Scanner(System.in);
  * sc.next(), nextInt()

  표준출력

  * System.out.println()
  * System.out.print()
  * System.out.printf()

* 파일의 내용을 표준 입력으로 읽어오는 방법

  ```java
  System.setIn(new java.io.FileInputStream("sample_input.txt"));
  ```



##### 비트 연산자

* Bit를 이용한 부분 집합 생성 코드

  ```C
  #include <stdio.h>
  void printSubsets(char arr[], int n){
      for (int i=0; i<(1<<n); ++i){ // (1<<n) == 16
          printf("{");
          for(int j=0; j<n; ++j){
              if(i & (1<<j)){
                  printf("%c ", arr[j]);
              }
          }
          printf("}\n");
      }
  }
  int main(int argc, char** argv)
  {
      char data[] = {'A', 'B', 'C', 'D'};
      printSubsets(data, 4);
      return 0;
  }
  ```



##### 실수

* 실수는 근사값으로 표현

* 부동 소수점(floating-point) 표기법 사용

  소수점의 위치를 고정시켜 표현하는 방식

* 실수를 저장하기 위한 형식

  * 단정도 실수(32비트)

    부호1비트 + 지수8비트(2가 몇제곱인지) + 가수23비트

  * 배정도 실수(64비트)

