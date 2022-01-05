# 使用 C++ STL 打印给定范围内的质数

> 原文:[https://www . geesforgeks . org/print-质数-给定范围-使用-c-stl/](https://www.geeksforgeeks.org/print-prime-numbers-given-range-using-c-stl/)

生成两个给定数之间的所有素数。任务是打印该范围内的质数。厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)是寻找所有小于 n 的素数的最有效方法之一，其中 n 小于 1000 万左右。

示例:

```
Input : start = 50 end = 100
Output : 53 59 61 67 71 73 79 83 89 97

Input : start = 900 end = 1000
Output : 907 911 919 929 937 941 947 953 967 971 977 983 991 997

```

想法是使用厄拉多塞筛作为子程序。首先，从 0 开始寻找素数，并将其存储在向量中。类似地，找到从 0 到结束范围内的素数，并存储在另一个向量中。现在取两个向量的集合差，得到需要的答案。去掉向量中多余的零。

```
// C++ STL program to print all primes 
// in a range using Sieve of Eratosthenes 
#include<bits/stdc++.h>
using namespace std;

typedef unsigned long long int ulli;

vector<ulli> sieve(ulli n)
{
    // Create a boolean vector "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    vector<bool> prime(n+1,true);

    prime[0] = false;
    prime[1] = false;
    int m = sqrt(n);

    for (ulli p=2; p<=m; p++)
    {

        // If prime[p] is not changed, then it
        // is a prime 
        if (prime[p])
        {
            // Update all multiples of p
            for (ulli i=p*2; i<=n; i += p)
            prime[i] = false;
        }
    }

    // push all the primes into the vector ans
    vector<ulli> ans;
    for (int i=0;i<n;i++)
        if (prime[i])
            ans.push_back(i);
    return ans;
}

// Used to remove zeros from a vector using 
// library function remove_if()
bool isZero(ulli i)
{
    return i == 0;
}

vector<ulli> sieveRange(ulli start,ulli end)
{
    // find primes from [0..start] range
    vector<ulli> s1 = sieve(start);  

    // find primes from [0..end] range 
    vector<ulli> s2 = sieve(end);  

    vector<ulli> ans(end-start);

    // find set difference of two vectors and
    // push result in vector ans
    // O(2*(m+n)-1) 
    set_difference(s2.begin(), s2.end(), s1.begin(), 
                             s2.end(), ans.begin());

    // remove extra zeros if any. O(n)
    vector<ulli>::iterator itr =
                    remove_if(ans.begin(),ans.end(),isZero);

    // resize it. // O(n)
    ans.resize(itr-ans.begin());

    return ans;
}

// Driver Program to test above function
int main(void)
{ 
    ulli start = 50;
    ulli end = 100;
    vector<ulli> ans = sieveRange(start,end);
    for (auto i:ans)
        cout<<i<<' ';
    return 0;
}
```

输出:

```
53 59 61 67 71 73 79 83 89 97

```

本文由**瓦润·塔库尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。