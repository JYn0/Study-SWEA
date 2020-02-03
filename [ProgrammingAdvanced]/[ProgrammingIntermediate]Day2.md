# SW 문제해결 기본

[Learn > Course > Programming Advanced]

## 1245. [S/W 문제해결 응용] 2일차 - 균형점 D5

  ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

무중력 공간에 n개의 자성체들이 존재한다.

각 자성체들의 중심점이 자성체의 위치, 즉 공간 좌표(x,y,z)가 된다.

n개의 자성체들의 y와 z의 좌표들은 모두 동일하고 x의 좌표만 다르다.

즉, 그림과 같이 일직선 상에 존재한다고 가정한다.

자성체들의 위치는 어떤 외부의 힘에 의해서도 절대 변경되지 않는다.

이때, 어떤 물체가 n개의 자성체들이 위치한 직선의 임의의 위치에 존재하면 각 자성체로부터 인력이 작용한다.

자성체에서 물체에 작용하는 인력은 자성체와 물체 사이의 거리(d)와 자성체와 물체의 질량(m)으로 구한다.

자성체로부터 물체에 작용하는 인력을 구하는 공식: F = G*m1*m2/(d*d), G는 양의 상수 값  

  이 때, 물체의 왼쪽에 있는 자성체들의 인력과 오른쪽의 자성체들의 인력들에서 더 큰 쪽으로 물체가 이동할 것이다.

양쪽의 힘이 같은 지점에 물체가 있다면 물체는 움직이지 않고 정지 상태가 된다.

물체에 작용하는 양쪽이 힘이 같은 지점을 찾아보자. n개의 자성체가 있다면 n-1개의 균형점이 존재한다.   

좌표값의 오차가 10 -12(1e-12) 보다는 작아야 함에 주의하자.

**[입력]**

가장 첫줄은 전체 테스트 케이스의 수 이다.

각 테스트 케이스는 자성체의 개수 N이 쓰여지고 다음 줄에  N개의 자성체에 대한 N개의 x좌표와 N개의 질량 값이 순차적으로 입력된다.

자성체의 개수 (N)는 2에서 10 사이의 값이다 (2 ≤ N ≤ 10)

**[출력]**

각 테스트 케이스마다, 첫 줄에는 “#C”를 출력해야 하는데 C는 케이스 번호이다.

같은 줄에 빈 칸을 하나 사이에 두고 균형점들의 x좌표 값을 출력하시오.

좌표 값이 소수점 이하 10자리 이상이면 10자리까지만 출력한다.

```java
import java.util.Scanner;

class Solution
{
	static int N;
	static int Loc[];
	static int Mass[];

	public static double biSection(int pos) {
		double mid = 0, low = Loc[pos], high = Loc[pos+1];
		for(int i=0; i<100; i++) {
			mid = (low+high)/2;
			double left=0, right=0;
			
			for(int j=0; j<=pos; j++) {
				double dx = mid - Loc[j];
				left += Mass[j] / (dx*dx);
			}
			for(int j=pos+1; j<N; j++) {
				double dx = Loc[j] - mid;
				right += Mass[j] / (dx*dx);
			}
			
			if(left > right) {
				low = mid;
			}else if(left < right) {
				high = mid;
			}else {
				return mid;
			}
		}
		return mid;
	}
	
	public static void main(String[] args) throws Exception{
		Scanner sc = new Scanner(System.in);
		int TC = sc.nextInt();
		for(int test_case=1; test_case<=TC; test_case++) {
			
			N = sc.nextInt();
			Loc = new int[N];
			Mass = new int[N];
			for(int i=0; i<N; i++) {
				Loc[i] = sc.nextInt();
			}
			for(int i=0; i<N; i++) {
				Mass[i] = sc.nextInt();
			}
			
			double ans[] = new double[N-1];
			for(int i=0; i<N-1; i++) {
				ans[i] = biSection(i);
			}
			
			System.out.printf("#"+test_case);
			for(int i=0; i<ans.length; i++) {
				System.out.printf(" %.10f",ans[i]);
			}
			System.out.println();
		}
		sc.close();
	}
}
```

