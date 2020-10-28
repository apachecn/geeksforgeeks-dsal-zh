# 串联时可被 K 整除的 Array 元素对的数量

给定数组 **arr []** 和整数 **K** ，任务是对索引对**（i，j）**进行计数，以使 **i！ ＝ j** ，并且 **a [i]** 和 **a [j]** 的串联可被 **K** 整除。

**示例**：

> **输入**：arr [] = [4，5，2]，K = 2
> **输出**：4
> **说明**：
> 全部 可能的连接是{45，42，54，52，24，25}。
> 其中，被 2 整除的数字为{42，52，24，54}。
> 因此，计数为 4。
> 
> **输入**：arr [] = [45，1，10，12，11，7]，K = 11
> **输出**：7

**天真的方法**：

解决问题的最简单方法如下：

*   使用带有变量 **i** 和 **j** 的嵌套循环遍历数组。

*   对于每个 **i！= j** ，通过等式将 **arr [i]** 和 **arr [j]** 连接起来：

> arr [i]和 arr [j]的串联= **（arr [i] * 10 <sup>lenj</sup> ）+ arr [j]** ，其中 **lenj** 是数字 **arr [j]** 中的位数

*   通过 **K** 检查连接数的**除数**。

> 当且仅当**（arr [j]％k）**和**（（arr [i] * 10 <sup>lenj [</sup> ）％k）**为 **0** mod **k** 。

*   对于所有此类**对（arr [i]，arr [j]）**，增加**计数**。

*   打印**计数**的最终值。

***时间复杂度**：O（N <sup>2</sup> * len（maxm），其中 maxm 表示数组中的最大元素，len（maxm）表示 maxm 的位数。*

***辅助空间**：O（1）*

**有效方法**：

要优化上述方法，请按照以下步骤操作：

*   为了应用上述公式，对于从 **1** 到 **10** 的每个长度，维持一个[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。

*   将{ **len [a [i]]** ， **a [i]％k** }存储在地图中。

*   为了对数进行计数，对于 **[1，10]** 中的每个 **j** ，将**计数**增加**的频率（k –（（ar i] * 10 ^ j）％k））以 **{j，k –（（arr [i] * 10 ^ j）％k）}** 形式存储在 **Map** 中的** ]映射。

*   如果计数了**对（arr [i]，arr [i]）**，则将**计数**减少 **1** 。

*   遍历数组后，打印最终的**计数**。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to count pairs
// of array elements which are
// divisible by K when concatenated
#include <bits/stdc++.h>
using namespace std;

map<int, int> rem[11];

// Function to calculate and return the
// count of pairs
int countPairs(vector<int> a, int n, int k)
{

    vector<int> len(n);

    // Compute power of 10 modulo k
    vector<int> p(11);
    p[0] = 1;
    for (int i = 1; i <= 10; i++) {
        p[i] = (p[i - 1] * 10) % k;
    }

    for (int i = 0; i < n; i++) {
        int x = a[i];

        // Calculate length of a[i]
        while (x > 0) {
            len[i]++;
            x /= 10;
        }

        // Increase count of remainder
        rem[len[i]][a[i] % k]++;
    }

    int ans = 0;

    for (int i = 0; i < n; i++) {

        for (int j = 1; j <= 10; j++) {

            // Calculate (a[i]* 10^lenj) % k
            int r = (a[i] * p[j]) % k;

            // Calculate (k - (a[i]* 10^lenj)% k) % k
            int xr = (k - r) % k;

            // Increase answer by count
            ans += rem[j][xr];

            // If a pair (a[i], a[i]) is counted
            if (len[i] == j
                && (r + a[i] % k) % k == 0)
                ans--;
        }
    }

    // Return the count of pairs
    return ans;
}

// Driver Code
int main()
{
    vector<int> a = { 4, 5, 2 };
    int n = a.size(), k = 2;
    cout << countPairs(a, n, k);
}

```

## Java

```java

// Java program to count pairs 
// of array elements which are 
// divisible by K when concatenated 
import java.util.*;
import java.lang.*;

