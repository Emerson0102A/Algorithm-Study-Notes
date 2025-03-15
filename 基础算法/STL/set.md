### set

默认升序

```cpp
set<int, greater<int>> mySet//降序排列
    
mySet.insert(114514);
```



```cpp
//运算符重载
struct MyCompare{
    bool operator()(const int &a, const int &b) const {
        //自定义比较逻辑
        return a > b;
    }
};

set<int, MyCompare> mySet;

```





### multiset多重集合

允许存储重复的元素

```cpp
//{x,x,x,y,z}
st.erase(x);
//{y,z}

//若只想删一个
st.erase(st.find(x));
```







### unordered_map无序集合(了解即可)

