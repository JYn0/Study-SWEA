# SW 문제해결 기본 Self Study Book



## [Learn > Course > ProgrammingIntermediate > SW 문제해결 Self Study Book I]



### [Array]

##### Gravity

```C
#include <stdio.h>
#define EMPTY 0
#define BOX 1
int main(){
	int i;
	int testCase,T;
	int roomWidth,roomHeight;
	int maxFallen;
	int room[100][100]={EMPTY,};
	int boxTop[100]={0,};
	int countEmptySpace;
	scanf("%d",&testCase);
	for(T =0;T <testCase;T++){
		scanf("%d%d",&roomWidth,&roomHeight);
		maxFallen =0;
		for(i =0;i <roomWidth;i++){ //방에상자들을채운다.
			scanf("%d",&boxTop[i]);
			for(intj =0;j <boxTop[i];j++)
				room[i][j]=BOX;
		}
		//각상자열(column)의가장위에있는상자의낙차를구한다.
		for(inti =0;i <roomWidth;i++){
			if(boxTop[i]>0){
				countEmptySpace =0;
				for(intj =i +1;j <roomWidth;j++){
					//room[i][j]가박스일때빈칸의개수를셈으로서낙차를구한다.
					if(room[j][boxTop[i]-1]==EMPTY){
						countEmptySpace +=1;
					}
				}
				//이전에구한낙차보다현재낙차가크다면업데이트한다.
				if(countEmptySpace >maxFallen){
					maxFallen =countEmptySpace;
				}
			}
		}
		printf("%d\n",maxFallen);
	}
}
/////////////////////////////////////////////////////////////
#define EMPTY 0
#define BOX 1

intmain(){
    inti,j,k;
    inttestCase;
    intT;
    introom[100]100];
    introomWidth,roomHeight;
    intboxHeight;intmaxFallen;
    intcountEmptySpace;
    scanf("%d",&testCase);
    for(T =0;T <testCase;T++){
        scanf("%d%d",&roomWidth,&roomHeight);//초기화
        for(i =0;i <roomWidth;i++){
            for(j =0;j <roomHeight;j++){
                room[i][j]=EMPTY;
            }
            maxFallen =0;
        }
        for(i =0;i <roomWidth;i++){ //방에상자들을채운다.
            scanf("%d",&boxHeight);
            for(j =0;j <boxHeight;j++){
                room[i][j]=BOX;
            }
        }
        
        //각상자의낙차를구한다.
        for(i =0;i <roomWidth;i++){
            for(j =0;j <roomHeight;j++){
                //room[i][j]가박스일때빈칸의개수를셈으로서낙차를구한다.
                if(room[i][j]==BOX){
                    countEmptySpace =0;
                    for(k =i +1;k <roomWidth;k++){
                        if(room[k][j]==EMPTY)
                            countEmptySpace +=1;
                    }
                    //이전에구한낙차보다현재낙차가크다면업데이트한다.
                    if(countEmptySpace >maxFallen)
                        maxFallen =countEmptySpace;
                }
            }
        }
        printf("%d\n",maxFallen);
    }
}
```



##### **정렬**

* 버블 정렬(Bubble Sort) : 인접한 두개의 원소를 비교하며 자리를 계속 교환하는 방식

  ```C
  // tempCount : 배열의 크기
  for(loop =0;loop <tempCount -1;loop++){
      for(i =0;i <tempCount -1-loop;i++){
          // 인접한원소가작으면교환한다.
          if(temp[i]>temp[i +1]){
              hold =temp[i];
              temp[i]=temp[i +1];
              temp[i +1]=hold;
          }
      }
  }
  ```

* 카운팅 정렬(Counting Sort) : 항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘

  ```C
  // {0, 4, 1, 3, 1, 2, 3, 1} 오름차순으로 출력
  // 각항목들발생횟수세기
  for(inti =0;i <size;i++){
      if(maxValue <data[i])maxValue =data[i];
      counts[data[i]]++;
  }
  // 각항목위치설정을위한카운트조정
  for(inti =1;i <=maxValue;i++){
      counts[i]=counts[i]+counts[i -1];
  }
  // 카운트를사용하여각항목위치결정
  for(inti =size -1;i >=0;i--){
      temp[--counts[data[i]]]=data[i];
  }
  ```

* 탐욕(Greedy) 알고리즘

  ```C
  // 10, 50, 100, 250, 500원으로 890원 거스름돈 줄이기
  int coins[]={500,250,100,50,10};
  int count[5];
  int money;
  int i =0;
  int main(){
      scanf("%d",&money);
      while(money !=0){
          if(money <0){//거스름돈을많이준경우
              count[i]--;
              money +=coins[i++];
          }
          else{//거스름돈을더주어야하는경우
              count[i]++;
              money -=coins[i];
          }
      }
      for(i =0;i <5;i++){
          printf("%d : %d\n",coins[i],count[i]);
      }
  }
  ```

  

