```cpp
#include <iostream>
#include <sstream>
#define f float
using namespace std;




int main(){
    string s;//s = "  a   b c 112     "
    getline(cin,s);
    istringstream iss(s);
    int cnt = 0;
    string token;
    while(iss >> token){
        cnt++;
    }
    cout << cnt << endl;//4

    return 0;
}
```

