# 选择 X 轴上 K 条相交线段的方式数

> 原文:[https://www . geesforgeks . org/x 轴上选择 k 相交线段的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-choose-k-intersecting-line-segments-on-x-axis/)

给定 x 轴上线段的**数组 arr【】**和**整数 K** ，任务是计算选择 **K** 线段的方法数，使得它们在任意点相交。因为答案可能很大，所以将其打印为模 10^9+7.

**示例:**

> **输入:** arr[] = [[1，3]，[4，5]，[5，7]]，K = 2
> **输出:** 2
> **说明:**
> 第一种方式选择[1，3]，[4，5]，第二种方式是[1，3]，[5，7]。由于[4，5]，[5，7]的交集不为零，因此不能包含在答案中。
> 
> **输入:** [[3，7]，[1，4]，[6，9]，[8，13]，[9，11]]，K = 1
> **输出:** 0
> **解释:**
> 既然我们只找单个线段，但是对于每个单个线段交集总是非空的。

**方法:**
为了解决上面提到的问题，我们将尝试找出奇数个案例意味着那些交集非空的案例。所以很明显，我们的答案将是**总案例–特例。**
要计算病例总数，请遵循以下方法:

*   所有可能的情况是**“n 选择 k”或<sup>n</sup>C<sub>k</sub>T5】**
*   我们预先计算所需数字的倒数和阶乘来计算**<sup>n</sup>C<sub>k</sub>T5】**
*   在 O(1)时间内
*   k 线线段相交好像最小(R1，R2，..，R{k-1}) >= Li 其中线段[Li，Ri]正在考虑中。维持多集，维持秩序。首先，按照李的升序对线段进行排序。如果李是一样的，那么 Ri 小的段第一。

对于每一个线段[Li，Ri]，遵循下面的方法来寻找奇数情况的数量。

*   当多集不为空，且线不相交时，从多集中删除 Ri 最小的线，并再次检查。
*   使用此段位[Li，Ri]的违规方式数为 **<sup>p</sup> C <sub>k-1</sub>**
*   其中 p = size_of_multiset。
*   在多集合中插入该线段的端点。

下面是上述方法的实现:

## C++

```
// C++ program to find Number of ways
// to choose K intersecting
// line segments on X-axis

#include <bits/stdc++.h>
using namespace std;

const long long mod = 1000000007;
const int MAXN = 1001;
long long factorial[MAXN], inverse[MAXN];

// Function to find (a^b)%mod in log b
long long power(long long a, long long b)
{
    long long res = 1;

    // Till power becomes 0
    while (b > 0) {

        // If power is odd
        if (b % 2 == 1) {
            res = (res * a) % mod;
        }
        // Multiply base
        a = (a * a) % mod;

        // Divide power by 1
        b >>= 1;
    }

    return res;
}

// Function to find nCk
long long nCk(int n, int k)
{
    // Base case
    if (k < 0 || k > n) {
        return 0;
    }

    // Apply formula to find nCk
    long long ans = factorial[n];
    ans = (ans * inverse[n - k]) % mod;
    ans = (ans * inverse[k]) % mod;

    return ans;
}

// Function to find the number of ways
void numberOfWays(vector<pair<int, int> > lines, int K,
                  int N)
{

    // sort the given lines
    sort(lines.begin(), lines.end());

    // Find the number of total case
    long long total_case = nCk(N, K);

    // Declare a multiset
    multiset<int> m;

    // loop till N
    for (int i = 0; i < N; i++)
    {

        // Check if smallest element is
        // smaller than lines[i]
        while (!m.empty()
               && (*m.begin() < lines[i].first)) {

            // Erase first element
            m.erase(m.begin());
        }
        // Exclude the odd cases
        total_case -= nCk(m.size(), K - 1);

        // Modulus operation
        total_case += mod;
        total_case %= mod;

        // Insert into multiset
        m.insert(lines[i].second);
    }

    cout << total_case << endl;
}

// Function to precompute
// factorial and inverse
void preCompute()
{
    long long fact = 1;

    factorial[0] = 1;
    inverse[0] = 1;

    // Pre-compute factorial and inverse
    for (int i = 1; i < MAXN; i++) {

        fact = (fact * i) % mod;
        factorial[i] = fact;
        inverse[i] = power(factorial[i], mod - 2);
    }
}

// Driver code
int main()
{

    int N = 3, K = 2;
    vector<pair<int, int> > lines;

    // Function to pre-compute
    // factorial and inverse
    preCompute();

    lines.push_back({ 1, 3 });
    lines.push_back({ 4, 5 });
    lines.push_back({ 5, 7 });

    numberOfWays(lines, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Number of ways
// to choose K intersecting line
// segments on X-axis
import java.util.*;
import java.lang.*;

class GFG {

    static long mod = 1000000007;
    static int MAXN = 1001;
    static long factorial[] = new long[MAXN],
                inverse[] = new long[MAXN];

    // Function to find (a^b)%mod in log b
    static long power(long a, long b)
    {
        long res = 1;

        // Till power becomes 0
        while (b > 0) {

            // If power is odd
            if (b % 2 == 1) {
                res = (res * a) % mod;
            }

            // Multiply base
            a = (a * a) % mod;

            // Divide power by 1
            b >>= 1;
        }
        return res;
    }

    // Function to find nCk
    static long nCk(int n, int k)
    {

        // Base case
        if (k < 0 || k > n) {
            return 0;
        }

        // Apply formula to find nCk
        long ans = factorial[n];
        ans = (ans * inverse[n - k]) % mod;
        ans = (ans * inverse[k]) % mod;

        return ans;
    }

    // Function to find the number of ways
    static void numberOfWays(ArrayList<int[]> lines, int K,
                             int N)
    {

        // sort the given lines
        Collections.sort(lines, (a, b) -> a[0] - b[0]);

        // Find the number of total case
        long total_case = nCk(N, K);

        // Declare a multiset
        PriorityQueue<Integer> m = new PriorityQueue<>();

        // Loop till N
        for (int i = 0; i < N; i++) {

            // Check if smallest element is
            // smaller than lines[i]
            while (!m.isEmpty()
                   && (m.peek() < lines.get(i)[0])) {

                // Erase first element
                m.poll();
            }

            // Exclude the odd cases
            total_case -= nCk(m.size(), K - 1);

            // Modulus operation
            total_case += mod;
            total_case %= mod;

            // Insert into multiset
            m.add(lines.get(i)[1]);
        }
        System.out.println(total_case);
    }

    // Function to precompute
    // factorial and inverse
    static void preCompute()
    {
        long fact = 1;

        factorial[0] = 1;
        inverse[0] = 1;

        // Pre-compute factorial and inverse
        for (int i = 1; i < MAXN; i++) {
            fact = (fact * i) % mod;
            factorial[i] = fact;

            inverse[i] = power(factorial[i], mod - 2);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 3, K = 2;
        ArrayList<int[]> lines = new ArrayList<>();

        // Function to pre-compute
        // factorial and inverse
        preCompute();

        lines.add(new int[] { 1, 3 });
        lines.add(new int[] { 4, 5 });
        lines.add(new int[] { 5, 7 });

        numberOfWays(lines, K, N);
    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find Number of ways
# to choose K ersecting
# line segments on X-axis

import heapq as hq

mod = 1000000007
MAXN = 1001
factorial=[1]*MAXN; inverse=[1]*MAXN

# Function to find (a^b)%mod in log b
def power(a, b):
    res = 1

    # Till power becomes 0
    while (b > 0) :

        # If power is odd
        if (b % 2 == 1) :
            res = (res * a) % mod

        # Multiply base
        a = (a * a) % mod

        # Divide power by 1
        b >>= 1

    return res

# Function to find nCk
def nCk(n, k):
    # Base case
    if (k < 0 or k > n) :
        return 0

    # Apply formula to find nCk
    ans = factorial[n]
    ans = (ans * inverse[n - k]) % mod
    ans = (ans * inverse[k]) % mod

    return ans

# Function to find the number of ways
def numberOfWays(lines, K, N):

    # sort the given lines
    lines.sort()

    # Find the number of total case
    total_case = nCk(N, K)

    # Declare a heap
    m=[]

    # loop till N
    for i in range(N):

        # Check if smallest element is
        # smaller than lines[i]
        while (m and m[0] < lines[i][0]):

            # Erase first element
            hq.heappop(m)

        # Exclude the odd cases
        total_case -= nCk(len(m), K - 1)

        # Modulus operation
        total_case += mod
        total_case %= mod

        # Insert into heap
        hq.heappush(m,lines[i][1])

    print(total_case)

# Function to precompute
# factorial and inverse
def preCompute():
    global factorial
    fact = 1

    factorial[0] = 1
    inverse[0] = 1

    # Pre-compute factorial and inverse
    for i in range(1,MAXN) :

        fact = (fact * i) % mod
        factorial[i] = fact
        inverse[i] = power(factorial[i], mod - 2)

# Driver code
if __name__ == '__main__':

    N = 3; K = 2
    lines=[]

    # Function to pre-compute
    # factorial and inverse
    preCompute()

    lines.append((1, 3))
    lines.append((4, 5))
    lines.append((5, 7))

    numberOfWays(lines, K, N)
```

**Output**

```
2
```

**时间复杂度:** O(MAXN * log(MAXN) + N * log(N))。
**辅助空间:** O(MAXN + N)。