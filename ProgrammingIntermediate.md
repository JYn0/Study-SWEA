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





## [Learn > Course > Programming Intermediate > Stack2]



##### **백트래킹**

* 백트래킹

  해를 찾는 도중 막히면(해가 아니면) 되돌아가서 다시 해를 찾아가는 기법

  어떤 노드에서 출발하는 경로가 해결책으로 이어질 것 같지 않으면 더 이상 그 경로를 따라가지 않음으로써 시도의 횟수를 줄인다.(Prunning: 가지치기)

  최적화 문제, 결정 문제
  
  * 미로찾기
  
  * n queen
  
  * Power Set
  
    어떤 집합의 공집합과 자기 자신을 포함한 모든 부분 집합을 말하며, 구하고자 하는 어떤 집합의 원소 개수가 n일 경우, 부분 집합의 개수는 2의 n제곱이 나온다.
  
    ```C
    #include <stdio.h>
    #define MAXCANDIDATES 100
    #define NMAX 100
    
    void construct_candidates(int a[], int k, int n, int c[], int* ncandidates){
        c[0] = 1;
        c[1] = 0;
        *ncandidates = 2;
    }
    void backtrack(int a[], int k, int input){
        int c[MAXCANDIDATES] = {0,};
        int ncandidates = 0;
        int i = 0;
        if(k == input){ // 답이면 원하는 작업을 한다
            printf("(");
            for(i=0; i<=k; i++){
                if(a[i] == 1){
                    printf("%d", i);
                }
            }
            printf(")\n");
        } else{
            k++;
            construct_candidates(a, k, input, c, &ncandidates);
            for(i=0; i<ncandidates; i++){
                a[k] = c[i];
                backtrack(a, k, input);
            }
        }
    }
    void main(void){
        int a[MAX];
        backtrack(a, 0, 3);
    }
    ```
  
  * 순열
  
    ```C
    #include <stdio.h>
    #define MAXCANDIDATES 100
    #define NMAX 100
    
    void construct_candidates(int a[], int k, int n, int c[], int* ncandidates){
        int i;
        bool in_perm[NMAX] = {0,};
        for(i=0; i<k; i++){
            in_perm[a[i]] = 1;
        }
        *ncandidates = 0;
        for(i=1; i<=n, i++){
            if(in_perm[i] == 0){
                c[*ncandidates] = i;
                (*ncandidates)++;
            }
        }
    }
    void backtrack(int a[], int k, int input){
        int c[MAXCANDIDATES] = {0,};
        int ncandidates = 0;
        int i = 0;
        if(k == input){
            printf("(");
            for(i=1; i<=k; i++){
                printf("%d", a[i]);           
            }
            printf(")\n");
        } else{
            k++;
            construct_candidates(a, k, input, c, &ncandidates);
            for(i=0; i<ncandidates; i++){
                a[k] = c[i];
                backtrack(a, k, input);
            }
        }
    }
    void main(void){
        int a[MAX];
        backtrack(a, 0, 3);
    }
    ```
  
    
  
* 알고리즘 절차

  1. 상태 공간 Tree의 깊이 우선 검색을 실시
  2. 각 노드가 유망한지를 점검
  3. 만일 그 노드가 유망하지 않으면, 그 노드의 부모 노드로 돌아가서 검색을 계속



##### **분할 정복**

* 분할

  * 거듭제곱

    ```java
    Power(Base, Exponent){
        if Exponent = 1 then return Base;
        else if Base = 0 then return 1;
        
        if Exponent % 2 = 0 then
        {
            NewBase <- Power(Base, Exponent/2);
            return NewBase*NewBase;
        }
        else
        {
            NewBase <- Power(Base, (Exponent-1)/2);
            return (NewBase*NewBase)*Base;
        }
    }
    // O(log2n)
    ```

  * 퀵 정렬

    ```java
    quickSort(a[], begin, end)
        if begin < end then
        {
            p <- partition(a, begin, end);
            quickSort(a[], begin, p-1);
            quickSort(a[], p+1, end);
        }
    end quickSort()
    
    partition(a[], begin, end)
        pivot <- (begin+end)/2;
    	L <- begin;
    	R <- end;
    	while(L<R) do
        {
            while(a[L] < a[pivot] and L<R) do L	L+1;
            while(a[R] >= a[pivot] and L<R) do R	R-1;
            if(L<R)
            {
                if(L==pivot) then pivot <- R;
                exchange a[L] and a[R]
            }
        }
    	exchange a[pivot] and a[R]
    	return R;
    end partition()
    ```