##### Baby Gin Game

```C
scanf("%d",&input);
for(i =0;i <6;i++){//각자리숫자를카운팅
    c[(input %10)]++;
    input /=10;
}
for(i =0;i <10;i++){
    if(c[i]>=3){// triplet 조사
        c[i]-=3;
        tri +=1;
        i--;
    }
    if((c[i]>=1)&&(c[i +1]>=1)&&(c[i +2]>=1)){// run 조사
        c[i]-=1;
        c[i +1]-=1;
        c[i +2]-=1;
        run +=1;i--;
    }
}
if(run +tri ==2)
    printf("Baby Gin");
else
    printf("Lose");
```



##### 비트연산자

* AND(&), OR(|), XOR(^)

* 시프트

  * 비트 왼쪽 시프트

    0101 << 1 = 1010

    a<<b : a의 비트들을 b칸씩 왼쪽으로 이동, a*(2^b)

  * 비트 오른쪽시프트

    0101 >> 1 = 0010

    a>>b : a의 비트들을 b칸씩 오른쪽으로 이동, a/(2^b)

  * 비트 보수

    하나의 이진수의 모든 비트를 뒤집는다.

    ~0101 = 1010



##### 부분 집합의 합 해결하기

```C
// {-7, -3, -2, 5, 8} 부분집합 중 원소의 합이 0이되는 부분집합이 있는지
void main(void){
    int i,j;
    int arr[]={-7,-3,-2,5,8};
    int n =sizeof(arr)/sizeof(arr[0]);// n:원소의개수
    int sum;
    int ret = 0;
    for(i =1;i <(1<<(n));i++){// 1<<n: 부분집합의개수
        sum =0;
        for(j =0;j <n;j++){// 원소의수만큼비트를비교함
            if(i &(1<<j)){// i의j번째비트가1이면j번째원소출력
                sum +=arr[j];
            }
        }
        if(sum ==0){
            ret = 1;
            break;
        }
    }
    printf("%s\n", ret ? "True": "False");
}
```



##### 검색

* 순차 검색(Sequential Search) : 일렬로 되어 있는 자료를 순서대로 검색하는 방법

* 이진 검색 : 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정학고 검색을 계속 진행하는 방법

  ```C
  int binarySearch(int*ar,intnum,intkey){
      intup,down,mid;down =0;
      up =num -1;
      for(;;){
          // 중앙원소
          mid =(up +down)/2;
          if(ar[mid]==key)returnmid;
          // 목표값이원소보다작다면왼쪽반수행
          if(ar[mid]>key){
              up =mid -1;
          }
          else{
              down =mid +1;
          }
          // 검색이끝남
          if(up <down){
              return-1;
          }
      }
  }
  ```

  

##### 선택 정렬

* 선택정렬(Selection Sort) : 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식, 셀렉션 알고리즘을 전체 자료에 적용



##### Ladder

```C
int search(intMap[102][102],intstart){
    inty =100,x =start;
    while(y !=1){
        if(Map[y][x -1]==1){// 좌측사다리가있으면
            while(Map[y][x -1]!=0){
                x--;
            }
            y--;
        } elseif(Map[y][x +1]==1){
            while(Map[y][x +1]!=0){// 우측사다리가있으면
                x++;
            }
            y--;
        } else{
            y--;
        }
    }
    returnx;
}
int testCase,t;
int i,j;
int main(){
    int Map[102][102];
    int num_of_testcase;
    int target;
    scanf("%d",&testCase);
    for(t =0;t <testCase;t++){
        scanf("%d",&num_of_testcase);
        // 사다리초기화
        for(i =0;i <102;i++)
            for(j =0;j <102;j++)
                Map[i][j]=0;
        for(i =1;i <101;i++)
            for(j =1;j <101;j++)
                scanf("%d",&Map[i][j]);
        
        //도착지점찾기
        for(i =0;i <102;i++){
            if(Map[100][i]==2){
                target =i;
                break;
            }
        }
        printf("%d\n",search(Map,target)-1);
    }
    return0;
}
```



##### 평탄화

```C
dump(data[100],dumpCount){
    int max ← 0;// 최고높이
    int min ← 0;// 최저높이
    int maxIndex,minIndex;// 최고,최저높이의인덱스값을저장
    while(dumpCount !=0){// 카운트가0이되면loop를나옴
        max ← data[0];// 순차검색을위한초기화
        min ← data[0];
        maxIndex ← 0;
        minIndex ← 0;
        for i from 1to 99{
            if(max <data[i]){// 최고높이의상자찾기
            	max ← data[i];maxIndex ← i;
            }
            if(min >data[i]){// 최저높이의상자찾기
                min ← data[i];
                minIndex ← i;
            }
        }
        data[maxIndex]← data[maxIndex]-1;// 최고높이감소
        data[minIndex]← data[maxIndex]+1;// 최저높이증가
        dumpCount ← dumpCount -1;// 카운트감소
    }
    /* 최종덤프수행후, 최고점과최저점의높이차반환*/
    max ← data[0];// 순차검색을위한초기화
    min ← data[0];
    fori from 1to 99{
        if(max <data[i]){// 최고높이의상자찾기
            max ← data[i];
        }
        if(min >data[i]){// 최저높이의상자찾기
            min ← data[i];
        }
    }
    return max-min;
}
main(){
    int dumpCount;
    int data[100];
    for i from 0 to 9{
        read dumpCount;
        for j from 0 to 99{
            read data[j];
        }
        print '#',i+1,' ',dump(data,dumpCount);
    }
    return0;
}
```