class GFG{

static int[][] rem = new int[11][11];

// Function to calculate and return the
// count of pairs
static int countPairs(int[] a, int n, int k)
{
    int[] len = new int[n];

    // Compute power of 10 modulo k
    int[] p = new int[11];
    p[0] = 1;

    for(int i = 1; i <= 10; i++)
    {
        p[i] = (p[i - 1] * 10) % k;
    }

    for(int i = 0; i < n; i++)
    {
        int x = a[i];

        // Calculate length of a[i]
        while (x > 0) 
        {
            len[i]++;
            x /= 10;
        }

        // Increase count of remainder
        rem[len[i]][a[i] % k]++;
    }

    int ans = 0;

    for(int i = 0; i < n; i++)
    {
        for(int j = 1; j <= 10; j++)
        {

            // Calculate (a[i]* 10^lenj) % k
            int r = (a[i] * p[j]) % k;

            // Calculate (k - (a[i]* 10^lenj)% k) % k
            int xr = (k - r) % k;

            // Increase answer by count
            ans += rem[j][xr];

            // If a pair (a[i], a[i]) is counted
            if (len[i] == j && 
             (r + a[i] % k) % k == 0)
                ans--;
        }
    }

    // Return the count of pairs
    return ans;
}   

// Driver code
public static void main (String[] args)
{
    int[] a = { 4, 5, 2 };
    int n = a.length, k = 2;

    System.out.println(countPairs(a, n, k));
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program to count pairs
# of array elements which are
# divisible by K when concatenated
rem = [ [ 0 for x in range(11) ]
            for y in range(11) ]

# Function to calculate and return the
# count of pairs
def countPairs(a, n, k):

    l = [0] * n

    # Compute power of 10 modulo k
    p = [0] * (11)
    p[0] = 1

    for i in range(1, 11):
        p[i] = (p[i - 1] * 10) % k

    for i in range(n):
        x = a[i]

        # Calculate length of a[i]
        while (x > 0):
            l[i] += 1
            x //= 10

        # Increase count of remainder
        rem[l[i]][a[i] % k] += 1

    ans = 0

    for i in range(n):
        for j in range(1, 11):

            # Calculate (a[i]* 10^lenj) % k
            r = (a[i] * p[j]) % k

            # Calculate (k - (a[i]* 10^lenj)% k) % k
            xr = (k - r) % k

            # Increase answer by count
            ans += rem[j][xr]

            # If a pair (a[i], a[i]) is counted
            if (l[i] == j and
               (r + a[i] % k) % k == 0):
                ans -= 1

    # Return the count of pairs
    return ans

# Driver Code
a = [ 4, 5, 2 ]
n = len(a)
k = 2

print(countPairs(a, n, k))

# This code is contributed by chitranayal

```

## C#

```cs

// C# program to count pairs 
// of array elements which are 
// divisible by K when concatenated 
using System;
class GFG{

static int [,]rem = new int[11, 11];

// Function to calculate and 
// return the count of pairs
static int countPairs(int[] a, 
                      int n, int k)
{
  int[] len = new int[n];

  // Compute power of 10 modulo k
  int[] p = new int[11];
  p[0] = 1;

  for(int i = 1; i <= 10; i++)
  {
    p[i] = (p[i - 1] * 10) % k;
  }

  for(int i = 0; i < n; i++)
  {
    int x = a[i];

    // Calculate length of a[i]
    while (x > 0) 
    {
      len[i]++;
      x /= 10;
    }

    // Increase count of remainder
    rem[len[i], a[i] % k]++;
  }

  int ans = 0;

  for(int i = 0; i < n; i++)
  {
    for(int j = 1; j <= 10; j++)
    {
      // Calculate (a[i]* 10^lenj) % k
      int r = (a[i] * p[j]) % k;

      // Calculate (k - (a[i]* 10^lenj)% k) % k
      int xr = (k - r) % k;

      // Increase answer by count
      ans += rem[j, xr];

      // If a pair (a[i], a[i]) is counted
      if (len[i] == j && 
         (r + a[i] % k) % k == 0)
        ans--;
    }
  }

  // Return the count of pairs
  return ans;
}   

// Driver code
public static void Main(string[] args)
{
  int[] a = {4, 5, 2};
  int n = a.Length, k = 2;
  Console.Write(countPairs(a, n, k));
}
}

// This code is contributed by rutvik_56

```

**Output**

```
4

```

***时间复杂度**：O（N * len（maxm））*

***辅助空间**：O（N）*



* * *

* * *