```C++
#include<iostream>
#define MAX_N 10
using namespace std;

int N, Loc[MAX_N], Mass[MAX_N];

double bisection(int pos){
    double mid, low = Loc[pos], high = Loc[pos+1];
    for(int k=0; k<100; ++k){ // 오차때문에 100번 돌림, 2^100으로 나눠져서 오차범위보다 작아짐
        mid = (low+high) / 2.0;
        double leftForce = 0, rightForce = 0;
        for(int i=0; i<=pos; ++i){
            double dx = mid - Loc[i];
            leftForce += Mass[i] / (dx*dx);
        }
        for(int i=pos+1; i<N; ++i){
            double dx = Loc[i] - mid;
            rightForce += Mass[i] / (dx*dx);
        }
        
        if(leftForce > rightForce)
            low = mid;
        else if(leftForce == rightForce)
            return mid;
        else
            high = mid;
    }
    return mid;
}

int main(int argc, char** argv){
    int tcCnt;
    cin >> tcCnt;
    for(int t=1; t<=tcCnt; ++t){
        cin >> N;
        for(int i=0; i<N; ++i){
            cin >> Loc[i];
        }
        for(int i=0; i<N; ++i){
            cin >> Mass[i];
        }
        // printf("#%d", t);
        // for(int i=0; i<N-1; ++i){
        //  	printf(" %.10f", solve(i));
    	// }
        // printf("\n");
        cout.setf(ios::fixed, ios::floatfield);
        cout.precision(10);
        cout << "#" << t;
        for(int i=0; i<N-1; ++i){
            cout << ' ' << bisection(i);
        }
        cout << endl;
    }
    return 0;
}
```



## 1244. [S/W 문제해결 응용] 2일차 - 최대 상금 D3

   ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

퀴즈 대회에 참가해서 우승을 하게 되면 보너스 상금을 획득할 수 있는 기회를 부여받는다.

우승자는 주어진 숫자판들 중에 두 개를 선택에서 정해진 횟수만큼 서로의 자리를 위치를 교환할 수 있다.

예를 들어, 다음 그림과 3, 2, 8, 8, 8 의 5개의 숫자판들이 주어지고 교환 횟수는 2회라고 하자.

교환전>  

처음에는 첫번째 숫자판의 3과 네 번째 숫자판의 8을 교환해서 8, 2, 8, 3, 8이 되었다.

다음으로, 두 번째 숫자판 2와 마지막에 있는 8을 교환해서 8, 8, 8, 3, 2이 되었다.
정해진 횟수만큼 교환이 끝나면 숫자판의 위치에 부여된 가중치에 의해 상금이 계산된다.

숫자판의 오른쪽 끝에서부터 1원이고 왼쪽으로 한자리씩 갈수록 10의 배수만큼 커진다.

위의 예에서와 같이 최종적으로 숫자판들이 8,8,8,3,2의 순서가 되면 88832원의 보너스 상금을 획득한다.

여기서 주의할 것은 반드시 횟수만큼 교환이 이루어져야 하고 동일한 위치의 교환이 중복되어도 된다.

다음과 같은 경우 1회의 교환 횟수가 주어졌을 때 반드시 1회 교환을 수행하므로 결과값은 49가 된다.  

  94의 경우 2회 교환하게 되면 원래의 94가 된다.

정해진 횟수만큼 숫자판을 교환했을 때 받을 수 있는 가장 큰 금액을 계산해보자.

**[입력]**

가장 첫 줄은 전체 테스트 케이스의 수이다.

최대 10개의 테스트 케이스가 표준 입력을 통하여 주어진다.

각 테스트 케이스에는 숫자판의 정보와 교환 횟수가 주어진다.

숫자판의 정보는 정수형 숫자로 주어지고 최대 자릿수는 6자리이다.

**[출력]**

각 테스트 케이스마다, 첫 줄에는 “#C”를 출력해야 하는데 C는 케이스 번호이다.

같은 줄에 빈 칸을 하나 사이에 두고 교환 후 받을 수 있는 가장 큰 금액을 출력한다.  

```java

```

```C++

```