### [String]

##### Palindrome(회문)

```C
#include <stdio.h>
int main(){
    int length;
    int count;
    int i,j,k,m;
    char map[8][8]={0,};
    bool flag;
    for(i =0;i <10;i++){
        cin >>length;
        for(j =0;j <8;j++)
            for(k =0;k <8;k++)
                cin >>map[j][k];
        count =0;for(j =0;j <8;j++){//row
            for(k =0;k <(8-length +1);k++){
                flag =true;
                for(m =0;m <(length /2);m++){
                    if(map[j][m +k]!=map[j][k +length -m -1])
                        flag =false;
                }
                if(flag)count++;
            }
        }
        for(j =0;j <8;j++){//col
            for(k =0;k <(8-length +1);k++){
                flag =true;
                for(m =0;m <(length /2);m++){
                    if(map[m +k][j]!=map[k +length -m -1][j])
                        flag =false;
                }
                if(flag)count++;
            }
        }
        cout <<count <<endl;
    }
    return0;
}
```



##### 패턴매칭

```C
int main(){
    int T,i,j,tc_len,str_len,flag=0,cnt;
    char t c[5000];
    char str[10];
    for(T=0;T<10;T++){
        tc_len =str_len =0;
        scanf("%s"str);
        scanf("%s"tc);
        while(str[str_len]!='\0')//검색할문자열의길이를구한다.
            str_len++;
        while(tc[tc_len]!='\0')//문장의길이를구한다.
            tc_len++;
        cnt =0;
        for(i=0;i<tc_len;i++){
            flag =0;
            if(tc[i]==str[0]){
                for(j=1;j<str_len;j++){
                    if(tc[i+j]!=str[j]){
                        flag =0;
                        break;
                    }
                    else
                        flag =1;
                }
            }
            if(flag)
                cnt++;
        }
        printf("%d\n",cnt);
    }
    return0;
}
```







## [Learn > Course > ProgrammingIntermediate > SW 문제해결 Self Study Book II]



### [Stack]

##### 스택(stack)

* 먼저 들어간 것이 맨 나중에 나온다

  제한적으로 접근할 수 있는나열식 자료구조

  First In Last Out or Last In First Out

  

##### 계산기

```C
int testCase;
char input[10001];
char stack[10001];
int stackCounter;
char pair[256]={0,};
int main(){
    int i;//짝이되는괄호를할당한다.
    pair[')']='(';
    pair[']']='[';
    pair['}']='{';
    scanf("%d",&testCase);
    while(testCase--){
        stackCounter =0;//스택을비운다
        scanf("%d",&i);
        scanf("%s",input);
        while(i--){
            if(input[i]=='('||input[i]=='['||input[i]=='{')
                stack[stackCounter++]=input[i];//PUSH
            else{
                if(stackCounter ==0)//짝지을괄호가없으므로무효
                	break;
            	else if(stack[stackCounter -1]==pair[input[i]])
                    //스택의탑에있는괄호와input의괄호와짝이되는지확인
                    stackCounter--;//POP
                else//짝이되지않으므로무효break;
            }
        }
        if(i ==-1&&stackCounter ==0)
            printf("1\n");
        else
            printf("0\n");
    }
}
```



##### 후위 표기법

