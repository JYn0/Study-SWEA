# SW 문제해결 기본

[Learn > Course > Programming Advanced]

## 1248. [S/W 문제해결 응용] 3일차 - 공통조상 D5

  ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

이진 트리에서 임의의 두 정점의 공통 조상 중 가장 가까운 것을 찾으려 한다.

예를 들어, 아래의 이진 트리에서 정점 8과 13의 공통 조상은 정점 3와 1 두 개가 있다.

이 중 8, 13에 가장 가까운 것은 정점 3이다.

정점 3을 루트로 하는 서브 트리의 크기(서브 트리에 포함된 정점의 수)는 8이다.  

  임의의 이진 트리가 주어지고, 두 정점이 명시될 때 이들의 공통 조상 중 이들에 가장 가까운 정점을 찾고, 그 정점을 루트로 하는 서브 트리의 크기를 알아내는 프로그램을 작성하라.

입력에서 주어지는 두 정점이 서로 조상과 자손 관계인 경우는 없다.

위의 트리에서 예를 든다면 두 정점이 “11과 3”과 같이 주어지는 경우는 없다.

**[입력]**

가장 첫줄은 전체 테스트케이스의 수이다.

10개의 테스트 케이스가 주어진다.

두 줄이 하나의 테스트 케이스가 되며, 따라서 전체 입력은 20줄로 이루어진다.

각 케이스의 첫줄에는 트리의 정점의 총 수 V와 간선의 총 수 E, 공통 조상을 찾는 두 개의 정점 번호가 주어진다 (정점의 수 V는 10 ≤ V ≤ 10000 이다). 

그 다음 줄에는 E개 간선이 나열된다. 간선은 간선을 이루는 두 정점으로, 항상 “부모 자식” 순서로 표기된다.

위에서 예로 든 트리에서 정점 5와 8을 잇는 간선은 “5 8”로 표기되고, 절대로 “8 5”와 같이 표기되지는 않는다.

간선이 입력되는 순서는 정해져 있지 않다. 입력에서 이웃한 수는 모두 공백으로 구분된다.

정점의 번호는 1부터 V까지의 정수이며, 전체 트리에서 루트가 되는 정점은 항상 1번으로 표기된다.

부모 정점이 자식 정점보다 항상 번호가 작은 것은 아니다. 즉, 40번 정점이 20번 정점의 부모가 될 수도 있다.

이 문제에서 자식 정점이 부모 정점의 왼쪽 자식인지 오른쪽 자식인지는 중요하지 않다.

**[출력]**

총 10줄에 10개의 테스트 케이스 각각에 대한 답을 출력한다.

각 줄은 테스트 케이스의 번호를 의미하는 ‘#x’로 시작하고 공백을 하나 둔 다음 답을 기록한다.

답은 공통조상 중 가장 가까운 것의 번호, 그것을 루트로 하는 서브 트리의 크기를 뜻하는 2개의 정수로 구성된다. 이 두 정수는 공백으로 구분한다.  

```java
package swAdvanced;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

class Node_inform{
	int data;
	int p; // parent
	int l; // left
	int r; // right
	int level; // depth
	int size; // size
	
	public Node_inform(int data) {
		this.data = data;
		this.p = 0;
		this.l = 0;
		this.r = 0;
		this.level = 0;
		this.size = 0;
	}
}


public class Day4LCA {

	static Node_inform[] nodes;

	public static int level(int node, int depth) {
		int size = 0;
		if(nodes[node].l != 0) {
			size++;
			size += level(nodes[node].l, depth+1);
		}
		if(nodes[node].r != 0) {
			size++;
			size += level(nodes[node].r, depth+1);
		} 
		nodes[node].level = depth;
		nodes[node].size = size;
		return size;
	}
	
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int TC = Integer.parseInt(br.readLine());
		StringTokenizer st;
		for(int test_case=1; test_case<=TC; test_case++) {
			int answer_p = 0;
			int answer_s = 0;
			
			st = new StringTokenizer(br.readLine());
			int V = Integer.parseInt(st.nextToken());
			int E = Integer.parseInt(st.nextToken());
			int x = Integer.parseInt(st.nextToken());
			int y = Integer.parseInt(st.nextToken());

			nodes = new Node_inform[V+1];
			for(int i=1; i<V+1; i++) {
				nodes[i] = new Node_inform(i);
			}
			
			st = new StringTokenizer(br.readLine());
			nodes[1].level = 0;
			for(int i=1; i<E+1; i++) {
				int data_v = Integer.parseInt(st.nextToken());
				int child_v = Integer.parseInt(st.nextToken());
				
				nodes[data_v].data = data_v;
				nodes[child_v].p = data_v;
				
				// child(left or right)
				if(nodes[data_v].l == 0) {
					nodes[data_v].l = child_v;
				}else {
					nodes[data_v].r = child_v;
				}
			}
			
			level(1, 0); // node and level
			
			int u_level = nodes[x].level < nodes[y].level ? nodes[x].data : nodes[y].data;
			int d_level = nodes[x].level > nodes[y].level ? nodes[x].data : nodes[y].data;
			
			while(true) { 
				// 공통조상 찾기
				if(nodes[u_level].level == nodes[d_level].level) {
					if(nodes[u_level].p == nodes[d_level].p) {
						answer_p = nodes[u_level].p;
						break;
					}else {
						u_level = nodes[u_level].p;
						d_level = nodes[d_level].p;
					}
				}else {
					d_level = nodes[d_level].p;
				}
			}
			answer_s = nodes[nodes[u_level].p].size + 1;
			
			System.out.println("#" + test_case + " " + answer_p + " " + answer_s);
			
		}
	}
}

```

