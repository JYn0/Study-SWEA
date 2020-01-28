# SW 문제해결 기본

[Learn > Course > Programming Advanced]

## 1240. [S/W 문제해결 응용] 1일차 - 단순 2진 암호코드 D3

※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

어떤 국가에서는 자국 내 방송국에서 스파이가 활동하는 사실을 알아냈다. 스파이는 영상물에 암호 코드를 삽입하여 송출하고 있었다. 암호 코드는 국가 내 중요 시설을 의미하는 숫자임을 알아냈다. 암호 코드의 규칙은 아래와 같다.


A 업체에서는 이 암호코드들을 빠르고 정확하게 인식할 수 있는 스캐너를 개발하려고 한다. 스캐너의 성능은 아래와 같은 방법으로 측정된다.

배열에 포함되어 있는 암호코드의 세부 규칙은 아래와 같다.

암호코드 정보가 포함된 2차원 배열을 입력으로 받아 정상적인 암호코드를 판별하는 프로그램을 작성하라.

**[입력]**

가장 첫줄은 전체 테스트 케이스의 수이다.

각 테스트 케이스의 첫 줄에 두 자연수가 주어지는데 각각 배열의 세로 크기 N, 배열의 가로크기 M이다 (1≤N<50, 1≤M<100).

그 다음 N개의 줄에는 M개의 배열의 값이 주어진다.

**[출력]**

각 테스트 케이스의 답을 순서대로 표준출력으로 출력하며, 각 케이스마다 줄의 시작에 “#C”를 출력하여야 한다.

이때 C는 케이스의 번호이다. 같은 줄에 빈칸을 하나 두고, 입력에 주어진 배열에서 정상적인 암호코드들에 포함된 숫자들의 합을 출력한다.

**[예제 풀이]**

1번 케이스의 암호코드 정보를 추출하면 아래와 같다.

01110110110001011101101100010110001000110100100110111011
01110110110001011101101100010110001000110100100110111011
01110110110001011101101100010110001000110100100110111011
01110110110001011101101100010110001000110100100110111011
01110110110001011101101100010110001000110100100110111011
01110110110001011101101100010110001000110100100110111011
01110110110001011101101100010110001000110100100110111011

이 숫자가 나타내는 정보는 각각 아래와 같다.
0111011(7) 0110001(5) 0111011(7) 0110001(5) 0110001(5) 0001101(0) 0010011(2) 0111011(7)

검증코드가 맞는지 살펴보면, (7 + 7 + 5 + 2) * 3 + 5 + 5 + 0 + 7 = 80 이므로 올바른 암호코드라고 할 수 있다. 따라서 1번의 출력 값은 38이 된다.

2번 케이스도 같은 방식으로 계산할 경우, 검증코드가 틀렸음을 알 수 있다. 따라서 2번의 출력 값은 0이 된다.

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
		int T = Integer.parseInt(br.readLine());
		
		String pwd_code_num[] = {"0001101", "0011001", "0010011", "0111101", "0100011", "0110001", "0101111", "0111011", "0110111", "0001011"};
		
		for(int test_case = 1; test_case <= T; test_case++) {
			int answer = 0;
			st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken()); // 세로
			int M = Integer.parseInt(st.nextToken()); // 가로
			int num[] = new int[8];
			
			for(int i=0; i<N; i++) {
				String pwd_code = br.readLine();
				int last_1 = pwd_code.lastIndexOf("1");
				if(last_1 == -1) {
					continue;
				}else {
					pwd_code = pwd_code.substring(last_1 - 55, last_1+1);
					for(int j=0; j<8; j++) {
						String code = pwd_code.substring(j*7, j*7+7);
						for(int k=0; k<10; k++) {
							if(code.equals(pwd_code_num[k])) {
								num[j] = k;
								break;
							}
						}
					}
				}
			}
			
			int result = (num[0]+num[2]+num[4]+num[6])*3 + num[1]+num[3]+num[5] + num[7];
			if(result%10 == 0) {
				for(int i=0; i<8; i++) {
					answer += num[i];
				}
			}
			
			System.out.println("#"+test_case+" "+answer);
		}
	}
}
```

```C++
#include <iostream>
using namespace std;
int HashTable[7000];
int Row, Col;
char Arr[50][100];

int main(int argc, char** argv){
    for(int i=0; i<7000; ++i)
        HashTable[i] = -1;
    HsahTable[3211] = 0;
    HsahTable[2221] = 1;
    HsahTable[2122] = 2;
    HsahTable[1411] = 3;
    HsahTable[1132] = 4;
    HsahTable[1231] = 5;
    HsahTable[1114] = 6;
    HsahTable[1312] = 7;
    HsahTable[1213] = 8;
    HsahTable[3112] = 9;
    int tcCnt;
    cin >> tcCnt;
    for(int t=1; t<=tcCnt; ++t){
        cin >> Row >> Col;
        for(int i=0; i<Row; ++i){
            for(int j=0; j<Col; ++j){
                cin >> Arr[i][j];
            }
        }
        cout << "#" << t << ' ' << solve() << endl;
    }
    return 0;
}

