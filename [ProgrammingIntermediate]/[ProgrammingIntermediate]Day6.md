# SW 문제해결 기본

[Learn > Course > Programming Intermediate > Stack2]

## 1222. [S/W 문제해결 기본] 6일차 - 계산기1 D4

문자열로 이루어진 계산식이 주어질 때, 이 계산식을 후위 표기식으로 바꾸어 계산하는 프로그램을 작성하시오.

예를 들어

“3+4+5+6+7”

라는 문자열로 된 계산식을 후위 표기식으로 바꾸면 다음과 같다.

"34+5+6+7+"

변환된 식을 계산하면 25를 얻을 수 있다.

문자열 계산식을 구성하는 연산자는 + 하나뿐이며 피연산자인 숫자는 0 ~ 9의 정수만 주어진다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 문자열 계산식의 길이가 주어진다. 그 다음 줄에 문자열 계산식이 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 답을 출력한다.  

```java
import java.util.Scanner;

class Solution
{
	public static void main(String args[]) throws Exception
	{
        Scanner sc = new Scanner(System.in);
		for(int test_case=1; test_case<=10; test_case++) {
			int answer = 0;
			
			int n = sc.nextInt();
			String s = sc.next();
			for(int i=0; i<=n/2; i++) {
				answer += Integer.parseInt(String.valueOf(s.charAt(i*2)));
			}
			
			System.out.println("#"+test_case+" "+answer);
		}
		sc.close();
	}
}
```



## 1223. [S/W 문제해결 기본] 6일차 - 계산기2 D4

  문자열로 이루어진 계산식이 주어질 때, 이 계산식을 후위 표기식으로 바꾸어 계산하는 프로그램을 작성하시오.

예를 들어

“3+4+5*6+7”

라는 문자열로 된 계산식을 후위 표기식으로 바꾸면 다음과 같다.

"34+56*+7+"

변환된 식을 계산하면 44를 얻을 수 있다.

문자열 계산식을 구성하는 연산자는 +, * 두 종류이며 피연산자인 숫자는 0 ~ 9의 정수만 주어진다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 길이가 주어진다. 그 다음 줄에 바로 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 답을 출력한다.  

```java
import java.util.Scanner;
import java.util.Stack;

class Solution
{
	public static void main(String args[]) throws Exception
	{
        Scanner sc = new Scanner(System.in);
		for(int test_case=1; test_case<=10; test_case++) {
			int answer = 0;
			
			int N = sc.nextInt();
			String str = sc.next();
			
			Stack<Character> operator = new Stack<Character>();
			char calc[] = new char[N+1]; // 후위표기식
			int calc_index = 0;
			
			for(int i=0; i<N; i++) {
				char ref = str.charAt(i);
				
				if(ref == '+') {
					while(!operator.isEmpty() && (operator.peek()=='*' || (operator.peek()=='+'))) {
						calc[calc_index++] = operator.pop();
					}
					operator.push(ref);
				}else if(ref == '*') {
					while(!operator.isEmpty() && operator.peek()=='*') {
						calc[calc_index++] = operator.pop();
					}
					operator.push(ref);
				}else { // Number
					calc[calc_index++] = ref;
				}
			}
			while(!operator.isEmpty()) {
				calc[calc_index++] = operator.pop();
			}
//			System.out.println(calc);

			Stack<Integer> calculation = new Stack<Integer>();
			for(int i=0; i<N; i++) {
				if(calc[i]=='+') {
					// 숫자 두개 꺼내서 계산하고 다시 스택에 넣기
					int tmp1 = calculation.pop();
					int tmp2 = calculation.pop();
					calculation.push(tmp2+tmp1);
				}else if (calc[i]=='*') {
					// 숫자 두개 꺼내서 계산하고 다시 스택에 넣기
					int tmp1 = calculation.pop();
					int tmp2 = calculation.pop();
					calculation.push(tmp2*tmp1);
				}else {
					calculation.push(Integer.parseInt(String.valueOf(calc[i])));
				}
			}
			answer = calculation.pop();
			System.out.println("#"+test_case+" "+answer);
		}
		sc.close();
    }
}
```



## 1224. [S/W 문제해결 기본] 6일차 - 계산기3 D4

  문자열로 이루어진 계산식이 주어질 때, 이 계산식을 후위 표기식으로 바꾸어 계산하는 프로그램을 작성하시오.

예를 들어

“3+(4+5)*6+7”

라는 문자열로 된 계산식을 후위 표기식으로 바꾸면 다음과 같다.

"345+6*+7+"

변환된 식을 계산하면 64를 얻을 수 있다.

문자열 계산식을 구성하는 연산자는 +, * 두 종류이며 문자열 중간에 괄호가 들어갈 수 있다.

이 때 괄호의 유효성 여부는 항상 옳은 경우만 주어진다.

피연산자인 숫자는 0 ~ 9의 정수만 주어진다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 길이가 주어진다. 그 다음 줄에 바로 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 답을 출력한다.  

```java
import java.util.Scanner;
import java.util.Stack;

class Solution
{
	public static void main(String args[]) throws Exception
	{
        Scanner sc = new Scanner(System.in);
		for(int test_case=1; test_case<=10; test_case++) {
			
			System.out.println("#"+test_case+" "+answer);
		}
		sc.close();
    }
}
```

