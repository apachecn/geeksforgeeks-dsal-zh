# 将一个数表示为以 9 结尾的正数之和

> 原文:[https://www . geesforgeks . org/represent-a-number-as-sum-of-正数-以-9 结尾/](https://www.geeksforgeeks.org/represent-a-number-as-the-sum-of-positive-numbers-ending-with-9/)

给定一个整数 **N** ，任务是检查 **N** 是否可以表示为以 **9** 为最后一位数字(9，19，29，39…)的整数之和。如果发现是真的，那么找到获得 **N** 所需的此类整数的最小计数。否则打印 **-1** 。

**示例:**

> **输入:**N = 156
> T3】输出:4
> T6】解释:T8】156 = 9+9+9+129
> 
> **输入:** N = 60
> **输出:** -1
> **解释:**
> 无法从以 9 为最后一位数字的数字中得到和 60。

**天真的做法:**这个问题可以看作是[硬币兑换问题](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)的变种。对于这个问题，硬币可以用[9，19，29，39…直到最后一个以 9 结尾的小于 N 的数字]。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以基于以下观察进行优化:如果 N 的**最后一位数字是 K** ，那么正好**(10–K)**需要最小的数字来形成 **N** 。

> 一个和 N 可以通过加 10–K 个数得到，其中 K 是 N 的最后一位数字
> 因此，和 N 可以通过加 9，(9–K)次，最后加 N –( 9 *(9–K))得到。

按照以下步骤解决问题:

1.  提取给定数字的最后一位， **K = N % 10**
2.  使用上述观察，总共需要**(10–K)**个数字。现在，计算**9 *(9–K)**，因为获得 **N** 所需的第一个**9–K**号是 **9** 。
3.  现在，计算**N–9 *(9–K)**并存储在一个变量中，比如 **z** 。如果 **z** 大于或等于 **9** 且最后一位数字为 **9** ，则打印**10–K**作为答案。否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count
// of numbers ending with 9 to form N
int minCountOfNumbers(int N)
{
    // Extract last digit of N
    int k = N % 10;

    // Calculate the last digit
    int z = N - (9 * (9 - k));

    // If the last digit
    // satisfies the condition
    if (z >= 9 && z % 10 == 9) {
        return 10 - k;
    }
    else
        return -1;
}

// Driver Code
int main()
{
    int N = 156;
    cout << minCountOfNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum count
// of numbers ending with 9 to form N
static int minCountOfNumbers(int N)
{

    // Extract last digit of N
    int k = N % 10;

    // Calculate the last digit
    int z = N - (9 * (9 - k));

    // If the last digit
    // satisfies the condition
    if (z >= 9 && z % 10 == 9)
    {
        return 10 - k;
    }
    else
        return -1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 156;
    System.out.print(minCountOfNumbers(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum count
# of numbers ending with 9 to form N
def minCountOfNumbers(N):

    # Extract last digit of N
    k = N % 10

    # Calculate the last digit
    z = N - (9 * (9 - k))

    # If the last digit
    # satisfies the condition
    if (z >= 9 and z % 10 == 9):
        return 10 - k
    else:
        return -1

# Driver Code
if __name__ == '__main__':

    N = 156

    print(minCountOfNumbers(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum count
// of numbers ending with 9 to form N
static int minCountOfNumbers(int N)
{

    // Extract last digit of N
    int k = N % 10;

    // Calculate the last digit
    int z = N - (9 * (9 - k));

    // If the last digit
    // satisfies the condition
    if (z >= 9 && z % 10 == 9)
    {
        return 10 - k;
    }
    else
        return -1;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 156;

    Console.Write(minCountOfNumbers(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// java script  program for the above approach

// Function to find the minimum count
// of numbers ending with 9 to form N
function minCountOfNumbers(N){

    // Extract last digit of N
    let k = N % 10;

    // Calculate the last digit
    let z = N - (9 * (9 - k));

    // If the last digit
    // satisfies the condition
    if (z >= 9 && z % 10 == 9)
    {
        return 10 - k;
    }
    else
    {
        return -1;
    }
}

 // Driver Code   
    let N = 156;
    document.write(minCountOfNumbers(N));

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)