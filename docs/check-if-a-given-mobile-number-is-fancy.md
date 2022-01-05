# 检查给定的手机号码是否花哨

> 原文:[https://www . geesforgeks . org/check-if-a-给定的手机号码是-花式/](https://www.geeksforgeeks.org/check-if-a-given-mobile-number-is-fancy/)

给定一个手机号码和一个花哨号码的一些条件，找出给定号码是否花哨。如果一个 10 位数的手机号码满足以下三个条件中的任何一个，它就被称为花式号码。

1.  一个数字连续出现三次。比如 777。
2.  三个连续的数字不是递增就是递减。比如 456 或者 987。
3.  一个数字在数字中出现四次或更多次。像 9859009976 一样，这里的数字 9 出现了 4 次。

**例:**

> 输入:9859009976
> 输出:是
> 给定的手机号满足上面给定的条件
> 三。
> 输入:7609438921
> 输出:否
> 给定的三个条件都不满足。

想法是用[到 _string](https://www.geeksforgeeks.org/stdto_string-in-cpp/) 把数字转换成字符串，这样就变得容易遍历了。对于计算每个数字的频率的条件三，使用了字符串散列的基本概念。
来源:[甲骨文面试集](https://www.geeksforgeeks.org/oracle-interview-experience-application-developer-2-5-years-experienced/)
以下是以上问题的解答。

## C++

```
// C++ program to check if a given mobile
// number is fancy or not.
#include <bits/stdc++.h>
using namespace std;

// Returns true if s has three consecutive
// same digits.
bool cond1(string s)
{
    for (int i = 0; i < s.size() - 2; i++) {
        if (s[i] == s[i + 1] && s[i + 1] == s[i + 2])
            return true;
    }
    return false;
}

// Returns true if s has three increasing or
// decreasing digits.
bool cond2(string s)
{
    for (int i = 0; i < s.size() - 2; i++) {
        if ((s[i] < s[i + 1] && s[i + 1] < s[i + 2]) ||
            (s[i] > s[i + 1] && s[i + 1] > s[i + 2]))
            return true;
    }
    return false;
}

// Checks if a single digit occurs 4 times.
bool cond3(string s)
{
    int a[10];
    memset(a, 0, sizeof(a));

    for (int i = 0; i < s.size(); i++)
        a[s[i] - '0']++;

    for (int i = 0; i < 9; i++)
        if (a[i] >= 4)
            return true;

    return false;
}

bool isFancy(string s)
{
    if (cond1(s) || cond2(s) || cond3(s))
        return true;
    else
        return false;
}

// Driver condition
int main()
{
    long int n = 7609438921;
    string s = to_string(n);
    if (isFancy(s))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given mobile
// number is fancy or not.
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

public static void main(String[] args) {

        String mobileNumber = "7654449244";

        if (isFancy(mobileNumber))
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    public static boolean isFancy(String mobileNumber) {
        int incrementCount = 0;
        int decrementCount = 0;
        int consecutiveCount = 1;
        int[] countArray = new int[10];
        int prevDigit = -1;
        for(int i = 0; i < mobileNumber.length(); i++) {

            int digit = Integer.parseInt(String.valueOf(mobileNumber.charAt(i)));
            countArray[digit] += 1;
            // Checking for Number of occurrences of any digit is greater than 3

            if(countArray[digit] > 3)
                return true;
            // Checking for consecutive digits are same

            if(prevDigit == digit)
                consecutiveCount += 1;

            else if(prevDigit == digit+1 && prevDigit != -1) {
                incrementCount += 1;
                decrementCount = 0;
                consecutiveCount = 1;
            }

            else if(digit == prevDigit+1) {
                decrementCount += 1;
                incrementCount = 0;
                consecutiveCount = 1;
            }

            if(consecutiveCount == 3)
                return true;

            if(incrementCount == 2 || decrementCount == 2)
                return true;

            prevDigit = digit;
        }
        return false;
    }
}

// This code is contributed by Vasishta Balla
```

## 蟒蛇 3

```
# Python3 program to check if a
# given mobile number is fancy or not.

# Returns true if s has three
# consecutive same digits.
def cond1(s):

    for i in range(len(s) - 2):
        if (s[i] == s[i + 1] and
            s[i + 1] == s[i + 2]):
            return True

    return False

# Returns true if s has three
# increasing or decreasing digits.
def cond2(s):
    for i in range(len(s) - 2):
        if ((s[i] < s[i + 1] and
             s[i + 1] < s[i + 2]) or
            (s[i] > s[i + 1] and
             s[i + 1] > s[i + 2])):
            return True

    return False

# Checks if a single digit
# occurs 4 times.
def cond3(s):
    a = [0] * 10
    for i in range(len(s)):
        a[s[i] - '0'] = a[s[i] - '0'] + 1

    for i in range(len(9)):

        if (a[i] >= 4):
            return True

    return False

def isFancy(s):
    if (cond1(s) or cond2(s) or cond3(s)):
        return True
    else:
        return False

# Driver condition
s = "7609438921"
if (isFancy(s)):
    print("Yes")
else:
    print("No")

# This code is contributed by ash264
```

## C#

```
// C# program to check if a given mobile
// number is fancy or not.
using System;

class GFG
{

    public static void Main(String[] args)
    {

        String mobileNumber = "7654449244";

        if (isFancy(mobileNumber))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }

    public static bool isFancy(String mobileNumber)
    {
        int incrementCount = 0;
        int decrementCount = 0;
        int consecutiveCount = 1;
        int[] countArray = new int[10];
        int prevDigit = -1;
        for (int i = 0; i < mobileNumber.Length; i++)
        {

            int digit = Int32.Parse(String.Join("",mobileNumber[i]));
            countArray[digit] += 1;

            // Checking for Number of occurrences
            // of any digit is greater than 3
            if (countArray[digit] > 3)
            {
                return true;
            }

            // Checking for consecutive digits are same
            if (prevDigit == digit)
            {
                consecutiveCount += 1;
            }
            else if (prevDigit == digit + 1 && prevDigit != -1)
            {
                incrementCount += 1;
                decrementCount = 0;
                consecutiveCount = 1;
            }
            else if (digit == prevDigit + 1)
            {
                decrementCount += 1;
                incrementCount = 0;
                consecutiveCount = 1;
            }
            if (consecutiveCount == 3)
            {
                return true;
            }
            if (incrementCount == 2 || decrementCount == 2)
            {
                return true;
            }
            prevDigit = digit;
        }
        return false;
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript  program to check if a given mobile
// number is fancy or not

// Returns true if s has three consecutive
// same digits.
function cond1( s)
{
    for (var i = 0; i < s.length - 2; i++) {
        if (s[i] == s[i + 1] && s[i + 1] == s[i + 2])
            return true;
    }
    return false;
}

// Returns true if s has three increasing or
// decreasing digits.
function cond2( s)
{
    for (var i = 0; i < s.length - 2; i++) {
        if ((s[i] < s[i + 1] && s[i + 1] < s[i + 2]) ||
            (s[i] > s[i + 1] && s[i + 1] > s[i + 2]))
            return true;
    }
    return false;
}

// Checks if a single digit occurs 4 times.
function cond3( s)
{
    var a = new Array(10);
    a.fill(0);

    for (var i = 0; i < s.length; i++)
        a[s[i] - '0']++;

    for (var i = 0; i < 9; i++)
        if (a[i] >= 4)
            return true;

    return false;
}

function isFancy( s)
{
    if (cond1(s) || cond2(s) || cond3(s))
        return true;
    else
        return false;
}

 var  n = "7609438921";

    // var s = to_string(n);
    if (isFancy(n))
        document.write( "Yes");
    else
       document.write( "No");

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Yes
```