# SW 문제해결 기본



## [Learn > Course > Programming Intermediate > Array1]



**Algorithm 성능분석과 시간복잡도(빅-오(O) 표기법)**

* 완전검색(Exhaustive Search)

* 탐욕 알고리즘(Greedy Algorithm)

* Sort

  * Bubble Sort : 인접한 두개의 원소를 비교하여 자리를 계속 교환
  $$
    O(n^2)
  $$
  
  * Counting Sort : 항목들의  순서를 결정하기 위해 집합에 각 항목이 몇개씩 있는지 세는 작업을 하여, 선형시간에 정렬하는 효율적인 알고리즘(n:항목의 개수, k:정수의 최대값)
    $$
    O(n+k)
    $$
    





## [Learn > Course > Programming Intermediate > Array2]



##### **2차원 Array**

* Array 순회 : n * m 배열의 n*m개의 모든 원소를 빠짐없이 조사하는 방법

  * 행 우선 순회

    ```java
    int i; // 행
    int j; // 열
    for i from 0 to n-1
        for j from 0 to m-1
            Array[i][j];
    ```

  * 열 우선 순회

    ```java
    for j from 0 to n-1
        for i from 0 to m-1
            Array[i][j];
    ```

  * 지그재그 순회 : 첫행은 우측으로, 다음행은 좌측으로 진행

    ```java
    for i from 0 to n-1
        for j from 0 to m-1
            Array[i][j + (m-1-2*j) * (i%2)];
    ```



* 델타를  이용한 2차 Array 탐색

  : 2차 Array의 한 좌표에서 네 방향의 인접Array 요소를 탐색할 때 사용하는 방법 

  * 델타값 : 한 좌표에서 네 방향의 좌표와 x, y의 차이를 저장한 Array
  * 델타값을 이용하여 특정 원소의 상하좌우에 위치한 원소에 접근

  ```java
  ary[0...n-1][0...n-1]
  dx[] <- {0, 0, -1, -1};
  dy[] <- {-1, -1, 0, 0};
  for x,y from 0 to n-1
      for i from 0 to 3{
          testX <- x + dx[mode];
          testY <- y + dy[mode];
          test(ary[textX][testY]);
      }
  ```



* 전치행렬

  : 행과 열의 값이 반대인 행렬

  ```java
  int ary[n][n];
  int i, j;
  for i from 0 to n-1
      for j from 0 to n-1
          if(i < j)
              swap(ary[i][j], ary[j][i]);
  ```



##### **검색**

* 검색

  저장되어 있는 자료 중에서 목적하는 탐색키를 가진 항목을 찾는 작업

  탐색키(Search Key) : 자료를 구별하여 인식할 수 있는 키

  

  * 순차검색 : 일렬로 되어있는 자료를 순서대로 검색하는 방법

    Array, 연결 리스트 등 순차구조로 구현된 자료구조에 유용

    검색대상이 많은 경우 비효율적
    $$
    O(n)
    $$

    ```java
    // 비정렬
    sequentialSearch(a[], n, key)
        i <- 0;
    	while (i<n and a[i]!=key) do{
            i <- i+1;
        }
    	if (i<n) then return i;
    	else return -1;
    end sequentialSearch();
    
    // 정렬
    sequentialSearch(a[], n, key)
        i <- 0;
    	while (a[i]!=key) do{
            i <- i+1;
        }
    	if (a[i]!=key) then return i;
    	else return -1;
    end sequentialSearch();
    ```

  

  * 이진검색 : 자료의 가운데에 있는 항목의 키 값과 비교 후 다음 검색 위치 결정

    자료가 정렬된 상태여야 함

    ```java
    binarySearch(a[], low, high, key)
        middle <- (low+high)/2;
    	if (key = a[middle]) then
    		return true;
    	else if (key < a[middle]) then
    		binarySearch(a[], low, middle-1, key);
    	else if (key > a[middle]) then
    		binarySearch(a[], middle+1, high, key);
    	else
            return false;
    end binarySearch();
    
    binarySearch(a[], key)
        start <- 0, end <- length(a)-1;
    	while(start <= end){
            middle = start+(end-start)/2;
            if(a[middle] == key){
                return true;
            }
            else if(a[miidle] > key){
                end = middle -1;
            }
            else start = middle+1;
        }
    	return false;
    end binarySearch();
    ```

  

  * 인덱스

    : 테이블에 대한 동작 속도를 높여주는 자료구조(Look up table)

    인덱스를 저장하는 데 필요한 공간은 보통 테이블을 저장하는 공간보다 작음, 보통 인덱스는 키-필드만 갖고있기 때문이다.



##### **정렬**

* 셀렉션 알고리즘

  : 저장되어있는 자료로부터 k번째로 크거나 작은 원소 찾는 방법

  최대값, 최소값, 중간값 찾는 알고리즘
  $$
  O(kn)
  $$
  ㅇ자료 정렬 -> 원하는 순서에 있는 원소

  ```java
  // k번째로 작은 원소 찾는 알고리즘
  Select(list[], k)
      for i from 1 to k
      	minIndex = i;
  		minValue = list[i];
  		for j from i+1 to k
  			if list[j] < minValue
  				minIndex = j;
  				minValue = list[j];
  		swap list[i] and list[minIndex];
  	return list[k]
  end Select();
  ```