int parse(int row, int col){
    int key = 0;
    int cnt = 1;
    for(int i=0; i<7; ++i){
        if(col+i < Col-1 && Arr[row][col+i] == Arr[row][col+i+1]){
            ++cnt;
        }else{
            key *= 10;
            key += cnt;
            cnt = 1;
        }
    }
    return HashTable[key];
}

int solve(){
    int code[8], sum = 0;
    for(int i=0; i<Row; ++i){
        for(int j=Col-1; j>=55; --j){
            if(Arr[i][j] == '1'){
                bool flag = true;
                for(int k=0; k<8; ++k){
                    code[k] = parse(i, j-55 +k * 7);
                    if(code[k] < 0){
                        flag = false;
                        break;
                    }
                }
                if(flag)
                    break;
            }
        }
    }
    if(((code[0]+code[2]+code[4]+code[6])*3 + (code[1]+code[3]+code[5]+code[7])) % 10 == 0){
        for(int i=0; i<8; i++){
            sum += code[i];
        }
    }
    return sum;
}
```



## 1242. [S/W 문제해결 응용] 1일차 - 암호코드 스캔 D5

※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

어떤 국가에서는 자국 내 방송국에서 스파이가 활동하는 사실을 알아냈다.

스파이는 영상물에 암호 코드를 삽입하여 송출하고 있었다.

암호 코드는 국가 내 중요 시설을 의미하는 숫자임을 알아냈다. 암호 코드의 규칙은 아래와 같다.

 A 업체에서는 이 암호코드들을 빠르고 정확하게 인식할 수 있는 스캐너를 개발하려고 한다. 스캐너의 성능은 아래와 같은 방법으로 측정된다.

 배열에 포함되어 있는 암호코드의 세부 규칙은 아래와 같다.

 암호코드 정보가 포함된 2차원 배열을 입력으로 받아 정상적인 암호코드를 판별하는 프로그램을 작성하라.

**[입력]**

표준 입력으로 T개의 테스트 케이스가 이어져서 주어진다.

각 테스트 케이스의 첫 줄에 두 자연수가 주어지는데 각각 배열의 세로 크기 N, 배열의 가로크기 M이다 (1≤N<2000, 1≤M<500).

그 다음 N 개의 줄에는 M개의 배열의 값이 주어진다. 문제의 모든 배열의 값은 16진수이다.

**[출력]**

각 테스트 케이스의 답을 순서대로 표준출력으로 출력하며, 각 케이스마다 줄의 시작에 “#C”를 출력하여야 한다. 이때 C는 케이스의 번호이다.

같은 줄에 빈칸을 하나 두고, 입력에 주어진 배열에서 정상적인 암호코드들에 포함된 숫자들의 합을 출력한다.

**[참고]**

각 테스트 케이스의 구성은 아래와 같다.

 

| 테스트 케이스 | N * M      | 암호코드 가로 길이 | 암호코드 개수 |
| ------------- | ---------- | ------------------ | ------------- |
| 그룹 1        | 100 * 26   | 56                 | 1             |
| 그룹 2        | 200 * 50   | 56 ~ 112           | 2             |
| 그룹 3        | 500 * 126  | 56 ~ 280           | 5             |
| 그룹 4        | 1000 * 250 | 제한 없음          | 제한 없음     |
| 그룹 5        | 2000 * 500 | 제한 없음          | 제한 없음     |

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

class Solution
{
	static String pwd_code_num[] = { "0001101", "0011001", "0010011", "0111101", "0100011", "0110001", "0101111", "0111011", "0110111", "0001011"};
	
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		int T = Integer.parseInt(br.readLine());
		for (int test_case = 1; test_case <= T; test_case++) {
			st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken());
			int M = Integer.parseInt(st.nextToken());
			int answer = 0;
			int Arr[][] = new int[N][M * 4];

			// hex to bin input Arr
			for (int i = 0; i < N; i++) {
				st = new StringTokenizer(br.readLine(),"");
				String str = st.nextToken();
				for (int j = 0; j < M; j++) {
					String str_tmp = String.valueOf(str.charAt(j));
					String tmp = Integer.toBinaryString(Integer.parseInt(str_tmp, 16));
					
					for (int k = 4; k > 0; k--) {
						if (k - tmp.length() != 0) {
							Arr[i][j * 4 + 4 - k] = 0;
						} else {
							Arr[i][j * 4 + 4 - k] = Integer.parseInt(String.valueOf(tmp.charAt(0)));
							tmp = tmp.substring(1);
						}
					}
				}
			}

			int M4 = M * 4;
			for (int i = 0; i < N; i++) {
				int num[] = new int[8];
				boolean flag = true;
				for (int j = M4 - 1; j >= 55; j--) {
					if(Arr[i][j] == 1) {
						// scale check
						int scale = scaleCheck(Arr, i, j, M4);
						// start point
						int start_p = j - (56 * scale) + 1;

						for (int k = 0; k < 8; k++) {
							num[k] = parse(Arr, i, start_p + k * 7 * scale, scale);
							if(num[k] < 0) {
								flag = false;
								break;
							}
						}
						
						if (flag) {
							for(int x=i+1; x<N; x++) {
								for(int y=start_p; y<=j; y++) {
									if(Arr[i][y] == Arr[x][y]) {
										Arr[x][y] = 0;
									}else {
										x = N;
										break;
									}
								}
							}
							
							// answer
							int result = (num[0] + num[2] + num[4] + num[6]) * 3 + num[1] + num[3] + num[5] + num[7];
							if (result % 10 == 0) {
								for (int a = 0; a < 8; a++) {
									answer += num[a];
								}
							}
						}
						break;
					}
				}
			}

			System.out.println("#" + test_case + " " + answer);
		}
	}

	public static int parse(int Arr[][], int row, int col_start, int scale) {
		
		String code = "";
		for (int i = col_start; i < col_start + scale * 7; i++) {
			if (i % scale == 0) {
				code += Integer.toString(Arr[row][i]);
			}
		}
		for (int l = 0; l < 10; l++) {
			if (code.equals(pwd_code_num[l])) {
				return l;
			}
		}
		return -1;
	}

	public static int scaleCheck(int Arr[][], int row, int col, int M4) {
		
		int cnt = 0;
		for (int i = col; i > 0; i--) {
			if (Arr[row][i] != Arr[row][i - 1]) {
				++cnt;
			}
			if (cnt == 4) {
				return (col - i + 1) / 7;
			}
		}
		return 1;
	}
}
```

