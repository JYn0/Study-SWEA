# SW 문제해결 기본

[Learn > Course > Programming Intermediate > String]

## 1213. [S/W 문제해결 기본] 3일차 - String D3

주어지는 영어 문장에서 특정한 문자열의 개수를 반환하는 프로그램을 작성하여라.

Starteatingwellwiththeseeighttipsforhealthyeating,whichcoverthebasicsofahealthydietandgoodnutrition.

위 문장에서 ti 를 검색하면, 답은 4이다.

[제약 사항]

총 10개의 테스트 케이스가 주어진다.

문장의 길이는 1000자를 넘어가지 않는다.

한 문장에서 검색하는 문자열의 길이는 최대 10을 넘지 않는다.

한 문장에서는 하나의 문자열만 검색한다. 

[입력]

각 테스트 케이스의 첫 줄에는 테스트 케이스의 번호가 주어지고 그 다음 줄에는 찾을 문자열, 그 다음 줄에는 검색할 문장이 주어진다.

[출력]

#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 답을 출력한다.

```java
import java.util.Scanner;

public class Solution {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int T = 10;
		for(int test_case=1; test_case<=T; test_case++) {
			int num = sc.nextInt();
			String find_str = sc.next();
			String str = sc.next();
			int start = 0;
			int answer = 0;
			
			while(start < str.length()) {
				int find = str.indexOf(find_str, start);
				if(find != -1) {
					answer++;
					start = find+1;
				}else {
					break;
				}
			}
			System.out.println("#"+num+" "+answer);
			
		}
		sc.close();
	}
}

```



## 1215.  [S/W 문제해결 기본] 3일차 - 회문1 D3

"기러기" 또는 "level" 과 같이 거꾸로 읽어도 앞에서부터 읽은 것과 같은 문장이나 낱말을 회문(回文, palindrome)이라 한다.

주어진 8x8 평면 글자판에서 가로, 세로를 모두 보아 제시된 길이를 가진 회문의 총 개수를 구하는 문제이다.
 위와 같은 글자판이 주어졌을 때, 길이가 5인 회문은 붉은색 테두리로 표시된 4개가 있으며 따라서 4를 반환하면 된다.
**[제약 사항]**

각 칸의 들어가는 글자는 c언어 char type으로 주어지며 'A', 'B', 'C' 중 하나이다.

글자 판은 무조건 정사각형으로 주어진다.

ABA도 회문이며, ABBA도 회문이다. A또한 길이 1짜리 회문이다.

가로, 세로 각각에 대해서 직선으로만 판단한다.

즉, 아래 예에서 노란색 경로를 따라가면 길이 7짜리 회문이 되지만 직선이 아니기 때문에 인정되지 않는다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 찾아야 하는 회문의 길이가 주어지며, 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.
**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 찾은 회문의 개수를 출력한다.  

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Solution {

	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		for(int test_case=1; test_case < 11; test_case++) {
			int n = Integer.parseInt(br.readLine());
			char Array[][] = new char[8][8];
			for(int i=0; i<8; i++) {
				String s = br.readLine();
				for(int j=0; j<8; j++) {
					Array[i][j] = s.charAt(j);
				}
			}
			int answer = 0 ;
			boolean flag = true;
			// 행
			for(int i=0; i<Array.length; i++) {
				for(int j=0; j<(Array.length-n+1); j++) {
					flag = true;
					for(int k=0; k<(n/2); k++) {
						if(Array[i][j+k] != Array[i][j+n-1-k]) {
							flag = false;
						}
					}
					if(flag) {
						answer++;
					}
				}
			}
			flag=true;
			// 열
			for(int i=0; i<Array.length; i++) {
				for(int j=0; j<Array.length-n+1; j++) {
					flag = true;
					for(int k=0; k<(n/2); k++) {
						if(Array[j+k][i] != Array[j+n-1-k][i]) {
							flag = false;
						}
					}
					if(flag) {
						answer++;
					}
				}
			}		
			System.out.println("#"+test_case+" "+answer);
		}
	}
}

```



## 1216. [S/W 문제해결 기본] 3일차 - 회문2 D3

   "기러기" 또는 "level" 과 같이 거꾸로 읽어도 제대로 읽은 것과 같은 문장이나 낱말을 회문(回文, palindrome)이라 한다.

주어진 100x100 평면 글자판에서 가로, 세로를 모두 보아 가장 긴 회문의 길이를 구하는 문제이다.
   위와 같은 글자 판이 주어졌을 때, 길이가 가장 긴 회문은 붉은색 테두리로 표시된 7칸짜리 회문이다.

예시의 경우 설명을 위해 글자판의 크기가 100 x 100이 아닌 8 x 8으로 주어졌음에 주의한다.

**[제약사항]**

각 칸의 들어가는 글자는 c언어 char type으로 주어지며 'A', 'B', 'C' 중 하나이다.

글자 판은 무조건 정사각형으로 주어진다.

ABA도 회문이며, ABBA도 회문이다. A또한 길이 1짜리 회문이다.

가로, 세로 각각에 대해서 직선으로만 판단한다. 즉, 아래 예에서 노란색 경로를 따라가면 길이 7짜리 회문이 되지만 직선이 아니기 때문에 인정되지 않는다.  

  **[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 찾은 회문의 길이를 출력한다.  

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Solution {

	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;

		for (int test_case = 1; test_case < 11; test_case++) {
			st = new StringTokenizer(br.readLine());
			int T = Integer.parseInt(st.nextToken());
			char Array[][] = new char[100][100];
			for (int i = 0; i < 100; i++) {
				st = new StringTokenizer(br.readLine(), "");
				String s = st.nextToken();
				for (int j = 0; j < 100; j++) {
					Array[i][j] = s.charAt(j);
				}
			}
			int answer = 0;
			boolean flag = true;
			// 행
			for (int n = 1; n <= Array.length; n++) {
				for (int i = 0; i < Array.length; i++) {
					for (int j = 0; j <= (Array.length - n); j++) {
						flag = true;
						for (int k = 0; k < (n / 2); k++) {
							if (Array[i][j + k] != Array[i][j + n - 1 - k]) {
								flag = false;
							}
						}
						if (flag && answer<n) {
							answer = n;
						}
					}
				}
			}
			flag = true;
			// 열
			for (int n = 1; n <= Array.length; n++) {
				for (int i = 0; i < Array.length; i++) {
					for (int j = 0; j <= Array.length - n; j++) {
						flag = true;
						for (int k = 0; k < (n / 2); k++) {
							if (Array[j + k][i] != Array[j + n - 1 - k][i]) {
								flag = false;
							}
						}
						if (flag && answer<n) {
							answer = n;
						}
					}
				}
			}
			System.out.println("#" + T + " " + answer);
		}
	}
}
```

