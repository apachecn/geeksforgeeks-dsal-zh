# 求给定整数是否为 3 的幂

> 原文:[https://www . geesforgeks . org/find-不管给定整数-幂-3-not/](https://www.geeksforgeeks.org/find-whether-given-integer-power-3-not/)

给定一个正整数，写一个函数，看看它是否是三的幂。
示例:

```
Input : 3
Output :Yes

Input :6
Output :No
```

**递归方法:**

检查这个数是否能被 3 整除，如果能，就递归地检查这个数是否能被 3 整除。如果这个数可以减为 1，那么这个数可以被 3 整除，否则不能。

## C++

```
#include <bits/stdc++.h>
#define ll long long
using namespace std;
bool isPower_of_Three(ll n)
{
    if (n <= 0)
        return false;
    if (n % 3 == 0)
        return isPower_of_Three(n / 3);
    if (n == 1)
        return true;
    return false;
}
int main()
{
    ll num1;
    num1 = 243;
    if (isPower_of_Three(num1))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    ll num2 = 6;
    if (isPower_of_Three(num2))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{
static boolean isPower_of_Three(long n)
{
    if (n <= 0)
        return false;
    if (n % 3 == 0)
        return isPower_of_Three(n / 3);
    if (n == 1)
        return true;
    return false;
}

  // Driver code
public static void main(String[] args)
{
    long  num1 = 243;
    if (isPower_of_Three(num1))
        System.out.print("Yes" +"\n");
    else
        System.out.print("No" +"\n");
    long num2 = 6;
    if (isPower_of_Three(num2))
        System.out.print("Yes" +"\n");
    else
        System.out.print("No" +"\n");
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
def isPower_of_Three(n):

    if (n <= 0):
        return False
    if (n % 3 == 0):
        return isPower_of_Three(n // 3)
    if (n == 1):
        return True
    return False

 # Driver code
num1 = 243
if (isPower_of_Three(num1)):
    print("Yes")
else:
    print("No")

num2 = 6
if (isPower_of_Three(num2)):
    print("Yes")
else:
    print("No")

# This code is contributed by shivanisinghss2110
```

## C#

```
using System;

class GFG{
static Boolean isPower_of_Three(long n)
{
    if (n <= 0)
        return false;
    if (n % 3 == 0)
        return isPower_of_Three(n / 3);
    if (n == 1)
        return true;
    return false;
}

  // Driver code
public static void Main(String[] args)
{
    long  num1 = 243;
    if (isPower_of_Three(num1))
        Console.Write("Yes" +"\n");
    else
        Console.Write("No" +"\n");
    long num2 = 6;
    if (isPower_of_Three(num2))
        Console.Write("Yes" +"\n");
    else
        Console.Write("No" +"\n");
}
}

// this code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
function isPower_of_Three(n)
{
    if (n <= 0)
        return false;
    if (n % 3 == 0)
        return isPower_of_Three(n / 3);
    if (n == 1)
        return true;
    return false;
}

    let num1 = 243;
    if (isPower_of_Three(num1))
      document.write("Yes");
    else
          document.write("No");
    let num2 = 6;
    if (isPower_of_Three(num2))
      document.write("Yes");
    else
        document.write("</br>No");

        //This code is contributed by vaibhavrabadiyaa3.
</script>
```

**Output**

```
Yes
No
```