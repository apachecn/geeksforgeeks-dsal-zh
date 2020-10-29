# 从给定的主要因子列表中得出的数的除数

> 原文：[https://www.geeksforgeeks.org/product-of-divisors-of-a-number-from-a-given-list-of-its-prime-factors/](https://www.geeksforgeeks.org/product-of-divisors-of-a-number-from-a-given-list-of-its-prime-factors/)

给定表示给定数字素数列表的数组 **arr []** ，任务是找到该数字除数的乘积。

**注意**：由于产品可以打印得很大，因此答案模版 10 <sup>9</sup> +7。

**示例**：

> **输入**：arr [] = {2，2，3}
> **输出**：1728
> **说明**：
> 因数= 2 * 2 * 3 =12。
> 除数 12 为{1,2,3,4,6,12}。
> 因此，除数的乘积为 1728。
> 
> **输入**：arr [] = {11，11}。
> **输出**：1331

**天真的方法**：

从其主要因子列表生成数字 **N** ，然后以 O（√N）计算复杂度找到其所有除数，并继续计算其乘积。 打印获得的最终产品。

**时间复杂度**：O（N <sup>3/2</sup> ）

**辅助空间**：`O(1)`

**高效方法**：

要解决此问题，需要考虑以下几点：

1.  根据[费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)， **a <sup>（m – 1）</sup> = 1（mod m）**可以进一步扩展为 **a <sup>x</sup> = a <sup>x％（m – 1）</sup>（mod m）**

2.  对于素数 **p** 升至幂 **a** ， **f（p <sup>a</sup> ）= p <sup>（a *（a + 1）/ 2））</sup>** 。

3.  因此， **f（a * b）= f（a）<sup>（d（b））</sup> * f（b）<sup>（d（a））</sup>** ， d（a），d（b）分别表示 a 和 b 中的除数。

请按照以下步骤解决问题：

*   在给定列表中找到每个素数的频率（使用 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) / [Dictionary](https://www.geeksforgeeks.org/python-dictionary/) ）。

*   Using the second observation, for every i <sup>th</sup> prime, calculate: 

    > fp = power（p [i]，（cnt [i] +1）* cnt [i] / 2），其中 cnt [i]表示该素数的频率

*   Using the third observation, update the required product: 

    > ans = power（ans，（cnt [i] + 1））* power（fp，d）％MOD，其中 d 是除以 **（i – 1） <sup>th</sup> 素数的除数**

*   使用费马小定理更新除数 **d** 的数量：

    > d = d *（cnt [i] + 1）％（MOD – 1）

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 

#include <bits/stdc++.h>  
using namespace std; 

int MOD = 1000000007; 

// Function to calculate (a^b)% m 
int power(int a, int b, int m) 
{ 
    a %= m; 
    int res = 1; 
    while (b > 0) { 
        if (b & 1) 
            res = ((res % m) * (a % m)) 
                  % m; 

        a = ((a % m) * (a % m)) % m; 

        b >>= 1; 
    } 

    return res % m; 
} 

// Function to calculate and return 
// the product of divisors 
int productOfDivisors(int p[], int n) 
{ 

    // Stores the frequencies of 
    // prime divisors 
    map<int, int> prime;  

    for (int i = 0; i < n; i++) { 
        prime[p[i]]++; 
    } 
    int product = 1, d = 1; 

    // Iterate over the prime 
    // divisors 
    for (auto itr : prime) { 

        int val 
            = power(itr.first, 
                    (itr.second) * (itr.second + 1) / 2, 
                    MOD); 

        // Update the product 
        product = (power(product, itr.second + 1, MOD) 
                   * power(val, d, MOD)) 
                  % MOD; 

        // Update the count of divisors 
        d = (d * (itr.second + 1)) % (MOD - 1); 
    } 

    return product; 
} 

// Driver Code 
int main() 
{ 

    int arr[] = { 11, 11 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout <<productOfDivisors(arr,n); 

 } 

```

## Java

```java

// Java Program to implement 
// the above approach 
import java.util.*; 
class GFG{ 

static int MOD = 1000000007; 

// Function to calculate (a^b)% m 
static int power(int a, int b, int m) 
{ 
    a %= m; 
    int res = 1; 
    while (b > 0)  
    { 
        if (b % 2 == 1) 
            res = ((res % m) * (a % m)) % m; 

        a = ((a % m) * (a % m)) % m; 

        b >>= 1; 
    } 
    return res % m; 
} 

// Function to calculate and return 
// the product of divisors 
static int productOfDivisors(int p[], int n) 
{ 

    // Stores the frequencies of 
    // prime divisors 
    HashMap<Integer, 
            Integer> prime = new HashMap<Integer, 
                                         Integer>();  

    for (int i = 0; i < n; i++)  
    { 
        if(prime.containsKey(p[i])) 
            prime.put(p[i], prime.get(p[i]) + 1); 
        else
            prime.put(p[i], 1); 

    } 
    int product = 1, d = 1; 

    // Iterate over the prime 
    // divisors 
    for (Map.Entry<Integer, 
                   Integer> itr : prime.entrySet()) 
    { 
        int val = power(itr.getKey(), 
                       (itr.getValue()) * 
                       (itr.getValue() + 1) / 2, MOD); 

        // Update the product 
        product = (power(product, itr.getValue() + 1, MOD) * 
                   power(val, d, MOD)) % MOD; 

        // Update the count of divisors 
        d = (d * (itr.getValue() + 1)) % (MOD - 1); 
    } 
    return product; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int arr[] = { 11, 11 }; 
    int n = arr.length; 

    System.out.println(productOfDivisors(arr,n)); 
} 
} 

// This code is contributed by sapnasingh4991

```

## Python3

```py

# Python3 program to implement  
# the above approach  
from collections import defaultdict 

MOD = 1000000007

# Function to calculate (a^b)% m 
def power(a, b, m): 

    a %= m 
    res = 1

    while (b > 0): 
        if (b & 1): 
            res = ((res % m) * (a % m)) % m 

        a = ((a % m) * (a % m)) % m 
        b >>= 1

    return res % m 

# Function to calculate and return 
# the product of divisors 
def productOfDivisors(p, n): 

    # Stores the frequencies of 
    # prime divisors 
    prime = defaultdict(int) 

    for i in range(n): 
        prime[p[i]] += 1

    product, d = 1, 1

    # Iterate over the prime 
    # divisors 
    for itr in prime.keys(): 
        val = (power(itr, (prime[itr]) * 
                          (prime[itr] + 1) // 2, MOD)) 

        # Update the product 
        product = (power(product, 
                         prime[itr] + 1, MOD) *
                   power(val, d, MOD) % MOD) 

        # Update the count of divisors 
        d = (d * (prime[itr] + 1)) % (MOD - 1) 

    return product 

# Driver Code 
if __name__ == "__main__": 

    arr = [ 11, 11 ] 
    n = len(arr) 

    print(productOfDivisors(arr, n)) 

# This code is contributed by chitranayal 

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

static int MOD = 1000000007;                      

// Function to calculate (a^b)% m 
static int power(int a, int b, int m) 
{ 
    a %= m; 
    int res = 1; 
    while (b > 0)  
    { 
        if (b % 2 == 1) 
            res = ((res % m) * (a % m)) % m; 

        a = ((a % m) * (a % m)) % m; 
        b >>= 1; 
    } 
    return res % m; 
} 

// Function to calculate and return 
// the product of divisors 
static int productOfDivisors(int []p, int n) 
{ 

    // Stores the frequencies of 
    // prime divisors 
    Dictionary<int, 
               int> prime = new Dictionary<int, 
                                           int>();  

    for(int i = 0; i < n; i++)  
    { 
        if(prime.ContainsKey(p[i])) 
            prime[p[i]] = prime[p[i]] + 1; 
        else
            prime.Add(p[i], 1); 
    } 
    int product = 1, d = 1; 

    // Iterate over the prime 
    // divisors 
    foreach(KeyValuePair<int, 
                         int> itr in prime) 
    { 
        int val = power(itr.Key, 
                       (itr.Value) * 
                       (itr.Value + 1) / 2, MOD); 

        // Update the product 
        product = (power(product, itr.Value + 1, MOD) * 
                   power(val, d, MOD)) % MOD; 

        // Update the count of divisors 
        d = (d * (itr.Value + 1)) % (MOD - 1); 
    } 
    return product; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { 11, 11 }; 
    int n = arr.Length; 

    Console.WriteLine(productOfDivisors(arr,n)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:** 

```
1331

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



