# 从数组中移除的最少数量，以使 GCD 更大

> 原文：[https://www.geeksforgeeks.org/minimum-removals-from-array-to-make-gcd-greater/](https://www.geeksforgeeks.org/minimum-removals-from-array-to-make-gcd-greater/)

给定 N 个数字，任务是找到最小的数字去除率，以使剩余数字的 GCD 大于 N 个数字的初始 GCD。 如果无法增加 GCD，请打印“否”。

**示例**：

> 输入：a [] = {1,2,4}
> 输出：1
> 删除第一个元素，然后新的 GCD 为 2，大于初始的 GCD 即 1。
> 
> 输入：a [] = {6，9，15，30}
> 输出：2
> 初始 gcd 为 3，删除 6 和 9，以获得大于 3 的 15 gcd。您也可以删除 9 和 15 得到 gcd 为 6。

请按照以下步骤解决上述问题：

1.  最初使用[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)找到 N 个数字的 gcd。

2.  将所有数字除以获得的 gcd。

3.  使用质数分解的多重查询方法，找到`O(log n)`中每个数字的质数分解。 该方法可以在此处读取[。](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)

4.  将所有素因子插入集合中，以删除使用此方法获得的重复项。

5.  使用哈希映射，计算每个第 i 个元素中主要因子的频率。

6.  一旦数字分解完成，并且计数已存储在频率表中，请在哈希映射中进行迭代，找出出现最大次数的素数。 它不能为 N，因为我们已经将数组元素初始除以 N 个数字的初始 gcd。

7.  如果在初始 gcd 划分之后有任何此类因素，则移除次数将始终为 n-（hash [prime_factor]）。

下面是上述方法的实现。

## CPP

```

// C++ program to find the minimum removals 
// such that gcd of remaining numbers is more 
// than the initial gcd of N numbers 
#include <bits/stdc++.h> 
using namespace std; 

#define MAXN 100001 

// stores smallest prime factor for every number 
int spf[MAXN]; 

// Calculating SPF (Smallest Prime Factor) for every 
// number till MAXN. 
// Time Complexity : O(nloglogn) 
void sieve() 
{ 
    spf[1] = 1; 
    for (int i = 2; i < MAXN; i++) 

        // marking smallest prime factor for every 
        // number to be itself. 
        spf[i] = i; 

    // separately marking spf for every even 
    // number as 2 
    for (int i = 4; i < MAXN; i += 2) 
        spf[i] = 2; 

    for (int i = 3; i * i < MAXN; i++) { 

        // checking if i is prime 
        if (spf[i] == i) { 

            // marking SPF for all numbers divisible by i 
            for (int j = i * i; j < MAXN; j += i) 

                // marking spf[j] if it is not 
                // previously marked 
                if (spf[j] == j) 
                    spf[j] = i; 
        } 
    } 
} 

// A O(log n) function returning primefactorization 
// by dividing by smallest prime factor at every step 
vector<int> getFactorization(int x) 
{ 
    vector<int> ret; 
    while (x != 1) { 
        ret.push_back(spf[x]); 
        x = x / spf[x]; 
    } 
    return ret; 
} 

// Function which returns the minimal 
// removals required to make gcd 
// greater than previous 
int minimumRemovals(int a[], int n) 
{ 
    int g = 0; 

    // finding initial gcd 
    for (int i = 0; i < n; i++) 
        g = __gcd(a[i], g); 

    unordered_map<int, int> mpp; 

    // divides all number by initial gcd 
    for (int i = 0; i < n; i++) 
        a[i] = a[i] / g; 

    // iterating for all numbers 
    for (int i = 0; i < n; i++) { 

        // primt factorisation to get the prime 
        // factors of i-th element in the array 
        vector<int> p = getFactorization(a[i]); 
        set<int> s; 

        // insert all the prime factors in 
        // set to remove duplicates 
        for (int j = 0; j < p.size(); j++) { 
            s.insert(p[j]); 
        } 

        /// increase the count of prime 
        // factor in map for every element 
        for (auto it = s.begin(); it != s.end(); it++) { 
            int el = *it; 
            mpp[el] += 1; 
        } 
    } 

    int mini = INT_MAX; 
    int mini1 = INT_MAX; 

    // iterate in map and check for every factor 
    // and its count 
    for (auto it = mpp.begin(); it != mpp.end(); it++) { 
        int fir = it->first; 
        int sec = it->second; 

        // check for the largest appearing factor 
        // which does not appears in any one or more 
        if ((n - sec) <= mini) { 
            mini = n - sec; 
        } 
    } 
    if (mini != INT_MAX) 
        return mini; 
    else
        return -1; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 6, 9, 15, 30 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    sieve(); 
    cout << minimumRemovals(a, n); 
    return 0; 
} 

```

## Python3

```py

# Python3 program to find the minimum removals 
# such that gcd of remaining numbers is more 
# than the initial gcd of N numbers 
from math import gcd as __gcd 

MAXN = 100001

# stores smallest prime factor for every number 
spf = [i for i in range(MAXN)] 

# Calculating SPF (Smallest Prime Factor) for every 
# number till MAXN. 
# Time Complexity : O(nloglogn) 
def sieve(): 

    # separately marking spf for every even 
    # number as 2 
    for i in range(4, MAXN, 2): 
        spf[i] = 2

    for i in range(3, MAXN): 

        if i * i > MAXN: 
            break

        # checking if i is prime 
        if (spf[i] == i): 

            # marking SPF for all numbers divisible by i 
            for j in range(2 * i, MAXN, i): 

                # marking spf[j] if it is not 
                # previously marked 
                if (spf[j] == j): 
                    spf[j] = i 

# A O(log n) function returning primefactorization 
# by dividing by smallest prime factor at every step 
def getFactorization(x): 
    ret = [] 
    while (x != 1): 
        ret.append(spf[x]) 
        x = x // spf[x] 
    return ret 

# Function which returns the minimal 
# removals required to make gcd 
# greater than previous 
def minimumRemovals(a, n): 
    g = 0

    # finding initial gcd 
    for i in range(n): 
        g = __gcd(a[i], g) 

    mpp = dict() 

    # divides all number by initial gcd 
    for i in range(n): 
        a[i] = a[i] // g 

    # iterating for all numbers 
    for i in range(n): 

        # primt factorisation to get the prime 
        # factors of i-th element in the array 
        p = getFactorization(a[i]) 
        s = dict() 

        # insert all the prime factors in 
        # set to remove duplicates 
        for j in range(len(p)): 
            s[p[j]] = 1

        # increase the count of prime 
        # factor in map for every element 
        for i in s: 
            mpp[i] = mpp.get(i, 0) + 1

    mini = 10**9
    mini1 = 10**9

    # iterate in map and check for every factor 
    # and its count 
    for i in mpp: 
        fir = i 
        sec = mpp[i] 

        # check for the largest appearing factor 
        # which does not appears in any one or more 
        if ((n - sec) <= mini): 
            mini = n - sec 

    if (mini != 10**9): 
        return mini 
    else: 
        return -1

# Driver code 
a = [6, 9, 15, 30] 
n = len(a) 
sieve() 
print(minimumRemovals(a, n)) 

# This code is contributed by mohit kumar 29 

```

**Output:**

```
2

```

 **时间复杂度**：O（log log N）用于筛分的预先计算，`O(N * log N)`用于计算。

**辅助空间**：`O(n)`



* * *

* * *



