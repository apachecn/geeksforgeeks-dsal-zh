# 给定 LCM 和 HCF 时找到另一个数字

> 原文:[https://www . geeksforgeeks . org/find-the-other-number-when-LCM-and-hcf-given/](https://www.geeksforgeeks.org/find-the-other-number-when-lcm-and-hcf-given/)

给定一个数字 **A** 和 [L.C.M](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) 和 [H.C.F.](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 任务是确定另一个数字 B.
**示例:**

```
Input: A = 10, Lcm = 10, Hcf = 50.
Output: B = 50

Input: A = 5, Lcm = 25, Hcf = 4.
Output: B = 20
```

**公式:-**

> A * B = LCM * HCF
> B =(LCM * HCF)/A
> 例:A = 15，B = 12
> HCF = 3，LCM = 60
> 我们可以看到 3 * 60 = 15 * 12。
> **这个公式是怎么用的？**
> 既然 HCF 把两个数都除了，那就让。
> A = HCF * x
> B = HCF * y
> 注意 x 和 y 不是共同的因素，所以 LCM 必须包含 HCF、x 和 y
> 这样就可以得出结论。
> LCM = HCF * x * y
> 所以 LCM * HCF = HCF * x * y * HCF 等于 A * B

以下是上述方法的实现:

## C++

```
// CPP program to find other number from given
// HCF and LCM
#include <bits/stdc++.h>
using namespace std;

// Function that will calculates
// the zeroes at the end
int otherNumber(int A, int Lcm, int Hcf)
{
    return (Lcm * Hcf) / A;
}

// Driver code
int main()
{
    int A = 8, Lcm = 8, Hcf = 1;

    // Calling function.
    int result = otherNumber(A, Lcm, Hcf);

    cout << "B = " << result;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find other number from given
// HCF and LCM
class GFG{

// Function that will calculates
// the zeroes at the end
static int otherNumber(int A, int Lcm, int Hcf)
{
    return (Lcm * Hcf) / A;
}

// Driver code
public static void main(String args[])
{
    int A = 8, Lcm = 8, Hcf = 1;

    // Calling function.
    int result = otherNumber(A, Lcm, Hcf);

    System.out.println("B = "+ result);

}
}
```

## 蟒蛇 3

```
# Python 3 program to find other
# number from given HCF and LCM

# Function that will calculates
# the zeroes at the end
def otherNumber(a, Lcm, Hcf):
    return (Lcm * Hcf) // A

# Driver code
A = 8; Lcm = 8; Hcf = 1

# Calling function
result = otherNumber(A, Lcm, Hcf)
print("B =", result)

# This code is contributed
# by Shrikant13
```

## C#

```
// C# program to find other number
// from given HCF and LCM
using System;

class GFG
{

// Function that will calculates
// the zeroes at the end
static int otherNumber(int A, int Lcm,
                              int Hcf)
{
    return (Lcm * Hcf) / A;
}

// Driver code
static public void Main(String []args)
{
    int A = 8, Lcm = 8, Hcf = 1;

    // Calling function.
    int result = otherNumber(A, Lcm, Hcf);

    Console.WriteLine("B = " + result);
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find other number
// from given HCF and LCM

// Function that will calculates
// the zeroes at the end
function otherNumber($A, $Lcm, $Hcf)
{
    return ($Lcm * $Hcf) / $A;
}

// Driver code
$A = 8; $Lcm = 8; $Hcf = 1;

// Calling function.
$result = otherNumber($A, $Lcm, $Hcf);

echo "B = " . $result;

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript program to find other number from given
// HCF and LCM

// Function that will calculates
// the zeroes at the end
function otherNumber(A, Lcm, Hcf)
{
    return (Lcm * Hcf) / A;
}

// Driver code

    let A = 8, Lcm = 8, Hcf = 1;

    // Calling function.
    let result = otherNumber(A, Lcm, Hcf);

    document.write("B = " + result);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
B = 1
```