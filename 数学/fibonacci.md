#### 递归调用

```cpp
int fibonacci(int n){
    if(n <= 1){
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}
//时间复杂度 O(2^n)
//因为每个递归调用会产生两个额外的递归调用

//空间复杂度  O(n)
//递归深度为n，因此需要的堆栈空间为O(n)
```

```cpp
//优化：记忆化搜索
int fib(int n){
    if(dp[n]) return dp[n];
    if(n <= 1) return n;
    return dp[n] = fib(n-1) + fib(n-2);
}
//优化后：时间复杂度O(n)，每个点只会算1次
```



![image-20241209083917659](C:\Users\Emerson\AppData\Roaming\Typora\typora-user-images\image-20241209083917659.png)

​	这样一个二叉树，时间复杂度为O(2^n)





#### 迭代

```cpp
int fibonacci(int n){
    if(n <= 1){
        return n;
    }
    
    int prev1 = 0;
    int prev2 = 1;
    int fib = 0;
    
    for(int i = 2;i <= n;i++){
        fib = prev1 + prev2;
        prev1 = prev2;
        prev2 = fib;
    }
    
    return fib;
}


//时间复杂度   O(n)
//循环遍历n次

//空间复杂度   O(1)
```