```C
#define STACK_MAX_SIZE 1000
#define STRING_MAX_LENGTH 1000//입력된수식을후위표기법으로변경하기위한스택
char notationStack[STACK_MAX_SIZE];
int notationStackCount;
int notationStackPush(char c);
int notationStackPop(char &c);
int notationStackTop(char &c);
int notationStackIsEmpty();
int notationStackIsFull();//후위표기법으로표기된수식을계산하기위한스택
int calculationStack[STACK_MAX_SIZE];
int calculationStackCount;
int calculationStackPush(int i);
int calculationStackPop(int &i);
int calculationStackTop(int &i);
int calculationStackIsEmpty();
int calculatuinStackIsFull();//연산자우선순위
int priority(char c){
    if(c =='(')return5;elseif(c =='*')
        return1;
    else if(c =='+')
        return2;
    else return-1;
}
int main()
{
    int length;//입력되는수식의길이
    char input[STRING_MAX_LENGTH];//입력되는수식
    char ans[STRING_MAX_LENGTH];//수식을후위표기법으로저장
    int ansLength;//후위표기법으로표기된수식의길이
    int temp;
    char temp2;
    char temp3;
    int &i_temp =temp;
    char &c_temp =temp2;
    char &c_temp2 =temp3;
    int i,j;
    int t;
    scanf("%d",&t);
    while(t--){
        notationStackCount =0;
        calculationStackCount =0;
        ansLength =0;
        
        //입력된수식을후위표기법으로변경하기
        for(j =0;j <length;j++){
            if(input[j]>='0'&&input[j]<='9'){
                ans[ansLength]=input[j];
                ansLength++;
            }else{
                if(input[j]=='(')
                    notationStackPush(input[j]);
                else if(input[j]==')'){
                    notationStackTop(c_temp);
                    while(c_temp !='('){
                        notationStackPop(c_temp2);
                        ans[ansLength]=c_temp2;
                        ansLength++;notationStackTop(c_temp);
                    }
                    notationStackPop(c_temp2);
                }else{
                    notationStackTop(c_temp);
                    if(notationStackIsEmpty()!=1){
                        while(priority(input[j])>=priority(c_temp)){
                            notationStackPop(c_temp2)
                                ans[ansLength]=c_temp2;
                            ansLength++;
                            notationStackTop(c_temp);
                            if(notationStackIsEmpty()==1)
                                break;
                        }
                    }
                    notationStackPush(input[j]);
                }
            }
        }while(notationStackIsEmpty()!=1){
            notationStackPop(c_temp2);
            ans[ansLength]=c_temp2;ansLength++;
        }
        
        //계산하기
        int x;
        int y;
        int &xx =x;
        int &yy =y;
        for(j =0;j <ansLength;j++){
            if(ans[j]>='0'&&ans[j]<='9'){
                calculationStackPush((int)(ans[j]-48));
            }elseif(ans[j]=='*'){
                calculationStackPop(xx);
                calculationStackPop(yy);
                calculationStackPush(xx *yy);
            }elseif(ans[j]=='+'){
                calculationStackPop(xx);
                calculationStackPop(yy);
                calculationStackPush(xx +yy);
            }
        }
        calculationStackPop(xx);
        printf("%d\n",xx);
    }
    return0;
}
```



##### 깊이 우선 탐색(DFS)

* DFS(Depth First Search / 깊이 우선 탐색)

  비선형 구조인 그래프 구조에서 그래프 형태로 표현된 모든 자료를 빠짐없이 검색하는 하나의 방법

  시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 돌아와서 다른 방향의 정점으로 탐색을 반복하여 결구 모든 정점을 방문하는 순회방법

  ```C
  int stack[8]={0,};
  int top =-1;
  int visited[8]={0,};
  int arr[8][8]={0,};
  void push(int v){
      printf("%d ",v);
      stack[++top]=v;
      visited[v]=1;
      return;
  }
  void pop(){
      top--;
      return;
  }
  void dfs(int v){
      push(v);
      while(top >=0){
          for(inti =1;i <=7;i++){
              if(visited[i]==0&&arr[stack[top]][i]==1){
                  push(i);
                  i =1;
              }
          }
          pop();
      }
  }
  int main(){
      int a,b;
      for(inti =0;i <7;i++){
          scanf("%d %d",&a,&b);
          arr[a][b]=1;
          arr[b][a]=1;
      }
      dfs(1);
      return0;
  }
  ```



##### 백트래킹 기법

* 백트래킹

  해를 찾는 도중에 막히면 즉, 해가 아닌 것이 확실해 지면, 다시 돌아가서 다시 해를 찾아 가는 기법

  DFS에 기본을 두고 있음

  최적화 문제와 결정 문제를 해결할 수 있음

  DFS 발전한 기법

  ```C
  int visited[8]={0,};
  int arr[8][8]={0,};
  void dfs(int v){
      printf("%d ",v);
      visited[v]=1;
      for(inti =1;i <=7;i++){
          if(visited[i]==0&&arr[v][i]==1){
              dfs(i);
          }
      }
  }
  int main(){
      int a,b;
      for(int i =0;i <7;i++){
          scanf("%d %d",&a,&b);
          arr[a][b]=1;
          arr[b][a]=1;
      }
      dfs(1);
      return0;
  }
  ```



##### 미로찾기

