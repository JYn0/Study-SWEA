# SW 문제해결 기본

[Learn > Course > Programming Intermediate > Queue]

## 1225. [S/W 문제해결 기본] 7일차 - 암호생성기 D3

  다음 주어진 조건에 따라 n개의 수를 처리하면 8자리의 암호를 생성할 수 있다.

\- 8개의 숫자를 입력 받는다.

\- 첫 번째 숫자를 1 감소한 뒤, 맨 뒤로 보낸다. 

다음 첫 번째 수는 2 감소한 뒤 맨 뒤로, 그 다음 첫 번째 수는 3을 감소하고 맨 뒤로, 그 다음 수는 4, 그 다음 수는 5를 감소한다.

이와 같은 작업을 한 사이클이라 한다.

\- 숫자가 감소할 때 0보다 작아지는 경우 0으로 유지되며, 프로그램은 종료된다. 이 때의 8자리의 숫자 값이 암호가 된다.  

[제약 사항]

주어지는 각 수는 integer 범위를 넘지 않는다.

마지막 암호 배열은 모두 한 자리 수로 구성되어 있다.

[입력]

각 테스트 케이스의 첫 줄에는 테스트 케이스의 번호가 주어지고, 그 다음 줄에는 8개의 데이터가 주어진다.

[출력]

#부호와 함께 테스트케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 답을 출력한다.

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

class Solution
{
	public static void main(String args[]) throws Exception
	{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		for(int test_case=1; test_case<11; test_case++) {
			String answer = "";
			st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken());
			st = new StringTokenizer(br.readLine(), " ");
			Queue<Integer> pwd = new LinkedList<Integer>();
			for(int i=0; i<8; i++) {
				pwd.add(Integer.parseInt(st.nextToken()));
			}
			boolean flag = true;
			while(flag) {
				for(int i=1; i<=5; i++) {
					int tmp = pwd.poll() - i;
					if(tmp <= 0) {
						pwd.add(0);
						flag = false;
						break;
					}else {
						pwd.add(tmp);
					}
				}
			}
			for(int i=0; i<8; i++) {
				answer += pwd.poll() + " ";
			}
			System.out.println("#"+N+" "+answer);
		}
	}
}
```



## 1226. [S/W 문제해결 기본] 7일차 - 미로1 D4

  아래 그림과 같은 미로가 있다. 16*16 행렬의 형태로 만들어진 미로에서 흰색 바탕은 길, 노란색 바탕은 벽을 나타낸다.

가장 좌상단에 있는 칸을 (0, 0)의 기준으로 하여, 가로방향을 x 방향, 세로방향을 y 방향이라고 할 때, 미로의 시작점은 (1, 1)이고 도착점은 (13, 13)이다.

주어진 미로의 출발점으로부터 도착지점까지 갈 수 있는 길이 있는지 판단하는 프로그램을 작성하라.

  **[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트케이스가 주어진다.

테스트 케이스에서 1은 벽을 나타내며 0은 길, 2는 출발점, 3은 도착점을 나타낸다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 도달 가능 여부를 1 또는 0으로 표시한다 (1 - 가능함, 0 - 가능하지 않음).  

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

class Solution
{
	public static void main(String args[]) throws Exception
	{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		for(int test_case=1; test_case<11; test_case++) {
			int answer = 0;
			
			int map[][] = new int[16][16];
			boolean visited[][] = new boolean[16][16];
			
			int[] dx = {0, 0, -1, 1};
			int[] dy = {1, -1, 0, 0};
			int x_start = 1, y_start = 1; // start point
			
			st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken());
			for(int i=0; i<16; i++) {
				st = new StringTokenizer(br.readLine());
				String str = st.nextToken();
				for(int j=0; j<16; j++) {
					map[i][j] = str.charAt(j) - '0';
					if(map[i][j] == 2) {
						x_start = i;
						y_start = j;
					}
				}
			}
			
			Queue<Integer> q = new LinkedList<Integer>();
			q.add(x_start);
			q.add(y_start);
			while(!q.isEmpty()) {
				int x = q.poll();
				int y = q.poll();
				for(int i=0; i<4; i++) {
					int qx = x + dx[i];
					int qy = y + dy[i];
					if(map[qx][qy] == 0 && visited[qx][qy] == false) {
						q.add(qx);
						q.add(qy);
						visited[qx][qy] = true;
					}else if(map[qx][qy] == 3) {
						answer = 1;
						break;
					}
				}
			}
			
			System.out.println("#"+N+" "+answer);
		}	
	}
}
```



## 1227. [S/W 문제해결 기본] 7일차 - 미로2 D4

   아래 그림과 같은 미로가 있다. 100*100 행렬의 형태로 만들어진 미로에서 흰색 바탕은 길, 노란색 바탕은 벽을 나타낸다.

가장 좌상단에 있는 칸을 (0, 0)의 기준으로 하여, 가로방향을 x 방향, 세로방향을 y 방향이라고 할 때, 미로의 시작점은 (1, 1)이고 도착점은 (13, 13)이다.

주어진 미로의 출발점으로부터 도착지점까지 갈 수 있는 길이 있는지 판단하는 프로그램을 작성하라.  

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

테스트 케이스에서 1은 벽을 나타내며 0은 길, 2는 출발점, 3은 도착점을 나타낸다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 도달 가능 여부를 1 또는 0으로 표시한다 (1 - 가능함, 0 - 가능하지 않음).

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

class Solution
{
	public static void main(String args[]) throws Exception
	{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		for(int test_case=1; test_case<11; test_case++) {
			int answer = 0;
			
			int map[][] = new int[100][100];
			boolean visited[][] = new boolean[100][100];
			
			int[] dx = {0, 0, -1, 1};
			int[] dy = {1, -1, 0, 0};
			int x_start = 1, y_start = 1; // start point
			
			st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken());
			for(int i=0; i<100; i++) {
				st = new StringTokenizer(br.readLine());
				String str = st.nextToken();
				for(int j=0; j<100; j++) {
					map[i][j] = str.charAt(j) - '0';
					if(map[i][j] == 2) {
						x_start = i;
						y_start = j;
					}
				}
			}
			
			Queue<Integer> q = new LinkedList<Integer>();
			q.add(x_start);
			q.add(y_start);
			while(!q.isEmpty()) {
				int x = q.poll();
				int y = q.poll();
				for(int i=0; i<4; i++) {
					int qx = x + dx[i];
					int qy = y + dy[i];
					if(map[qx][qy] == 0 && visited[qx][qy] == false) {
						q.add(qx);
						q.add(qy);
						visited[qx][qy] = true;
					}else if(map[qx][qy] == 3) {
						answer = 1;
						q.clear();
						break;
					}
				}
			}
			
			System.out.println("#"+N+" "+answer);
		}
	}
}
```

