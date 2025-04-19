![image-20250406085252455](C:\Users\Emerson\AppData\Roaming\Typora\typora-user-images\image-20250406085252455.png)

![image-20250406085644921](C:\Users\Emerson\AppData\Roaming\Typora\typora-user-images\image-20250406085644921.png)

```cpp
int dp[N][N];

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    int n,m,q;cin >> n >> m >> q;
    //初始化
    for(int i = 1;i <= n;++i){
        for(int j = 1;j <= n;++j){
            dp[i][j] = inf;
        }
    }
    for(int i = 1;i <= n;++i){
        dp[i][i] = 0;
    }
    //输入
    for(int i = 1;i <= m;++i){
        int u,v,w;cin >> u >> v >> w;
        dp[u][v] =min(dp[u][v],w);
        dp[v][u] =min(dp[v][u],w);
    }
    //Floyd
    for(int k = 1;k <= n;++k){
        for(int i = 1;i <= n;++i){
            for(int j = 1;j <= n;++j){
                dp[i][j] = min(dp[i][j],dp[i][k] + dp[k][j]);
            }
        }
    }
    //询问
    while(q--){
        int st,ed;cin >> st >> ed;
        //注意判断是否等于inf
        cout << ((dp[st][ed] >= inf)?-1:dp[st][ed] )<< '\n';
    }

	return 0;
}
```

![image-20250406092820268](C:\Users\Emerson\AppData\Roaming\Typora\typora-user-images\image-20250406092820268.png)

![image-20250406093053946](C:\Users\Emerson\AppData\Roaming\Typora\typora-user-images\image-20250406093053946.png)

![image-20250406093455506](C:\Users\Emerson\AppData\Roaming\Typora\typora-user-images\image-20250406093455506.png)

```cpp
struct node{
    int v,w;
    bool operator<(const node &other) const{
        return w > other.w;
    }
};

int d[N],vis[N];
int n,m;
vector<node> g[N];

void dijkstra(int st){
    //初始化
    for(int i = 1;i <= n;++i) d[i] = inf,vis[i] = 0;
    d[st] = 0;
    priority_queue<node> pq;

    pq.push({st,d[st]});
    while(pq.size()){
        node top = pq.top();
        int u = top.v;
        pq.pop();
        if(vis[u]) continue;
        vis[u] = 1;
        for(auto &p : g[u]){
            int v = p.v;
            int w = p.w;
            if(d[u] + w < d[v]){
                d[v] = d[u] + w;
                pq.push({v,d[v]});
            }
        }
    }
}

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    cin >> n >> m;
    while(m--){
        int u,v,w;cin >> u >> v >> w;
        g[u].push_back({v,w});
    }
    dijkstra(1);

    for(int i = 1;i <= n;++i){
        if(d[i] == inf){
            cout << -1 << ' ';
        }else{
            cout << d[i] << ' ';
        }
    }
	return 0;
}
```