```C
// 스택 사용
#define MAX_MAZE_SIZE 100
#define IS_VISITED 1
#define NOT_VISITED 0
#define POSSIBLE_WAY 1
#define IMPOSSIBLE_WAY 0
int testCase;
int w,h;
int maze[MAX_MAZE_SIZE][MAX_MAZE_SIZE];//미로
int visited[MAX_MAZE_SIZE][MAX_MAZE_SIZE];//각칸에방문했는지에대한정보
int i,j;
char input[MAX_MAZE_SIZE]; 
int finePath(int x,int y){
    inttempResult =0;
    if(maze[x][y]==1||visited[x][y]==IS_VISITED)//벽이거나이미방문했던곳이면더이상진행하지않는다.
        returnIMPOSSIBLE_WAY;
    elseif(maze[x][y]==3)//출구를찾은경우
        returnPOSSIBLE_WAY;
    else{//갈수있는길이면4방향에대해서갈수있는지조사한다.
        visited[x][y]=IS_VISITED;//현재위치를지나온길로표시한다.
        
        //4방향에대해서이동할수있는지판단한다.
        tempResult +=finePath(x -1,y);
        tempResult +=finePath(x +1,y);
        tempResult +=finePath(x,y -1);
        tempResult +=finePath(x,y +1);
        
        //되돌아갈때지나온길로표시해둔것을해제한다.
        visited[x][y]=NOT_VISITED;
        return tempResult;
    }
}
int main(){
    scanf("%d",&testCase);
    while(testCase--){
        //초기화
        for(i =0;i <MAX_MAZE_SIZE;i++){
            for(j =0;j <MAX_MAZE_SIZE;j++){
                maze[i][j]=1;
                visited[i][j]=NOT_VISITED;                   
            }
        }
        scanf("%d%d",&w,&h);
        for(i =0;i <h;i++){
            scanf("%s",input);
            for(j =0;j <w;j++){
                maze[i][j]=input[j]-'0';
            }
        }
        if(finePath(1,1)>0)
            printf("1\n");
        else printf("0\n");
    }
}
```

```C
#define TRUE 1
#define FALSE 0
type defstruct{
    intx,y;
}PAIR;

int g_map[100][100];
char g_resultmap[100][100];
PAIR g_stack[10000];
int g_top;
int main(){
    int T;
    int start_x,start_y,now_x,now_y;
    int is_findpath;
    int W,H,i,j;
    char str[101];
    scanf("%d",&T);
    while(T--){
        is_findpath =FALSE;
        g_top =0;
        scanf("%d%d",&W,&H);
        for(i =0;i <H;i++){
            scanf("%s",str);
            for(j =0;j <W;j ++){
                if(str[j]=='2'){
                    start_x =j;
                    start_y =i;
                }
                g_map[i][j]=str[j]-'0';
            }
        }
        //시작점Push
        g_stack[g_top].x =start_x;
        g_stack[g_top].y =start_y;
        g_top++;
        while(g_top){
            now_x =g_stack[g_top -1].x;
            now_y =g_stack[g_top -1].y;
            if(g_map[now_y][now_x]==3){
                //도착지점인경우
                is_findpath =TRUE;
                break;
            }
            g_map[now_y][now_x]=1;
            if(now_x >0&&g_map[now_y][now_x -1]!=1){
                //Push
                g_stack[g_top].x =now_x -1;
                g_stack[g_top].y =now_y;
                g_top++;
            }elseif(now_x <W -1&&g_map[now_y][now_x +1]!=1){
                //Push
                g_stack[g_top].x =now_x +1;
                g_stack[g_top].y =now_y;
                g_top++;
            }else if(now_y >0&&g_map[now_y -1][now_x]!=1){
                //Push
                g_stack[g_top].x =now_x;
                g_stack[g_top].y =now_y -1;
                g_top++;
            }else if(now_y <H -1&&g_map[now_y +1][now_x]!=1){
                //Push
                g_stack[g_top].x =now_x;
                g_stack[g_top].y =now_y +1;
                g_top++;
            }else{
                //갈곳이없는경우Pop
                g_top--;
            } 
        }
        if(is_findpath ==FALSE)//경로가없는경우
            printf("Can not Find Path.\n");
        else//경로가있는경우
            for(i =0;i <H;i++)
                for(j =0;j <W;j++)
                    g_resultmap[i][j]='X';
        	while(g_top){
            	g_top--;
            	now_x =g_stack[g_top].x;
            	now_y =g_stack[g_top].y;
            	g_resultmap[now_y][now_x]='.';
        	}
        	for(i =0;i <H;i++){
            	for(j =0;j <W;j++){
                	printf("%c",g_resultmap[i][j]);
            	}
            	printf("\n");
        	}
    	}
	}
	return0;
}
```



##### Memoization

* 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술

  ```C
  int f(int n){
      A[0]=0;
      A[1]=1;
      for(inti =2;i <=n;i++){
          A[i]=A[i -1]+A[i -2];
      }
      returnA[n];
  }
  ```

  

##### 동적 계획법(Dynamic Programming)

* Memoization을 기반으로 한 계획법

  * Optimal Substructure

    큰 문제의 최적 솔루션에 작은 문제의 최적 솔루션이 포함되는 경우

  * Overlapping Recursive Calls

    재귀적 해법으로 풀면 같은 문제에 대한 재귀호출이 심하게 중복되는 경우

