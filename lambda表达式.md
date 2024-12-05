# lambda表达式

[C++ Lambda表达式详解_c++ lamda-CSDN博客](https://blog.csdn.net/qq_37085158/article/details/124626913?ops_request_misc=%7B%22request%5Fid%22%3A%22ea98b04c8882f164c9286ed01b88dfd4%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=ea98b04c8882f164c9286ed01b88dfd4&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-124626913-null-null.142^v100^pc_search_result_base7&utm_term=c%2B%2Blambda表达式&spm=1018.2226.3001.4187)



### 常用示例

##### erase与remove_if

```cpp
	vector<int> vec = {1, 2, 3, 4, 5, 6, 7, 8, 9};
	
	//删除
	vec.erase(remove_if(vec.begin(),vec.end(),[](int i){
		return i < 5;	
	})
	,vec.end());
	
	//输出
	for_each(vec.begin(),vec.end(),[](int i){
		cout << i << endl;	
	});
```

##### sort排序

*vector版本*

```cpp
	int data[6] = { 3, 4, 12, 2, 1, 6 };
    vector<int> vec;
    vec.insert(vec.begin(), data, data + 6);

    // 对于比较大小的逻辑，使用lamdba不需要在重新定义一个函数
    sort(vec.begin(), vec.end(), [](int a, int b){ 
        return a > b; 
    });
	for_each(vec.begin(),vec.end(),[](int i){
       cout << i << endl;
    });

```

*数组版本*

```cpp
	int a[6] = { 3, 4, 12, 2, 1, 6 };
	
	sort(a,a+6,[](int a,int b){
		return a > b;	
	});
	for_each(a,a+6,[](int i){
		cout << i << endl;	
	});	
```

