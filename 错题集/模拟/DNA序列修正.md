[16届蓝桥杯省赛无忧班（C&C++ 组）1期 - DNA序列修正 - 蓝桥云课 (lanqiao.cn)](https://www.lanqiao.cn/courses/40610/learning/?id=2751648&compatibility=false)





```cpp
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int N; cin >> N;
    string s1, s2;
    cin >> s1 >> s2;
    for (int i=0; i<N; i++)
    {
        if (s1[i]=='A') s1[i] = 'T';
        else if (s1[i]=='T') s1[i] = 'A';
        else if (s1[i]=='C') s1[i] = 'G';
        else s1[i] = 'C';
    }
    //假如ans尽可能小，那么swap就尽可能多
    int ans = 0;
    for (int i=0; i<N; i++){
        if (s1[i] == s2[i]) continue;
        for (int j=i+1; j<N; j++){
            if (s1[i] == s2[j] && s2[i] == s1[j]){
                swap(s2[i], s2[j]);               
            }
        }
        ans += 1;
        //只要不同，操作数就会增加
        //swap是让后面的无需操作，从而减少了操作数
    }
    cout << ans;
}