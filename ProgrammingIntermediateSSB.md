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

