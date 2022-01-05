# 使用 STL | Set 2

给定范围内的质数

> 原文:[https://www . geesforgeks . org/给定范围内的质数-使用-stl-set-2/](https://www.geeksforgeeks.org/prime-numbers-in-a-given-range-using-stl-set-2/)

生成两个给定数之间的所有素数。任务是打印该范围内的质数。厄拉多塞筛是寻找所有小于 n 的素数的最有效方法之一，其中 n 小于 1000 万左右。

示例:

```
Input : start = 50 end = 100
Output : 53 59 61 67 71 73 79 83 89 97

Input : start = 900 end = 1000
Output : 907 911 919 929 937 941 947 953 967 971 977 983 991 997

```

想法是使用厄拉多塞筛作为子程序。我们已经讨论了使用 STL | Set 1 在给定范围内的[素数中的一个实现](https://www.geeksforgeeks.org/print-prime-numbers-given-range-using-c-stl/)

1.  找到从 0 到结束范围内的素数，并将其存储在向量中
2.  使用二分搜索法查找小于起始值的元素的索引。我们在 STL 中使用[下界()。](https://www.geeksforgeeks.org/stdlower_bound-in-c/)
3.  从向量的开始到索引删除元素。我们使用[矢量擦除()](https://www.geeksforgeeks.org/vectorclear-vectorerase-c-stl/)

维奥拉。向量包含从头到尾的素数。

```
// C++ program to print all primes
// in a range using Sieve of Eratosthenes
#include <algorithm>
#include <cmath>
#include <iostream>
#include <vector>
using namespace std;

#define all(v) v.begin(), v.end()
typedef unsigned long long int ulli;

vector<ulli> sieve(ulli n)
{
    // Create a boolean vector "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    vector<bool> prime(n + 1, true);

    prime[0] = false;
    prime[1] = false;
    int m = sqrt(n);

    for (ulli p = 2; p <= m; p++) {

        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p]) {

            // Update all multiples of p
            for (ulli i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // push all the primes into the vector ans
    vector<ulli> ans;
    for (int i = 0; i < n; i++)
        if (prime[i])
            ans.push_back(i);
    return ans;
}

vector<ulli> sieveRange(ulli start, ulli end)
{
    // find primes from [0..end] range
    vector<ulli> ans = sieve(end);

    // Find index of first prime greater than or
    // equal to start
    // O(sqrt(n)loglog(n))
    int lower_bound_index = lower_bound(all(ans), start) - 
                                              ans.begin();

    // Remove all elements smaller than start.
    // O(logn)
    ans.erase(ans.begin(), ans.begin() + lower_bound_index);

    return ans;
}

// Driver Program to test above function
int main(void)
{
    ulli start = 50;
    ulli end = 100;
    vector<ulli> ans = sieveRange(start, end);
    for (auto i : ans)
        cout << i << ' ';
    return 0;
}
```

**Output:**

```
53 59 61 67 71 73 79 83 89 97

```