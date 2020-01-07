# SW 문제해결 기본

[Learn > Course > Programming Intermediate > Array2]

## 1209. [S/W 문제해결 기본] 2일차 - Sum D3

 다음 100X100의 2차원 배열이 주어질 때, 각 행의 합, 각 열의 합, 각 대각선의 합 중 최댓값을 구하는 프로그램을 작성하여라.

다음과 같은 5X5 배열에서 최댓값은 29이다.  

[제약 사항]

총 10개의 테스트 케이스가 주어진다.

배열의 크기는 100X100으로 동일하다.

각 행의 합은 integer 범위를 넘어가지 않는다.

동일한 최댓값이 있을 경우, 하나의 값만 출력한다.

[입력]

각 테스트 케이스의 첫 줄에는 테스트 케이스 번호가 주어지고 그 다음 줄부터는 2차원 배열의 각 행 값이 주어진다.

[출력]

#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 답을 출력한다.

```java
import java.util.Scanner;

public class Solution {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		for(int tc=1; tc<11; tc++) {
			int num = sc.nextInt();
			int map[][] = new int[100][100];
			for(int i=0; i<100; i++) {
				for(int j=0; j<100; j++) {
					map[i][j] = sc.nextInt();
				}
			}
			// row sum
			int answer = 0;
			int tmp = 0;
			for(int i=0; i<100; i++) {
				for(int j=0; j<100; j++) {
					tmp += map[i][j];
				}
				if(tmp > answer) {
					answer = tmp;
				}
				tmp = 0;
			}
			// column sum
			tmp = 0;
			for(int i=0; i<100; i++) {
				for(int j=0; j<100; j++) {
					tmp += map[j][i];
				}				
				if(tmp > answer) {
					answer = tmp;
				}
				tmp = 0;
			}
			// \ sum
			tmp = 0;
			for(int i=0; i<100; i++) {
				tmp += map[i][i];
				if(tmp > answer) {
					answer = tmp;
				}
			}
			// / sum
			tmp = 0;
			for(int i=9; i>=00; i--) {
				tmp += map[i][i];
				if(tmp > answer) {
					answer = tmp;
				}
			}
			System.out.println("#" + num + " " + answer);
		}
		sc.close();
	}

}

```



## 1210. [S/W 문제해결 기본] 2일차 - Ladder1 D4

점심 시간에 산책을 다니는 사원들은 최근 날씨가 더워져, 사다리 게임을 통하여 누가 아이스크림을 구입할지 결정하기로 한다.

김 대리는 사다리타기에 참여하지 않는 대신 사다리를 그리기로 하였다.

사다리를 다 그리고 보니 김 대리는 어느 사다리를 고르면 X표시에 도착하게 되는지 궁금해졌다. 이를 구해보자.

아래 <그림 1>의 예를 살펴보면, 출발점 x=0 및 x=9인 세로 방향의 두 막대 사이에 임의의 개수의 막대들이 랜덤 간격으로 추가되고(이 예에서는 2개가 추가됨) 이 막대들 사이에 가로 방향의 선들이 또한 랜덤하게 연결된다.

X=0인 출발점에서 출발하는 사례에 대해서 화살표로 표시한 바와 같이, 아래 방향으로 진행하면서 좌우 방향으로 이동 가능한 통로가 나타나면 방향 전환을 하게 된다.

방향 전환 이후엔 다시 아래 방향으로만 이동하게 되며, 바닥에 도착하면 멈추게 된다.

문제의 X표시에 도착하려면 X=4인 출발점에서 출발해야 하므로 답은 4가 된다. 해당 경로는 별도로 표시하였다.  

[제약 사항]

가로 길이는 항상 1000이하로 주어진다.

맨 왼쪽 두 칸과 맨 오른쪽 두 칸에는 건물이 지어지지 않는다. (예시에서 빨간색 땅 부분)

각 빌딩의 높이는 최대 255이다.

[입력]

입력 파일의 첫 번째 줄에는 테스트케이스의 길이가 주어진다. 그 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트케이스가 주어진다.

[출력]

#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 조망권이 확보된 세대의 수를 출력한다.

