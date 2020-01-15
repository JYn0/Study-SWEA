# SW 문제해결 기본

[Learn > Course > Programming Intermediate > Tree]

## 1231. [S/W 문제해결 기본] 9일차 - 중위순회 D4

다음은 특정 단어(또는 문장)를 트리 형태로 구성한 것으로, in-order 형식으로 순회하여 각 노드를 읽으면 원래 단어를 알 수 있다고 한다.


![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XZLzKDdkBBASl)


위 트리를 in-order 형식으로 순회할 경우 SOFTWARE 라는 단어를 읽을 수 있다.

**[제약 사항]**

총 10개의 테스트 케이스가 주어진다.

총 노드의 개수는 100개를 넘어가지 않는다.

트리는 완전 이진 트리 형식으로 주어지며, 노드당 하나의 알파벳만 저장할 수 있다.

노드가 주어지는 순서는 아래 그림과 같은 숫자 번호대로 주어진다.

![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XZQcKDdoBBASl)

**[입력]**

각 테스트 케이스의 첫 줄에는 각 케이스의 트리가 갖는 정점의 총 수 N(1≤N≤100)이 주어진다. 그 다음 N줄에 걸쳐 각각의 정점 정보가 주어진다.

해당 정점에 대한 정보는 해당 정점의 알파벳, 해당 정점의 왼쪽 자식, 오른쪽 자식의 정점번호가 차례대로 주어진다.

정점번호는 1부터 N까지의 정수로 구분된다. 입력에서 정점 번호를 매기는 규칙은 위와 같으며, 루트 정점의 번호는 반드시 1이다.

입력에서 이웃한 알파벳이나 자식 정점의 번호는 모두 공백으로 구분된다.

위의 예시에서, 알파벳 S가 7번 정점에 해당하면 “7 S”으로 주어지고, 알파벳 ‘F’가 2번 정점에 해당하면 두 자식이 각각 알파벳 ‘O’인 4번 정점과 알파벳 ‘T’인 5번 정점이므로 “2 F 4 5”로 주어진다.

총 10개의 테스트 케이스가 주어진다,

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 답을 출력한다.  

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

class Solution
{
	public static String answer;
	
	public static void inorder_tree(int node, int N, String[] word) {
		if(1<=node && node<=N) {
			inorder_tree(node*2, N, word);
			answer += word[node];
			inorder_tree(node*2+1, N, word);
		}
	}
	
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		
		for(int test_case=1; test_case<11; test_case++) {
			st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken());
			
			String word[] = new String[N+1];
			for(int i=0; i<N; i++) {
				answer = "";
				st = new StringTokenizer(br.readLine());
				int num = Integer.parseInt(st.nextToken()); // 어차피 N이랑 같아서 버려도됨
				word[num] = st.nextToken();
				while(st.hasMoreTokens()) {
					st.nextToken(); // 버리기
				}
			}
			
