# 给定数组所有子集的立方之和

> 原文:[https://www . geesforgeks . org/给定数组所有子集的立方之和/](https://www.geeksforgeeks.org/sum-of-cubes-of-all-subsets-of-given-array/)

给定一个数组 **arr[]** ，任务是计算给定数组所有可能的非空子集的立方之和。既然，答案可以是大的，打印值为 **mod** 1000000007。

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** 18
> 子集({1}) = 1 <sup>3</sup> = 1
> 子 tval({2}) = 2 <sup>3</sup> = 8
> 子集({1，2 })= 1<sup>3</sup>+2<sup>3</sup>= 1+8 = 9
> 所有子集的立方体之和= 1+1
> 
> **输入:** arr[] = {1，1，1 }
> T3】输出: 12

**天真的方法:**一个简单的方法是[找到所有的子集](https://www.geeksforgeeks.org/find-distinct-subsets-given-set/)，然后对该子集中的每个元素进行立方，并将其添加到结果中。这种方法的时间复杂度将是 **O(2 <sup>N</sup> )**

**高效方法:**

*   可以观察到，原始数组的每个元素在所有子集中出现 2<sup>(N–1)</sup>次。
*   因此最终答案中任何元素**arr<sub>I</sub>T4】的贡献都将是

    ```
    arri * 2(N – 1)
    ```** 
*   所以，所有子集的立方之和将是

    ```
    [arr03 + arr13 + arr23 + … + arr(N-1)3] * 2(N – 1)

    ```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;

// Function to return (2^P % mod)
long long power(int p)
{
    long long res = 1;
    for (int i = 1; i <= p; ++i) {
        res *= 2;
        res %= mod;
    }
    return res % mod;
}

// Function to return
// the sum of cubes of subsets
long long subset_cube_sum(vector<int>& A)
{

    int n = (int)A.size();

    long long ans = 0;

    // cubing the elements
    // and adding it to ans
    for (int i : A) {
        ans += (1LL * i * i * i) % mod;
        ans %= mod;
    }

    return (1LL * ans * power(n - 1))
           % mod;
}

// Driver code
int main()
{
    vector<int> A = { 1, 2 };

    cout << subset_cube_sum(A);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach 
mod = int(1e9) + 7; 

# Function to return (2^P % mod) 
def power(p) :

    res = 1; 
    for i in range(1, p + 1) :
        res *= 2; 
        res %= mod; 

    return res % mod; 

# Function to return 
# the sum of cubes of subsets 
def subset_cube_sum(A) : 

    n = len(A); 

    ans = 0; 

    # cubing the elements 
    # and adding it to ans 
    for i in A :
        ans += (i * i * i) % mod; 
        ans %= mod; 

    return (ans * power(n - 1)) % mod; 

# Driver code 
if __name__ == "__main__" : 

    A = [ 1, 2 ]; 

    print(subset_cube_sum(A)); 

# This code is contributed by Yash_R
```

**Output:**

```
18

```

**时间复杂度:** O(N)