* 선택 정렬

  : 주어진 자료들 중 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식(셀렉션 알고리즘을 전체 자료에 적용)

  최소값 찾고 가장 첫번째 자리와 교환한 뒤, 셀렉션 알고리즘 
  $$
  O(n^2)
  $$

  ```java
  SelectionSort(a[], size)
  {
      i, j, t, min ,temp;
      for i from 0 to size-2 {
          min <- i;
          for j from i+1 to size-1 {
              if (a[j] < a[min]) min <- j;
          }
          temp <- a[i];
          a[i] <- a[min];
          a[min] <- temp;
      }
  }
  ```

  

### 정렬 알고리즘의 특성 비교

| 알고리즘    | 평균 수행시간 | 최악 수행시간 | 알고리즘 기법 | 비고                                |
| ----------- | ------------- | ------------- | ------------- | ----------------------------------- |
| 버블 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 코딩 쉬움                           |
| 카운팅 정렬 | O(n+k)        | O(n+k)        | 비교환 방식   | n이 작을때만                        |
| 선택 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 교환 회수가 버블, 삽입정렬보다 작음 |
| 퀵 정렬     | O(n log n)    | O(n^2)        | 분할 정복     | 평균적으로는 가장 빠름              |
| 삽입 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | n이 작을떄 효과적                   |
| 병합 정렬   | O(n log n)    | O(n log n)    | 분할 정복     | 연결리스트의 경우 가장 효율적       |





## [Learn > Course > Programming Intermediate > String]



* C언어 vs Java 에서의 String 처리

  * C언어

    가변길이 String - 구분자 String

    문자들의 배열 형태로 구현된 응용 자료형

    문자배열 마지막에 끝을 표시하는 Null(\0)넣어줘야 함

    String 처리에 필요한 연산을 함수 형태로 제공(strlen(), strcpy(), strcmp(), ...)

  * Java

    가변길이 String - 길이조절 String

    String 데이터를 저장, 처리해주는 클래스 제공

    String 클래스 사용

    String 처리에 필요한 연산을 연산자, 메쏘드 형태로 제공(-+, length(), replace(), split(), substring(), ...)



* 패턴매칭 

  * 보이어-무어 알고리즘

    : 오른쪽에서 왼쪽으로 String을 비교한다.

    오른쪽 끝의 문자가 불일치 하는 경우 Skip 테이블을 참조하여 패턴 혹은 Skip 테이블에 명기된 길이만큼 점프한다.

    텍스트를 모두 보지 않아도 검색 가능, 패턴의 오른쪽부터 비교

    수행시간 O(n)보다 적음, 최악O(mn)

  ![a](https://user-images.githubusercontent.com/50862497/71876253-ac48ca00-3169-11ea-99a6-141fae66b0a9.JPG)





## [Learn > Course > Programming Intermediate > Stack1]



##### **Stack**

* 자료를 쌓아 올린 형태의 자료구조(선형구조: 자료간의 관계가 1대1)

* 후입선출(LIFO, Last-In-First-Out)

* 삽입(push), 삭제(pop), 공백확인(isEmpty), 참조(peek)

  ```C
  int Stack[100];
  int top = -1;
  void push(int item){
      if(top >= 99) return;
      else Stack[++top] = item;
  }
  int pop(){
      if(top == -1){
          // Stack is Empty
          return 0;
      }
      else return Stack[top--];
  }
  void main(void){
      int item;
      push(1);
      push(2);
      push(3);
      item = pop; // 3
      item = pop; // 2
      item = pop; // 1
  }
  ```

  괄호검사, 함수호출 등



* **프로그램 메모리 공간**
  * 코드 영역

    실행할 프로그램의 코드가 저장되는 메모리 공간

    CPU는 코드 영역에 저장된 명령문을 하나씩 가져다가 실행

  * 데이터 영역

    전역변수와 Static 변수가 할당되는 영역

    프로그램 시작과 동시에 할당되어 종료 시까지 남아있는 특징의 변수가 저장되는 영역

  * 힙 영역

    프로그래머가 원하는 시점에 메모리 공간에 할당 및 소멸을 하기 위한 영역

  * Stack 영역

    지역변수와 매개변수가 할당되는 영역

    함수를 빠져나가면 소멸되는 변수를 저장하는 영역



##### **Memoization**

* 컴퓨터 프로그램을 실행할 때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술

  DP(동적계획)의 핵심 기술

* 피보나치 수열



##### **DP(동적 계획법)**

* Dynamic Programming

  그리디 알고리즘 설계 기법과 같이 최적화 문제를 해결하는 알고리즘 설계기법

* 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결

  최종적으로 원래 주어진 입력의 문제를 해결



##### **DFS(깊이우선탐색)**

* 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이우선탐색을 반복해야 하므로 후입선출 구조의 Stack을 사용

  1. 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색
  2. 더이상 갈 곳이 없게되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아옴
  3. 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하여 순회

  ![dfs_stack](https://user-images.githubusercontent.com/50862497/71959870-124f5300-3237-11ea-886f-2a3811c3ad62.JPG)

  ```java
  visited[], Stack[] 초기화
  DFS(v)
      v 방문;
  	visited[v] <- true;
  	do {
          if ( v의 인접 정점 중 방문 안 한 w 찾기)
              push(v);
          wihle(w){
              w 방문;
              visited[w] <- true;
              push(w);
              v <- w;
              v의 인접 정점 중 방문 안 한 w찾기
          }
          v <- pop(Stack);
      }while(v)
  end DFS()
  ```

* 한 쪽 방향으로 계속 탐색하다가 더 이상 진행할 수 없으면 다시 되돌아 오는 방법으로 탐색

  다시 되돌아오기 위해 사용한 자료구조로 Stack 사용