* Bottom-Up 상향식 방법

  ```C
  #define MAXSIZE 1000
  int f(int n){
      int i;
      int A[MAXSIZE];
      A[0]=0;
      A[1]=1;
      for(i =2;i <=n;i++){
          A[i]=A[i -1]+A[i -2];
      }
      returnA[n];
  }
  int main(){
      int n;
      scanf("%d",&n);
      printf("%d\n",f(n));
      return0;
  }
  ```

  

##### 피보나치 수열

```C
#define MAXSIZE 1000
int f(int n){
    int i;
    int A[MAXSIZE];
    A[0]=0;
    A[1]=1;
    for(i =2;i <=n;i++){
        A[i]=A[i -1]+A[i -2];
    }
    returnA[n];
}
int main(){
    int n;
    scanf("%d",&n);
    printf("%d\n",f(n));
    return0;
}
```





### [Queue]

##### Queue

* 먼저 넣은 데이터가 먼저 나오는 First In First Out 구조로 저장하는 형식
  * 선형 큐
  * 원형 큐
  * 연결 리스트 큐
  * 우선 순위 큐



##### 너비 우선 탐색(BFS)

* BFS(Breadth First Search)

  탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식

  큐를 이용하여 앞으로 방문할 정점을 표시

```C
#define QUEUE_SIZE 10001
#define MAX_VERTEX_COUNT 10001
#define TRUE 1
#define FALSE 0
#define IS_VISITED 1
#define NOT_VISITED 0
int queue[QUEUE_SIZE];
int front;
int rear;
int isEmpty()
int isFull()
void enQueue(int item)
int deQueue()
void createQueue()
int Qpeek()
int t;
int n;//정점의개수
int m;//간선의개수
int i,j;
int a,b;//입력되는두정점
int adjacent[MAX_VERTEX_COUNT][MAX_VERTEX_COUNT];//정점들이연결이되어있는지파악
int visited[MAX_VERTEX_COUNT];//각노드에방문했는지에대한정보
int visitingVertex;// 현재방분하는정점의인덱스, 인접한정점을찾는데사용된다.
int main(){
    scanf("%d",&t);
    while(t--){
        //초기화
        for(i =1;i <=n;i++){
            visited[i]=NOT_VISITED;
            for(j =1;j <=n;j++){
                adjacent[i][j]=FALSE;
            }
        }
        scanf("%d%d",&n,&m);
        //두정점이주어지면두정점을연결이되어있는것으로표시
        for(i =0;i <m;i++){
            scanf("%d%d",&a,&b);
            adjacent[a][b]=TRUE;
            adjacent[b][a]=TRUE;
        }
        //큐생성
        createQueue();
        //첫시작점인정점1을큐에넣고, 방문한것으로표시
        enQueue(1);
        visited[1]=IS_VISITED;
        while(isEmpty()==FALSE){
            visitingVertex =deQueue();
            printf("%d ",visitingVertex);
            //인접한정점을찾는다.
            for(i =1;i <=n;i++){
                if(adjacent[visitingVertex][i]==TRUE &&visited[i]==FALSE){
                    enQueue(i);
                    visited[i]=IS_VISITED;
                }
            }
        }
        printf("\n");
    }
    return0;
}
```





## [Learn > Course > ProgrammingIntermediate > SW 문제해결 Self Study Book III]



### [List]

##### 리스트

* 순서를 가진 데이터의 집합을 가리키는 추상자료형

  동일한 데이터를 가지고 있어도 상관없음

  * 순차리스트

  * 연결리스트

    자료의 논리적인 순서와 메모리 상의 물리적인 순서가 일치하지 않고, 개별적으로 위차하고 있는 원소의 주소를 연결하여 하나의 전체적인 자료구조를 이룸

    링크를 통해 원소에 접근

* 삽입정렬

* 병합정렬



##### Josephus Problem

```C
#include<stdio.h>
#include<malloc.h>
struct NODE{
    int index;
    NODE* link;
};
int main(){
    int N,K,i,j;
    NODE * delete_node;
    NODE * first =(NODE*)malloc(sizeof(NODE));
    NODE * node =first;
    scanf("%d%d",&N,&K);
    //첫번째노드생성
    node->index =1;
    for(i =2;i <=N;i++){
        node->link =(NODE*)malloc(sizeof(NODE));
        node =node->link;
        node->index =i;
    }
    //마지막노드와첫노드를연결해준다.
    node->link =first;
    node =node->link;
    for(i =0;i <N -1;i++){
        //node를K -1만큼이동시킨다.
        for(j =1;j <K;j++){
            node =node->link;
        }
        //node의다음노드를지운다.
        delete_node =node->link;
        node->link =delete_node->link;
        free(delete_node);
        node =node->link;
    }
    printf("%d\n",node->index);
    return0;
}
```





### [Tree]

##### 트리

* 자료들 사이가 1:n(n>=0)의 관계를 가지며 부분집합도 재귀적으로 같은 정의가 적용되는 자료 구조

  비선형 구조

  원소들 간에 1:n관계를 가지는 자료구조

  원소들 간의 계층관계를 가지는 계층형 자료구조

  상위 원소에서 하위 원소로 내려가면서 확장되는 나무 모양의 구조

