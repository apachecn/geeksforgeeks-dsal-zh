# 查找给定电话号码的最后两位缺失数字

> 原文:[https://www . geesforgeks . org/find-给定电话号码的最后两位缺失数字/](https://www.geeksforgeeks.org/find-the-last-two-missing-digits-of-the-given-phone-number/)

给定一个电话号码的八位数字为整数 **N** ，任务是当最后两位数字为给定的八位数字之和时，找出缺失的最后两位数字并打印出完整的号码。
**例:**

> **输入:** N = 98765432
> **输出:** 9876543244
> **输入:** N = 10000000
> **输出:**100000001

**进场:**

*   使用模 10 运算符(%10)从 N 中逐个获取电话号码的八位数字。
*   将这些数字加在一个变量中，比如 **sum** ，得到这八个数字的总和。
*   现在，有两种情况:
    *   如果**加上< 10** ，那么它就是一个位数，即在开头插入 **0** ，使其成为两位数，而不影响数值。
    *   Else **sum** 是最后两位数字代表的数字。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <iostream>
using namespace std;

// Function to find the last two
// digits of the number and
// print the complete number
void findPhoneNumber(int n)
{

    int temp = n;
    int sum;

    // Sum of the first eight
    // digits of the number
    while (temp != 0) {
        sum += temp % 10;
        temp = temp / 10;
    }

    // if sum < 10, then the two digits
    // are '0' and the value of sum
    if (sum < 10)
        cout << n << "0" << sum;

    // if sum > 10, then the two digits
    // are the value of sum
    else
        cout << n << sum;
}

// Driver code
int main()
{
    long int n = 98765432;

    findPhoneNumber(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the last two
// digits of the number and
// print the complete number
static void findPhoneNumber(int n)
{

    int temp = n;
    int sum = 0;

    // Sum of the first eight
    // digits of the number
    while (temp != 0)
    {
        sum += temp % 10;
        temp = temp / 10;
    }

    // if sum < 10, then the two digits
    // are '0' and the value of sum
    if (sum < 10)
        System.out.print(n + "0" + sum);

    // if sum > 10, then the two digits
    // are the value of sum
    else
        System.out.print(n +""+ sum);
}

// Driver code
public static void main(String[] args)
{
    int n = 98765432;

    findPhoneNumber(n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to find the last two
# digits of the number and
# print the complete number
def findPhoneNumber(n):
    temp = n
    sum = 0

    # Sum of the first eight
    # digits of the number
    while (temp != 0):
        sum += temp % 10
        temp = temp // 10

    # if sum < 10, then the two digits
    # are '0' and the value of sum
    if (sum < 10):
        print(n,"0",sum)

    # if sum > 10, then the two digits
    # are the value of sum
    else:
        n = str(n)
        sum = str(sum)
        n += sum
        print(n)

# Driver code
if __name__ == '__main__':
    n = 98765432

    findPhoneNumber(n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the last two
// digits of the number and
// print the complete number
static void findPhoneNumber(int n)
{
    int temp = n;
    int sum = 0;

    // Sum of the first eight
    // digits of the number
    while (temp != 0)
    {
        sum += temp % 10;
        temp = temp / 10;
    }

    // if sum < 10, then the two digits
    // are '0' and the value of sum
    if (sum < 10)
        Console.Write(n + "0" + sum);

    // if sum > 10, then the two digits
    // are the value of sum
    else
        Console.Write(n + "" + sum);
}

// Driver code
static public void Main ()
{
    int n = 98765432;

    findPhoneNumber(n);
}
}

// This code is contributed by jit_t
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the last two
// digits of the number and
// print the complete number
function findPhoneNumber(n)
{

    let temp = n;
    let sum=0;

    // Sum of the first eight
    // digits of the number
    while (temp != 0) {
        sum += temp % 10;
        temp = Math.floor(temp / 10);
    }

    // if sum < 10, then the two digits
    // are '0' and the value of sum
    if (sum < 10)
        document.write(n + "0" + sum);

    // if sum > 10, then the two digits
    // are the value of sum
    else
        document.write(n + "" + sum);
}

// Driver code

    let n = 98765432;

    findPhoneNumber(n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
9876543244
```