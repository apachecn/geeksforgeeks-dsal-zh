# 所有上升到 K 次方的对的绝对差之和

> 原文:[https://www . geesforgeks . org/全对绝对差之和-升幂-k/](https://www.geeksforgeeks.org/sum-of-absolute-difference-of-all-pairs-raised-to-power-k/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个数 **K** ，任务是求给定数组即![\sum_{i=1}^{N} \sum_{j=1}^{N} \ |arr[i]-arr[j]|^K ](img/2df5401c369790fd9b09352a4a4b5eb1.png "Rendered by QuickLaTeX.com")中所有乘方 **K** 对的绝对差之和。
**举例:**

> **输入:** arr[] = {1，2，3}，K = 1
> **输出:** 8
> **解释:**
> 1-1 |+| 1-2 |+| 1-3 |+| 2-1 |+| 2-3 |+| 3-1 |+| 3-2 |+| 3-3 |+| 3-3 | = 8
> **输入:** arr[] = {1，2，3} K = 3
> **输出:** 20
> **说明:**
> 1–1 |<sup>3</sup>+| 1–2 |<sup>3</sup>+| 1–3 |<sup>3</sup>+| 2–1 |<sup>3</sup>+| 2–2 |<sup>3</sup>+| 2–3 |<sup>3</sup>+| 2

**天真的做法:**想法是生成所有可能的对，找到每一对提升到幂的绝对差 **K** 一起求和。
**时间复杂度:***O((log K)* N<sup>2</sup>)*
**辅助空间:** *O(1)*
**高效方法:**我们可以通过下面的计算来提高朴素方法的时间复杂度:
对于所有可能的对，我们必须找到
的值

> ![Sum = \sum_{i=1}^{N} \sum_{j=1}^{N} |arr[i] - arr[j]|^{K} ](img/5c17e7cba1949e4b315ae6250abb0043.png "Rendered by QuickLaTeX.com")

因为对于对(arr[i]，arr[j])，![|arr[i]-arr[j]|^{K} ](img/f87f0341601af9103df140f1466a30e8.png "Rendered by QuickLaTeX.com")的值被计算了两次。所以上面的等式也可以写成:

> ![Sum = 2 * \sum_{i=1}^{N} \sum_{j=1}^{i-1} |arr[i] - arr[j]|^{K} ](img/5138571e71849348c5554f7fb7b7411f.png "Rendered by QuickLaTeX.com")

用二项式公式书写【T0:

> ![Sum = 2 * \sum_{i=1}^{N} \sum_{j=1}^{i-1} \sum_{a=0}^{K} \binom{K}{a}arr[i]^{K}*(-arr[j])^{K - a} ](img/71afaa8124fe50f16a18774e426f1c3c.png "Rendered by QuickLaTeX.com")(等式 1)

让 Pre[i][a] = ![\sum_{j=1}^{i-1}(-arr[j])^{K - a} ](img/08a627d0fd3ffc560364da8354fb8b34.png "Rendered by QuickLaTeX.com")(等式 2)
从等式 1 和等式 2，我们得到

> ![Sum = 2 * \sum_{i=1}^{N} \sum_{a=0}^{K} \binom{K}{a}Pre[i][a]*arr[i]^{K} ](img/c0cc38a45e98b71194aeece535ba909b.png "Rendered by QuickLaTeX.com")

**Pre[i][a]** 的值可以计算为:

> pre[I][a]= {(-arr[1])<sup>K–a</sup>+(-arr[2])<sup>K–a</sup>…。。+(-arr[I–1])<sup>K–a</sup>}。
> 所以，Pre[I+1][a]= Pre[I][a]+(-arr[I])<sup>K–a</sup>

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define ll long long
using namespace std;

class Solution {

public:
    // Since K can be 100 max
    ll ncr[101][101];
    int n, k;
    vector<ll> A;

    // Constructor
    Solution(int N, int K, vector<ll> B)
    {
        // Initializing with -1
        memset(ncr, -1, sizeof(ncr));

        n = N;
        k = K;
        A = B;

        // Making vector A as 1-Indexing
        A.insert(A.begin(), 0);
    }

    ll f(int N, int K);

    ll pairsPower();
};

// To Calculate the value nCk
ll Solution::f(int n, int k)
{
    if (k == 0)
        return 1LL;

    if (n == k)
        return 1LL;

    if (n < k)
        return 0;

    if (ncr[n][k] != -1)
        return ncr[n][k];

    // Since nCj = (n-1)Cj + (n-1)C(j-1);
    return ncr[n][k] = f(n - 1, k)
                       + f(n - 1, k - 1);
}

// Function that summation of absolute
// differences of all pairs raised
// to the power k
ll Solution::pairsPower()
{
    ll pre[n + 1][k + 1];
    ll ans = 0;

    // Sort the given array
    sort(A.begin() + 1, A.end());

    // Precomputation part, O(n*k)
    for (int i = 1; i <= n; ++i) {
        pre[i][0] = 1LL;

        for (int j = 1; j <= k; j++) {
            pre[i][j] = A[i]
                        * pre[i][j - 1];
        }

        if (i != 1) {
            for (int j = 0; j <= k; ++j)
                pre[i][j] = pre[i][j]
                            + pre[i - 1][j];
        }
    }

    // Traverse the array arr[]
    for (int i = n; i >= 2; --i) {

        // For each K
        for (int j = 0; j <= k; j++) {

            ll val = f(k, j);

            ll val1 = pow(A[i], k - j)
                      * pre[i - 1][j];

            val = val * val1;

            if (j % 2 == 0)
                ans = (ans + val);

            else
                ans = (ans - val);
        }
    }

    ans = 2LL * ans;

    // Return the final answer
    return ans;
}

// Driver Code
int main()
{
    // Given N and K
    int N = 3;
    int K = 3;

    // Given array
    vector<ll> arr = { 1, 2, 3 };

    // Creation of Object of class
    Solution obj(N, K, arr);

    // Function Call
    cout << obj.pairsPower() << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
class Solution:

    def __init__(self, N, K, B):

        self.ncr = []

        # Since K can be 100 max
        for i in range(101):
            temp = []
            for j in range(101):

                # Initializing with -1
                temp.append(-1)

            self.ncr.append(temp)

        self.n = N
        self.k = K

        # Making vector A as 1-Indexing
        self.A = [0] + B

    # To Calculate the value nCk
    def f(self, n, k):

        if k == 0:
            return 1
        if n == k:
            return 1
        if n < k:
            return 0

        if self.ncr[n][k] != -1:
            return self.ncr[n][k]

        # Since nCj = (n-1)Cj + (n-1)C(j-1);
        self.ncr[n][k] = (self.f(n - 1, k) +
                          self.f(n - 1, k - 1))

        return self.ncr[n][k]

    # Function that summation of absolute
    # differences of all pairs raised
    # to the power k
    def pairsPower(self):

        pre = []

        for i in range(self.n + 1):
            temp = []
            for j in range(self.k + 1):
                temp.append(0)

            pre.append(temp)

        ans = 0

        # Sort the given array
        self.A.sort()

        # Precomputation part, O(n*k)
        for i in range(1, self.n + 1):
            pre[i][0] = 1

            for j in range(1, self.k + 1):
                pre[i][j] = (self.A[i] *
                                pre[i][j - 1])

            if i != 1:
                for j in range(self.k + 1):
                    pre[i][j] = (pre[i][j] +
                                 pre[i - 1][j])

        # Traverse the array arr[]
        for i in range(self.n, 1, -1):

            # For each K
            for j in range(self.k + 1):
                val = self.f(self.k, j)
                val1 = (pow(self.A[i],
                            self.k - j) *
                             pre[i - 1][j])

                val = val * val1

                if j % 2 == 0:
                    ans = ans + val
                else:
                    ans = ans - val

        ans = 2 * ans

        # Return the final answer
        return ans

# Driver code
if __name__ == '__main__':

    # Given N and K
    N = 3
    K = 3

    # Given array
    arr = [ 1, 2, 3 ]

    # Creation of object of class
    obj = Solution(N, K, arr)

    # Function call
    print(obj.pairsPower())

# This code is contributed by Shivam Singh
```

**Output:** 

```
20
```

**时间复杂度:***O(N * K)*
T5】辅助空间: *O(N*K)*