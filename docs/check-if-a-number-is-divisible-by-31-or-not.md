# 检查一个数是否能被 31 整除

> 原文:[https://www . geesforgeks . org/check-如果一个数能被 31 整除或不能被 31 整除/](https://www.geeksforgeeks.org/check-if-a-number-is-divisible-by-31-or-not/)

给定一个数 **N** ，任务是检查这个数是否能被 31 整除。
**例:**

> **输入:** N = 1922
> **输出:**是
> **说明:**
> 31 * 62 = 1922
> **输入:** N = 2722400
> **输出:**否

**方法:**31 的可除性检验为:

1.  提取最后一位数字。
2.  从去掉最后一个数字后得到的剩余数字中减去 **3 *最后一个数字**。
3.  重复上述步骤，直到得到一个两位数或零。
4.  如果两位数能被 31 整除，或者是 0，那么原始数也能被 31 整除。

**例如:**

```
If N = 49507

Step 1:
  N = 49507
  Last digit = 7
  Remaining number = 4950
  Subtracting 3 times last digit
  Resultant number = 4950 - 3*7 = 4929

Step 2:
  N = 4929
  Last digit = 9
  Remaining number = 492
  Subtracting 3 times last digit
  Resultant number = 492 - 3*9 = 465

Step 3:
  N = 465
  Last digit = 5
  Remaining number = 46
  Subtracting 3 times last digit
  Resultant number = 46 - 3*5 = 31

Step 4:
  N = 31
  Since N is a two-digit number,
  and 31 is divisible by 31

Therefore N = 49507 is also divisible by 31
```

以下是上述方法的实现:

## C++

```
// C++ program to check whether a number
// is divisible by 31 or not
#include<bits/stdc++.h>
#include<stdlib.h>

using namespace std;

// Function to check if the number is divisible by 31 or not
bool isDivisible(int n)
{
    int d;

    // While there are at least two digits
    while (n / 100)
    {

        // Extracting the last
        d = n % 10;

        // Truncating the number
        n /= 10;

        // Subtracting three times the last
        // digit to the remaining number
        n = abs(n-(d * 3));
    }

    // Finally return if the two-digit
    // number is divisible by 31 or not
    return (n % 31 == 0) ;
}

// Driver Code
int main()
{
    int N = 1922;

    if (isDivisible(N))
        cout<<"Yes"<<endl ;
    else
        cout<<"No"<<endl ;

    return 0;    
}

// This code is contributed by ANKITKUMAR34
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a number
// is divisible by 31 or not
import java.util.*;

class GFG{

// Function to check if the number is divisible by 31 or not
static boolean isDivisible(int n)
{
    int d;

    // While there are at least two digits
    while ((n / 100) > 0)
    {

        // Extracting the last
        d = n % 10;

        // Truncating the number
        n /= 10;

        // Subtracting three times the last
        // digit to the remaining number
        n = Math.abs(n - (d * 3));
    }

    // Finally return if the two-digit
    // number is divisible by 31 or not
    return (n % 31 == 0) ;
}

// Driver Code
public static void main(String[] args)
{
    int N = 1922;

    if (isDivisible(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}    
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python program to check whether a number
# is divisible by 31 or not

# Function to check if the number is
# divisible by 31 or not
def isDivisible(n) :

    # While there are at least two digits
    while n // 100 :

        # Extracting the last
        d = n % 10

        # Truncating the number
        n //= 10

        # Subtracting three times the last
        # digit to the remaining number
        n = abs(n-(d * 3))

    # Finally return if the two-digit
    # number is divisible by 31 or not
    return (n % 31 == 0)

# Driver Code
if __name__ == "__main__" :

    n = 1922

    if (isDivisible(n)) :
        print("Yes")
    else :
        print("No")
```

## C#

```
// C# program to check whether a number
// is divisible by 31 or not
using System;

class GFG{

// Function to check if the number is divisible by 31 or not
static bool isDivisible(int n)
{
    int d;

    // While there are at least two digits
    while ((n / 100) > 0)
    {

        // Extracting the last
        d = n % 10;

        // Truncating the number
        n /= 10;

        // Subtracting three times the last
        // digit to the remaining number
        n = Math.Abs(n - (d * 3));
    }

    // Finally return if the two-digit
    // number is divisible by 31 or not
    return (n % 31 == 0) ;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 1922;

    if (isDivisible(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}    
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to check whether a number
// is divisible by 31 or not

// Function to check if the number is divisible by 31 or not
function isDivisible(n)
{
    let d;

    // While there are at least two digits
    while (Math.floor(n / 100) > 0)
    {

        // Extracting the last
        d = n % 10;

        // Truncating the number
        n = Math.floor(n / 10);

        // Subtracting three times the last
        // digit to the remaining number
        n = Math.abs(n - (d * 3));
    }

    // Finally return if the two-digit
    // number is divisible by 31 or not
    return (n % 31 == 0) ;
}

// Driver Code

    let N = 1922;

    if (isDivisible(N) != 0)
        document.write("Yes") ;
    else
        document.write("No");

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
Yes
```

时间复杂度:0(对数 <sub>10</sub> N)

辅助空间:0(1)