* 이진 트리(Binary tree)

  한 노드가 최대 두개의 자손 노드를 가지는 트리

  * 포화 이진 트리

    모든 레벨에 노드가 포화상태로 차 있는 이진 트리

    높이가 h일때, 최대의 노드 개수인 (2^(h+1))-1의 노드를 가진 이진 트리

  * 완전 이진 트리(Complete Binary Tree)

    높이가 h이고 노드 수가 n개일 때의 이진 트리

  * 편향 이진 트리(Skewed Binary Tree)

* 이진 트리의 순회(Traversal)

  트리의 각 노드를 중복되지 않게 전부 방문하는 것

  루트 V, 왼쪽 서브트리 L, 오른쪽 서브트리 R

  전위 순회(VLR) : 자손노드보다 루트노드를 먼저 방문

  중위 순회(LVR) : 왼쪽 자손, 루트, 오른쪽 자손 순으로 방문

  후위 순회(LRV) : 루트노드보다 자손을 먼저 방문

  ```C
  struct Node{
      int data;// 노드의값
      Node *left;// 왼쪽서브트리
      Node *right;// 오른쪽서브트리
  };Node *Root;
  Root =(Node*)malloc(sizeof(Node));// 루트노드생성
  Root->data =data;// 루트노드에값삽입
  /* 반복과정*/
  Node *New;// 새로운노드생성
  New =(Node *)malloc(sizeof(Node));// 새로운노드
  New->data =data;// 새로운노드값삽입
  New->left =NULL;// 빈값으로초기화N
  ew->right =NULL;
  if(bLeft){// 부모노드가새로운노드를찾을수있게참조
      Parent->left =New;
  }else{
      Parent->right =New;
  }
  /* 전위순회*/
  void preorder_traverse(Node *R){
      printf("%d ",R->data);
      if(R->left)
          preorder_traverse(R->left);
      if(R->right)
          preorder_traverse(R->right);
  }
  /* 중위순회*/
  void inorder_traverse(Node *R){
      if(R->left)
          inorder_traverse(R->left);
      printf("%d ",R->data);
      if(R->right)
          inorder_traverse(R->right);}
  /* 후위순회*/
  void postorder_traverse(Node *R){
      if(R->left)
          postorder_traverse(R->left);
      if(R->right)postorder_traverse(R->right);
      printf("%d ",R->data);
  }
  ```



* 이진 탐색 트리

  ```C
  // 이진탐색트리탐색
  int search(int value){
      // 노드의순회
      Node *Temp =Root;
      while(Temp){
          // 찾으려는노드의값이더큰경우, 오른쪽으로
          if(Temp->value <value){
              Temp =Temp->right;
          }
          // 찾으려는노드의값이더작은경우, 왼쪽으로
          else if(Temp->value >value){
              Temp =Temp->left;
          }else if(Temp->value ==value){
              return 1;
          }
      }
      return 0;
  }
  ```

  

##### 힙

- Heap

  완전 이진트리에 있는 노드 중에서 키값이 가장 큰 노드나 키값이 가장 작은 노드를 찾기 위해서 만든 자료구조

  힙의 삭제는 항상 루트의 원소 삭제해야 함



##### 중위순회

```C
#include <stdio.h>
struct _Node{
    char word;
    int left;
    int right;
}node[101];
int N,addr;
char str[10];
// 중위순회
void solve(int v){
    if(node[v].left  >0)
        solve(node[v].left);
    printf("%c",node[v].word);
    if(node[v].right >0)
        solve(node[v].right);
}
// 입력값
void input(){
    int i;
    for(i=0;i <N;i++){
        scanf("%d",&addr);
        scanf("%s",str);
        node[addr].word =str[0];
        node[addr].left =0,node[addr].right =0;
        // N가지의정점이존재한다. 
        // 입력정점의단말노드를체크
        if(addr *2<=N){
            scanf("%d ",&node[addr].left);
            if(addr *2+1<=N)// 입력정점의오른쪽자손노드
                scanf("%d ",&node[addr].right);
        }
    }
}
int main(){
    int test_case;
    for(test_case =1;test_case <=2;test_case++){
        scanf("%d",&N);
        input();
        solve(1);
        printf("\n");
    }
    return 0;
}
```



##### 수식 트리

* 수식 이진 트리(Expression Binary Tree)

  연산자는 루트노드이거나 가지노드, 피연산자는 모두 단말노드



##### 사칙연산 유효성 검사

노드의 데이터는 node 배열에 저장한다.

왼쪽 자손은 (현재 노드 번호)X2이고, 오른족 자손은 (현재 노드 번호)X2+1

왼쪽 자손의 노드 번호와 오른쪽 자손의 노드 번호는 각각 따로 left, right를 만들어 저장

