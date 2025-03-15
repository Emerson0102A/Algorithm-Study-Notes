# 自下而上的树形DP

[1.保卫国王大道 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/4503/learning/?page=1&first_category_id=1&problem_id=4503)



```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define db double
const int N = 2e5+8;

int dp[N][2];
//dp[i][0]表示i点不是军营
//dp[i][1]表示i点是军营的最小军营数量 
int n;
vector<int> g[N];

void dfs(int x,int fa)
{
	dp[x][1] = 1;
	for(const auto &y : g[x])
	{
		if(y == fa) continue;
		dfs(y, x);
		dp[x][0] += dp[y][1];
		dp[x][1] += min(dp[y][0],dp[y][1]);
	}
}


signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> n;
    for(int i = 1;i < n;++i)
    {
    	int x,y;cin >> x >> y;
    	g[x].push_back(y),g[y].push_back(x);
	}
	dfs(1,0);
	
	cout << min(dp[1][0],dp[1][1]) << endl;

	return 0;
}
```



[1.左孩子右兄弟 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/1451/learning/?page=1&first_category_id=1&sort=students_count&problem_id=1451)



```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int N = 1e6+10;

int dp[N];
int fa[N];
vector<int> g[N];

void dfs(int x,int fa){
	for(auto &y : g[x])
	{
        if(y == fa) continue;
		dfs(y,x);
		dp[x] = max(dp[x],(ll)g[x].size()+dp[y]);
	}
}

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    int n;cin >> n;
    for(int i = 2;i <= n;++i)
    {
    	cin >> fa[i];
    	g[fa[i]].push_back(i);
	}
	dfs(1,0);
	cout << dp[1] << endl;



	return 0;
}
```



[1.树的连边II - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/4329/learning/?page=1&first_category_id=1&sort=students_count&problem_id=4329)



```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int N = 2e5+9;
int n,dp[N],dep[N];

vector<int> g[N];

void dfs(int x,int fa)
{
	dep[x] = 1; 
	for(auto &y : g[x]){
	
		if( y == fa) continue;
		dfs(y,x);
		dp[x] = max(dp[x],dep[x]+dep[y]);
		dep[x] = max(dep[x],dep[y]+1);
	}
}


signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> n;
    for(int i = 2;i <= n;++i)
    {
    	
    	int x,y;
    	cin >> x >> y;
    	g[x].push_back(y);
    	g[y].push_back(x);
	}
	dfs(1,0);
	int ans = 0;
	for(int i = 1;i <= n;++i)
	{
		ans = max(ans,dp[i]);
	}
	cout << ans - 1 << endl;



	return 0;
}
```