```C++
#include <iostream>
using namespace std;

char HexaToBin[16][5] = {"0000", "0001", "0010", "0011", "0100", "0101", "0110", "0111", "1000", "1001", "1010", "1011", "1100", "1101", "1110", "1111"};
int HashTable[7000], Row, Col;
char Arr[2000][2000];
int main(int argc, char** argv){
    for(int i=0; i<7000; ++i)
        HashTable[i] = -1;
    HsahTable[3211] = 0;
    HsahTable[2221] = 1;
    HsahTable[2122] = 2;
    HsahTable[1411] = 3;
    HsahTable[1132] = 4;
    HsahTable[1231] = 5;
    HsahTable[1114] = 6;
    HsahTable[1312] = 7;
    HsahTable[1213] = 8;
    HsahTable[3112] = 9;
    int tcCnt;
    char a;
    cin >> tcCnt;
    for(int t=1; t<=tcCnt; ++t){
        cin >> Row >> Col;
        for(int i=0; i<Row; ++i){
            for(int j=0; j<Col; ++j){
                cin >> a;
                if(a<'A')
                    a -= '0';
                else
                    a = a-'A' + 10;
                for(int k=0; k<4; ++k)
                    Arr[i][j*4+k] = HexaToBin[a][k];
            }
        }
        Col *= 4;
        cout << "#" << t << ' ' << solve() << endl;
    }
    return 0;
}

int calcScale(int row, int col){ // 몇배 확대되었는지 배율 구하는 함수
    int cnt = 0;
    for(int i=col; i>0; --i){
        if(Arr[row][i] != Arr[row][i-1])
            ++cnt;
        if(cnt == 4)
            return (col-i+1)/7;
    }
    return 1;
}

int parse(int row, int col, int scale){
    int key = 0;
    int cnt = 1;
    for(int i=0; i<7*scale; ++i){
        if(col+i < Col-1 && Arr[row][col+i] == Arr[row][col+i+1]){
            ++cnt;
        }else{
            cnt /= scale;
            key = key*10+cnt;
            cnt = 1;
        }
    }
    return HashTable[key];
}

int solve(){
    int code[8], sum = 0;
    for(int i=0; i<Row; ++i){
        for(int j=Col-1; j>=55; --j){
            if(Arr[i][j] == '1'){
                int scale = calcScale(i,j);
                int startCol = j-(56*scale)+1;
                bool flag = true;
                for(int k=0; k<8; ++k){
                    code[k] = parse(i, startCol+k*7*scale, scale);
                    if(code[k] < 0){
                        flag = false;
                        break;
                    }
                }
                if(flag){
                    for(int a=i+1; a<Row; ++a){
                        for(int b= startCol; b<=j; ++b){
                            if(Arr[i][b] = Arr[a][b])
                                Arr[a][b] = 0;
                            else{
                                a = Row;
                                break;
                            }
                        }
                    }
                    if(((code[0]+code[2]+code[4]+code[6])*3 + (code[1]+code[3]+code[5]+code[7])) % 10 == 0){
                        for(int i=0; i<8; i++){
                            sum += code[i];
                        }
                    }
                    j = startCol - 1;
                }
            }
        }
    }
    return sum;
}
```

