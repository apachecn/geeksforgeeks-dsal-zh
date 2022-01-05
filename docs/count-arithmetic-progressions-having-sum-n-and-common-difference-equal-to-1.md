# 计算和 N 和公共差等于 1 的算术级数

> 原文:[https://www . geeksforgeeks . org/count-算术-progressions-having-sum-n-and-common-difference-equal-to-1/](https://www.geeksforgeeks.org/count-arithmetic-progressions-having-sum-n-and-common-difference-equal-to-1/)

给定一个整数 **N** ，任务是计算所有[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)，其中公差等于 **1** ，其所有元素之和等于 **N.**

**示例:**

> **输入:** N = 12
> **输出:** 3
> **说明:**
> 以下三个 AP 满足要求条件:
> 
> *   {3, 4, 5}
> *   {−2, −1, 0, 1, 2, 3, 4, 5}
> *   {−11, −10, −9, …, 10, 11, 12]}
> 
> **输入:** N = 963761198400
> 输出: 1919

**方法:**给定的问题可以使用 **AP 的以下属性来解决:**

*   一个 **AP** 系列 的 [和的和由公式**S =(N/2)*(2 * A+N-1)**给出，其中第一项为 **A** 而共同的区别为 **1** 。](https://www.geeksforgeeks.org/program-sum-arithmetic-series/)
*   求解上述方程:

> s = N/2[2 * A+N-1]。
> 
> 重新排列并乘以 2
> =>2 * S = N *(N+2 * a1)
> 
> 进一步重新排列
> =>A =((2 * N/I)I+1)/2。
> 
> 现在，迭代 **2 * N** 的所有因子，检查每个因子 **i** 、**(2 * N/I)I+1**是否为偶数。

按照以下步骤解决问题:

*   初始化一个变量，比如**计数，**来存储给定条件下可能的 AP 系列的数量。
*   遍历 **2 * N** 的所有因子，对于每个**I**T4 因子，检查**(2 * N/I)I+1**是否为偶数。
*   如果发现为真，则增加计数。
*   打印**计数–1**作为所需答案，因为仅由 **N** 组成的序列需要丢弃。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count all possible
// AP series with common difference
// 1 and sum of elements equal to N
void countAPs(long long int N)
{
    // Stores the count of AP series
    long long int count = 0;

    // Traverse through all factors of 2 * N
    for (long long int i = 1;
         i * i <= 2 * N; i++) {

        long long int res = 2 * N;
        if (res % i == 0) {

            // Check for the given conditions
            long long int op = res / i - i + 1;

            if (op % 2 == 0) {

                // Increment count
                count++;
            }
            if (i * i != res
                and (i - res / i + 1) % 2 == 0) {
                count++;
            }
        }
    }

    // Print count - 1
    cout << count - 1 << "\n";
}

// Driver Code
int main()
{
    // Given value of N
    long long int N = 963761198400;

    // Function call to count
    // required number of AP series
    countAPs(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG {

  // Function to count all possible
  // AP series with common difference
  // 1 and sum of elements equal to N
  static void countAPs(long N)
  {

    // Stores the count of AP series
    long count = 0;

    // Traverse through all factors of 2 * N
    for (long i = 1; i * i <= 2 * N; i++) {

      long res = 2 * N;
      if (res % i == 0) {

        // Check for the given conditions
        long op = res / i - i + 1;

        if (op % 2 == 0) {

          // Increment count
          count++;
        }
        if (i * i != res
            && (i - res / i + 1) % 2 == 0) {
          count++;
        }
      }
    }

    // Print count - 1
    System.out.println(count - 1);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given value of N
    long N = 963761198400L;

    // Function call to count
    // required number of AP series
    countAPs(N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

#  Function to count all possible
#  AP series with common difference
#  1 and sum of elements equal to N
def countAPs(N) :

    #  Stores the count of AP series
    count = 0

    #  Traverse through all factors of 2 * N
    i = 1
    while(i * i <= 2 * N) :

        res = 2 * N
        if (res % i == 0) :

            #  Check for the given conditions
            op = res / i - i + 1

            if (op % 2 == 0) :

                #  Increment count
                count += 1
            if (i * i != res
                and (i - res / i + 1) % 2 == 0) :
                count += 1     
        i += 1

    #  Prcount - 1
    print(count - 1)

#  Driver Code

#  Given value of N
N = 963761198400

#  Function call to count
#  required number of AP series
countAPs(N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for above approach
using System;
public class GFG
{

  // Function to count all possible
  // AP series with common difference
  // 1 and sum of elements equal to N
  static void countAPs(long N)
  {

    // Stores the count of AP series
    long count = 0;

    // Traverse through all factors of 2 * N
    for (long i = 1; i * i <= 2 * N; i++) {

      long res = 2 * N;
      if (res % i == 0) {

        // Check for the given conditions
        long op = res / i - i + 1;

        if (op % 2 == 0) {

          // Increment count
          count++;
        }
        if (i * i != res
            && (i - res / i + 1) % 2 == 0) {
          count++;
        }
      }
    }

    // Print count - 1
    Console.WriteLine(count - 1);
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Given value of N
    long N = 963761198400L;

    // Function call to count
    // required number of AP series
    countAPs(N);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

  // Function to count all possible
  // AP series with common difference
  // 1 and sum of elements equal to N
  function countAPs(N)
  {

    // Stores the count of AP series
    let count = 0;

    // Traverse through all factors of 2 * N
    for (let i = 1; i * i <= 2 * N; i++) {

      let res = 2 * N;
      if (res % i == 0) {

        // Check for the given conditions
        let op = res / i - i + 1;

        if (op % 2 == 0) {

          // Increment count
          count++;
        }
        if (i * i != res
            && (i - res / i + 1) % 2 == 0) {
          count++;
        }
      }
    }

    // Print count - 1
    document.write(count - 1);
  }

// Driver code

    // Given value of N
    let N = 963761198400;

    // Function call to count
    // required number of AP series
    countAPs(N);

</script>
```

**Output:** 

```
1919
```

***时间复杂度:** O(√N)*
***辅助** **空间:** O(1)*