## [Learn > Course > Programming Intermediate > Queue]



##### **Queue**

* 삽입, 삭제의 위치가 제한적인 자료구조

  뒤: 삽입/ 앞: 삭제

* 선입선출구조(FIFO: First In First Out)

* enQueue(item) : Queue의 뒤쪽에 원소 삽입

  deQueue(): Queue 앞쪽에 원소 삭제하고 반환

  createQueue(): 공백 상태의 Queue를 생성

  isEmpty(): 공백상태인지 확인

  isFull(): 포화상태인지 확인

  Qpeek(): 앞쪽에서 원소를 삭제없이 반환



##### **선형 Queue**

* Queue의 크기 = 배열의 크기

  front : 저장된 첫 번째 원소의 인덱스

  rear : 저장된 마지막 원소의 인덱스

* 초기 상태: front = rear = -1

  공백 상태: front = rear

  포화 상태: rear = n-1

* 구현

  * createQueue()

  * enQueue(item)

    ```java
    enQueue(item)
        if(isFull()) then Queue_Full();
    	else{
            rear <- rear + 1;
            Q[rear] <- item;
        }
    end enQueue()
    ```

  * deQueue()

    ```java
    deQueue()
        if(isEmpty()) then Queue_Empty();
    	else{
            front <- front + 1;
            return Q[front];
        }
    end deQueue()
    ```

  * isEmpty(), isFull()

    ```java
    isEmpty()
        if(front==rear) then retrun true;
    	else return false;
    end isEmpty()
    isFull()
        if(rear == n-1) then return true;
    	else return false;
    end isFull()
    ```

  * Qpeek()

    ```java
    Qpeek()
        if(isEmpty()) then Queue_Empty();
    	else return Q[front+1];
    end Qpeek()
    ```



##### **원형Queue**

* 초기 공백 상태 : front = rear = 0

* Index의 순환(n-1 -> 0)

* 구현

  * createQueue()

    크기 n인 1차원 배열 생성

    front, rear = 0

  * isEmpty(), isFull()

    공백상태: front = rear

    포화상태: 삽입할 rear의 다음 위치 = 현재 front

    (rear+1) mod n = front(삽입할 rear값의 다음 위치)

    ```java
    isEmpty()
        if(front==rear) then retrun true;
    	else return false;
    end isEmpty()
    isFull()
        if((rear+1) mod n = front) then return true;
    	else return false;
    end isFull()
    ```

  * enQueue(item)

    ```java
    enQueue(item)
        if(isFull()) then Queue_Full();
    	else{
            rear <- (rear+1) mod n;
            cQ[rear] <- item;
        }
    end enQueue()
    ```

  * deQueue(), delete()

    ```java
    deQueue()
        if(isEmpty()) then Queue_Empty();
    	else{
            front <- (front+1) mod n;
            return cQ[front];
        }
    end deQueue()
    delete()
        if(isEmpty()) then Queue_Empty();
    	else front <- (front+1) mod n;
    end delete()
    ```

  ```C
  #define Q_SIZE 4
  int queue[Q_SIZE];
  int front, rear = 0;
  void enQueue(int item){
      if(isFull()) exit(1);
      else{
          rear = (rear+1) & Q_SIZE;
          queue[rear] = item;
      }
  }
  int deQueue(int[] queue){
      if(isEmpty()) exit(1);
      else{
          front = (front+1) % Q_SIZE;
          return queue[front];
      }
  }
  ```



##### **연결 Queue**

