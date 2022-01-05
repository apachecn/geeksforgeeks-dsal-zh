# 检查给定的数是否能被 71 整除

> 原文:[https://www . geeksforgeeks . org/check-如果给定的数字可被 71 整除或不可被整除/](https://www.geeksforgeeks.org/check-if-the-given-number-is-divisible-by-71-or-not/)

给定一个数 **N** ，任务是检查这个数是否能被 71 整除。

**示例:**

> **输入:**N = 25411681
> T3】输出:是
> T6】说明:T8】71 * 357911 = 25411681
> 
> **输入:**N = 5041
> T3】输出:是
> T6】说明:T8】71 * 71 = 5041

**方法:**71 的可除性检验为:

1.  提取最后一位数字。
2.  从去掉最后一个数字后得到的剩余数字中减去 **7 *最后一个数字**。
3.  重复上述步骤，直到得到一个两位数或零。
4.  如果两位数能被 71 整除，或者是 0，那么原始数也能被 71 整除。

**例如:**

```
If N = 5041

Step 1:
  N = 5041
  Last digit = 1
  Remaining number = 504
  Subtracting 7 times last digit
  Resultant number = 504 - 7*1 = 497

Step 2:
  N = 497
  Last digit = 7
  Remaining number = 49
  Subtracting 7 times last digit
  Resultant number = 49 - 7*7 = 0

Step 3:
  N = 0
  Since N is a two-digit number,
  and 0 is divisible by 71

Therefore N = 5041 is also divisible by 71
```

下面是上述方法的实现:

## C++

```
// C++ program to check whether a number
// is divisible by 71 or not
#include<bits/stdc++.h>
#include<stdlib.h>

using namespace std;

// Function to check if the number is divisible by 71 or not
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

        // Subtracting seven times the last
        // digit to the remaining number
        n = abs(n - (d * 7));
    }
    // Finally return if the two-digit
    // number is divisible by 71 or not
    return (n % 71 == 0) ;
}

// Driver Code
int main() {
    int N = 5041;

    if (isDivisible(N))
        cout << "Yes" << endl ;
    else
        cout << "No" << endl ;

    return 0;    
}

// This code is contributed by ANKITKUMAR34
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a number
// is divisible by 71 or not
import java.util.*;

class GFG{

// Function to check if the number is divisible by 71 or not
    static boolean isDivisible(int n)
    {
        int d;
        // While there are at least two digits
        while ((n / 100) <=0)
        {

            // Extracting the last
            d = n % 10;

            // Truncating the number
            n /= 10;

            // Subtracting seven times the last
            // digit to the remaining number
            n = Math.abs(n - (d * 7));
        }

        // Finally return if the two-digit
        // number is divisible by 71 or not
        return (n % 71 == 0) ;
    }

    // Driver Code
    public static void main(String args[]){
        int N = 5041;

        if (isDivisible(N))
            System.out.println("Yes") ;
        else
            System.out.println("No");
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python program to check whether a number
# is divisible by 71 or not

# Function to check if the number is
# divisible by 71 or not
def isDivisible(n) :

    # While there are at least two digits
    while n // 100 :

        # Extracting the last
        d = n % 10

        # Truncating the number
        n //= 10

        # Subtracting seven times the last
        # digit to the remaining number
        n = abs(n-(d * 7))

    # Finally return if the two-digit
    # number is divisible by 71 or not
    return (n % 71 == 0)

# Driver Code
if __name__ == "__main__" :

    N = 5041

    if (isDivisible(N)) :
        print("Yes")
    else :
        print("No")
```

## C#

```
// C# program to check whether a number
// is divisible by 71 or not
using System;

class GFG
{

// Function to check if the number is divisible by 71 or not
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
        n = Math.Abs(n - (d * 7));
    }

    // Finally return if the two-digit
    // number is divisible by 71 or not
    return (n % 71 == 0);
}

// Driver Code
public static void Main()
{
    int N = 5041;

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
// is divisible by 71 or not

// Function to check if the number is divisible by 71 or not
function isDivisible(n)
{
    let d;
        // While there are at least two digits
        while (Math.floor(n / 100) <=0)
        {

            // Extracting the last
            d = n % 10;

            // Truncating the number
            n = Math.floor(n/10);

            // Subtracting seven times the last
            // digit to the remaining number
            n = Math.abs(n - (d * 7));
        }

        // Finally return if the two-digit
        // number is divisible by 71 or not
        return (n % 71 == 0) ;
}

// Driver Code
let N = 5041;
if (isDivisible(N))
    document.write("Yes") ;
else
    document.write("No");

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Yes
```