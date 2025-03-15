# string

### 1.字符串创建与初始化

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1 = "Hello, World!";  // 使用字符串字面量初始化
    string s2("USTC");           // 使用构造函数初始化
    string s3(5, 'a');           // 创建一个包含5个字符'a'的字符串
    string s4 = s1;              // 复制构造
    cout << s1 << " " << s3 << endl;
    return 0;
}
```

### 2.基本操作

* 获取长度

  ```cpp
  string str = "Hello";
  cout << str.size() << endl;  // 输出字符串长度，结果为5
  cout << str.length() << endl;  // 等同于size()
  ```

* 访问字符

  ```cpp
  string str = "abc";
  cout << str[1] << endl;   // 输出'b'
  str[2] = 'z';             // 修改字符串内容
  ```

### 3.字符串拼接

```cpp
string str1 = "Hello";
string str2 = "World";
string result = str1 + ", " + str2 + "!";  // 使用'+'拼接
cout << result << endl;

str1 += " C++";  // 使用'+='直接修改原字符串
cout << str1 << endl;
```

### 4.查找和替换

* 查找子串

  ```cpp
  string str = "I love UESTC";
  size_t pos = str.find("UESTC");
  if (pos != string::npos) {
      cout << "Found at: " << pos << endl;
  } else {
      cout << "Not found!" << endl;
  }
  ```

* **替换子串**

  ```cpp
  string str = "I love UESTC";
  str.replace(7, 5, "C++");  // 从索引7开始，替换长度为5的子串为"C++"
  cout << str << endl;  // 输出: I love C++
  ```

  * 例题

    ```cpp
    //输入str,查找其中的target，全部替换为target的翻转
    
    
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    
    signed main(){
        string str,target;
        cin >> str >> target;
        string replacement = target;
        reverse(replacement.begin(),replacement.end());
        auto pos = str.find(target);
        while(pos != string::npos){
            str.replace(pos,target.size(),replacement);
            pos = str.find(target,pos + replacement.size());
        }
        cout << str << endl;
    
    
        return 0;
    }
    ```

    

### 5. 截取子串

```cpp
string str = "Hello, World!";
string sub = str.substr(7, 5);  // 从索引7开始截取长度为5的子串
cout << sub << endl;  // 输出: World
```

### 6.比较字符串

```cpp
string str1 = "abc";
string str2 = "def";
if (str1 == str2) {
    cout << "Equal" << endl;
} else if (str1 < str2) {
    cout << "str1 is less than str2" << endl;
} else {
    cout << "str1 is greater than str2" << endl;
}
```

### 7.清空、插入、删除

* 清空字符串

  ```cpp
  string str = "abc";
  str.clear();  // 清空字符串内容
  cout << str.empty() << endl;  // 输出: 1 (true)
  ```

* 插入子串

  ```cpp
  string str = "Hello";
  str.insert(5, ", World");  // 在索引5处插入子串
  cout << str << endl;  // 输出: Hello, World
  ```

* 删除子串

  ```cpp
  string str = "Hello, World!";
  str.erase(5, 7);  // 从索引5开始删除长度为7的子串
  cout << str << endl;  // 输出: Hello!
  ```

  * 例题
	```cpp
	//删除指定字符(小规模)
	str.erase(std::remove_if(str.begin(), str.end(),
                               [](char c) { return c == 's' || c == 'S'; }),
                str.end());
  //版本二(大规模)
  string charsToRemove = "sS"; // 需要移除的字符
  str.erase(std::remove_if(str.begin(), str.end(),
                           [&](char c) { return charsToRemove.find(c) != string::npos; }),
            str.end());
  
    



### 8.字符串遍历

```cpp
string str = "Hello";
for (char c : str) {
    cout << c << " ";
}
cout << endl;

// 或者使用传统方式
for (size_t i = 0; i < str.size(); ++i) {
    cout << str[i] << " ";
}

//或用lambda表达式
for_each(s.begin(),c.end(),[](char c){
   cout << c << endl; 
});
```



### 删除特定字符

```cpp
//input 2006/01/02
//delete '/'
string s;cin >> s;
string S;
for(int i = 0;i < s.size();++i){
    if(s[i] != '/') S += s[i];
}
//真删啊，哥们？直接新建一个字符串不香吗？
```



### 去除前导零

```cpp
    // 去除前导零
    size_t start_a = a.find_first_not_of('0');
    size_t start_b = b.find_first_not_of('0');
    string a_num = (start_a == string::npos) ? "0" : a.substr(start_a);
    string b_num = (start_b == string::npos) ? "0" : b.substr(start_b);
```
