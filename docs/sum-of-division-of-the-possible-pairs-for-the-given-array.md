# 给定数组的可能对的除法之和

> 原文:[https://www . geeksforgeeks . org/给定数组的可能对除法之和/](https://www.geeksforgeeks.org/sum-of-division-of-the-possible-pairs-for-the-given-array/)

给定一个 **N** 正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。对于所有可能的对 **(x，y)** ，任务是找到 **x/y** 的总和。
**注:**如果 **(x/y)** 的小数部分为& ge 0.5，则加上 **(x/y)** 的 [ceil](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) ，否则加上 **(x/y)** 的 floor。
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 12
> **解释:**
> 所有可能的带除法的对是:
> (1/1) = 1，(1/2) = 1，(1/3) = 0
> (2/1) = 2，(2/2) = 1，(2/3) = 1
> (3/1) = 3，(3/2) = 2，(3/3) = 1
> **输入:** arr[] = {1，2，3，4}
> **输出:** 22
> **解释:**
> 所有可能有除法的对是:
> (1/1) = 1，(1/2) = 1，(1/3) = 0，(1/4) = 0
> (2/1) = 2，(2/2) = 1，(2/3) = 1，(2/4) = 1 (4/4) = 1
> 总和= 1+1+0+0+2+1+1+1+3+2+1+1+4+2+1+1 = 22。

**天真方法:**想法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中所有可能的对，并为每个对 **(x，y)** 找到 **(x/y)** 的总和。
**时间复杂度:***O(N<sup>2</sup>)*
**高效方法:**
为了优化上述方法，我们必须计算**频率数组**，其中 freq[i]表示数字 I 的出现次数。

*   对于任何给定的数字 X，当除以 X 时，范围从[0.5X，1.5X]的所有数字将导致答案贡献 1。类似地，范围从[1.5X，2.5X]的所有数字将导致答案贡献 2
*   将这个事实推广到从 **[(n-0.5)X，(n+0.5)X]** 范围内的所有数字，当除以 X 时，将导致对答案贡献 n。
*   因此，对于 1 到 N 范围内的每一个数 P，我们可以通过计算频率数组的前缀和得到给定范围内的数的计数。
*   对于一个数字 P，我们最多需要查询 N/P 次的范围。

以下是上述方法的实现:

## C++

```
// C++ implementation to compute the
// sum of division of all the possible
// pairs for the given array

#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function to compute the sum
int func(int arr[], int n)
{

    double ans = 0;
    int maxx = 0;
    double freq[100005] = { 0 };
    int temp;

    // counting frequency
    // of each term
    // and finding maximum
    // among it
    for (int i = 0; i < n; i++) {
        temp = arr[i];
        freq[temp]++;
        maxx = max(maxx, temp);
    }

    // Making cumulative frequency
    for (int i = 1; i <= maxx; i++) {
        freq[i] += freq[i - 1];
    }

    for (int i = 1; i <= maxx; i++) {
        if (freq[i]) {
            i = (double)i;
            double j;
            ll value = 0;

            // Taking the ceil value
            double cur = ceil(0.5 * i) - 1.0;

            for (j = 1.5;; j++) {
                int val = min(maxx, (int)(ceil(i * j) - 1.0));
                int times = (freq[i] - freq[i - 1]), con = j - 0.5;

                // nos. in [(n-0.5)X, (n+0.5)X)
                // range will add n to the ans

                ans += times * con * (freq[(int)val] - freq[(int)cur]);
                cur = val;

                if (val == maxx)
                    break;
            }
        }
    }

    // Return the final result
    return (ll)ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << func(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to compute the
// sum of division of all the possible
// pairs for the given array
class GFG{

// Function to compute the sum
static long func(int arr[], int n)
{
    double ans = 0;
    int maxx = 0;
    double freq[] = new double[100005];
    int temp;

    // Counting frequency of each term
    // and finding maximum among it
    for(int i = 0; i < n; i++)
    {
       temp = arr[i];
       freq[temp]++;
       maxx = Math.max(maxx, temp);
    }

    // Making cumulative frequency
    for(int i = 1; i <= maxx; i++)
    {
       freq[i] += freq[i - 1];
    }

    for(int i = 1; i <= maxx; i++)
    {
       if (freq[i] != 0)
       {
           double j;

           // Taking the ceil value
           double cur = Math.ceil(0.5 * i) - 1.0;

           for(j = 1.5;; j++)
           {
              int val = Math.min(maxx,
                  (int)(Math.ceil(i * j) - 1.0));
              int times = (int)(freq[i] -
                                freq[i - 1]),
                    con = (int)(j - 0.5);

              // nos. in [(n-0.5)X, (n+0.5)X)
              // range will add n to the ans
              ans += times * con * (freq[(int)val] -
                                    freq[(int)cur]);
              cur = val;

              if (val == maxx)
                  break;
           }
       }
    }

    // Return the final result
    return (long)ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int n = arr.length;

    System.out.print(func(arr, n) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to compute the sum
# of division of all the possible
# pairs for the given array
from math import *

# Function to compute the sum
def func (arr, n):

    ans = 0
    maxx = 0
    freq = [0] * 100005
    temp = 0

    # Counting frequency of each term
    # and finding maximum among it
    for i in range(n):
        temp = arr[i]
        freq[temp] += 1
        maxx = max(maxx, temp)

    # Making cumulative frequency
    for i in range(1, maxx + 1):
        freq[i] += freq[i - 1]

    for i in range(1, maxx + 1):
        if (freq[i]):
            value = 0

            # Taking the ceil value
            cur = ceil(0.5 * i) - 1.0

            j = 1.5
            while (1):
                val = min(maxx, (ceil(i * j) - 1.0))
                times = (freq[i] - freq[i - 1])
                con = j - 0.5

                # nos. in [(n-0.5)X , (n+0.5)X)
                # range will add n to the ans
                ans += times * con * (freq[int(val)] -
                                      freq[int(cur)])
                cur = val

                if (val == maxx):
                    break
                j += 1

    return int(ans)

# Driver code
if __name__ == '__main__':

    arr = [ 1, 2, 3 ]
    n = len(arr)

    print(func(arr, n))

# This code is contributed by himanshu77
```

## C#

```
// C# implementation to compute the
// sum of division of all the possible
// pairs for the given array
using System;

class GFG{

// Function to compute the sum
static long func(int []arr, int n)
{
    double ans = 0;
    int maxx = 0;
    double []freq = new double[100005];
    int temp;

    // Counting frequency of each term
    // and finding maximum among it
    for(int i = 0; i < n; i++)
    {
       temp = arr[i];
       freq[temp]++;
       maxx = Math.Max(maxx, temp);
    }

    // Making cumulative frequency
    for(int i = 1; i <= maxx; i++)
    {
       freq[i] += freq[i - 1];
    }

    for(int i = 1; i <= maxx; i++)
    {
       if (freq[i] != 0)
       {
           double j;

           // Taking the ceil value
           double cur = Math.Ceiling(0.5 * i) - 1.0;

           for(j = 1.5;; j++)
           {
              int val = Math.Min(maxx,
                  (int)(Math.Ceiling(i * j) - 1.0));
              int times = (int)(freq[i] -
                                freq[i - 1]),
                    con = (int)(j - 0.5);

              // nos. in [(n-0.5)X, (n+0.5)X)
              // range will add n to the ans
              ans += times * con * (freq[(int)val] -
                                    freq[(int)cur]);
              cur = val;

              if (val == maxx)
                  break;
           }
       }
    }

    // Return the readonly result
    return (long)ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3 };
    int n = arr.Length;

    Console.Write(func(arr, n) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript implementation to compute the
// sum of division of all the possible
// pairs for the given array

// Function to compute the sum
function func(arr, n)
{
    let ans = 0;
    let maxx = 0;
    let freq = Array.from({length: 100005}, (_, i) => 0);
    let temp;

    // Counting frequency of each term
    // and finding maximum among it
    for(let i = 0; i < n; i++)
    {
       temp = arr[i];
       freq[temp]++;
       maxx = Math.max(maxx, temp);
    }

    // Making cumulative frequency
    for(let i = 1; i <= maxx; i++)
    {
       freq[i] += freq[i - 1];
    }

    for(let i = 1; i <= maxx; i++)
    {
       if (freq[i] != 0)
       {
           let j;

           // Taking the ceil value
           let cur = Math.ceil(0.5 * i) - 1.0;

           for(j = 1.5;; j++)
           {
              let val = Math.min(maxx,
                  (Math.ceil(i * j) - 1.0));
              let times = (freq[i] -
                                freq[i - 1]),
                    con = (j - 0.5);

              // nos. in [(n-0.5)X, (n+0.5)X)
              // range will add n to the ans
              ans += times * con * (freq[val] -
                                    freq[cur]);
              cur = val;

              if (val == maxx)
                  break;
           }
       }
    }

    // Return the final result
    return ans;
}

// Driver Code

     let arr = [ 1, 2, 3 ];
    let n = arr.length;

    document.write(func(arr, n));

</script>
```

**Output:** 

```
12
```

***时间复杂度:** O(N * log (N) )*