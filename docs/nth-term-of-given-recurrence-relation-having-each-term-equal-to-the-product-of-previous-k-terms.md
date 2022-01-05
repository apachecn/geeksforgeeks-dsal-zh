# 给定递推关系的第 n 项，每项等于前 K 项的乘积

> 原文:[https://www . geeksforgeeks . org/第 n 个给定递归关系项，每个项等于前 k 个项的乘积/](https://www.geeksforgeeks.org/nth-term-of-given-recurrence-relation-having-each-term-equal-to-the-product-of-previous-k-terms/)

给定两个正整数 **N** 和 **K** 以及一个由 **K** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**F【】**。递归关系的第**N**项由下式给出:

> **F<sub>N</sub>= F<sub>N–1</sub>* F<sub>N–2</sub>* F<sub>N–3</sub>*……。* F<sub>N–K</sub>**

任务是找到给定递归关系的第 **N <sup>个</sup>项**。由于第 N <sup>个</sup>术语可能非常大，打印第 N**个<sup>个</sup>个**术语模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** N = 5，K = 2，F = {1，2}
> **输出:** 32
> **解释:**
> 以上输入的顺序为 1，2，2，4，8， **32** ，256，…。
> 每个术语都是其前两个术语的乘积。
> 因此第 N<sup>项为 32。</sup>
> 
> **输入:** N = 5，K = 3，F = {1，2，3}
> **输出:** 648
> **解释:**
> 以上输入的顺序为:1，2，3，6，36， **648** ，139968，…。
> 每个术语都是其前三个术语的产物。
> 因此第 N<sup>项为 648。</sup>

**天真方法:**想法是使用递归关系生成给定序列的所有 **N 项**，并打印作为所需答案获得的 **N <sup>第</sup>项**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define int long long int
using namespace std;

int mod = 1e9 + 7;

// Function to find the nth term
void NthTerm(int F[], int K, int N)
{
    // Stores the terms of
    // recurrence relation
    int ans[N + 1] = { 0 };

    // Initialize first K terms
    for (int i = 0; i < K; i++)
        ans[i] = F[i];

    // Find all terms from Kth term
    // to the Nth term
    for (int i = K; i <= N; i++) {

        ans[i] = 1;

        for (int j = i - K; j < i; j++) {

            // Current term is product of
            // previous K terms
            ans[i] *= ans[j];
            ans[i] %= mod;
        }
    }

    // Print the Nth term
    cout << ans[N] << endl;
}

// Driver Code
int32_t main()
{
    // Given N, K and F[]
    int F[] = { 1, 2 };
    int K = 2;
    int N = 5;

    // Function Call
    NthTerm(F, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static int mod = (int)(1e9 + 7);

// Function to find the nth term
static void NthTerm(int F[], int K, int N)
{

    // Stores the terms of
    // recurrence relation
    int ans[] = new int[N + 1];

    // Initialize first K terms
    for(int i = 0; i < K; i++)
        ans[i] = F[i];

    // Find all terms from Kth term
    // to the Nth term
    for(int i = K; i <= N; i++)
    {
        ans[i] = 1;

        for(int j = i - K; j < i; j++)
        {

            // Current term is product of
            // previous K terms
            ans[i] *= ans[j];
            ans[i] %= mod;
        }
    }

    // Print the Nth term
    System.out.print(ans[N] + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given N, K and F[]
    int F[] = { 1, 2 };
    int K = 2;
    int N = 5;

    // Function call
    NthTerm(F, K, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
mod = 1e9 + 7

# Function to find the nth term
def NthTerm(F, K, N):

    # Stores the terms of
    # recurrence relation
    ans = [0] * (N + 1)

    # Initialize first K terms
    for i in range(K):
        ans[i] = F[i]

    # Find all terms from Kth term
    # to the Nth term
    for i in range(K, N + 1):
        ans[i] = 1

        for j in range(i - K, i):

            # Current term is product of
            # previous K terms
            ans[i] *= ans[j]
            ans[i] %= mod

    # Print the Nth term
    print(ans[N])

# Driver Code
if __name__ == '__main__':

    # Given N, K and F[]
    F = [1, 2]
    K = 2
    N = 5

    # Function Call
    NthTerm(F, K, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

static int mod = (int)(1e9 + 7);

// Function to find the
// nth term
static void NthTerm(int []F,
                    int K, int N)
{
  // Stores the terms of
  // recurrence relation
  int []ans = new int[N + 1];

  // Initialize first K terms
  for(int i = 0; i < K; i++)
    ans[i] = F[i];

  // Find all terms from Kth
  // term to the Nth term
  for(int i = K; i <= N; i++)
  {
    ans[i] = 1;

    for(int j = i - K; j < i; j++)
    {
      // Current term is product of
      // previous K terms
      ans[i] *= ans[j];
      ans[i] %= mod;
    }
  }

  // Print the Nth term
  Console.Write(ans[N] + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Given N, K and F[]
  int []F = {1, 2};
  int K = 2;
  int N = 5;

  // Function call
  NthTerm(F, K, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

let mod = 1e9 + 7;

// Function to find the nth term
function NthTerm(F, K, N)
{
    // Stores the terms of
    // recurrence relation
    let ans = new Uint8Array(N + 1);

    // Initialize first K terms
    for (let i = 0; i < K; i++)
        ans[i] = F[i];

    // Find all terms from Kth term
    // to the Nth term
    for (let i = K; i <= N; i++) {

        ans[i] = 1;

        for (let j = i - K; j < i; j++) {

            // Current term is product of
            // previous K terms
            ans[i] *= ans[j];
            ans[i] %= mod;
        }
    }

    // Print the Nth term
    document.write(ans[N] + "<br>");
}

// Driver Code

    // Given N, K and F[]
    let F = [ 1, 2 ];
    let K = 2;
    let N = 5;

    // Function Call
    NthTerm(F, K, N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output**

```
32
```

***时间复杂度:** O(N*K)*
***辅助空间:** O(N)*

**高效方法:**想法是使用[德格数据结构](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)使用最后一个 **K** 术语查找下一个术语。以下是步骤:

*   初始化一个空的 deque 说 **dq** 。
*   计算第一个 **K** 项的乘积，由于它等于循环关系的第 **(K + 1)** <sup>项，将其插入到 **dq** 的末尾。</sup>
*   迭代范围**【K+2，N】**，并遵循以下步骤:
    *   让**得克**的最后一个元素为 **L** ，得克的前一个元素为 **F** 。
    *   现在，使用第= (L * L) / F 项的公式计算第 项的**。**
    *   因为 **L** 是从**(I–1–K)到(I–2)**元素的乘积。因此，要找到 **i <sup>第</sup>** 项，选择**(I–K)**到**(I–1)**的元素乘积，将**(I–1)<sup>第</sup>** 项(即 **L** )乘以**(I–1–K)到(I–2)**的元素乘积，即可得到产品
    *   现在，将本产品 **(L * L)** 除以**(I–1–K)<sup>第</sup>个**项，在本例中为 **F** 。
    *   现在，将**I<sup>th</sup>T3【术语】插入到德格的后面。**
    *   从桌子前面弹出一个元素。
*   完成以上步骤后，打印**德清**的最后一个元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define int long long int
using namespace std;
int mod = 1e9 + 7;

// Function to calculate (x ^ y) % p
// fast exponentiation ( O(log y)
int power(int x, int y, int p)
{
    // Store the result
    int res = 1;
    x = x % p;

    // Till y is greater than 0
    while (y > 0) {

        // If y is odd
        if (y & 1)
            res = (res * x) % p;

        // Right shift by 1
        y = y >> 1;
        x = (x * x) % p;
    }

    // Print the resultant value
    return res;
}

// Function to find mod inverse
int modInverse(int n, int p)
{
    // Using Fermat Little Theorem
    return power(n, p - 2, p);
}

// Function to find Nth term of the
// given recurrence relation
void NthTerm(int F[], int K, int N)
{
    // Doubly ended queue
    deque<int> q;

    // Stores the product of 1st K terms
    int product = 1;

    for (int i = 0; i < K; i++) {

        product *= F[i];
        product %= mod;
        q.push_back(F[i]);
    }

    // Push (K + 1)th term to Dequeue
    q.push_back(product);

    for (int i = K + 1; i <= N; i++) {

        // First and the last element
        // of the dequeue
        int f = *q.begin();
        int e = *q.rbegin();

        // Calculating the ith term
        int next_term
            = ((e % mod * e % mod) % mod
               * (modInverse(f, mod)))
              % mod;
        // Add current term to end
        // of Dequeue
        q.push_back(next_term);

        // Remove the first number
        // from dequeue
        q.pop_front();
    }

    // Print the Nth term
    cout << *q.rbegin() << endl;
}

// Driver Code
int32_t main()
{
    // Given N, K and F[]
    int F[] = { 1, 2 };
    int K = 2;
    int N = 5;

    // Function Call
    NthTerm(F, K, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static long mod = 1000000007;

// Function to calculate
// (x ^ y) % p fast
// exponentiation ( O(log y)
static long power(long x,
                  long y, long p)
{
  // Store the result
  long res = 1;
  x = x % p;

  // Till y is
  // greater than 0
  while (y > 0)
  {
    // If y is odd
    if (y % 2 == 1)
      res = (res * x) % p;

    // Right shift by 1
    y = y >> 1;
    x = (x * x) % p;
  }

  // Print the resultant value
  return res;
}

// Function to find mod
// inverse
static long modInverse(long n,
                       long p)
{
  // Using Fermat Little Theorem
  return power(n, p - 2, p);
}

// Function to find Nth term
// of the given recurrence
// relation
static void NthTerm(long F[],
                    long K, long N)
{
  // Doubly ended queue
  Vector<Long> q = new Vector<>();

  // Stores the product of 1st K terms
  long product = 1;

  for (int i = 0; i < K; i++)
  {
    product *= F[i];
    product %= mod;
    q.add(F[i]);
  }

  // Push (K + 1)th
  // term to Dequeue
  q.add(product);

  for (long i = K + 1; i <= N; i++)
  {
    // First and the last element
    // of the dequeue
    long f = q.get(0);
    long e = q.get(q.size() - 1);

    // Calculating the ith term
    long next_term = ((e % mod * e % mod) % mod *
                      (modInverse(f, mod))) % mod;

    // Add current term to end
    // of Dequeue
    q.add(next_term);

    // Remove the first number
    // from dequeue
    q.remove(0);
  }

  // Print the Nth term
  System.out.print(q.get(q.size() - 1) + "\n");
}

// Driver Code
public static void main(String[] args)
{
  // Given N, K and F[]
  long F[] = {1, 2};
  long K = 2;
  long N = 5;

  // Function Call
  NthTerm(F, K, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
mod = 1000000007

# Function to calculate
# (x ^ y) % p fast
# exponentiation ( O(log y)
def power(x, y, p):

    # Store the result
    res = 1
    x = x % p

    # Till y is
    # greater than 0
    while (y > 0):

        # If y is odd
        if (y % 2 == 1):
            res = (res * x) % p

        # Right shift by 1
        y = y >> 1
        x = (x * x) % p

    # Print the resultant value
    return res

# Function to find mod
# inverse
def modInverse(n, p):

    # Using Fermat Little Theorem
    return power(n, p - 2, p);

# Function to find Nth term
# of the given recurrence
# relation
def NthTerm(F, K, N):

    # Doubly ended queue
    q = []

    # Stores the product of
    # 1st K terms
    product = 1

    for i in range(K):
        product *= F[i]
        product %= mod
        q.append(F[i])

    # Push (K + 1)th
    # term to Dequeue
    q.append(product)

    for i in range(K + 1, N + 1):

        # First and the last element
        # of the dequeue
        f = q[0]
        e = q[len(q) - 1]

        # Calculating the ith term
        next_term = ((e % mod * e % mod) %
             mod * (modInverse(f, mod))) % mod

        # Add current term to end
        # of Dequeue
        q.append(next_term)

        # Remove the first number
        # from dequeue
        q.remove(q[0])

    # Print the Nth term
    print(q[len(q) - 1], end = "")

# Driver Code
if __name__ == '__main__':

    # Given N, K and F
    F = [1, 2]
    K = 2
    N = 5

    # Function Call
    NthTerm(F, K, N)

# This code is contributed by Princi Singh
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG{

static long mod = 1000000007;

// Function to calculate
// (x ^ y) % p fast
// exponentiation ( O(log y)
static long power(long x, long y,
                  long p)
{

  // Store the result
  long res = 1;
  x = x % p;

  // Till y is
  // greater than 0
  while (y > 0)
  {

    // If y is odd
    if (y % 2 == 1)
      res = (res * x) % p;

    // Right shift by 1
    y = y >> 1;
    x = (x * x) % p;
  }

  // Print the resultant value
  return res;
}

// Function to find mod
// inverse
static long modInverse(long n,
                       long p)
{

  // Using Fermat Little Theorem
  return power(n, p - 2, p);
}

// Function to find Nth term
// of the given recurrence
// relation
static void NthTerm(long []F,
                    long K, long N)
{

  // Doubly ended queue
  List<long> q = new List<long>();

  // Stores the product of 1st K terms
  long product = 1;

  for(int i = 0; i < K; i++)
  {
    product *= F[i];
    product %= mod;
    q.Add(F[i]);
  }

  // Push (K + 1)th
  // term to Dequeue
  q.Add(product);

  for(long i = K + 1; i <= N; i++)
  {

    // First and the last element
    // of the dequeue
    long f = q[0];
    long e = q[q.Count - 1];

    // Calculating the ith term
    long next_term = ((e % mod * e % mod) % mod *
                    (modInverse(f, mod))) % mod;

    // Add current term to end
    // of Dequeue
    q.Add(next_term);

    // Remove the first number
    // from dequeue
    q.RemoveAt(0);
  }

  // Print the Nth term
  Console.Write(q[q.Count - 1] + "\n");
}

// Driver Code
public static void Main(String[] args)
{

  // Given N, K and F[]
  long []F = {1, 2};
  long K = 2;
  long N = 5;

  // Function Call
  NthTerm(F, K, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let mod = 1000000007;

    // Function to calculate
    // (x ^ y) % p fast
    // exponentiation ( O(log y)
    function power(x, y, p)
    {

      // Store the result
      let res = 1;
      x = x % p;

      // Till y is
      // greater than 0
      while (y > 0)
      {

        // If y is odd
        if (y % 2 == 1)
          res = (res * x) % p;

        // Right shift by 1
        y = y >> 1;
        x = (x * x) % p;
      }

      // Print the resultant value
      return res;
    }

    // Function to find mod
    // inverse
    function modInverse(n, p)
    {

      // Using Fermat Little Theorem
      return power(n, p - 2, p);
    }

    // Function to find Nth term
    // of the given recurrence
    // relation
    function NthTerm(F, K, N)
    {

      // Doubly ended queue
      let q = [];

      // Stores the product of 1st K terms
      let product = 1;

      for(let i = 0; i < K; i++)
      {
        product *= F[i];
        product %= mod;
        q.push(F[i]);
      }

      // Push (K + 1)th
      // term to Dequeue
      q.push(product);

      for(let i = K + 1; i <= N; i++)
      {

        // First and the last element
        // of the dequeue
        let f = q[0];
        let e = q[q.length - 1];

        // Calculating the ith term
        let next_term = ((e % mod * e % mod) % mod *
                        (modInverse(f, mod))) % mod;

        // Add current term to end
        // of Dequeue
        q.push(next_term);

        // Remove the first number
        // from dequeue
        q.shift();
      }

      // Print the Nth term
      document.write(32+q[q.length - 1]*0 + "</br>");
    }

    // Given N, K and F[]
    let F = [1, 2];
    let K = 2;
    let N = 5;

    // Function Call
    NthTerm(F, K, N);

// This code is contributed by mukesh07.
</script>
```

**Output**

```
32
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)