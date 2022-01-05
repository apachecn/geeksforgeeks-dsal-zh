# 自身编号

> 原文:[https://www.geeksforgeeks.org/self-numbers/](https://www.geeksforgeeks.org/self-numbers/)

一个数 **N** 如果不能写成**M+M 的位数之和**对于任意 M
前几个自号是:

> 1, 3, 5, 7, 9, 20, 31, 42…………….

### 检查 N 是否为自编号

给定一个整数 **N** ，任务是找出这个数是不是 Self 数。
**例:**

> **输入:** N = 3
> **输出:**是
> **说明:**
> 1+sumofDigits(1)= 2
> 2+sumofDigits(2)= 4
> 3+sumofDigits(3)= 6
> 因此 3 不能写成
> m +任意 m 的 m 位数之和。
> **输入:** N = 4
> **输出**

**逼近**:思路是从 1 迭代到 N，对于每个数字，检查其值和其位数之和是否等于 N。如果是，则该号码不是自己的号码。否则，这个数就是一个自数。
**例如:**

> 如果 N = 3
> //检查每个数字
> //从 1 到 N
> 1+sumofDigits(1)= 1
> 2+sumofDigits(2)= 4
> 3+sumofDigits(3)= 6
> 因此 3 不能写成
> M +任何 M 的 M 位数之和

下面是上述方法的实现:

**例:**

## C++

```
// C++ implementation to check if the
// number is a self number or not

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of
// digits of a number N
int getSum(int n)
{
    int sum = 0;
    while (n != 0) {
        sum = sum + n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to check for Self number
bool isSelfNum(int n)
{
    for (int m = 1; m <= n; m++) {
        if (m + getSum(m) == n)
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int n = 20;

    if (isSelfNum(n)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if the
// number is a self number or not
class GFG{

// Function to find the sum
// of digits of a number N
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum = sum + n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to check for Self number
static boolean isSelfNum(int n)
{
    for(int m = 1; m <= n; m++)
    {
       if (m + getSum(m) == n)
           return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int n = 20;

    if (isSelfNum(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 implementation to check if the
# number is a self number or not

# Function to find the sum of
# digits of a number N
def getSum(n):

    sum1 = 0;
    while (n != 0):
        sum1 = sum1 + n % 10;
        n = n // 10;

    return sum1;

# Function to check for Self number
def isSelfNum(n):

    for m in range(1, n + 1):
        if (m + getSum(m) == n):
            return False;

    return True;

# Driver code
n = 20;

if (isSelfNum(n)):
    print("Yes");

else:
    print("No");

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to check if the
// number is a self number or not
using System;
class GFG{

// Function to find the sum
// of digits of a number N
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum = sum + n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to check for Self number
static bool isSelfNum(int n)
{
    for(int m = 1; m <= n; m++)
    {
       if (m + getSum(m) == n)
           return false;
    }
    return true;
}

// Driver code
public static void Main()
{
    int n = 20;

    if (isSelfNum(n))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation to check if the
// number is a self number or not

    // Function to find the sum
    // of digits of a number N
    function getSum( n)
    {
        let sum = 0;
        while (n != 0)
        {
            sum = sum + n % 10;
            n = parseInt(n / 10);
        }
        return sum;
    }

    // Function to check for Self number
    function isSelfNum( n) {
        for ( let m = 1; m <= n; m++) {
            if (m + getSum(m) == n)
                return false;
        }
        return true;
    }

    // Driver code    
    let n = 20;

    if (isSelfNum(n)) {
        document.write("Yes");
    } else {
        document.write("No");
    }

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log <sub>10</sub> N)*

***辅助空间:** O(1)*

**参考文献:**T2https://en.wikipedia.org/wiki/Self_number