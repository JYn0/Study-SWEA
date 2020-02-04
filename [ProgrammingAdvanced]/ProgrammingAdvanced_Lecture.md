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



## [Learn > Course > Programming Advanced > 강의형 > 02 완전탐색 & 그리디]

##### 반복(Iteration)과 재귀(Recursion)

* **반복**은 수행하는 작업이 완료될 때 까지 계속 반복

  * 초기화 / 조건검사 / 반복할 명령문 실행 / 업데이트

* **재귀**는 주어진 문제의 해를 구하기 위해 동일하면서 더 작은 문제의 해를 이용하는 방법

  * 하나 또는 그 이상의 기본 경우(base case)

    집합에 포함되어 있는 원소로 induction을 생성하기 위한 시드(seed) 역할

  * 하나 또는 그 이상의 유도된 경우(inductive part)

    새로운 집합의 원소를 생성하기 위해 결합되어지는 방법

* 재귀 함수(recursive function) 작성 절차

  * 더 작은 문제로 표한할 수 있는지 시도
  * 문제를 직접 풀 수 있는 것이 어떤 경우인지 Base case 확인
  * N이 줄어서 Base case를 만나게 되는지 확인
  * Base case와 Base case가 아닌 경우로 나누어서 코드를 작성

  ```C
  int fact(int n){
      if (n <= 1)				// Base part
          return 1;
      else
          return n*fact(n-1);	//Inductive part
  }
  ```

* 반복과 재귀의 비교

  |              |                      재귀                       |         반복          |
  | :----------: | :---------------------------------------------: | :-------------------: |
  |     종료     | 재귀함수호출이 종료되는 베이스케이스(base case) |  반복문의 종료 조건   |
  |   수행시간   |                  (상대적)느림                   |         빠름          |
  |  메모리공간  |                (상대적)많이 사용                |       적게 사용       |
  | 소스코드길이 |                    짧고 간결                    |         길다          |
  | 소스코드형태 |              선택 구조(if...else)               | 반복 구조(for, while) |
  |  무한반복시  |                 스택오버플로우                  |  CPU를 반복해서 점유  |



##### 조합적 문제

* 문제제시 : TSP

  Traveling Salesman Problem

  모든 도시들을 한번씩 방문하는데 필요한 최소 비용 구하기

* 순열(Permutation)

  서로 다른 것들 중 몇개를 뽑아서 한 줄로 나열하는 것

  서로 다른 n개 중 r개를 택하는 순열 : nPr

  nPr = n X (n-1) X ... X (n-r+1)

  nPn = n! = n X (n-1) X ... 2 X 1 -> Factorial

* 재귀 호출을 통한 순열로 TSP 해결

  ```C++
  #include <iostream>
  #include <stdio.h>
  using namespace std;
  
  #define INF 10000; // 임의의 큰값
  #define MAX_N 6;
  
  int N, Graph[Max_N][MAX_N];
  int solve(int pos, int visited);
  
  int main(){
      int tcCnt;
      freopen("tsp_input.txt","r", stdin);
      cin >> tcCnt;
      for(int t=1; t<=tcCnt; ++t){
          cin >> N;
          for(int i=0; i<N; ++i){
              for(int j=0; j<N; ++j){
                  cin >> Graph[i][j];
              }
          }
          int ans = INF;
          for(int i=0; i<N; ++i){
              int tmp = solve(i, 1<<i);
              if(ans > tmp)
                  ans = tmp
          }
          cout << "#" << t << ' '<< ans << endl;
      }
      return 0;
  }
  
  int solve(int pos, int visited){
      if(visited == (1<<N)-1)
          return 0;
      int ret = INF;
      for(int next=0; next<N; ++next){
          if(!(visited & (1<<next)) && Graph[pos][next]){
              int tmp = Graph[pos][next] + solve(next, visited | (1<<next));
              if(tmp < ret)
                  ret = tmp
          }
      }
      return ret;
  }
  ```

  

##### 조합

* 서로다른 n개의 원소 중 r개를 순서 없이 골라낸 것(combination)

  nCr = n! / (n-r)!r!, (n >= r) / nCr = n-1Cr-1 + n-1Cr / nC0 = 1

* 순열 : 선택의 순서가 결과에 영향을 주는 경우

  2개를 골라서 만들 수 있는 최대수 - 재귀 예제

  ```c++
  #include <iostream>
  #include <stdio.h>
  using namespace std;
  
  #define MAX_N 6;
  
  int N, Nums[MAX_N];
  int solve(int cnt, int used, int val);
  
  int main(){
      int tcCnt;
      freopen("number_input.txt","r", stdin);
      cin >> tcCnt;
      for(int t=1; t<=tcCnt; ++t){
          cin >> N;
          for(int i=0; i<N; ++i){
              cin >> Nums[i];
          }
          cout << "#" << t << ' '<< solve(0,0,0) << endl;
      }
      return 0;
  }
  
  int solve(int cnt, int used, int val){
      if(cnt == 2)
          return val;
      int ret = 0;
      for(int i=0; i<N; ++i){
          if(used & (1<<i))
              continue;
          int tmp = sovle(cnt+1, used | (1<<i), val*10+Nums[i]);
          if(tmp > ret)
              ret = tmp
      }
      return ret;
  }
  ```

  

* 조합 : 선택의 순서가 결과에 영향을 주지 않는 경우

  2개를 더해서 만들 수 있는 최대값 - 재귀 예제

  ```C++
  #include <iostream>
  #include <stdio.h>
  using namespace std;
  
  #define MAX_N 10;
  
  int N, Nums[MAX_N];
  int solve(int cnt, int used, int val);
  
  int main(){
      int tcCnt;
      freopen("number_input.txt","r", stdin);
      cin >> tcCnt;
      for(int t=1; t<=tcCnt; ++t){
          cin >> N;
          for(int i=0; i<N; ++i){
              cin >> Nums[i];
          }
          cout << "#" << t << ' '<< solve(0,0,0) << endl;
      }
      return 0;
  }
  
  int solve(int cnt, int used, int val){
      if(cnt == 2)
          return val;
      if(pos == N)
          return -1;
      
      int ret = 0, tmp;
      tmp = solve(pos+1, cnt+1, val+Nums[pos]);
      if(tmp > ret)
          ret = tmp;
      
      tmp = solve(pos+1, cnt, val);
      if(tmp > ret)
          ret = tmp
      return ret;
  }
  // --------------------------------------------------
  
  // Bit 부분 집합 예제
  int CountBits(int value){
      int count = 0;
      while (value > 0){
          if((value & 1) == 1)
              count++;
          value = value >> 1;
      }
  	return count;
  }
  
  int solve(){
      int ret = 0;
      for(int i=0; i < (1<<N); ++i){
          if(countBits(i) == 2){ // Bit가 2개인 것만
              int sum = 0;
              for(int j=0; j<N; ++j){
                  if(i & (1 << j))
                      sum += Nums[j];
              }
              if(sum > ret)
                  ret = sum;
          }
      }
      return ret;
  }
  ```

  

##### 완전 탐색 기법