			inorder_tree(1, N, word);
			System.out.println("#"+test_case+" "+answer);
		}
	}
}
```



## 1233. [S/W 문제해결 기본] 9일차 - 사칙연산 유효성 검사 D4

사칙연산으로 구성되어 있는 식은 이진 트리로 표현할 수 있다.

아래는 식 “(8/2)*(6-4)”을 이진 트리로 표현한 것이다.

임의의 정점에 연산자가 있으면 해당 연산자의 왼쪽 서브 트리의 결과와 오른쪽 서브 트리의 결과를 사용해서 해당 연산자를 적용한다.


 ![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XZqfqDeQBBASl)


사칙연산 “+, -, *, /”와 양의 정수로만 구성된 임의의 이진 트리가 주어질 때, 이 식의 유효성을 검사하는 프로그램을 작성하여라.

여기서 말하는 유효성이란, 사칙연산 “+, -, *, /”와 양의 정수로 구성된 임의의 식이 적절한 식인지를 확인하는 것으로, 계산이 가능하다면 “1”, 계산이 불가능할 경우 “0”을 출력한다.

(단, 계산이 가능한지가 아닌 유효성을 검사하는 문제이므로 

0으로 나누는 경우는 고려하지 않는다.

 )

 

​       ![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XZufqDeUBBASl)![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XZ4V6DeYBBASl)                         

 

​            
[연산이 가능한 경우]                                                  [연산이 불가능한 경우]

**[제약 사항]**

총 10개의 테스트 케이스가 주어진다.

총 노드의 개수는 200개를 넘어가지 않는다.

트리는 완전 이진 트리 형식으로 주어지며, 노드당 하나의 연산자 또는 숫자만 저장할 수 있다.

노드는 아래 그림과 같은 숫자 번호대로 주어진다.

 

![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XaGO6DecBBASl)


**[입력]**

각 테스트 케이스의 첫 줄에는 각 케이스의 트리가 갖는 정점의 총 수 N(1≤N≤200)이 주어진다.

그 다음 N줄에 걸쳐 각각의 정점 정보가 주어진다.

해당 정점에 대한 정보는 해당 정점의 알파벳, 해당 정점의 왼쪽 자식, 오른쪽 자식의 정점번호가 차례대로 주어진다.

정점 번호는 1부터 N까지의 정수로 구분된다. 입력에서 정점 번호를 매기는 규칙은 위와 같으며, 루트 정점의 번호는 반드시 1이다.

입력에서 이웃한 숫자 또는 연산자, 자식 정점의 번호는 모두 공백으로 구분된다.

위의 예시에서, 숫자 8이 4번 정점에 해당하면 “4 8”으로 주어지고, 연산자 ‘/’가 2번 정점에 해당하면 두 자식이 각각 숫자 ‘8’인 4번 정점과 숫자 ‘2’인 5번 정점이므로 “2 / 4 5”로 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 정답을 출력한다.

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

class Solution
{
	public static void main(String args[]) throws Exception
	{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		for(int test_case=1; test_case<11; test_case++) {
			int answer = 0;
			st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken());
			String data[] = new String[N+1];
			for(int i=0; i<N; i++) {
				st = new StringTokenizer(br.readLine());
				int num = Integer.parseInt(st.nextToken());
				data[num] = st.nextToken();
				while(st.hasMoreTokens()) {
					st.nextToken();
				}
			}

			for(int i=1; i<=N; i++) {
				if(N/2 < i) { // leaf node 검사
					if(data[i].equals("+") || data[i].equals("-") || data[i].equals("*") || data[i].equals("/")) {
						answer = 0;
                        break;
					}else {
						answer = 1;
						break;
					}
				}else { // leaf node 아닌곳은 숫자이면 X
					if(data[i].equals("+") || data[i].equals("-") || data[i].equals("*") || data[i].equals("/")) {
					}else {
						answer = 0;
						break;
					}
				}
			}
			System.out.println("#"+test_case+" "+answer);
		}

	}
}
```



## 1232. [S/W 문제해결 기본] 9일차 - 사칙연산 D4

사칙연산으로 구성되어 있는 식은 이진 트리로 표현할 수 있다. 아래는 식 “(9/(6-4))*3”을 이진 트리로 표현한 것이다.

임의의 정점에 연산자가 있으면 해당 연산자의 왼쪽 서브 트리의 결과와 오른쪽 서브 트리의 결과를 사용해서 해당 연산자를 적용한다.


 ![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XZexKDeABBASl)

사칙연산 “+, -, *, /”와 양의 정수로만 구성된 임의의 이진트리가 주어질 때, 이를 계산한 결과를 출력하는 프로그램을 작성하라.

단, 중간 과정에서의 연산은 실수 연산으로 하되, 최종 결과값이 정수로 떨어지지 않으면 정수부만 출력한다.

위의 예에서는 최종 결과값이 13.5이므로 13을 출력하면 된다.

[제약 사항]

정점의 총 수 N은 1≤N≤1000.

[입력]

각 테스트 케이스의 첫 줄에는 각 케이스의 트리가 갖는 정점의 총 수 N(1≤N≤1000)이 주어진다. 그 다음 N줄에 걸쳐 각각의 정점 정보가 주어진다.

정점이 단순한 수이면 정점번호와 해당 양의 정수가 주어지고, 정점이 연산자이면 정점번호, 연산자, 해당 정점의 왼쪽 자식, 오른쪽 자식의 정점번호가 차례대로 주어진다.

정점번호는 1부터 N까지의 정수로 구분된다. 입력에서 정점 번호를 매기는 특별한 규칙은 없으나, 루트 정점의 번호는 반드시 1이다.

입력에서 이웃한 수나 연산자는 모두 공백으로 구분된다.

위의 예시에서, 숫자 4가 7번 정점에 해당하면 “7 4”으로 주어지고, 연산자 ‘/’가 2번 정점에 해당하면 두 자식이 각각 숫자 9인 4번 정점과 연산자 ‘-’인 5번 정점이므로 “2 / 4 5”로 주어진다.

총 10개의 테스트 케이스가 주어진다.

[출력]

#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스에 대한 답을 출력한다. 답은 항상 정수값으로 기록한다.

```java

```

