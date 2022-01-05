# 有序对的数量，使得(Ai)【Aj】= 0

> 原文:[https://www.geeksforgeeks.org/number-ordered-pairs-ai-aj-0/](https://www.geeksforgeeks.org/number-ordered-pairs-ai-aj-0/)

给定一个由 n 个整数组成的数组 A[]，求有序对的个数，使 A <sub>i</sub> & A <sub>j</sub> 为零，其中 0 < =(i，j) < n .考虑(I，j)和(j，I)不同。
**约束:**
1<= n<= 10<sup>4</sup>
1<= A<sub>I</sub>T24】= 10<sup>4</sup>
**示例:**

```
Input : A[] = {3, 4, 2}
Output : 4
Explanation : The pairs are (3, 4) and (4, 2) which are 
counted as 2 as (4, 3) and (2, 4) are considered different. 

Input : A[]={5, 4, 1, 6}
Output : 4 
Explanation : (4, 1), (1, 4), (6, 1) and (1, 6) are the pairs
```

**简单方法**:一个简单的方法是检查所有可能的对，并计算按位&返回 0 的有序对的数量。
以下是上述思路的实现:

## C++

```
// CPP program to calculate the number
// of ordered pairs such that their bitwise
// and is zero
#include <bits/stdc++.h>
using namespace std;

// Naive function to count the number
// of ordered pairs such that their
// bitwise and is 0
int countPairs(int a[], int n)
{
    int count = 0;

    // check for all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++)
            if ((a[i] & a[j]) == 0)

                // add 2 as (i, j) and (j, i) are
                // considered different
                count += 2;
    }

    return count;
}

// Driver Code
int main()
{
    int a[] = { 3, 4, 2 };
    int n = sizeof(a) / sizeof(a[0]);   
    cout << countPairs(a, n);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the number
// of ordered pairs such that their bitwise
// and is zero

class GFG {

    // Naive function to count the number
    // of ordered pairs such that their
    // bitwise and is 0
    static int countPairs(int a[], int n)
    {
        int count = 0;

        // check for all possible pairs
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++)
                if ((a[i] & a[j]) == 0)

                    // add 2 as (i, j) and (j, i) are
                    // considered different
                    count += 2;
        }

        return count;
    }

    // Driver Code
    public static void main(String arg[])
    {
        int a[] = { 3, 4, 2 };
        int n = a.length;
        System.out.print(countPairs(a, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to calculate the number
# of ordered pairs such that their
# bitwise and is zero

# Naive function to count the number
# of ordered pairs such that their
# bitwise and is 0
def countPairs(a, n):
    count = 0

    # check for all possible pairs
    for i in range(0, n):
        for j in range(i + 1, n):
            if (a[i] & a[j]) == 0:

                # add 2 as (i, j) and (j, i) are
                # considered different
                count += 2
    return count

# Driver Code
a = [ 3, 4, 2 ]
n = len(a)
print (countPairs(a, n))

# This code is contributed
# by Shreyanshi Arun.
```

## C#

```
// C# program to calculate the number
// of ordered pairs such that their
// bitwise and is zero
using System;

class GFG {

    // Naive function to count the number
    // of ordered pairs such that their
    // bitwise and is 0
    static int countPairs(int []a, int n)
    {
        int count = 0;

        // check for all possible pairs
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
                if ((a[i] & a[j]) == 0)

                    // add 2 as (i, j) and (j, i)
                    // arev considered different
                    count += 2;
        }

        return count;
    }

    // Driver Code
    public static void Main()
    {
        int []a = { 3, 4, 2 };
        int n = a.Length;
        Console.Write(countPairs(a, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate the number
// of ordered pairs such that their
// bitwise and is zero

// Naive function to count the number
// of ordered pairs such that their
// bitwise and is 0
function countPairs($a, $n)
{
    $count = 0;

    // check for all possible pairs
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = $i + 1; $j < $n; $j++)
            if (($a[$i] & $a[$j]) == 0)

                // add 2 as (i, j) and (j, i) are
                // considered different
                $count += 2;
    }

    return $count;
}

// Driver Code
{
    $a = array(3, 4, 2);
    $n = sizeof($a) / sizeof($a[0]);
    echo countPairs($a, $n);
    return 0;
}

// This code is contributed by nitin mittal
```

## Java Script 语言

```
<script>
    // JavaScript program to calculate the number
    // of ordered pairs such that their bitwise
    // and is zero

    // Naive function to count the number
    // of ordered pairs such that their
    // bitwise and is 0
    const countPairs = (a, n) => {
        let count = 0;

        // check for all possible pairs
        for (let i = 0; i < n; i++) {
            for (let j = i + 1; j < n; j++)
                if ((a[i] & a[j]) == 0)

                    // add 2 as (i, j) and (j, i) are
                    // considered different
                    count += 2;
        }

        return count;
    }

    // Driver Code

    let a = [3, 4, 2];
    let n = a.length;
    document.write(countPairs(a, n));

    // This code is contributed by rakeshsahni

</script>

?>
```

**输出:**

```
4
```

**时间复杂度:** O(n <sup>2</sup> )
**高效方法**:一种高效的方法是使用[子集动态规划](https://www.geeksforgeeks.org/sum-subsets-dynamic-programming/)上的求和方法，统计有序对的个数。在 SOS DP 中，我们找出按位&返回 0 的对。这里我们需要数一数对的数量。
一些关键观察是约束，一个数组元素最多可以是 10 <sup>4</sup> 。把面具计算到(1 < < 15)会给我们答案。使用哈希计算每个元素的出现次数。如果最后一位是关闭的，那么与 SOS dp 相关，我们将有一个基本情况，因为只有一个关闭位的可能性。

```
dp[mask][0] = freq(mask)
```

如果最后一位设置为开，那么基本情况为:

```
dp[mask][0] = freq(mask) + freq(mask^1)
```

我们加上 freq(mask^1)来增加 OFF bit 的另一种可能性。
**迭代 N=15 位，这是最大可能。**
让我们考虑**第 I 位为 0** ，那么没有子集可以与第 I 位的掩码不同，因为这意味着数字在第 I 位将具有 1，其中掩码具有 0，这意味着它不是掩码的子集。因此，我们得出结论，这些数字现在只在第一(i-1)位不同。因此，

```
DP(mask, i) = DP(mask, i-1)
```

现在**第二种情况，如果第 I 位为 1，**可以分为两个不相交的集合。一种包含第 I 位为 1 的数字，与下一个(i-1)位中的掩码不同。第二个包含数字，第 I 位为 0，不同于掩码

![\oplus    ](img/54434a76f3769722dd21279761f4b531.png "Rendered by QuickLaTeX.com")

(2 <sup>i</sup> )在下一个(i-1)位。于是，

```
DP(mask, i) = DP(mask, i-1) + DP(mask
```

```
*** QuickLaTeX cannot compile formula:

*** Error message:
Error: Nothing to show, formula is empty

```

```
2<sup>i</sup>, i-1).
```

**DP[掩码][i]** 存储仅在前 I 位与掩码不同的掩码子集的数量。迭代所有数组元素，对于每个数组元素，将子集的数量(DP[((1<<n)–1)^ a[I]][n])加到对的数量上。N =最大位数。
**DP[((1<<n)–1)^ a[i]][n]与对的数量相加的解释:**以 a[I]为 5 为例，在二进制中为 101。为了更好地理解，假设在这种情况下 N=3，因此，101 的倒数将是 010，在应用按位&时给出 0。所以(1 < < 3)给出 1000，从 1 减去 111。111

![\oplus    ](img/54434a76f3769722dd21279761f4b531.png "Rendered by QuickLaTeX.com")

101 给出 010，它是反转位。所以 DP[(1<<n will="" have="" the="" number="" of="" subsets="" that="" returns="" on="" applying="" bitwise="" operator.="">下面是上面思路的实现:</n> 

## C++

```
// CPP program to calculate the number
// of ordered pairs such that their bitwise
// and is zero

#include <bits/stdc++.h>
using namespace std;

const int N = 15;

// efficient function to count pairs
long long countPairs(int a[], int n)
{
    // stores the frequency of each number
    unordered_map<int, int> hash;

    long long dp[1 << N][N + 1];

    memset(dp, 0, sizeof(dp)); // initialize 0 to all

    // count the frequency of every element
    for (int i = 0; i < n; ++i)
        hash[a[i]] += 1;

    // iterate for al possible values that a[i] can be
    for (long long mask = 0; mask < (1 << N); ++mask) {

        // if the last bit is ON
        if (mask & 1)
            dp[mask][0] = hash[mask] + hash[mask ^ 1];
        else // is the last bit is OFF
            dp[mask][0] = hash[mask];

        // iterate till n
        for (int i = 1; i <= N; ++i) {

            // if mask's ith bit is set
            if (mask & (1 << i))
            {
                dp[mask][i] = dp[mask][i - 1] +
                        dp[mask ^ (1 << i)][i - 1];
            }   
            else // if mask's ith bit is not set
                dp[mask][i] = dp[mask][i - 1];
        }
    }

    long long ans = 0;

    // iterate for all the array element
    // and count the number of pairs
    for (int i = 0; i < n; i++)
        ans += dp[((1 << N) - 1) ^ a[i]][N];

    // return answer
    return ans;
}

// Driver Code
int main()
{
    int a[] = { 5, 4, 1, 6 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countPairs(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the number of ordered pairs
// such that their bitwise
// and is zero
import java.util.*;
class GFG{

static int N = 15;

// Efficient function to count pairs
public static int countPairs(int a[],
                             int n)
{
  // Stores the frequency of
  // each number
  HashMap<Integer,
          Integer> hash = new HashMap<>();

  int dp[][] = new int[1 << N][N + 1];

  // Initialize 0 to all

  // Count the frequency
  // of every element
  for (int i = 0; i < n; ++i)
  {
    if(hash.containsKey(a[i]))
    {
      hash.replace(a[i],
      hash.get(a[i]) + 1);
    }
    else
    {
      hash.put(a[i], 1);
    }
  }

  // Iterate for al possible
  // values that a[i] can be
  for (int mask = 0;
           mask < (1 << N); ++mask)
  {
    // If the last bit is ON
    if ((mask & 1) != 0)
    {
      if(hash.containsKey(mask))
      {
        dp[mask][0] = hash.get(mask);
      }
      if(hash.containsKey(mask ^ 1))
      {
        dp[mask][0] += hash.get(mask ^ 1);
      }
    }
    else
    {
      // is the last bit is OFF
      if(hash.containsKey(mask))
      {
        dp[mask][0] = hash.get(mask); 
      }
    }

    // Iterate till n
    for (int i = 1; i <= N; ++i)
    {
      // If mask's ith bit is set
      if ((mask & (1 << i)) != 0)
      {
        dp[mask][i] = dp[mask][i - 1] +
                      dp[mask ^ (1 << i)][i - 1];
      }    
      else
      {
        // If mask's ith bit is not set
        dp[mask][i] = dp[mask][i - 1];
      }
    }
  }

  int ans = 0;

  // Iterate for all the
  // array element and
  // count the number of pairs
  for (int i = 0; i < n; i++)
  {
    ans += dp[((1 << N) - 1) ^ a[i]][N];
  }

  // return answer
  return ans;
}

// Driver code   
public static void main(String[] args)
{
  int a[] = {5, 4, 1, 6};
  int n = a.length;
  System.out.print(countPairs(a, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python program to calculate the number
# of ordered pairs such that their bitwise
# and is zero
N = 15

# efficient function to count pairs
def countPairs(a, n):

    # stores the frequency of each number
    Hash = {}

    # initialize 0 to all
    dp = [[0 for i in range(N + 1)] for j in range(1 << N)]

    # count the frequency of every element
    for i in range(n):
        if a[i] not in Hash:
            Hash[a[i]] = 1
        else:
            Hash[a[i]] += 1

    # iterate for al possible values that a[i] can be
    mask = 0
    while(mask < (1 << N)):
        if mask not in Hash:
            Hash[mask] = 0

        # if the last bit is ON
        if(mask & 1):
            dp[mask][0] = Hash[mask] + Hash[mask ^ 1]

        else:    # is the last bit is OFF
            dp[mask][0] = Hash[mask]

        # iterate till n
        for i in range(1, N + 1):

            # if mask's ith bit is set
            if(mask & (1 << i)):
                dp[mask][i] = dp[mask][i - 1] + dp[mask ^ (1 << i)][i - 1]

            else:    # if mask's ith bit is not set
                dp[mask][i] = dp[mask][i - 1]

        mask += 1

    ans = 0

    # iterate for all the array element
    # and count the number of pairs
    for i in range(n):
        ans += dp[((1 << N) - 1) ^ a[i]][N]

    # return answer
    return ans

# Driver Code
a = [5, 4, 1, 6]
n = len(a)
print(countPairs(a, n))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to calculate
// the number of ordered pairs
// such that their bitwise
// and is zero
using System;
using System.Collections.Generic;

class GFG {

    static int N = 15;

    // Efficient function to count pairs
    static int countPairs(int[] a, int n)
    {
      // Stores the frequency of
      // each number
      Dictionary<int, int> hash = new Dictionary<int, int>();

      int[, ] dp = new int[1 << N, N + 1];

      // Initialize 0 to all

      // Count the frequency
      // of every element
      for (int i = 0; i < n; ++i)
      {
        if(hash.ContainsKey(a[i]))
        {
          hash[a[i]] += 1;
        }
        else
        {
          hash.Add(a[i], 1);
        }
      }

      // Iterate for al possible
      // values that a[i] can be
      for (int mask = 0;
               mask < (1 << N); ++mask)
      {
        // If the last bit is ON
        if ((mask & 1) != 0)
        {
          if(hash.ContainsKey(mask))
          {
            dp[mask, 0] = hash[mask];
          }
          if(hash.ContainsKey(mask ^ 1))
          {
            dp[mask, 0] += hash[mask ^ 1];
          }
        }
        else
        {
          // is the last bit is OFF
          if(hash.ContainsKey(mask))
          {
            dp[mask, 0] = hash[mask]; 
          }
        }

        // Iterate till n
        for (int i = 1; i <= N; ++i)
        {

          // If mask's ith bit is set
          if ((mask & (1 << i)) != 0)
          {
            dp[mask, i] = dp[mask, i - 1] +
                          dp[mask ^ (1 << i), i - 1];
          }    
          else
          {

            // If mask's ith bit is not set
            dp[mask, i] = dp[mask, i - 1];
          }
        }
      }

      int ans = 0;

      // Iterate for all the
      // array element and
      // count the number of pairs
      for (int i = 0; i < n; i++)
      {
        ans += dp[((1 << N) - 1) ^ a[i], N];
      }

      // return answer
      return ans;
    }

  // Driver code
  static void Main()
  {
      int[] a = {5, 4, 1, 6};
      int n = a.Length;
      Console.WriteLine(countPairs(a, n));
  }
}

// This code is contributed by divyesh072019
```

**输出:**

```
4
```

**时间复杂度:** O(N*2 <sup>N</sup> )其中 N=15，这是可能的最大位数，因为 A <sub>max</sub> =10 <sup>4</sup> 。