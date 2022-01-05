# 最多减少一个数字 N D，以最大化尾随 9 的数量

> 原文:[https://www . geeksforgeeks . org/最多减少一个数字 n 乘以 d 以最大化尾随 9 的数量/](https://www.geeksforgeeks.org/reduce-a-number-n-by-at-most-d-to-maximize-count-of-trailing-nines/)

给定两个正整数 **N** 和 **D** ，任务是将 **N** 的值最多递减 **D** ，使得 **N** 包含最大数量的尾随 **9** s

**示例:**

> **输入:** N = 1025，D = 6
> **输出:** 1019
> **解释:**
> N 减 6 将 N 修改为 1019，其中包含最大可能的尾随 9 计数。
> 因此，所需输出为 1019。
> 
> **输入:** N = 1025，D = 5
> **输出:** 1025
> 将 N 递减所有可能的值，直到 D(= 5)，不能获得包含尾随 9 的数字。
> 因此，要求输出为 1025。

**天真方法:**解决这个问题最简单的方法是使用变量 **i** 迭代范围**【0，D】**，并将 **N** 的值递减 **i** 。最后，打印 **N** 的值，该值包含尾随 **9** 的最大可能计数。
***时间复杂度:**O(D * log<sub>10</sub>(N))*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> N %幂(10，I)给出 N 的最后 I 位

按照以下步骤解决问题:

*   初始化一个变量，比如说 **res** 存储 **N** 的递减值，最大计数跟随 **9** 。
*   初始化一个变量，比如说**计数**将[计数存储在 N](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/) 中。
*   使用变量 **i** 迭代范围**【1，碳数】**，检查 **N %幂(10，i)** 是否大于或等于 **D** 。如果发现为真，则打印 **res** 的值。
*   否则，将 **res** 更新为 **N %功率(10，I)–1**。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find a number with
// maximum count of trailing nine
void maxNumTrailNine(int n, int d)
{
    int res = n;

    // Stores count of digits in n
    int cntDigits = log10(n) + 1;

    // Stores power of 10
    int p10 = 10;

    for (int i = 1; i <= cntDigits; i++) {

        // If last i digits greater than
        // or equal to d
        if (n % p10 >= d) {
            break;
        }

        else {

            // Update res
            res = n - n % p10 - 1;
        }

        // Update p10
        p10 = p10 * 10;
    }
    cout << res;
}

// Driver Code
int main()
{
    int n = 1025, d = 6;

    // Function Call
    maxNumTrailNine(n, d);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to find a number with
    // maximum count of trailing nine
    static void maxNumTrailNine(int n, int d)
    {
        int res = n;

        // Stores count of digits in n
        int cntDigits = (int)Math.log10(n) + 1;

        // Stores power of 10
        int p10 = 10;

        for (int i = 1; i <= cntDigits; i++)
        {

            // If last i digits greater than
            // or equal to d
            if (n % p10 >= d)
            {
                break;
            }

            else
            {

                // Update res
                res = n - n % p10 - 1;
            }

            // Update p10
            p10 = p10 * 10;
        }
        System.out.println(res);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 1025, d = 6;

        // Function Call
        maxNumTrailNine(n, d);
    }
}

// This code is contribute by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log10

# Function to find a number with
# maximum count of trailing nine
def maxNumTrailNine(n, d):
    res = n

    # Stores count of digits in n
    cntDigits = int(log10(n) + 1)

    # Stores power of 10
    p10 = 10

    for i in range(1, cntDigits + 1):

        # If last i digits greater than
        # or equal to d
        if (n % p10 >= d):
            break

        else:

            # Update res
            res = n - n % p10 - 1

        # Update p10
        p10 = p10 * 10

    print (res)

# Driver Code
if __name__ == '__main__':
    n, d = 1025, 6

    # Function Call
    maxNumTrailNine(n, d)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find a number with
  // maximum count of trailing nine
  static void maxNumTrailNine(int n, int d)
  {
    int res = n;

    // Stores count of digits in n
    int cntDigits = (int)Math.Log10(n) + 1;

    // Stores power of 10
    int p10 = 10;     
    for (int i = 1; i <= cntDigits; i++)
    {

      // If last i digits greater than
      // or equal to d
      if (n % p10 >= d)
      {
        break;
      }

      else
      {

        // Update res
        res = n - n % p10 - 1;
      }

      // Update p10
      p10 = p10 * 10;
    }
    Console.WriteLine(res);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int n = 1025, d = 6;

    // Function Call
    maxNumTrailNine(n, d);
  }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find a number with
// maximum count of trailing nine
function maxNumTrailNine(n, d)
{
    let res = n;

    // Stores count of digits in n
    let cntDigits = parseInt(Math.log(n) /
                             Math.log(10)) + 1;

    // Stores power of 10
    let p10 = 10;

    for(let i = 1; i <= cntDigits; i++)
    {

        // If last i digits greater than
        // or equal to d
        if (n % p10 >= d)
        {
            break;
        }
        else
        {

            // Update res
            res = n - n % p10 - 1;
        }

        // Update p10
        p10 = p10 * 10;
    }
    document.write(res);
}

// Driver Code
let n = 1025, d = 6;

// Function Call
maxNumTrailNine(n, d);

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
1019
```

***时间复杂度:** O(min(log <sub>10</sub> (D)，log<sub>10</sub>(N))*
***辅助空间:** O(1)*