# 检查一个数是否能被 47 整除

> 原文:[https://www . geeksforgeeks . org/check-如果一个数字被 47 整除或不被整除/](https://www.geeksforgeeks.org/check-if-a-number-is-divisible-by-47-or-not/)

给定一个数 **N** ，任务是检查这个数是否能被 47 整除。
**例:**

> **输入:** N = 1645
> **输出:**是
> **解释:**
> 47 * 35 = 1645
> **输入:** N = 4606
> **输出:**是
> **解释:**
> 47 * 98 = 4606

**方法:**47 的可除性检验为:

1.  提取最后一位数字。
2.  从去掉最后一个数字后得到的剩余数字中减去 **14 *最后一个数字**。
3.  重复上述步骤，直到得到一个两位数或零。
4.  如果两位数能被 47 整除，或者是 0，那么原始数也能被 47 整除。

**例如:**

```
If N = 59173

Step 1:
  N = 59173
  Last digit = 3
  Remaining number = 5917
  Subtracting 14 times last digit
  Resultant number = 5917 - 14*3 = 5875

Step 2:
  N = 5875
  Last digit = 5
  Remaining number = 587
  Subtracting 14 times last digit
  Resultant number = 587 - 14*5 = 517

Step 3:
  N = 517
  Last digit = 7
  Remaining number = 51
  Subtracting 14 times last digit
  Resultant number = 51 - 14*7 = -47

Step 4:
  N = -47
  Since N is a two-digit number,
  and -47 is divisible by 47

Therefore N = 59173 is also divisible by 47
```

以下是上述方法的实现:

## C++

```
// C++ program to check whether a number
// is divisible by 47 or not
#include<bits/stdc++.h>
#include<stdlib.h>

using namespace std;

// Function to check if the number is  divisible by 47 or not
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

        // Subtracting fourteen times the last
        // digit to the remaining number
        n = abs(n-(d * 14));
    }
    // Finally return if the two-digit
    // number is divisible by 47 or not
    return (n % 47 == 0) ;
}

// Driver Code
int main() {
    int N = 59173;

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
// is divisible by 47 or not
import java.util.*;

class GFG{

// Function to check if the number is  divisible by 47 or not
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

        // Subtracting fourteen times the last
        // digit to the remaining number
        n = Math.abs(n - (d * 14));
    }

    // Finally return if the two-digit
    // number is divisible by 47 or not
    return (n % 47 == 0) ;
}

// Driver Code
public static void main(String[] args) {
    int N = 59173;

    if (isDivisible(N))
        System.out.print("Yes") ;
    else
        System.out.print("No");

 }    
}   

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python program to check if a number
# is divisible by 47 or not

# Function to check if the number is
# divisible by 47 or not
def isDivisible(n) :

    # While there are at least two digits
    while n // 100 :

        # Extracting the last
        d = n % 10

        # Truncating the number
        n //= 10

        # Subtracting fourteen times the last
        # digit to the remaining number
        n = abs(n- (d * 14))

    # Finally return if the two-digit
    # number is divisible by 43 or not
    return (n % 47 == 0)

# Driver Code
if __name__ == "__main__" :

    n = 59173

    if (isDivisible(n)) :
        print("Yes")
    else :
        print("No")
```

## C#

```
// C# program to check whether a number
// is divisible by 47 or not
using System;

class GFG
{

// Function to check if the number is divisible by 47 or not
static bool isDivisible(int n)
{
    int d;

    // While there are at least two digits
    while (n / 100 > 0)
    {

        // Extracting the last
        d = n % 10;

        // Truncating the number
        n /= 10;

        // Subtracting fourteen times the last
        // digit to the remaining number
        n = Math.Abs(n - (d * 14));
    }

    // Finally return if the two-digit
    // number is divisible by 47 or not
    return (n % 47 == 0);
}

// Driver Code
public static void Main()
{
    int N = 59173;

    if (isDivisible(N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>
// Javascript program to check whether a number
// is divisible by 47 or not

// Function to check if the number is  divisible by 47 or not
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

        // Subtracting fourteen times the last
        // digit to the remaining number
        n = Math.abs(n - (d * 14));
    }

    // Finally return if the two-digit
    // number is divisible by 47 or not
    return (n % 47 == 0) ;
}

// Driver Code

    let N = 59173;

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