전역변수로 수식의 유효성 여부를 체크할 bool형 flag 선언

입력받은 데이터의 저장이 끝났으면, 현재 위치를 1로 초기화하고, 중위순회

부모 노드에는 자손 노드가 존재할 시, 왼쪽과 오른쪽 노드가 둘 다 있어야 함

그리고 계산을 하기 위해서는 리프노드는 숫자노드이어야 함

```C
#include <stdio.h>
#include <malloc.h>
struct _Node{
    int value; 
    char opp;
    int left;
    int right;
}node[1001];
int N,a;// 정점의개수, 정점번호
char a2[20];// 한줄단위
int state =1;// 결과
// 입력값받기
voidinput(){
    int b[3]={0,},top =0;
    int i;
    scanf("%d\n",&a);// 정점번호
    gets(a2);// 그다음한줄읽기
    int t =1;
    for(i =1;a2[i];i++){        
        if(a2[i]>='0'&&a2[i]<='9'){// 숫자
            a2[i]=a2[i]-'0';
            b[top]=b[top]*t +a2[i];
            t =10;
        }else if(a2[i]!=' '){// 연산자
            if(top ==0)
                node[a].opp =a2[i];
            else if(top ==1)
                node[a].left =a2[i];
            else
                node[a].right =a2[i];
            b[top]=-1,top++;
            t =1;continue;
        }
        
        if(a2[i +1]==' '||a2[i +1]=='\0'){// 띄어쓰기또는한줄이끝났을경우
            if(b[top]!=-1){
                if(top ==0)
                    node[a].value =b[top];
                else if(top ==1)
                    node[a].left =b[top];
                else
                    node[a].right =b[top];
            }
            top++,t =1;//continue;
        }
    }
}
// 중위순회
void solve(int v){
    if(node[v].left >0)
        solve(node[v].left);
    // 연산자인경우, 두개의자손노드가존재해야한다.
    if(node[v].opp >=42&&node[v].opp <=47){
        if(node[v].left ==0||node[v].right ==0){
            state =0;
        }
    }
    // 숫자인경우, 두개의자손노드가존재하면안된다.
    else if(node[v].value >0)
        if(!(node[v].left ==0&&node[v].right ==0)){
            state =0;
        }
    
    if(node[v].right >0)
        solve(node[v].right);
}
int main(){
    int test_case,i;
    for(int test_case =1;test_case <=10;test_case++){
        scanf("%d",&N);
        for(inti =0;i <N;i++){
            input();
        }
        state =1;
        solve(1);//중위순회
        // 결과
        printf("#%d ",test_case);
        if(state)
            printf("1\n");
        else
            printf("0\n");
        // 초기화
        for(i =0;i<1001;i++){
            node[i].left =0,node[i].right =0,node[i].opp =' ',node[i].value =0;
        }
    }
    return 0;
}
```



##### 사칙연산

연산자 노드가 가지는 서브트리는 두개의 서브트리가 존재해야한다.

숫자 노드가 가지는 서브트리는 서브트리가 존재하면 안된다.

중위순회로 접근

왼쪽서브트리와 오른쪽서브트리를 방문한 다음, 자신의 노드에 접근할때, 자신의 노드는 연산자가 되므로 이때 계산을 해야함

```C
#include <stdio.h>
#include <malloc.h>
struct _Node{
    int value;
    char opp;
    int left;
    int right;
}node[10001];
int N,a,num1,num2;
char a2[10000];
// 입력값받기
void input(){
    scanf("%d %s",&a,a2);
    // 정점이양의정수인지, 연산자인지확인
    if(a2[0]>='0'&&a2[0]<='9'){
        node[a].value =atoi(a2);
        node[a].left =0,node[a].right =0;
    }else{
        scanf("%d %d",&num1,&num2);
        node[a].opp =a2[0];
        node[a].left =num1;
        node[a].right =num2;
    }
}
// 후위순회
void solve(int v){
	if(node[v].left >0)
    	solve(node[v].left);
    if(node[v].right >0)
        solve(node[v].right);
    // 현재정점이연산자일경우왼쪽과오른쪽서브트리연산
    if(node[v].opp =='+')
        node[v].value =node[node[v].left].value +node[node[v].right].value;
    else if(node[v].opp =='-')
        node[v].value =node[node[v].left].value -node[node[v].right].value;
    else if(node[v].opp =='*')
        node[v].value =node[node[v].left].value *node[node[v].right].value;
    else if(node[v].opp =='/')
        node[v].value =node[node[v].left].value /node[node[v].right].value;
}
int main(){
    int test_case,i;
    for(test_case =1;test_case <=10;test_case++){
        scanf("%d",&N);
        for(i =0;i <N;i++){
            input();
        }
        solve(1);
        printf("#%d %d\n",test_case,node[1].value);
        for(i =1;i <=N;i++)
            node[i].left =0,node[i].right =0,node[i].value =0,node[i].opp =' ';
    }
    return 0;
}
```

