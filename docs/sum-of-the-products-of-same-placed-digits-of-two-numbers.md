# 两个数字相同位置数字的乘积之和

> 原文:[https://www . geeksforgeeks . org/两位数乘积之和/](https://www.geeksforgeeks.org/sum-of-the-products-of-same-placed-digits-of-two-numbers/)

给定两个正整数 **N1 和 N2** ，任务是求这两个数相同位置数字的乘积之和。
**注:**长度不等的数字，较小数字的前几位需要按 0 处理。
**例:**

> **输入:** N1 = 5，N2 = 67
> **输出:** 35
> **说明:**
> 在原地，我们有数字 5 和 7，他们的乘积是 35。在 10 的位置，我们在 N2 有 6 个。由于 **N1** 在十位没有数字，所以 6 会乘以 0，对总和没有影响。因此，计算出的总和是 35。
> **输入:** N1 = 25，N2 = 1548
> **输出:** 48
> **解释:**
> 总和= 5 * 8 + 2 * 4 + 0 * 5 + 0 * 1 = 48。

**进场:**
要解决上面提到的问题，我们需要按照以下步骤:

*   提取这两个数字最右边的数字并相乘，将它们的乘积加到**和**上。
*   现在去掉数字。
*   继续重复以上两个步骤，直到其中一个减少到 0。然后，打印计算出的**和**的最终值。

以下是上述方法的实现:

## C++

```
// C++ program to calculate the
// sum of same placed digits
// of two numbers
#include <bits/stdc++.h>
using namespace std;

int sumOfProductOfDigits(int n1, int n2)
{
    int sum = 0;

    // Loop until one of the numbers
    // have no digits remaining
    while (n1 > 0 && n2 > 0)
    {
        sum += ((n1 % 10) * (n2 % 10));
        n1 /= 10;
        n2 /= 10;
    }
    return sum;
}

// Driver Code
int main()
{
    int n1 = 25;
    int n2 = 1548;

    cout << sumOfProductOfDigits(n1, n2);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the
// sum of same placed digits of
// two numbers

class GFG {

    // Function to find the sum of the
    // products of their corresponding digits
    static int sumOfProductOfDigits(int n1,
                                    int n2)
    {
        int sum = 0;
        // Loop until one of the numbers
        // have no digits remaining
        while (n1 > 0 && n2 > 0) {
            sum += ((n1 % 10) * (n2 % 10));
            n1 /= 10;
            n2 /= 10;
        }

        return sum;
    }

    // Driver Code
    public static void main(String args[])
    {

        int n1 = 25;
        int n2 = 1548;

        System.out.println(
            sumOfProductOfDigits(n1, n2));
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate the
# sum of same placed digits
# of two numbers

def sumOfProductOfDigits(n1, n2):

    sum1 = 0;

    # Loop until one of the numbers
    # have no digits remaining
    while (n1 > 0 and n2 > 0):

        sum1 += ((n1 % 10) * (n2 % 10));
        n1 = n1 // 10;
        n2 = n2 // 10;

    return sum1;

# Driver Code
n1 = 25;
n2 = 1548;

print(sumOfProductOfDigits(n1, n2));

# This code is contributed by Nidhi_biet
```

## C#

```
// C# program to calculate the
// sum of same placed digits of
// two numbers
using System;
class GFG{

// Function to find the sum of the
// products of their corresponding digits
static int sumOfProductOfDigits(int n1,
                                int n2)
{
    int sum = 0;

    // Loop until one of the numbers
    // have no digits remaining
    while (n1 > 0 && n2 > 0)
    {
        sum += ((n1 % 10) * (n2 % 10));
        n1 /= 10;
        n2 /= 10;
    }
    return sum;
}

// Driver Code
public static void Main()
{
    int n1 = 25;
    int n2 = 1548;

    Console.WriteLine(
            sumOfProductOfDigits(n1, n2));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to calculate the
// sum of same placed digits
// of two numbers

function sumOfProductOfDigits(n1, n2)
{
    let sum = 0;

    // Loop until one of the numbers
    // have no digits remaining
    while (n1 > 0 && n2 > 0)
    {
        sum += ((n1 % 10) * (n2 % 10));
        n1 = Math.floor(n1/10);
        n2 = Math.floor(n2/10);
    }
    return sum;
}

// Driver Code

    let n1 = 25;
    let n2 = 1548;

    document.write(sumOfProductOfDigits(n1, n2));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
48
```