* 단순 연결 리스트(Linked List)를 이용한 Queue

  Queue의 원소 : 단순 연결 리스트의 노드

  Queue의 원소 순서 : 노드의 연결 순서, 링크로 연결되어 있음

* 상태 표현

  front = rear = NULL (초기, 공백)

  각 노드에 다음 노드를 가리키는 링크를 포함하고 있음

* 구현

  * createLinkedQueue()

    리스트 노드 없이 포인터 변수만 생성

    ```java
    createLinkedQueue()
        front <- NULL;
    	rear <- NULL;
    end createLinkedQueue()
    ```

  * isEmpty()

    공백상태 : front = rear = NULL

    ```java
    isEmpty()
        if(front=null) then return true;
    	else return false;
    end isEmpty()
    ```

  * enQueue(item)

    1. 새로운 노드 생성 후 데이터 필드에 item 저장
    2. 연결 Queue가 공백인 경우, 아닌 경우에 따라 front, rear 변수 지정

    ```java
    enQueue(item)
        new <- getNode(); // getNode(): 새로운 노드 할당 후 리턴
    	new.data <- item;
    	new.link <- NULL;
    	if(front = NULL) then{
            rear <- new;
            front <- new;
        } else{
            rear.link <- new;
            rear <- new;
        }
    end enQueue()
    ```

  * deQueue(), delete()

    1. old가 지울 노드를 가리키게 하고, front 재설정
    2. 삭제 후 공백 Queue가 되는 경우, rear도 NULL로 설정
    3. old가 가리키는 노드를 삭제하고 메모리 반환

    ```java
    deQueue()
        if(isEmpty()) then Queue_Empty();
    	else{
            old <- front;
            item <- front.data;
            front <- front.link;
            if(isEmpty()) then rear <- NULL;
            free(old);
            return item;
        }
    end deQueue()
    ```

  ```C
  typedef int element;
  typedef struct Node{
      element data;
      struct Node *next;
  }
  typedef struct{
      Node *front, *rear;
  } QueuePointer;
  QueuePointer *LQ;
  QueuePointer *createLinkedQueue(){
      LQ = (QueuePointer*)malloc(sizeof(QueuePointer));
      LQ->front = NULL;
      LQ->rear = NULL;
      return LQ;
  }
  void enQueue(element item){
      Node *newNode = (Node*)malloc(sizeof(Node));
      newNode->data = item;
      newNode->next = NULL;
      if(LQ->front == NULL){
          LQ->front = newNode;
      }else{
          LQ->rear->next = newNode;
          LQ->rear = newNode;
      }
  }
  element deQueue(){
      Node *old = LQ->front;
      element item;
      if(isEmpty(LQ)) return 0;
      else{
          itme = old->data;
          LQ->front = LQ->front->next;
          if(LQ->front == NULL) LQ->rear = NULL;
          free(old);
          return item;
      }
  }
  ```



##### **활용**

* 우선순위 Queue

  우선순위가 높은 순서대로 먼저 나가게 됨

  시뮬레이션 시스템, 네트워크 트래픽 제어, 운영체제의 태스크 스케쥴링 등

* 버퍼

  데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역

  버퍼링 : 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작을 의미

  입출력 및 네트워크 기능



##### **BFS(Breadth First Search너비 우선 탐색)**

* 시작점의 인접한 정점들을 모두 차례로 방문한 후 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식
* 인접한 정점들을 탐색한 후, 차례로 너비 우선 탐색을 진행해야 하므로, 선입선출 형태의 자료구조인 **Queue 활용**

```java
BFS(G,v) // 그래프 G, 탐색 시작점 v
    큐 생성
    시작점 v를 뷰에 삽입
    점 v를 방문한 것으로 표시
    while(큐가 비어있지 않은 경우){
    	t <- 큐의 첫번째 원소 반환
    	for(t와 연결된 모든 선에 대해){
    		 u <- t의 이웃점
    		 u가 방문되지 않은 곳이면,
    		 u를 큐에 넣고, 방문한 것으로 표시
    	}
    }
    return none
end BFS()    
```





