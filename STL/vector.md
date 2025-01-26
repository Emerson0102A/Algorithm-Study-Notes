# vector

### 利用unique对vector去重

```cpp
vector<int> v;
//一定要先排序
sort(v.begin(),v.end());
auto last = unique(v.begin(),v.end());
//unique的本质是把多出来的重复元素移到末尾，所以需要erase删除
v.erase(last,v.end());
```



### 删除特定值

```cpp
a.erase(remove(a.begin(),a.end(),max_val),a.end());
```

### 求和

```cpp
int sum = accumulate(a.begin(),a.end(),0);
```