```java
import java.util.Scanner;

public class Solution {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		for(int tc=1; tc<11; tc++) {
			int answer = 0;
			int num = sc.nextInt();
			int ladder[][] = new int[100][100];
			for(int i=0; i<ladder.length; i++) {
				for(int j=0; j<ladder.length; j++) {
					ladder[i][j] = sc.nextInt();
				}
			}
			
			int ref = 100;
			for(int i=0; i<ladder.length; i++) {
				if(ladder[ladder.length-1][i] == 2) {
					ref = i;
				}
			}			
			for(int i=ladder.length-1; i>0; i--) {
				if(ref != 0 && ladder[i][ref-1] == 1) { // left
					while(ladder[i][ref-1] != 0) {
						ref = ref-1;
						if(ref-1 <0) {
							break;
						}
					}
				}else if(ref != ladder.length-1 && ladder[i][ref+1] == 1) { // right
					while(ladder[i][ref+1] != 0) {
						ref = ref + 1;
						if(ref+1 > ladder.length-1) {
							break;
						}
					}
				}
			}
			answer = ref;
			System.out.println("#"+tc+" "+answer);
		}
		sc.close();
	}
}

```



## 1211.  [S/W 문제해결 기본] 2일차 - Ladder2 D4

 점심 시간에 산책을 다니는 사원들은 최근 날씨가 더워져, 사다리 게임을 통하여 누가 아이스크림을 구입할지 결정하기로 한다.

김 대리는 사다리타기에 참여하지 않는 대신 사다리를 그리기로 하였다.

사다리를 다 그리고 보니 김 대리는 어느 사다리를 고르면 X표시에 도착하게 되는지 궁금해졌다. 이를 구해보자.

아래 <그림 1>의 예를 살펴보면, 출발점 x=0 및 x=9인 세로 방향의 두 막대 사이에 임의의 개수의 막대들이 랜덤 간격으로 추가되고(이 예에서는 2개가 추가됨) 이 막대들 사이에 가로 방향의 선들이 또한 랜덤하게 연결된다.

X=0인 출발점에서 출발하는 사례에 대해서 화살표로 표시한 바와 같이, 아래 방향으로 진행하면서 좌우 방향으로 이동 가능한 통로가 나타나면 방향 전환을 하게 된다.

방향 전환 이후엔 다시 아래 방향으로만 이동하게 되며, 바닥에 도착하면 멈추게 된다.

문제의 X표시에 도착하려면 X=4인 출발점에서 출발해야 하므로 답은 4가 된다. 해당 경로는 별도로 표시하였다.
아래 <그림 2>와 같은 **100 x 100 크기의 2차원 배열로 주어진 사다리에 대해서, 모든 출발점을 검사하여 가장 짧은 이동 거리를 갖는 시작점 x(복수 개인 경우 가장 큰 x좌표)를 반환하는 코드를 작성하라.**(‘0’으로 채워진 평면상에 사다리는 연속된 ‘1’로 표현된다. 도착 지점은 '2'로 표현된다.)

**[제약사항]**

한 막대에서 출발한 가로선이 다른 막대를 가로질러서 연속하여 이어지는 경우는 없다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 도착하게 되는 출발점의 x좌표를 출력한다.

```java
import java.util.Scanner;

public class Solution {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		for(int tc=1; tc<11; tc++) {
			int num = sc.nextInt();
			int ladder[][] = new int[100][100];
			for(int i=0; i<ladder.length; i++) {
				for(int j=0; j<ladder.length; j++) {
					ladder[i][j] = sc.nextInt();
				}
			}
			
			int answer = 0;
			int ref = 100;
			int R = 100;
			int count[] = new int[ladder.length];
			
			for(int i=0; i<ladder.length; i++) {
				if(ladder[0][i] == 1) {
					ref = i;
					R = ref;
				}else {
					continue;
				}
				int cnt = 0;
				for(int j=0; j<ladder.length; j++) {
					if(ref != 0 && ladder[j][ref-1] == 1) { // left
						while(ladder[j][ref-1] != 0) {
							cnt++;
							ref -= 1;
							if(ref-1 < 0) {
								break;
							}
						}
					}else if(ref != ladder.length-1 && ladder[j][ref+1] == 1) { // right
						while(ladder[j][ref+1] != 0) {
							cnt++;
							ref += 1;
							if(ref+1 >= ladder.length) {
								break;
							}
						}
					}
				}
				count[R] = cnt;
			}
			int min = count[0];
			for(int i=0; i<count.length; i++) {
				if(count[i] == 0) {
					continue;
				}else if(min >= count[i]) {
					min = count[i];
					answer = i;
				}
			}
			System.out.println("#"+num+" "+answer);
		}
		sc.close();
	}
}
```

