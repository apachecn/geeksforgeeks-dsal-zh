# 对给定范围内的数字进行计数，这些数字的二进制表示具有相同的第一位和最后一位数字

> 原文:[https://www . geesforgeks . org/count-numbers-from-a-给定范围-具有相同的二进制表示中的第一个和最后一个数字/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-having-same-first-and-last-digits-in-their-binary-representation/)

给定两个整数 **L** 和 **R** ，任务是找出在**【L，R】**范围内的数字的计数，它们在[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中的第一个和最后一个数字是相同的。

**示例:**

> **输入:** L = 1，R = 5
> **输出:** 3
> **解释:**
> (1)<sub>10</sub>=(1)<sub>2</sub>T13】(2)<sub>10</sub>=(10)<sub>2</sub>
> (3)<sub>10</sub>=(11)<sub>2</sub>T23
> 
> **输入:** L = 6，R = 30
> T3】输出: 12

**天真方法:**最简单的方法是迭代范围 **L** 到 **R** 找到所有数字的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)并检查每个数字，如果它们的二进制表示中的第一个和最后一个数字相同或不相同。
***时间复杂度:** O((R-L)日志(R-L))*
***辅助空间:** O(1)*

**有效方法:**给定的问题可以基于以下观察来解决:

*   奇数在其二进制表示中总是以 **1** 结尾。
*   在二进制表示中，每个数字的起始位都是 **1** 。
*   因此，问题简化为[寻找给定范围内奇数的计数。](https://www.geeksforgeeks.org/count-odd-and-even-numbers-in-a-range-from-l-to-r/)

按照以下步骤解决问题:

*   在范围**【1，R】**中找到奇数的[计数，并将其存储在变量中，比如 **X** 。](https://www.geeksforgeeks.org/count-odd-and-even-numbers-in-a-range-from-l-to-r/)
*   同样，[求范围](https://www.geeksforgeeks.org/count-odd-and-even-numbers-in-a-range-from-l-to-r/)**【1，L–1】**内奇数的计数。顺其自然 **Y** 。
*   打印**X–Y**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count numbers in range
// [L, R] having same first and last
// digit in the binary representation
void Count_numbers(int L, int R)
{
    int count = (R - L) / 2;

    if (R % 2 != 0 || L % 2 != 0)
        count += 1;

    cout << count << endl;
}

// Drivers code
int main()
{

    // Given range [L, R]
    int L = 6, R = 30;

    // Function Call
    Count_numbers(L, R);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to count numbers in range
// [L, R] having same first and last
// digit in the binary representation
static void Count_numbers(int L, int R)
{
    int count = (R - L) / 2;
    if (R % 2 != 0 || L % 2 != 0)
        count += 1;
    System.out.print(count);
}

// Driver code
public static void main(String[] args)
{
    // Given range [L, R]
    int L = 6, R = 30;

    // Function Call
    Count_numbers(L, R);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count numbers in range
# [L, R] having same first and last
# digit in the binary representation
def Count_numbers(L, R) :  
    count = (R - L) // 2
    if (R % 2 != 0 or L % 2 != 0) :
        count += 1
    print(count)

# Drivers code

# Given range [L, R]
L = 6
R = 30

# Function Call
Count_numbers(L, R)

# This code is contributed by code_hunt.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to count numbers in range
// [L, R] having same first and last
// digit in the binary representation
static void Count_numbers(int L, int R)
{
    int count = (R - L) / 2;
    if (R % 2 != 0 || L % 2 != 0)
        count += 1;
    Console.Write(count);
}

// Driver code
public static void Main(String[] args)
{

    // Given range [L, R]
    int L = 6, R = 30;

    // Function Call
    Count_numbers(L, R);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to count numbers in range
    // [L, R] having same first and last
    // digit in the binary representation
    function Count_numbers(L , R)
    {
        var count = (R - L) / 2;
        if (R % 2 != 0 || L % 2 != 0)
            count += 1;
        document.write(count);
    }

    // Driver code

        // Given range [L, R]
        var L = 6, R = 30;

        // Function Call
        Count_numbers(L, R);

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)