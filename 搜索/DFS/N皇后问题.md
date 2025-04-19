[16届蓝桥杯14天省赛冲刺营 1期 - N皇后 - 蓝桥云课](https://www.lanqiao.cn/courses/46292/learning/?id=3441380&compatibility=false)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
//#define int long long
#define db double
#define fl float
#define x first
#define y second
const ll inf = 2e18;
const int base = 1e9+7;
const int N = 15;

int n,ans;
int p[N],vis[N];

bool check(int c){
    for(int i = 1;i < c;++i){
        if(abs(c - i) == abs(p[i] - p[c])){
            //行 == 列 即在对角线上
            return false;
        }
    }
    return true;
}

void dfs(int cnt){
    if(cnt == n){
        ans++;
        return;
    }
    for(int i = 1;i <= n;++i){
        if(!vis[i]){
            vis[i] = 1;
            p[cnt + 1] = i;
            if(check(cnt + 1)){
                dfs(cnt + 1);
            }
            vis[i] = 0;
            p[cnt + 1] = 0;
        }
    }
}

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> n;
    dfs(0);
    cout << ans << endl;

	return 0;
}
```

