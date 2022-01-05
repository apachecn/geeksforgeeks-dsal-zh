# 从 1 到 n 的数字的最接近和划分(分成两个子集)

> 原文:[https://www . geeksforgeeks . org/最接近的从 1 到 n 的两个数字子集的和划分/](https://www.geeksforgeeks.org/closest-sum-partition-into-two-subsets-of-numbers-from-1-to-n/)

给定一个整数序列 **1，2，3，4，…，n** 。任务是将它分成两组 **A** 和 **B** ，每个元素恰好属于一组，**| sum(A)–sum(B)|**是最小可能。打印**| sum(A)–sum(B)|**的值。
**举例:**

> **输入:**3
> T3】输出: 0
> A = {1，2}和 B = { 3 } ans | sum(A)–sum(B)| = | 3–3 | = 0。
> **输入:** 6
> **输出:** 0
> A = {1，3，4}和 B = {2，5 } ans | sum(A)–sum(B)| = | 3–3 | = 0。
> **输入:** 5
> **输出:** 1

**进场:**取**mod = n % 4**

1.  如果 **mod = 0** 或 **mod = 3** ，则打印 **0** 。
2.  如果 **mod = 1** 或 **mod = 2** ，则打印 **1** 。

这是因为这些组将被选择为 A = {N，N–3，N–4，N–7，N–8，…..}，B = { N–1，N–2，N–5，N–6，…..}
从 N 到 1 开始，将第一个元素放在 A 组，然后每隔 2 个元素在 B，A，B，A，…..

*   当 **n % 4 = 0 时:** N = 8，A = {1，4，5，8}和 B = {2，3，6，7}
*   当 **n % 4 = 1:** N = 9，A = {1，4，5，8，9}和 B = {2，3，6，7}
*   当 **n % 4 = 2:** N = 10 时，A = {1，4，5，8，9}和 B = {2，3，6，7，10}
*   当 **n % 4 = 3:** N = 11 时，A = {1，4，5，8，9}和 B = {2，3，6，7，10，11}

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum required
// absolute difference
int minAbsDiff(int n)
{
    int mod = n % 4;

    if (mod == 0 || mod == 3)
        return 0;

    return 1;
}

// Driver code
int main()
{
    int n = 5;
    cout << minAbsDiff(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum required
// absolute difference

    static int minAbsDiff(int n)
    {
        int mod = n % 4;
        if (mod == 0 || mod == 3)
        {
            return 0;
        }
        return 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(minAbsDiff(n));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum required
# absolute difference
def minAbsDiff(n) :
    mod = n % 4;

    if (mod == 0 or mod == 3) :
        return 0;

    return 1;

# Driver code
if __name__ == "__main__" :

    n = 5;
    print(minAbsDiff(n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{

    // Function to return the minimum 
    // required absolute difference
    static int minAbsDiff(int n)
    {
        int mod = n % 4;
        if (mod == 0 || mod == 3)
        {
            return 0;
        }
        return 1;
    }

    // Driver code
    static public void Main ()
    {
        int n = 5;
        Console.WriteLine(minAbsDiff(n));
    }
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// required absolute difference
function minAbsDiff($n)
{
    $mod = $n % 4;

    if ($mod == 0 || $mod == 3)
        return 0;

    return 1;
}

// Driver code
$n = 5;
echo minAbsDiff($n);

// This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to return the minimum 
    // required absolute difference
    function minAbsDiff(n)
    {
        let mod = n % 4;
        if (mod == 0 || mod == 3)
        {
            return 0;
        }
        return 1;
    }

    let n = 5;
      document.write(minAbsDiff(n));

</script>
```

**Output:** 

```
1
```