# 状压DP

### 常用位运算

**1.**取出x的第i位 `x >> i & 1`

**2.**将x的第i位设置为1 `x |= (1 << i)`

**3.**将x的第i位反转 `x ^= (1 << i)`

**4.**得到一个低n位均为1的整数 `(1 << n) - 1`

[1.糖果 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/186/learning/?page=1&first_category_id=1&problem_id=186)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int inf = 2e18;
const int N = 105;

int a[N],dp[1 << 21];//dp[i]:达到i时，最少需要买的糖果包数 
//存储时是十进制编号
//运算时是二进制（位运算） 

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    int n,m,k;cin >> n >> m >> k;
    for(int i = 1;i <= n;++i){
    	for(int j = 1;j <= k;++j){
    		int x;cin >> x;
    		a[i] |= (1 << (x -  1));
    		//因为从索引0开始编号，所以x-1 
		}
	}
	for(int sta = 1;sta < (1 << m);++sta) dp[sta] = inf;
	for(int sta = 0;sta < (1 << m);++sta)
	{
		//dp[sta] -> dp[sta | a[i]]
		for(int i = 1;i <= n;++i)
			dp[sta | a[i]] = min(dp[sta | a[i]],dp[sta] + 1);
	}
	int ans = dp[(1 << m)-1];
	cout << (ans == inf ? - 1 : ans) << endl;

	return 0;
}
```

[1.再遇白骨精【算法赛】 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/problems/19748/learning/?page=1&first_category_id=1&problem_id=19748)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define db double
const int inf = 2e18,p = 998244353;

int dp[103][(1 << 11) + 5];
//dp[i][j]表示到第i列为止，且最后一列状态为j的方案数 
int lowbit(int x){
	return x & -x;//运用补码的特性，取得末尾1的位置 
}

//返回x中1的个数
int f(int x)
{
	int res = 0;
	while(x) res++, x-= lowbit(x);
	return res;
}

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
	int n,m,k;cin >> n >> m >> k;
	for(int sta = 0;sta < (1 << n); ++sta) dp[1][sta] = 1;
	//第一户是否显灵是独立的，因为没有前面的状态影响它 
	for(int i = 2;i <= m;++i)
	{
		for(int sta = 0;sta < (1 << n); ++sta)
		{	
			if(f(sta) < k) continue;
			for(int lst_sta = 0;lst_sta < (1 << n);++lst_sta)
			{
				if(f(sta & lst_sta) >= k)
				{
					dp[i][sta] = (dp[i][sta] + dp[i-1][lst_sta]) % p;
				}
			}
		}
	}
	
	int ans = 0;
	for(int sta = 0;sta < (1 << n); ++sta) ans = (ans + dp[m][sta]) % p;
	cout << ans << endl;
	
	return 0;
}
```

