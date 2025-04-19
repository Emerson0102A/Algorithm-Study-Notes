# getline

当输入的字符里有`空格`时，我们需要用getline进行读取

```cpp
string s;
while(cin.peek() == '\n'){
    cin.ignore();
}
//这个很重要，必须清除缓冲区，否则回读取到缓冲区的换行符，导致输入读取不完全
getline(cin,s);
```

