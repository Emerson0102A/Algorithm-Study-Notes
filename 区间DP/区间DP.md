# 区间DP

```cpp
//dp[i][j]表示区间[i,j]的最大价值或最小代价

//最小代价
//初始化
for(int i = 1;i <= n;++i){
    for(int j = i;j <= n;++j){
        dp[i][j] = inf;
    }
}
//特殊处理长度为1的
for(int i = 1;i <= n;++i)dp[i][i] = 1; 
//从长度为2开始枚举
for(int len = 2;len <= n;++len){
    //枚举起点i
    for(int i = 1;i + len - 1 <= n;++i){
        //计算终点j
        int j = i + len - 1;
        //状态转移
        if(a[i] == a[j]){
            dp[i][j] = min(dp[i][j],dp[i+1][j-1]+(len == 2));
        }
        for(int k = i;k + 1 <= j; ++k){
            dp[i][j] = min(dp[i][j],dp[i][k] + dp[k+1][j]);
        }
    }
}
```



### 例题

[1.石子合并 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/1233/learning/?page=1&first_category_id=1&problem_id=1233)

```cpp
//dp[i][j]表示将区间[i,j]的石子合并的代价
//将区间i,j划分为两部分[i,k]和[k+1,j]
//(从i到j求和)a[u]是再合并的代价
//dp[i][j] = min(dp[i][k] + dp[k+1][j] + (从i到j求和)a[u])
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int N = 205;
const int inf = 1e18;

int a[N],dp[N][N],pre[N];

int n;

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
	cin >> n;
	for(int i = 1;i <= n;++i)cin >> a[i];
	for(int i = 1;i <= n;++i)pre[i] = pre[i-1] + a[i];
	//初始化
	for(int i = 1;i <= n;++i){
		for(int j = i;j <= n;++j){
			dp[i][j] = inf;
		}
	}
	//特殊处理长度为1的
	for(int i = 1;i <= n;++i)dp[i][i] = 0;
	//从长度为2开始枚举
	for(int len = 2;len <= n;++len){
		//枚举起点i
		for(int i = 1;i + len - 1 <= n;++i){
			//计算终点j
			int j = i + len - 1;
			for(int k = i;k + 1 <= j;++k){
				dp[i][j] = min(dp[i][j],dp[i][k] + dp[k+1][j] + pre[j]-pre[i-1]);
			}
		} 
	}  
	cout << dp[1][n] << endl;

	return 0;
}
```

[1.小蓝吃苹果 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/8342/learning/?page=1&first_category_id=1&problem_id=8342)

```cpp
//dp[i][j]表示将区间[i][j]的苹果吃掉的最小代价
//若a[i] == a[j],a[i]、a[j]可以和[i+1][j-1]区间内的某一个回文串再拼成一个回文串，于是吃掉a[i]和a[j]的代价为0,特殊情况是[i+1,j-1]为空时，里面没有回文串，代价为1
//若a[i] != a[j]，将其划分为两部分，分别计算结果并求和
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int N = 505;
const int inf = 1e18;

int dp[N][N],a[N],pre[N];

int n;


signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
	cin >> n;
	for(int i = 1;i <= n;++i){
		cin >> a[i];
	}
	//初始化
	for(int i = 1;i <= n;++i){
		for(int j = i;j <= n;++j){
			dp[i][j] = inf;
		}
	} 
	//len == 1
	for(int i = 1;i <= n;++i)dp[i][i] = 1;
	//
	for(int len = 2;len <= n;++len){
		for(int i = 1;i + len - 1 <= n;++i){
			int j = i + len - 1;
			if(a[i] == a[j]){
				dp[i][j] = min(dp[i][j],dp[i+1][j-1] + (len == 2));
			}
			for(int k = i;k + 1 <= j;++k){
				dp[i][j] = min(dp[i][j],dp[i][k] + dp[k+1][j]);
			}
		}
	}
	cout << dp[1][n]; 


	return 0;
}
```

[1.涂色 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/926/learning/?page=1&first_category_id=1&problem_id=926)

```cpp
//dp[i][j] 表示将区间[i,j]刷成目标的最小代价
//若a[i] == a[j]，只需让[i,j-1]或[i+1,j]的那次操作延伸即可0代价转移
//否则，一定存在一个分界点k，使得[i][k]和[k+1][j]内操作最优
//注，最优操作只有包含，没有交叉，交叉重叠的部分属于浪费，可将两次有交叉的操作分解为两次无交叉的操作
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int inf = 1e18;
const int N = 55;

int dp[N][N];
char s[N];


signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
	cin >> s + 1;
	int n = strlen(s + 1);
	//初始化 
	for(int i = 1;i <= n;++i)
		for(int j = i;j <= n;++j)dp[i][j] = inf;
	for(int i = 1;i <= n;++i) dp[i][i] = 1;
	
	//枚举
	for(int len = 2;len <= n;++len){
		for(int i = 1;i + len - 1 <= n;++i){
			int j = i + len - 1;
			if(s[i] == s[j]) dp[i][j] = min(dp[i+1][j],dp[i][j-1]);//处理端点相同的情况
			for(int k = i;k < j;++k) dp[i][j] = min(dp[i][j],dp[i][k]+dp[k+1][j]);//处理端点不同的情况
		} 
	} 
	cout << dp[1][n] << endl;
	return 0;
}
```

[1.最少操作数 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/1548/learning/?page=1&first_category_id=1&problem_id=1548)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int inf = 1e18;
const int N = 104;

int dp[N][N],f[N];
//dp[i][j]表示将区间[i, j]从空串刷为b的代价
//f[i]表示将区间[1, i]从a刷到b的代价 
char a[N], b[N];


signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
	cin >> a + 1 >> b + 1;
	int n = strlen(a + 1);
	//初始化 
	for(int i = 1;i <= n;++i)
		for(int j = i;j <= n;++j)dp[i][j] = inf;
	for(int i = 1;i <= n;++i) dp[i][i] = 1;
	
	//枚举
	for(int len = 2;len <= n;++len){
		for(int i = 1;i + len - 1 <= n;++i){
			int j = i + len - 1;
			if(b[i] == b[j]) dp[i][j] = min(dp[i+1][j],dp[i][j-1]);
			for(int k = i;k < j;++k) dp[i][j] = min(dp[i][j],dp[i][k]+dp[k+1][j]);
		} 
	} 
	for(int i = 1;i <= n;++i)f[i] = dp[1][i];
	for(int i = 1;i <= n;++i)
	{
		if(a[i] == b[i]) f[i] = min(f[i], f[i -1]);
		for(int j = 1;j + 1 <= i;++j) f[i] = min(f[i], f[j] + dp[j+1][i]);
		//                                   前面的部分有刷有不刷 [j+1,i]需要刷 
	}
	cout << f[n] << endl;
	return 0;
}
```

