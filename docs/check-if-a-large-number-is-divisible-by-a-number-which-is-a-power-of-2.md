# 检查一个大数是否能被 2 的幂次数整除

> 原文:[https://www . geesforgeks . org/check-如果一个大数能被一个 2 的幂整除/](https://www.geeksforgeeks.org/check-if-a-large-number-is-divisible-by-a-number-which-is-a-power-of-2/)

给定一个字符串形式的大数 **str** 和一个数 **K** ，任务是检查字符串 **str** 形成的数是否能被 **K** 整除，其中 **K** 是 2 的幂。
**举例:**

> **输入:**str = " 5426987513245621541524288 "，num = 64
> **输出:**是
> **说明:**
> 既然 log <sub>2</sub> (64) = 6，那么字符串最后 6 位数字组成的数字可以被 64 整除。
> **输入:**str =“21346775656413259795656497974113461254”，num = 4
> **输出:**否
> **说明:**
> 自对数 <sub>2</sub> (4)=2，字符串最后 2 位数字组成的数字不能被 4 整除。

**进场:**
既然 **K** 是 **2** 的完美力量。让 **K** 可以表示为 2 <sup>X</sup> 。那么根据 2 的完美幂的可除性规则，如果给定数的最后 **X 位**可以被 **K** 整除，那么给定数就可以被 K 整除，否则就不能被 **K** 整除。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check divisibility
bool checkIfDivisible(string str,
                      long long int num)
{

    // Calculate the number of digits in num
    long long int powerOf2 = log2(num);

    // Check if the length of
    // the string is less than
    // the powerOf2 then
    // return false
    if (str.length() < powerOf2)
        return false;

    // Check if the powerOf2 is 0
    // that means the given number
    // is 1 and as every number
    // is divisible by 1 so return true
    if (powerOf2 == 0)
        return true;

    // Find the number which is
    // formed by the last n digits
    // of the string where n=powerOf2
    long long int i, number = 0;
    int len = str.length();

    for (i = len - powerOf2; i < len; i++) {
        number += (str[i] - '0')
                  * pow(10,
                        powerOf2 - 1);
        powerOf2--;
    }

    // Check if the number formed is
    // divisible by input num or not
    if (number % num)
        return false;
    else
        return true;
}

// Driver Code
int main()
{
    // Given number
    string str = "213467756564";
    long long int num = 4;

    // Function Call
    if (checkIfDivisible(str, num))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check divisibility
static boolean checkIfDivisible(String str,
                                long num)
{

    // Calculate the number of digits in num
    long powerOf2 = (int)(Math.log(num) /
                          Math.log(2));

    // Check if the length of
    // the string is less than
    // the powerOf2 then
    // return false
    if (str.length() < powerOf2)
        return false;

    // Check if the powerOf2 is 0
    // that means the given number
    // is 1 and as every number
    // is divisible by 1 so return true
    if (powerOf2 == 0)
        return true;

    // Find the number which is
    // formed by the last n digits
    // of the string where n=powerOf2
    long i, number = 0;
    int len = str.length();

    for(i = len - powerOf2; i < len; i++)
    {
        number += (str.charAt((int)i) - '0') *
                   Math.pow(10, powerOf2 - 1);
        powerOf2--;
    }

    // Check if the number formed is
    // divisible by input num or not
    if (number % num != 0)
        return false;
    else
        return true;
}

// Driver Code
public static void main(String[] args)
{

    // Given number
    String str = "213467756564";
    long num = 4;

    // Function call
    if (checkIfDivisible(str, num))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2

# Function to check divisibility
def checkIfDivisible(string, num):

    # Calculate the number of digits in num
    powerOf2 = int(log2(num));

    # Check if the length of
    # the string is less than
    # the powerOf2 then
    # return false
    if (len(string) < powerOf2):
        return False;

    # Check if the powerOf2 is 0
    # that means the given number
    # is 1 and as every number
    # is divisible by 1 so return true
    if (powerOf2 == 0):
        return True;

    # Find the number which is
    # formed by the last n digits
    # of the string where n=powerOf2
    number = 0;
    length = len(string);

    for i in range(length - powerOf2, length):
        number += ((ord(string[i]) - ord('0')) *
                  (10 ** (powerOf2 - 1)));

        powerOf2 -= 1;

    # Check if the number formed is
    # divisible by input num or not
    if (number % num):
        return False;
    else :
        return True;

# Driver Code
if __name__ == "__main__" :

    # Given number
    string = "213467756564";
    num = 4;

    # Function Call
    if (checkIfDivisible(string, num)):
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check divisibility
static bool checkIfDivisible(String str,
                             long num)
{

    // Calculate the number of digits in num
    long powerOf2 = (int)(Math.Log(num) /
                          Math.Log(2));

    // Check if the length of
    // the string is less than
    // the powerOf2 then
    // return false
    if (str.Length < powerOf2)
        return false;

    // Check if the powerOf2 is 0
    // that means the given number
    // is 1 and as every number
    // is divisible by 1 so return true
    if (powerOf2 == 0)
        return true;

    // Find the number which is
    // formed by the last n digits
    // of the string where n=powerOf2
    long i, number = 0;
    int len = str.Length;

    for(i = len - powerOf2; i < len; i++)
    {
        number += (long)((str[(int)i] - '0') *
                Math.Pow(10, powerOf2 - 1));
        powerOf2--;
    }

    // Check if the number formed is
    // divisible by input num or not
    if (number % num != 0)
        return false;
    else
        return true;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number
    String str = "213467756564";
    long num = 4;

    // Function call
    if (checkIfDivisible(str, num))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check divisibility
function checkIfDivisible(str, num)
{

    // Calculate the number of digits in num
    let powerOf2 = (Math.log(num) /
                          Math.log(2));

    // Check if the length of
    // the string is less than
    // the powerOf2 then
    // return false
    if (str.length < powerOf2)
        return false;

    // Check if the powerOf2 is 0
    // that means the given number
    // is 1 and as every number
    // is divisible by 1 so return true
    if (powerOf2 == 0)
        return true;

    // Find the number which is
    // formed by the last n digits
    // of the string where n=powerOf2
    let i, number = 0;
    let len = str.length;

    for(i = len - powerOf2; i < len; i++)
    {
        number += (str[i] - '0') *
                   Math.pow(10, powerOf2 - 1);
        powerOf2--;
    }

    // Check if the number formed is
    // divisible by input num or not
    if (number % num != 0)
        return false;
    else
        return true;
}

// Driver Code

    // Given number
    let str = "213467756564";
    let num = 4;

    // Function call
    if (checkIfDivisible(str, num))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(Len)，其中 Len 是字符串的长度。*
***辅助空间:** O(log <sub>2</sub> K)*