<https://jaejin89.tistory.com/112>

```C++
// LCA(Lowest common ancestor) - DP로 성능 개선
#include <iostream>
using namespace std;
#define MAXK 14;
int V, E, Tree[10001][2], Parent[10001][MAXK+1], Depth[10001], Size[10001];
int main(int argc, char** argv){
    int tcCnt, n1, n2;
    cin >> tcCnt;
    for(int t=1; t<=tcCnt; ++t){
        cin >> V >> E >> n1 >> n2;
        for(int i=1; i<=V; ++i){
            Tree[i][0] = Tree[i][1] = 0;
            for(int k=0; k<= MAXK; ++k){
                Parent[i][k] == -1;
            }
        }
        
        for(int i=0; i<E; ++i){
            int p, c;
            cin >> p >> c;
            if(Tree[p][0] == 0)
                Tree[p][0] = c;
            else
                Tree[p][1] = c;
            Parent[c][0] = p;
        }
        for(int k=0; k<MAXK; ++k){
            for(int i=1; i<=V; ++i){
                if(Parent[i][k] != -1)
                    Parent[i][k+1] = Parent[Parent[i][k]][k]; // 점화식
            }
        }
        traversal(1, 0); // Depth 구하기
        int anc = lca(n1, n2);
        cout << "#" << t << ' '<< anc << ' ' << Size[anc] << endl;
    }
    return 0;
}

int traversal(int node, int depth){
    int cnt = 0;
    if(node != 0){
        cnt++;
        cnt += traversal(Tree[node][0], depth+1);
        cnt += traversal(Tree[node][1], depth+1);
    }
    Depth[node] = depth;
    Size[node] = cnt;
    return cnt;
}

int lca(int n1, int n2){
    int u = Depth[n1] > Depth[n2] ? n1 : n2; // Depth 더 깊은거
    int v = Depth[n1] > Depth[n2] ? n2 : n1; // Depth 더 낮은거
    // Depth 맞추기
    int diff = Depth[u] - Depth[v];
    for(int k=0; diff; ++k){
        if(diff % 2)
            u = Parent[u][k];
        diff /= 2;
    }
    if(u != v){
        for(int k=MAXK; k>=0; --k){
            if(Parent[u][k] != -1 && Parent[u][k] != Parent[v][k]){
                u = Parent[u][k];
                u = Parent[v][k];
            }
        }
        u = Parent[u][0];
    }
       
    return u;
}

//////////////////////////////////////////////////////////////////////////////

// LCA(Lowest common ancestor)
#include <iostream>
using namespace std;
int V, E, Tree[10001][2], Parent[10001], Depth[10001], Size[10001];
int main(int argc, char** argv){
    int tcCnt, n1, n2;
    cin >> tcCnt;
    for(int t=1; t<=tcCnt; ++t){
        cin >> V >> E >> n1 >> n2;
        for(int i=1; i<=V; ++i){
            Tree[i][0] = Tree[i][1] = 0;
        }
        
        for(int i=0; i<E; ++i){
            int p, c;
            cin >> p >> c;
            if(Tree[p][0] == 0)
                Tree[p][0] = c;
            else
                Tree[p][1] = c;
            Parent[c] = p;
        }
        traversal(1, 0); // Depth 구하기
        int anc = lca(n1, n2);
        cout << "#" << t << ' '<< anc << ' ' << Size[anc] << endl;
    }
    return 0;
}

int traversal(int node, int depth){
    int cnt = 0;
    if(node != 0){
        cnt++;
        cnt += traversal(Tree[node][0], depth+1);
        cnt += traversal(Tree[node][1], depth+1);
    }
    Depth[node] = depth;
    Size[node] = cnt;
    return cnt;
}

int lca(int n1, int n2){
    int u = Depth[n1] > Depth[n2] ? n1 : n2; // Depth 더 깊은거
    int v = Depth[n1] > Depth[n2] ? n2 : n1; // Depth 더 낮은거
    // Depth 맞추기
    int diff = Depth[u] - Depth[v];
    for(int k=0; k<diff; ++k)
        u = Parent[u];
    while(u != v){
        u = Parent[u];
        v = Parent[v];
    }
    return u;
}
```



## 1244. [S/W 문제해결 응용] 2일차 - 최대 상금 D3



```java

```

```C++

```



