# SW 문제해결 기본

[Learn > Course > Programming Intermediate > Array1]

## 1204. [S/W 문제해결 기본] 1일차 - 최빈수 구하기 D2

어느 고등학교에서 실시한 1000명의 수학 성적을 토대로 통계 자료를 만들려고 한다.

이때, 이 학교에서는 최빈수를 이용하여 학생들의 평균 수준을 짐작하는데, 여기서 최빈수는 특정 자료에서 가장 여러 번 나타나는 값을 의미한다.

다음과 같은 수 분포가 있으면,

10, 8, 7, 2, 2, 4, 8, 8, 8, 9, 5, 5, 3

최빈수는 8이 된다.

최빈수를 출력하는 프로그램을 작성하여라 (단, 최빈수가 여러 개 일 때에는 가장 큰 점수를 출력하라).

[제약 사항]

학생의 수는 1000명이며, 각 학생의 점수는 0점 이상 100점 이하의 값이다.

[입력]

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 테스트 케이스의 첫 줄에는 테스트 케이스의 번호가 주어지고 그 다음 줄부터는 점수가 주어진다.

[출력]

#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스에 대한 답을 출력한다.

```java
import java.util.Scanner;

public class Solution {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		for(int tc=1; tc<11; tc++) {
			int answer = 0;
			int testcase = sc.nextInt();
			int score[] = new int[101];
			for(int i=0; i<1000; i++) {
				int tmp = sc.nextInt();
				score[tmp] += 1;
			}
			
			int ref = 0;
			for(int i=0; i<score.length; i++) {
				if(ref <= score[i]) {
					ref = score[i];
					answer = i;
				}
			}
			System.out.println("#"+tc+" "+answer);
		}
		sc.close();
	}

}

```



## 1206. [S/W 문제해결 기본] 1일차 - View D3

강변에 빌딩들이 옆으로 빽빽하게 밀집한 지역이 있다.

이곳에서는 빌딩들이 너무 좌우로 밀집하여, 강에 대한 조망은 모든 세대에서 좋지만 왼쪽 또는 오른쪽 창문을 열었을 때 바로 앞에 옆 건물이 보이는 경우가 허다하였다.

그래서 이 지역에서는 왼쪽과 오른쪽으로 창문을 열었을 때, 양쪽 모두 거리 2 이상의 공간이 확보될 때 조망권이 확보된다고 말한다.

빌딩들에 대한 정보가 주어질 때, 조망권이 확보된 세대의 수를 반환하는 프로그램을 작성하시오.

아래와 같이 강변에 8채의 빌딩이 있을 때, 연두색으로 색칠된 여섯 세대에서는 좌우로 2칸 이상의 공백이 존재하므로 조망권이 확보된다. 따라서 답은 6이 된다.

A와 B로 표시된 세대의 경우는 왼쪽 조망은 2칸 이상 확보가 되었지만 오른쪽 조망은 한 칸 밖에 확보가 되지 않으므로 조망권을 확보하지 못하였다.

C의 경우는 반대로 오른쪽 조망은 2칸이 확보가 되었지만 왼쪽 조망이 한 칸 밖에 확보되지 않았다.

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
import java.util.Arrays;
import java.util.Scanner;

public class Solution {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		for (int testcase = 1; testcase < 11; testcase++) {

			int n = sc.nextInt();
			int map[] = new int[n];
			for (int i = 0; i < map.length; i++) {
				map[i] = sc.nextInt();
			}
			// System.out.println(Arrays.toString(map));
			int answer = 0;

			for (int i = 2; i < map.length - 2; i++) {
				int ref = map[i];
				int min[] = new int[4];
				min[0] = ref - map[i + 1]; // r1
				min[1] = ref - map[i + 2]; // r2
				min[2] = ref - map[i - 1]; // l1
				min[3] = ref - map[i - 2]; // l2
				// System.out.println("min: " + Arrays.toString(min));
				if (min[0] > 0 && min[1] > 0 && min[2] > 0 && min[3] > 0) {
					// minimum value is answer
					Arrays.sort(min);
					// System.out.println("sort min: " + Arrays.toString(min));
					answer += min[0];
				}
			}
			System.out.println("#" + testcase + " " + answer);
		}
		sc.close();
	}

}

```



## 1208. [S/W 문제해결 기본] 1일차 - Flatten D3

  한 쪽 벽면에 다음과 같이 노란색 상자들이 쌓여 있다.

높은 곳의 상자를 낮은 곳에 옮기는 방식으로 최고점과 최저점의 간격을 줄이는 작업을 평탄화라고 한다.

평탄화를 모두 수행하고 나면, 가장 높은 곳과 가장 낮은 곳의 차이가 최대 1 이내가 된다.

평탄화 작업을 위해서 상자를 옮기는 작업 횟수에 제한이 걸려있을 때, 제한된 횟수만큼 옮기는 작업을 한 후 최고점과 최저점의 차이를 반환하는 프로그램을 작성하시오.  

가장 높은 곳에 있는 상자를 가장 낮은 곳으로 옮기는 작업을 덤프라고 정의한다.

**[제약 사항]**

가로 길이는 항상 100으로 주어진다.

모든 위치에서 상자의 높이는 1이상 100이하로 주어진다.

덤프 횟수는 1이상 1000이하로 주어진다.

주어진 덤프 횟수 이내에 평탄화가 완료되면 더 이상 덤프를 수행할 수 없으므로 그 때의 최고점과 최저점의 높이 차를 반환한다 (주어진 data에 따라 0 또는 1이 된다).

**[입력]**

총 10개의 테스트 케이스가 주어지며, 각 테스트 케이스의 첫 번째 줄에는 덤프 횟수가 주어진다. 그리고 다음 줄에 각 상자의 높이값이 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 최고점과 최저점의 높이 차를 출력한다.

```java
import java.util.Arrays;
import java.util.Scanner;

public class Solution {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		for(int tc = 1; tc < 11; tc++) {
			int answer = 0;
			int dump = sc.nextInt();
			int box[] = new int[100];
			for(int i=0; i<box.length; i++) {
				box[i]= sc.nextInt();
			}
			
			Arrays.sort(box);
			for(int i=0; i<dump; i++) {
				box[0] += 1;
				box[box.length-1] -= 1;
				Arrays.sort(box);
			}
			answer = box[box.length-1] - box[0];
			System.out.println("#"+tc+" "+answer);
		}
		sc.close();
	}

}

```

