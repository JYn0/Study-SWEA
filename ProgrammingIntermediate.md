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





## [Learn > Course > Programming Intermediate > List]



##### **List**

* 순서를 가진 데이터의 집합을 가리키는 추상자료형(abstract data type)

  동일한 데이터를 가지고 있어도 상관 없음

  |    함수명    |             기능             |
  | :----------: | :--------------------------: |
  | addtoFirst() |   List의 앞쪽에 원소 추가    |
  | addtoLast()  |   List의 뒤쪽에 원소 추가    |
  |    add()     | List의 특정 위치에 원소 추가 |
  |   delete()   | List의 특정 위치에 원소 삭제 |
  |     get      | List의 특정 위치에 원소 리턴 |



* **순차 List**

  배열 기반으로 구현

  * 1차원배열에 항목들을 순서대로 저장
  * 데이터 종류와 구조에 따라 구조화된 자료구조를 만들어 배열로 구현할 수 있음
  * 배열의 인덱스를 이용해 원하는 위치의 데이터에 접근



* **연결 List**

  메모리의 동적할당을 기반으로 구현

  * 자료의 논리적인 순서와 메모리 상의 물리적인 순서가 일치하지 않고, **개별적으로 위치하고 있는 원소의 주소를 연결하여 하나의 전체적인 자료구조**를 이룸
  * 링크를 통해 원소에 접근(물리적인 순서를 맞추기 위한 작업 필요없음)
  * **메모리의 효율적인 사용 가능**(자료구조의 크기를 동적으로 조정 가능)

  노드 : 연결 List에서 하나의 원소에 필요한 데이터를 갖고 있는 자료단위, 데이터 필드 (원소의 값 저장), 링크 필드(다음 노드의 주소 저장)

  헤드 : List의 처음 노드를 가리키는 자료구조

  * 단순연결List

    ```java
    addtoFirst(L,i)			// List 포인터 L, 원소 i
        new <-createNode();	// 새로운 노드 생성
    	new.data = i;		// 데이터 필드 작성
    	new.link = L;		// 링크 필드 작성
    end addtoFirst()
    
    add(L, pre, i)			// List L, 노드 pre, 원소 i
        // 노드 pre의 다음 위치에 노드 삽입
        new <- createNode();// 새로운 노드 생성
    	new.data = i;		// 데이터 필드 작성
    	if(L=NULL) then {
            L = new;
            new.link = NULL;
        }else{
            new.link = pre.link;
            pre.link = new;
        }
    end add()
        
    addtoLast(L, i)			// List L, 원소 i
        new <-createNode();	// 새로운 노드 생성
    	new.data = i;
    	new.link = NULL;
    	if(L=NULL) then {	// 빈 List일 때, 최초 노드 추가
            L = new;
            return;
        }
    	temp = L;			// 노드 링크 이용하여 List 순회
    	while(temp.link != NULL) do	// 마지막 노드 찾을 때까지 이동
            temp = temp.link;
    	temp.link = new;	// 마지막 노드 추가
    end addtoLast()
    ```

    ```java
    delete(L, pre)				// List L, 노드 pre
        // 노드 pre의 다음 위치에 있는 노드 삭제
        if(L == NULL) then error;
    	else{
            target = pre.link;	// 삭제 노드 지정
            if(target == NULL) then return;
            pre.link = target.link;
        }
    	freeNode(target)		// 할당된 메모리 반납
    end delete()
    ```

  * 이중 연결 List

    양쪽 방향으로 순회할 수 있도록 노드를 연결한 List

    두개의 링크 필드와 한개의 데이터 필드로 구성

    * 삽입

      ![list1](https://user-images.githubusercontent.com/50862497/72321269-cdb83180-36e6-11ea-9f81-e1b01118ea5b.JPG)

      새로운 노드 new 생성하고 데이터 필드에 data 저장

      new의 next에 cur의 next연결(다음 노드)

      cur의 next에 new 노드 연결

      new의 prev에 cur 노드 연결

      다음 노드의 prev에 new 노드 연결

      ![list2](https://user-images.githubusercontent.com/50862497/72321301-e0cb0180-36e6-11ea-87a7-22ce5d61cca5.JPG)

    * 삭제
      1. 삭제할 노드의 다음 노드의 주소를 삭제할 노드의 이전 노드의 next 필드에 저장하여 링크를 연결
      2. 삭제할 노드의 다음 노드의 prev 필드에 삭제할 노드의 이전 노드의 주소를 저장하여 링크를 연결
      3. 삭제할 노드의 다음 노드의 prev 필드에 삭제할 노드의 이전 노드의 주소를 저장하여 링크를 연결
      4. cur가 가리키는 노드에 할당된 메모리를 반환



**삽입 정렬**

* 삽입 정렬

  1. 정렬할 자료를 정렬된 부분집합 S와 정렬되지 않은 나머지 원소의 부분집합 U로 가정
  2. U의 원소를 하나씩 꺼내어 이미 정렬되어있는 S의 마지막 원소부터 비교하면서 위치를 찾아 삽입
  3. 삽입 정렬을 반복하면서 S의 원소는 하나씩 늘리고 U의 원소는 하나씩 감소하게 함
  4. 부분집합 U가 공집합이 되면 삽입정렬 완성

  O(n^2)



##### **병합 정렬**

* 병합 정렬

  여러 개의 정렬된 자료의 집합을 병합하여 한 개의 정렬된 집합으로 만드는 방식

  * 분할 정복 알고리즘 활용

    자료를 최소 단위의 문제까지 나눈 후에 차례대로 정렬하여 최종 결과를 얻어냄

    Top-Down 방식

  O(n log n)

  1. 분할 단계 : 전체 자료 집합에 대하여, 최소 크기의 부분집합이 될 때까지 분할 작업을 계속함
  2. 병합 단계 : 2개의 부분집합을 정렬하면서 하나의 집합으로 병합

  ```java
  function merge_sort(list m)
      // 사이즈가 0이거나 1인 경우, 바로 리턴
      if length(m) <= 1 then
      	return m
      // else list size is > 1, so split the list int two sublists
      // 1. DIVIDE 부분
      list left, right
      integer middle <- length(m) / 2
      for each x in m before middle
      	add x to left
      for each x in m after or equal middle
      	add x to right
      // List의 크기가 1이 될 때까지 merge_sort 재귀 호출
      left <- merge_sort(left)
      right <- merge_sort(right)
      // 분할된 List들 병합
      // 2. CONQUER part...
      return merge(left, right)
  function merge(left, right)
      var list result // 두 개의 분할된 List를 병합하여 result를 만듦
      // 서브 List의 길이가 0이 될 때까지 반복
      while length(left)>0 or length(right)>0
          if lenght(left)>0 and length(right)>0
              // 두 서브 List의 첫 원소들을 비교하여 작은 것부터 result에 추가함
              if first(left) <= first(right)
                  append first(left) to result
                  left <- rest(left)
              else
                  append first(right) to result
                  right <- rest(right)
          else if lenght(left)>0 // 왼쪽 List에 원소가 남아있는 경우
              append first(left) to result
              left <- rest(left)
          else if length(right)>0 // 오른쪽 List에 원소가 남아있는 경우
              append first(right) to result
              right <- rest(right)
      end while
  return result                
  ```



##### **List  활용**

* List를 이용한 **Stack**의 구현

  ```java
  // Push / Pop 연산의 알고리즘
  push(i)					// 원소 i를 Stack에 push
      temp = createNode()	// 새로운 노드 생성
      temp -> data = i;	// 데이터 필드 작성
  	temp -> link = top;
  	top = temp;
  end push()
  pop()					// Stack의 top을 pop
      element item;
  	stackNode* temp = top;
  	if(top == null){
          return 0;
      }else{
          item = temp -> data;
          top = temp -> link;	// top이 가리키는 노드를 바꿈
          free (temp);
          return item;
      }
  end pop()
  ```

* List를 이용한 우선순위 Queue 구현

  연결 List를 이용하여 자료 저장

  원소를 삽입하는 과정에서 List 내 노드의 원소들과 비교하여 적절한 위치에 노드를 삽입하는 구조

  List의 가장 앞쪽에 최고 우선순위가 위치하게 됨





## [Learn > Course > Programming Intermediate > Tree]



##### **Tree**

* 비선형 구조로 원소들 간에 1:n 관계를 가지는 자료구조

  원소들 간에 계층관계를 가지는 계층형 자료구조

  상위 원소에서 하위 원소로 내려가면서 확장되는 Tree 모양의 구조

* 한 개 이상의 노드로 이루어진 유한 집합

  루트(Root): 노드 중 최상위 노드

  나머지 노드들: n(>=0)개의 분리집합 T1, ..., TN으로 분리될 수 있음

* 분리집합 T1, ..., TN은 각각 하나의 Tree가 되며(재귀적 정의) 루트의 부트리(SubTree)라고 함

* ![tree](https://user-images.githubusercontent.com/50862497/72412281-4a631280-37b0-11ea-92ef-544975bb1e62.JPG)

  Tree T의 노드(node) : A, B, C, D, E, F, G, H, I, J, K

  간선(edge) : 노드를 연결하는 선

  * 루트 노드(Root node): Tree의 시작 노드 -> A

    형제 노드(Sibling node): 같은 부모 노드의 자식 노드들 -> BCD, EF, HIJ

    노상 노드(Ancestor node): 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들 -> K의 조상 노드는 F, B, A

    부트리(SubTree): 부모 노드와 연겨로딘 간선을 끊었을 때 생성되는 Tree -> A노드와 끊으면 BEFK / CG / DHIJ 가 각각 부트리가 됨

    자손 노드(Descendent node): 부트리에 있는 하위 레벨의 노드들 -> B의 자손 노드는 E, F, K

  * 차수(degree) : 노드에 연결된 자식 노드의 수 -> B의 차수=2, C의 차수=1

    Tree의 차수 : Tree에 있는 노드의 차수 중에서 가장 큰 값 -> Tree T의 차수=3

    단말 노드(리프 노드) : 차수가 0인 노드, 자식 노드가 없는 노드 -> E, K, G, H, I, J

  * 노드의 높이(레벨) : 루트에서 노드에 이르는 간선의 수 -> B의 높이=1, G의 높이=2

    Tree의 높이(최대 레벨) : Tree에 있는 노드의 높이 중에서 가장 큰 값 -> Tree T의 높이 = 3



##### **Binary Tree**

* 모든 노드들이 2개의 부트리를 갖는 특별한 형태의 Tree

  노드가 자식 노드를 최대한 2개까지만 가질 수 있는 Tree -> 왼쪽 자식 노드(Left child node), 오른쪽 자식 노드(Right child node)

* 레벨 i에서의 노드의 최대 개수는 2^i개

  높이가 h인 BinaryTree가 가질 수 있는 노드의 최소 개수는 (h+1)개, 최대 개수는((2^(h+1))-1)개



* Full Binary Tree(포화 이진 트리)

  모든 레벨에 노드가 포화상태로 차 있는 Binary Tree

  최대의 노드 개수인 ((2^(h+1))-1)의 노드를 가진 Binary Tree

  루트를 1번으로 하여 (2^(h+1))-1까지 정해진 위치에 대한 노드 번호를 가짐

* Complete Binary Tree(완전 이진 트리)

  높이가 h이고 노드 수가 n개일 때(단, h+1 <= n < (2^(h+1))-1), Full binary Tree의 노드번호 1번부터 n번까지 빈 자리가 없는 Binary Tree

* Skewed Binary Tree(편향 이진 트리)

  높이 h에 대한 최소 개수의 노드를 가지면서 **한쪽 방향의 자식 노드만을 가진 Binary Tree**



##### **순회(Traversal)**

* Tree의 각 노드를 중복되지 않게 전부 방문(Visit)하는 것

* 전위 순회(Preorder traversal)

  VLR, 자손노드보다 루트 노드를 먼저 방문

  1. 현재 노드 n을 방문하여 처리: V
  2. 현재 노드 n의 왼쪽 부트리로 이동: L
  3. 현재 노드 n의 오른쪽 부트리로 이동: R

  ```java
  preorder_traverse(T)
      if(T is not null)
          visit(T);
  		preorder_traverse(T.left);
  		preorder_traverse(T.right);
  End preorder_traverse
  ```

  

* 중위 순회(Inorder traversal)

  LVR, 왼쪽 자손, 루트, 오른쪽 자손 순으로 방문

  1. 현재 노드 n의 왼쪽 부트리로 이동: L
  2. 현재 노드 n을 방문하여 처리: V
  3. 현재 노드 n의 오른쪽 부트리로 이동: R

  ```java
  inorder_traverse(T)
      if(T is not null)
          inorder_traverse(T.left);
  		visit(T);
  		inorder_traverse(T.right);
  End inorder_traverse
  ```

  

* 후위 순회(Postorder traversal)

  LRV, 루트노드보다 자손을 먼저 방문

  1. 현재 노드 n의 왼쪽 부트리로 이동: L
  2. 현재 노드 n의 오른쪽 부트리로 이동: R
  3. 현재 노드 n을 방문하여 처리: V

  ```java
  postorder_traverse(T)
      if(T is not null)
          inorder_traverse(T.left);
  		inorder_traverse(T.right);
  		visit(T);
  End postorder_traverse
  ```

  

* Array를 이용한 Binary Tree

  노드 번호의 성질

  1. 노드 번호가 i인 노드의 부모 노드 번호 = i/2
  2. 노드 번호가 i인 노드의 왼쪽 자식 노드 번호 = 2*i
  3. 노드 번호가 i인 노드의 오른쪽 자식 노드 번호 = 2*i+1

  노드 번호를 Array의 인덱스로 사용

* 연결List를 이용한 Binayr Tree

  단순 연결 List 노드를 사용하여 구현

  

##### **Expression Tree**

* 수식 이진 트리

  수식을 표현하는 Binary Tree

  연산자는 루트 노드이거나 가지노드

  피연산자는 모두 리프 노드(단말 노드)

* 수식 표기법

  ![etree](https://user-images.githubusercontent.com/50862497/72420582-59eb5700-37c2-11ea-84ec-c84291da3efe.JPG)

  * 중위 순회 식의 중위 표기법 : A / B * C * D + E
  * 후위 순회 식의 후위 표기법 : A B / C * D * E +
  * 전위 순회 식의 전위 표기법 : + * * / A B C D E



##### **Binary search Tree**

* 탐색작업을 효율적으로 하기 위한 자룍조

  모든 원소는 서로 다른 유일한 키를 가짐

  key(왼쪽 부트리) < key(루트 노드) < key(오른쪽 부트리)

  왼쪽 부트리와 오른쪽 부트리도 Binary search Tree

  중위 순회하면 오름차순으로 정렬된 값을 얻을 수 있음

* 탐색 연산

  1. 루트에서 시작

  2. 탐색할 키 값 x를 루트 노드의 키값과 비교

     2-1. 키값 x = 루트 노드의 키값 : 원하는 원소를 찾았으므로 탐색연산 성공

     2-2. 키값 x < 루트 노드의 키값 : 루트 노드의 왼쪽 서브 Tree에 대해서 탐색연산 수행

     2-3. 키값 x > 루트 노드의 키값 : 루트 노드의 오른쪽 서브 Tree에 대해서 탐색연산 수행

  3. 부트리에 대해서 순환적으로 탐색 연산을 반복

* O(h), h:BST의 깊이(height)

  Binary Tree가 균형적인 경우 O(log n)

  최악의 경우 O(n)



##### **Heap**

* Complete binary Tree에 있는 노드 중에서 키값이 가장 큰 노드나 키값이 가장 작은 노드를 찾기 위해서 만든 자료구조

  * 최대 힙(Max heap)

    키값이 가장 큰 노드를 찾기 위한 Complete binary Tree

    부모 노드의 키 값 > 자식 노드의 키 값

    루트 노드 : 키 값이 가장 큰 노드

  * 최소 힙(Min heap)

    키값이 가장 작은 노드를 찾기 위한 Complete binary Tree

    부모 노드의 키 값 < 자식 노드의 키 값

    루트 노드 : 키 값이 가장 작은 노드

