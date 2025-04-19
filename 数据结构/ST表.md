### 预处理

```cpp
int f[N][20];
void init_st(int n, int *a) {
    for (int i = 1; i <= n; ++i) {
        f[i][0] = a[i];
    }
    for (int i = 1; i <= 20; ++i) {
        for (int j = 1; j + (1 << i) - 1 <= n; ++j) {
            f[j][i] = max(f[j][i - 1], f[j + (1 << (i - 1))][i - 1]);
        }
    }
}
```

### 询问

```cpp
int query_st(int l, int r) {
    int k = log2(r - l + 1);
    return max(f[l][k], f[r - (1 << k) + 1][k]);
}
```

