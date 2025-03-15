# 换根DP

[1.新咖啡店 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/8190/learning/?page=1&first_category_id=1&sort=students_count&problem_id=8190)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int N = 1e5+9;

int n;
int dp[N],sz[N],dep[N];//dp[i]表示所有节点到i的距离之和 
vector<int> g[N];

void dfs1(int x, int fa)
{
	sz[x] = 1;
	for(const auto &y : g[x])
	{
		if(y == fa)continue;
		dep[y] = dep[x] + 1;//从上到下，在前面
		dfs1(y,x);
		sz[x] += sz[y];//从下到上，在后面
	 } 
}

void dfs2(int x,int fa){
	for(auto &y : g[x]){
		if(y == fa)continue;
		dp[y] = dp[x] - sz[y] + n - sz[y];
		dfs2(y,x);
	}
}



signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> n;
    for(int i = 1;i < n;++i)
    {
    	int u,v;cin >> u >>v;
    	g[u].push_back(v);
    	g[v].push_back(u);
	}
	dfs1(1,0);
    for(int i = 1;i <= n;++i) dp[1] += dep[i];
    dfs2(1,0);
    int ans = dp[1];
    for(int i = 2;i <= n;++i) ans = min(ans,dp[i]);
    cout << ans << endl;



	return 0;
}
```



[1.举办聚会 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/4354/learning/?page=1&first_category_id=1&sort=students_count&problem_id=4354)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int N = 2e4+5;

int a[N];//存储节点上人数
int tot;//存储总人数
int sz[N],dp[N],dep[N];
//dp[i]:所有人到i的距离之和 
int n,k;

vector<int> g[N];

void dfs1(int x,int fa){
	sz[x] = a[x];
	for(auto &y : g[x]){
		if(y == fa) continue;
		dep[y] = dep[x] + 1;//自上而下
		dfs1(y,x);
		sz[x] += sz[y];//自下而上 
	}
}

void dfs2(int x,int fa){
	for(auto &y : g[x]){
		if(y == fa)continue;
		dp[y] = dp[x] - sz[y] + tot - sz[y];
		dfs2(y,x);
	}
}

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> n >> k;
    for(int i = 1;i <= n;++i) cin >> a[i],tot += a[i];
    for(int i = 2;i <= n;++i)
    {
    	int u,v;
    	cin >> u >> v;
    	g[u].push_back(v),g[v].push_back(u);
	}
	dfs1(1,0);
	for(int i = 1;i <= n;++i) dp[1] += dep[i];
	dfs2(1,0);
	vector<int> v;
	for(int i = 1;i <= n;++i) v.push_back(i);
	sort(v.begin(),v.end(),[](int &u,int &v){
		if(dp[u] != dp[v]) return dp[u] < dp[v];
		return u < v;	
	});
	cout << v[k-1] << endl; 

	return 0;
}
```

