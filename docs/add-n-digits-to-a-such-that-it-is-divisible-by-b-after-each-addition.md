# 将 N 个数字加到 A 上，使其在每次相加后可被 B 整除

> 原文:[https://www . geeksforgeeks . org/add-n-digits-to-a-so-it-by-b 每次相加后可被除尽/](https://www.geeksforgeeks.org/add-n-digits-to-a-such-that-it-is-divisible-by-b-after-each-addition/)

给定三个整数 **A** 、 **B** 和 **N** ，重复以下过程 **N** 次:

1.  给 **A** 加一个数字，这样加完之后， **A** 可以被 **B** 整除。
2.  经过上述操作的 **N** 次迭代后，打印出 **A** 可能的最小值。
3.  如果操作失败，打印 **-1** 。

注意:我们需要在每次数字相加后检查可除性。
**例:**

> **输入:** A = 10，B = 11，N = 1
> **输出:** -1
> 无论你加什么数字，10X 永远不会被 11 整除。
> **输入:** A = 5，B = 3，N = 3
> **输出:** 5100

**方法:**对于要从 **0** 添加到 **9** 的第一个数字，如果没有一个数字使 **A** 被 **B** 整除，那么答案是 **-1** 。否则加上满足条件的第一位数字，然后再加上 **0** 之后的 **(n-1)** 次，因为如果 **A** 被 **B** 整除，那么 **A*10，A*100，…** 也会被 **B** 整除。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int addNDigits(int a, int b, int n)
{
    int num = a;

    // Try all digits from (0 to 9)
    for (int i = 0; i <= 9; i++) {
        int tmp = a * 10 + i;
        if (tmp % b == 0) {
            a = tmp;
            break;
        }
    }

    // Fails in the first move itself
    if (num == a)
        return -1;

    // Add (n-1) 0's
    for (int j = 0; j < n - 1; j++)
        a *= 10;

    return a;
}

// Driver Program to test above function
int main()
{
    int a = 5, b = 3, n = 3;
    cout << addNDigits(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
  //Java implementation of the approach

import java.io.*;

class GFG {

static int addNDigits(int a, int b, int n)
{
    int num = a;

    // Try all digits from (0 to 9)
    for (int i = 0; i <= 9; i++) {
        int tmp = a * 10 + i;
        if (tmp % b == 0) {
            a = tmp;
            break;
        }
    }

    // Fails in the first move itself
    if (num == a)
        return -1;

    // Add (n-1) 0's
    for (int j = 0; j < n - 1; j++)
        a *= 10;

    return a;
}

// Driver Program to test above function

    public static void main (String[] args) {
    int a = 5, b = 3, n = 3;
    System.out.print( addNDigits(a, b, n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def addNDigits(a, b, n) :

    num = a

    # Try all digits from (0 to 9)
    for i in range(10) :
        tmp = a * 10 + i

        if (tmp % b == 0) :
            a = tmp
            break

    # Fails in the first move itself
    if (num == a) :
        return -1

    # Add (n-1) 0's
    for j in range(n - 1) :
        a *= 10

    return a

# Driver Code
if __name__ == "__main__" :

    a = 5
    b = 3
    n = 3

    print(addNDigits(a, b, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int addNDigits(int a,
                      int b, int n)
{
    int num = a;

    // Try all digits from (0 to 9)
    for (int i = 0; i <= 9; i++)
    {
        int tmp = a * 10 + i;
        if (tmp % b == 0)
        {
            a = tmp;
            break;
        }
    }

    // Fails in the first move itself
    if (num == a)
        return -1;

    // Add (n-1) 0's
    for (int j = 0; j < n - 1; j++)
        a *= 10;

    return a;
}

// Driver Code
public static void Main ()
{
    int a = 5, b = 3, n = 3;
    Console.WriteLine(addNDigits(a, b, n));
}
}

// This code is contributed
// by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

function addNDigits($a, $b, $n)
{
    $num = $a;

    // Try all digits from (0 to 9)
    for ($i = 0; $i <= 9; $i++)
    {
        $tmp = $a * 10 + $i;
        if ($tmp % $b == 0)
        {
            $a = $tmp;
            break;
        }
    }

    // Fails in the first move itself
    if ($num == $a)
        return -1;

    // Add (n-1) 0's
    for ($j = 0; $j < $n - 1; $j++)
        $a *= 10;

    return $a;
}

// Driver Code
$a = 5; $b = 3; $n = 3;
echo addNDigits($a, $b, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    function addNDigits(a, b, n)
    {
        let num = a;

        // Try all digits from (0 to 9)
        for (let i = 0; i <= 9; i++)
        {
            let tmp = a * 10 + i;
            if (tmp % b == 0)
            {
                a = tmp;
                break;
            }
        }

        // Fails in the first move itself
        if (num == a)
            return -1;

        // Add (n-1) 0's
        for (let j = 0; j < n - 1; j++)
            a *= 10;

        return a;
    }

    let a = 5, b = 3, n = 3;
    document.write(addNDigits(a, b, n));

</script>
```

**Output:** 

```
5100
```