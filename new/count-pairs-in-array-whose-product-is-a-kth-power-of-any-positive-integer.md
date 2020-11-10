# 数组中的乘积对，乘积为任何正整数的`K`次幂

> 原文：[https://www.geeksforgeeks.org/count-pairs-in-array-whose-product-is-a-kth-power-of-any-positive-integer/](https://www.geeksforgeeks.org/count-pairs-in-array-whose-product-is-a-kth-power-of-any-positive-integer/)

给定长度为`N`的数组`arr[]`和整数`K`，任务是数组中的对进行计数，乘积为正整数的`K`次幂，即：

> 对于任何正整数`Z`，`A[i] * A[j] = Z ^ K`。

**示例**：

> **输入**：`arr[] = {1, 3, 9, 8, 24, 1}, K = 3`
>
> **输出**：5
>
> **说明**：
>
> 有 5 对，可以表示为`Z ^ 3`：
>
> ```
> A[0] * A[3] = 1 * 8  = 2 ^ 3
> A[0] * A[5] = 1 * 1  = 1 ^ 3
> A[1] * A[2] = 3 * 9  = 3 ^ 3
> A[2] * A[4] = 9 * 24 = 6 ^ 3
> A[3] * A[5] = 8 * 1  = 2 ^ 3
> ```
>
> **输入**：`arr[] = {7, 4, 10, 9, 2, 8, 8, 7, 3, 7}, K = 2`
>
> **输出**：7
>
> **说明**：
>
> 共有 7 对，可以表示为`Z ^ 2`。

**方法**：该问题的关键观察在于以`Z ^ K`的形式表示任何数字，然后该数字的素因式分解的幂必须是`K`的倍数。下面是步骤：

*   Compute the prime factorization of each number of the array and store the prime factors in the form of key-value pair in a hash-map, where the key will be a prime factor of that element and value will be the power raised to that prime factor modulus K, in the prime factorization of that number.

    **For Example:**

    ```
    Given Element be - 360 and K = 2
    Prime Factorization = 23 * 32 * 51

    Key-value pairs for this would be,
    => {(2, 3 % 2), (3, 2 % 2),
        (5, 1 % 2)}
    => {(2, 1), (5, 1)}

    // Notice that prime number 3 
    // is ignored because of the 
    // modulus value was 0

    ```

*   遍历数组并创建一个频率哈希映射，其中键-值对的定义如下：

    ```
    Key: Prime Factors pairs mod K
    Value: Frequency of this Key

    ```

*   Finally, Traverse for each element of the array and check required prime factors are present in hash-map or not. If yes, then there will be **F** number of possible pairs, where F is the frequency.

    **示例**：

    ```
    Given Number be - 360, K = 3
    Prime Factorization -
    => {(3, 2), (5, 1)}

    Required Prime Factors -
    => {(p1, K - val1), ...(pn, K - valn)}
    => {(3, 3 - 2), (5, 3 - 1)}
    => {(3, 1), (5, 2)}  

    ```

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to count the 
// pairs whose product is Kth 
// power of some integer Z 

#include <bits/stdc++.h> 

#define MAXN 100005 

using namespace std; 

// Smallest prime factor 
int spf[MAXN]; 

// Sieve of eratosthenes 
// for computing primes 
void sieve() 
{ 
    int i, j; 
    spf[1] = 1; 
    for (i = 2; i < MAXN; i++) 
        spf[i] = i; 

    // Loop for markig the factors 
    // of prime number as non-prime 
    for (i = 2; i < MAXN; i++) { 
        if (spf[i] == i) { 
            for (j = i * 2; 
                 j < MAXN; j += i) { 
                if (spf[j] == j) 
                    spf[j] = i; 
            } 
        } 
    } 
} 

// Function to factorize the 
// number N into its prime factors 
vector<pair<int, int> > getFact(int x) 
{ 
    // Prime factors along with powers 
    vector<pair<int, int> > factors; 

    // Loop while the X is not 
    // equal to 1 
    while (x != 1) { 

        // Smallest prime 
        // factor of x 
        int z = spf[x]; 
        int cnt = 0; 
        // Count power of this 
        // prime factor in x 
        while (x % z == 0) 
            cnt++, x /= z; 

        factors.push_back( 
            make_pair(z, cnt)); 
    } 
    return factors; 
} 

// Function to count the pairs 
int pairsWithKth(int a[], int n, int k) 
{ 

    // Precomputation 
    // for factorisation 
    sieve(); 

    int answer = 0; 

    // Data structure for storing 
    // list L for each element along 
    // with frequency of occurence 
    map<vector<pair<int, 
                    int> >, 
        int> 
        count_of_L; 

    // Loop to iterate over the 
    // elements of the array 
    for (int i = 0; i < n; i++) { 

        // Factorise each element 
        vector<pair<int, int> > 
            factors = getFact(a[i]); 
        sort(factors.begin(), 
             factors.end()); 

        vector<pair<int, int> > L; 

        // Loop to iterate over the 
        // factors of the element 
        for (auto it : factors) { 
            if (it.second % k == 0) 
                continue; 
            L.push_back( 
                make_pair( 
                    it.first, 
                    it.second % k)); 
        } 

        vector<pair<int, int> > Lx; 

        // Loop to find the required prime 
        // factors for each element of array 
        for (auto it : L) { 

            // Represents how much remainder 
            // power needs to be added to 
            // this primes power so as to make 
            // it a multiple of k 
            Lx.push_back( 
                make_pair( 
                    it.first, 
                    (k - it.second + k) % k)); 
        } 

        // Add occurences of 
        // Lx till now to answer 
        answer += count_of_L[Lx]; 

        // Increment the counter for L 
        count_of_L[L]++; 
    } 

    return answer; 
} 

// Driver Code 
int main() 
{ 
    int n = 6; 
    int a[n] = { 1, 3, 9, 8, 24, 1 }; 
    int k = 3; 

    cout << pairsWithKth(a, n, k); 
    return 0; 
} 

```

**输出**：

```
5

```

**时间复杂度**：`O(N log N)`



* * *

* * *



