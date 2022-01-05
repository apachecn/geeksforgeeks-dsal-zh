# 最接近回文数(绝对差最小)

> 原文:[https://www . geesforgeks . org/close-回文-number-what-绝对值差-min/](https://www.geeksforgeeks.org/closest-palindrome-number-whose-absolute-difference-min/)

给定一个数 n，我们的任务是找到与给定数绝对差最小且绝对差必须大于 0 的最近的回文数。

**示例:**

```
Input :  N = 121 
Output : 131 or 111   
Both having equal absolute difference
with the given number.

Input : N = 1234
Output : 1221
```

问于:**亚马逊**

**简单解法**就是找到比给定数小的最大回文数，同时也找到比给定数大的第一个回文数，我们可以通过在给定数中简单地减一和增一来找到这些回文数，直到找到这些回文数。

以下是上述想法的实现:

## C++

```
// C++ Program to find the closest Palindrome
// number
#include <bits/stdc++.h>
using namespace std;

// function check Palindrome
bool isPalindrome(string n)
{
    for (int i = 0; i < n.size() / 2; i++)
        if (n[i] != n[n.size() - 1 - i])
            return false;
    return true;
}

// convert number into String
string convertNumIntoString(int num)
{

    // base case:
    if (num == 0)
        return "0";

    string Snum = "";
    while (num > 0) {
        Snum += (num % 10 - '0');
        num /= 10;
    }
    return Snum;
}

// function return closest Palindrome number
int closestPlandrome(int num)
{

    // case1 : largest palindrome number
    // which is smaller to given number
    int RPNum = num - 1;

    while (!isPalindrome(convertNumIntoString(abs(RPNum))))
        RPNum--;

    // Case 2 : smallest palindrome number
    // which is greater than given number
    int SPNum = num + 1;

    while (!isPalindrome(convertNumIntoString(SPNum)))
        SPNum++;

    // check absolute difference
    if (abs(num - RPNum) > abs(num - SPNum))
        return SPNum;
    else
        return RPNum;
}

// Driver program to test above function
int main()
{
    int num = 121;
    cout << closestPlandrome(num) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the closest
// Palindrome number
import java.io.*;

class GFG{

// Function to check Palindrome   
public static boolean isPalindrome(String s)
{
    int left = 0;
    int right = s.length() - 1;

    while (left < right)
    {
        if (s.charAt(left) !=
            s.charAt(right))
        {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Function return closest Palindrome number
public static void closestPalindrome(int num)
{

    // Case1 : largest palindrome number
    // which is smaller to given number
    int RPNum = num - 1;

    while (isPalindrome(Integer.toString(RPNum)) == false)
    {
        RPNum--;
    }

    // Case 2 : smallest palindrome number
    // which is greater than given number
    int SPNum = num + 1;

    while (isPalindrome(Integer.toString(SPNum)) == false)
    {
        SPNum++;
    }

    // Check absolute difference
    if (Math.abs(num - SPNum) <
        Math.abs(num - RPNum))
    {
        System.out.println(SPNum);
    }
    else
        System.out.println(RPNum);
}

// Driver code    
public static void main(String[] args)
{
    int n = 121;

    closestPalindrome(n);
}
}

// This code is contributed by kes333hav
```

## 蟒蛇 3

```
# Python3 program to find the
# closest Palindrome number

# Function to check Palindrome

def isPalindrome(n):

    for i in range(len(n) // 2):
        if (n[i] != n[-1 - i]):
            return False

    return True

# Convert number into String

def convertNumIntoString(num):

    Snum = str(num)
    return Snum

# Function return closest Palindrome number

def closestPalindrome(num):

    # Case1 : largest palindrome number
    # which is smaller than given number
    RPNum = num - 1
    while (not isPalindrome(
           convertNumIntoString(abs(RPNum)))):
        RPNum -= 1

    # Case2 : smallest palindrome number
    # which is greater than given number
    SPNum = num + 1
    while (not isPalindrome(
           convertNumIntoString(SPNum))):
        SPNum += 1

    # Check absolute difference
    if (abs(num - RPNum) > abs(num - SPNum)):
        return SPNum
    else:
        return RPNum

# Driver Code
if __name__ == '__main__':

    num = 121

    print(closestPalindrome(num))

# This code is contributed by himanshu77
```

## C#

```
// C# program to find the closest
// Palindrome number
using System;

class GFG{

// Function to check Palindrome
public static bool isPalindrome(string s)
{
    int left = 0;
    int right = s.Length - 1;

    while (left < right)
    {
        if (s[left] != s[right])
        {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Function return closest Palindrome number
public static void closestPalindrome(int num)
{

    // Case1 : largest palindrome number
    // which is smaller to given number
    int RPNum = num - 1;

    while (isPalindrome(RPNum.ToString()) == false)
    {
        RPNum--;
    }

    // Case 2 : smallest palindrome number
    // which is greater than given number
    int SPNum = num + 1;

    while (isPalindrome(SPNum.ToString()) == false)
    {
        SPNum++;
    }

    // Check absolute difference
    if (Math.Abs(num - SPNum) <
        Math.Abs(num - RPNum))
    {
        Console.WriteLine(SPNum);
    }
    else
        Console.WriteLine(RPNum);
}

// Driver code
public static void Main(string[] args)
{
    int n = 121;

    closestPalindrome(n);
}
}

// This code is contributed by ukasp
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// closest Palindrome number

// function check Palindrome
function isPalindrome($n)
{
 for ($i = 0; $i < floor(strlen($n) /  2); $i++)
    if ($n[$i] != $n[strlen($n) - 1 - $i])
    return false;
return true;
}

// convert number into String
function convertNumIntoString($num)
{

// base case:
if ($num == 0)
    return "0";
$Snum = "";
while ($num > 0)
{
    $Snum .= ($num % 10 - '0');
    $num =(int)($num / 10);
}
return $Snum;
}

// function return closest
// Palindrome number
function closestPlandrome($num)
{

// case1 : largest palindrome number
// which is smaller to given number
$RPNum = $num - 1;

while (!isPalindrome(convertNumIntoString(abs($RPNum))))
    $RPNum--;

// Case 2 : smallest palindrome number
// which is greater than given number
$SPNum = $num + 1;

while (!isPalindrome(convertNumIntoString($SPNum)))
    $SPNum++;

// check absolute difference
if (abs($num - $RPNum) > abs($num - $SPNum))
    return $SPNum;
else
    return $RPNum;
}

    // Driver code
    $num = 121;
    echo closestPlandrome($num)."\n";

// This code is contributed by mits
?>
```

**输出:**

```
111
```

一个**有效的解决方案**是考虑以下情况。
**情况 1:** 如果一个数包含所有的 9，那么我们只要在其中加 2 就可以得到下一个最接近的回文。num = 999:输出:num + 2 = 1001。
**例 2:**
**例 2 a :** 一种可能的获取最近回文的方法是复制前半部分，如果是，在末尾添加镜像。**左半部分:**例如“ **123** 456”的左侧为“123”，而“ **12** 345”的左半部分为“12”。要转换成回文，我们可以取其左半部分的镜像，也可以取其右半部分的镜像。然而，如果我们取右半部分的镜像，那么这样形成的回文不一定是最接近的回文。所以，我们必须把左边的镜子复制到右边。

```
Let's number : 123456 
After copy and append reverse of it at the end number looks like:
we get palindrome 123321
```

**情况 2 b 和 2c:** 在回文上通过中间数字递减和递增 1 来获得最近的回文数字的两种可能的方法。

下面是上述想法的实现:

## C++

```
// C++ program to find the closest Palindrome number
#include <bits/stdc++.h>
using namespace std;

#define CToI(x) (x - '0')
#define IToC(x) (x + '0')

// function check Palindrome
bool isPalindrome(string n)
{
    for (int i = 0; i < n.size() / 2; i++)
        if (n[i] != n[n.size() - 1 - i])
            return false;
    return true;
}

// check all 9's
bool checkAll9(string num)
{
    for (int i = 0; i < num.size(); i++)
        if (num[i] != '9')
            return false;
    return true;
}

// Add carry to the number of given size
string carryOperaion(string num, int carry, int size)
{
    if (carry == -1)
    {
        int i = size - 1;
        while (i >= 0 && num[i] == '0')
            num[i--] = '9';
        if (i >= 0)
            num[i] = IToC(CToI(num[i]) - 1);
    }
    else
    {
        for (int i = size - 1; i >= 0; i--)
        {
            int digit = CToI(num[i]);
            num[i] = IToC((digit + carry) % 10);
            carry = (digit + carry) / 10;
        }
    }
    return num;
}

// function return the closest number
// to given number
string MIN(long long int num,
           long long int num1,
           long long int num2,
           long long int num3)
{

    long long int Diff1 = abs(num - num1);
    long long int Diff2 = abs(num - num2);
    long long int Diff3 = abs(num3 - num);

    if (Diff1 < Diff2 && Diff1 < Diff3 &&
        num1 != num)
        return to_string(num1);
    else if (Diff3 < Diff2 && (Diff1 == 0 ||
             Diff3 < Diff1))
        return to_string(num3);
    else
        return to_string(num2);
}

// function return closest Palindrome number
string closestPlandrome(string num)
{

    // base case
    if (num.size() == 1)
        return (to_string(stoi(num) - 1));

    // case 2:
    // If a number contains all 9's
    if (checkAll9(num))
    {
        string str = "1";
        return str.append(num.size() - 1, '0') + "1";
    }

    int size_ = num.size();

    // case 1 a:
    // copy first half and reverse it and append it
    // at the end of first half
    string FH = num.substr(0, size_ / 2);
    string odd;

    // odd length
    if (size_ % 2 != 0)
        odd = num[size_ / 2];

    // reverse
    string SH = FH;
    reverse(SH.begin(), SH.end());

    // store three nearest Palindrome numbers
    string RPNUM = "", EPNUM = "", LPNUM = "";
    string tempFH = "";
    string tempSH = "";

    if (size_ % 2 != 0)
    {
        EPNUM = FH + odd + SH;
        if (odd == "0")
        {
            tempFH = carryOperaion(FH, -1, FH.size());
            tempSH = tempFH;
            reverse(tempSH.begin(), tempSH.end());
            RPNUM = tempFH + "9" + tempSH;
        }
        else
            RPNUM = FH + to_string(stoi(odd) - 1) + SH;

        // To handle carry
        if (odd == "9")
        {
            tempFH = carryOperaion(FH, 1, FH.size());
            tempSH = tempFH;
            reverse(tempSH.begin(), tempSH.end());
            LPNUM = tempFH + "0" + tempSH;
        }
        else
            LPNUM = FH + to_string(stoi(odd) + 1) + SH;
    }

    // for even case
    else
    {
        int n = FH.size();
        tempFH = FH;
        EPNUM = FH + SH;
        if (FH[n - 1] == '0')
            tempFH = carryOperaion(FH, -1, n);
        else
            tempFH[n - 1] = IToC(CToI(FH[n - 1]) - 1);

        tempSH = tempFH;
        reverse(tempSH.begin(), tempSH.end());
        RPNUM = tempFH + tempSH;

        tempFH = FH;
        if (FH[n - 1] == '9')
            tempFH = carryOperaion(FH, 1, n);
        else
            tempFH[n - 1] = IToC(CToI(tempFH[n - 1]) + 1);

        tempSH = tempFH;
        reverse(tempSH.begin(), tempSH.end());
        LPNUM = tempFH + tempSH;
    }

    // return the closest palindrome numbers
    return MIN(stoll(num), stoll(EPNUM), stoll(RPNUM),
                                         stoll(LPNUM));
}

// Driver program to test above function
int main()
{
    string num = "123456";
    cout << closestPlandrome(num) << endl;
    return 0;
}
```

**输出:**

```
123321
```

时间复杂度:O(d) ( d 为给定数字中的位数)