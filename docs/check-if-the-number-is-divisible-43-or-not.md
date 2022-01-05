# 检查数字是否能被 43 整除

> 原文:[https://www . geesforgeks . org/check-如果数字可被 43 整除或不可被整除/](https://www.geeksforgeeks.org/check-if-the-number-is-divisible-43-or-not/)

给定一个数 **N** ，任务是检查这个数是否能被 43 整除。
**例:**

> **输入:** N = 2795
> **输出:**是
> **解释:**
> 43 * 65 = 2795
> **输入:** N = 11094
> **输出:**是
> **解释:**
> 43 * 258 = 11094

**方法:**43 的可除性检验为:

1.  提取最后一位数字。
2.  从去掉最后一位数字后得到的剩余数字中加上 **13 *最后一位数字**。
3.  重复上述步骤，直到得到一个两位数或零。
4.  如果两位数可以被 43 整除，或者是 0，那么原数也可以被 43 整除。

**例如:**

```
If N = 11739

Step 1:
  N = 11739
  Last digit = 9
  Remaining number = 1173
  Adding 13 times last digit
  Resultant number = 1173 + 13*9 = 1290

Step 2:
  N = 1290
  Since 129 is divisible by 43 as 43 * 3 = 129

Therefore N = 11739 is also divisible by 43
```

以下是上述方法的实现:

## C++

```
// C++ program to check whether a number
// is divisible by 43 or not

#include<bits/stdc++.h>
#include<stdlib.h>

using namespace std;
// Function to check if the number is  divisible by 43 or not
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

        // adding thirteen times the last
        // digit to the remaining number
        n = abs(n+(d * 13));
    }
    // Finally return if the two-digit
    // number is divisible by 43 or not
    return (n % 43 == 0) ;
}

// Driver Code
int main() {
    int N = 2795;

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
// is divisible by 43 or not
class GFG
{

// Function to check if the number is  divisible by 43 or not
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

        // adding thirteen times the last
        // digit to the remaining number
        n = Math.abs(n+(d * 13));
    }
    // Finally return if the two-digit
    // number is divisible by 43 or not
    return (n % 43 == 0) ;
}

// Driver Code
public static void main(String[] args) {
    int N = 2795;

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
# is divisible by 43 or not

# Function to check if the number is
# divisible by 43 or not
def isDivisible(n) :

    # While there are at least two digits
    while n // 100 :

        # Extracting the last
        d = n % 10

        # Truncating the number
        n //= 10

        # Adding thirteen  times the last
        # digit to the remaining number
        n = abs(n+(d * 13))

    # Finally return if the two-digit
    # number is divisible by 43 or not
    return (n % 43 == 0)

# Driver Code
if __name__ == "__main__" :

    N = 2795

    if (isDivisible(N)):
        print("Yes")
    else :
        print("No")
```

## C#

```
// C# program to check whether a number
// is divisible by 43 or not
using System;

class GFG
{

// Function to check if the number is divisible by 43 or not
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

        // adding thirteen times the last
        // digit to the remaining number
        n = Math.Abs(n + (d * 13));
    }

    // Finally return if the two-digit
    // number is divisible by 43 or not
    return (n % 43 == 0) ;
}

// Driver Code
public static void Main()
{
    int N = 2795;

    if (isDivisible(N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");    
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>
//javascript program to check whether a number
// is divisible by 43 or not

// Function to check if the number is divisible by 43 or not
function isDivisible(n)
{
    let d;
    // While there are at least two digits
    while(parseInt(n/100) > 0)
    {

        // Extracting the last
        d = n % 10;

        // Truncating the number
    n = parseInt(n / 10)

        // adding thirteen times the last
        // digit to the remaining number
        n = Math.abs(n+(d * 13));
    }
    // Finally return if the two-digit
    // number is divisible by 43 or not
    return (n % 43 == 0) ;
}

// Driver Code
    let N = 2795;

    if (isDivisible(N))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
Yes
```

时间复杂度:O(log <sub>10</sub> N <sub>)</sub>

辅助空间:0(1)