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



## 12. [S/W 문제해결 응용] 

 

```java

```

```C++

```

