# SW 문제해결 기본

[Learn > Course > Programming Intermediate > Stack1]

## 1217. [S/W 문제해결 기본] 4일차 - 거듭 제곱 D3

다음과 같이 두 개의 숫자 N, M이 주어질 때, N의 M 거듭제곱 값을 구하는 프로그램을 재귀호출을 이용하여 구현해 보아라.

2 5 = 2 X 2 X 2 X 2 X 2 = 32

3 6 = 3 X 3 X 3 X 3 X 3 X 3 = 729

[제약 사항]

총 10개의 테스트 케이스가 주어진다.

결과 값은 Integer 범위를 넘어가지 않는다.

[입력]

각 테스트 케이스의 첫 줄에는 테스트 케이스의 번호가 주어지고 그 다음 줄에는 두 개의 숫자가 주어진다.

[출력]

#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스에 대한 답을 출력한다.

```java
import java.util.Scanner;

class Solution
{
    static int raisetopower(int N, int M) {
		if(M == 1) {
			return N;
		}
		return N*raisetopower(N, M-1);
	}
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		for(int test_case = 1; test_case <= 10; test_case++) {
			int T = sc.nextInt();
			int N = sc.nextInt();
			int M = sc.nextInt();
			int answer = raisetopower(N, M);
			System.out.println("#"+T+" "+answer);
		}
		sc.close();
	}
    /*
	public static void main(String args[]) throws Exception
	{
        Scanner sc = new Scanner(System.in);
		for(int test_case = 1; test_case <= 10; test_case++) {
			int T = sc.nextInt();
			int N = sc.nextInt();
			int M = sc.nextInt();
			int answer = N;
			for(int i=1; i<M; i++) {
				answer *= N;
			}
			System.out.println("#"+T+" "+answer);
		}
		sc.close();
	}
	*/
}
```



## 1218.  [S/W 문제해결 기본] 4일차 - 괄호 짝짓기 D4

 4 종류의 괄호문자들 '()', '[]', '{}', '<>' 로 이루어진 문자열이 주어진다.

이 문자열에 사용된 괄호들의 짝이 모두 맞는지 판별하는 프로그램을 작성한다.

  **[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트케이스의 길이가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 유효성 여부를 1 또는 0으로 표시한다 (1 - 유효함, 0 - 유효하지 않음).    

```java
import java.util.Scanner;
import java.util.Stack;

class Solution
{
	public static void main(String args[]) throws Exception
	{
        Scanner sc = new Scanner(System.in);
		for(int test_case = 1; test_case <= 10; test_case++)
		{
			int answer = 1;
			int N = sc.nextInt();
			String str = sc.next();
			Stack<Character> s = new Stack<Character>();
			for(int i=0; i<N; i++) {
				if(str.charAt(i) == '(' || str.charAt(i) == '[' || str.charAt(i) == '{' || str.charAt(i) == '<') {
					s.push(str.charAt(i));
				}else {
					char pop = (char)s.pop();
					if((pop == '(' && str.charAt(i) == ')')
					|| (pop == '[' && str.charAt(i) == ']')
					|| (pop == '{' && str.charAt(i) == '}')
					|| (pop == '<' && str.charAt(i) == '>')) {
						continue;
					}else {
						answer = 0;
						break;
					}
				}
			}
			System.out.println("#"+test_case+" "+answer);
		}
		sc.close();
	}
}
```



## 1219. [S/W 문제해결 기본] 4일차 - 길찾기 D4

 그림과 같이 도식화한 지도에서 A도시에서 출발하여 B도시로 가는 길이 존재하는지 조사하려고 한다.

길 중간 중간에는 최대 2개의 갈림길이 존재하고, 모든 길은 일방 통행으로 되돌아오는 것이 불가능하다.

다음과 같이 길이 주어질 때, A도시에서 B도시로 가는 길이 존재하는지 알아내는 프로그램을 작성하여라.

 - A와 B는 숫자 0과 99으로 고정된다.

 - 모든 길은 순서쌍으로 나타내어진다. 위 예시에서 2번에서 출발 할 수 있는 길의 표현은 (2, 5), (2, 9)로 나타낼 수 있다.

 - 가는 길의 개수와 상관없이 한가지 길이라도 존재한다면 길이 존재하는 것이다.

 - 단 화살표 방향을 거슬러 돌아갈 수는 없다.

  **[제약 사항]**

출발점은 0, 도착점은 99으로 표현된다.

정점(분기점)의 개수는 98개(출발점과 도착점 제외)를 넘어가지 않으며, 한 개의 정점에서 선택할 수 있는 길의 개수도 2개를 넘어가지 않는다.

아래 제시된 가이드 라인은 제안사항일 뿐 강제사항은 아니다.

**[데이터 저장 가이드]**

정점(분기점)의 개수가 최대 100개 이기 때문에, size [100]의 정적 배열 2개을 선언하여, 각 정점의 번호를 주소로 사용하고, 저장되는 데이터는 각 정점에서 도착하는 정점의 번호를 저장한다.

  **[입력]**

각 테스트 케이스의 첫 줄에는 테스트 케이스의 번호와 길의 총 개수가 주어지고 그 다음 줄에는 순서쌍이 주어진다.

순서쌍의 경우, 별도로 나누어 표현되는 것이 아니라 숫자의 나열이며, 나열된 순서대로 순서쌍을 이룬다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스에 대한 답을 출력한다.  

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

class Solution
{
    static int answer = 0;
	
	static void dfs(int line1[], int line2[], int now) {
		if(now == 99) {
			answer = 1;
			return;
		}
		
		if(line1[now] != 0) {
			dfs(line1, line2, line1[now]);
		}
		if(line2[now] != 0) {
			dfs(line1, line2, line2[now]);
		}
	}
	
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		
		for(int test_case=1; test_case<=10; test_case++) {
			answer = 0;
			st = new StringTokenizer(br.readLine(), " ");
			int T = Integer.parseInt(st.nextToken());
			int n = Integer.parseInt(st.nextToken());
			
			int line1[] = new int[100];
			int line2[] = new int[100];
			
			st = new StringTokenizer(br.readLine(), " ");
			for(int i=0; i<n; i++) {
				int start = Integer.parseInt(st.nextToken());
				int end = Integer.parseInt(st.nextToken());
				
				if(line1[start] != 0) { // line1[start] is not empty
					line2[start] = end;
				}else {
					line1[start] = end;
				}
			}
			dfs(line1, line2, 0);
			System.out.println("#"+T+" "+answer);
		}
	}
}
```

