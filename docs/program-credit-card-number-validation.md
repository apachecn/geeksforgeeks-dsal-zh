# 信用卡号验证程序

> 原文:[https://www . geesforgeks . org/program-credit-card-number-validation/](https://www.geeksforgeeks.org/program-credit-card-number-validation/)

**编写一个程序，提示用户输入一个长整数形式的信用卡号，并显示该卡是否有效。**
信用卡号码遵循一定的模式。
信用卡号必须有 13 到 16 位数字。必须从:
开始

*   4 张维萨卡
*   主卡 5 张
*   美国运通卡 37 元
*   6 张探索卡

问题可以用 [Luhn 算法](https://www.geeksforgeeks.org/luhn-algorithm/)解决。
**鲁恩检查**或 **Mod 10** 检查，可描述如下(举例说明，
考虑卡号 4388576018402626):
**步骤 1** 。从右向左每隔一个数字翻一倍。如果一个数字加倍得到一个
两位数，将两位数相加得到一个一位数(如 12:1+2，18=1+8)。
**第二步**。现在将步骤 1 中的所有一位数相加。
4+4+8+2+3+1+7+8 = 37
**第三步**。把卡号从右到左奇数位的所有数字加起来。
6+6+0+8+0+7+8+3 = 38
**第四步**。将步骤 2 和步骤 3 的结果相加。
37 + 38 = 75
**第五步**。如果步骤 4 的结果可被 10 整除，则卡号有效；否则无效。
**举例:**

```
Input : 379354508162306
Output : 379354508162306 is Valid

Input : 4388576018402626
Output : 4388576018402626 is invalid
```

## C++

```
// C++ program to check if a given credit
// card is valid or not.
#include <iostream>
using namespace std;

// Return this number if it is a single digit, otherwise,
// return the sum of the two digits
int getDigit(int number)
{
  if (number < 9)
    return number;
  return number / 10 + number % 10;
}

// Return the number of digits in d
int getSize(long d)
{
  string num = to_string(d);
  return num.length();
}

// Return the first k number of digits from
// number. If the number of digits in number
// is less than k, return number.
long getPrefix(long number, int k)
{
  if (getSize(number) > k)
  {
    string num = to_string(number);
    return stol(num.substr(0, k));
  }
  return number;
}

// Return true if the digit d is a prefix for number
bool prefixMatched(long number, int d)
{
  return getPrefix(number, getSize(d)) == d;
}

// Get the result from Step 2
int sumOfDoubleEvenPlace(long int number)
{
  int sum = 0;
  string num = to_string(number) ;
  for (int i = getSize(number) - 2; i >= 0; i -= 2)
    sum += getDigit(int(num[i] - '0') * 2);

  return sum;
}

// Return sum of odd-place digits in number
int sumOfOddPlace(long number)
{
  int sum = 0;
  string num = to_string(number) ;
  for (int i = getSize(number) - 1; i >= 0; i -= 2)
    sum += num[i] - '0';
  return sum;
}

// Return true if the card number is valid
bool isValid(long int number)
{
  return (getSize(number) >= 13 &&
          getSize(number) <= 16) &&
    (prefixMatched(number, 4) ||
     prefixMatched(number, 5) ||
     prefixMatched(number, 37) ||
     prefixMatched(number, 6)) &&
    ((sumOfDoubleEvenPlace(number) +
      sumOfOddPlace(number)) % 10 == 0);
}

// Driver Code
int main()
{
  long int number = 5196081888500645L;
  cout << number << " is " <<  (isValid(number) ? "valid" : "invalid");
  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given credit
// card is valid or not.
import java.util.Scanner;

public class CreditCard {
    // Main Method
    public static void main(String[] args)
    {
        long number = 5196081888500645L;

        System.out.println(number + " is " +
        (isValid(number) ? "valid" : "invalid"));
    }

    // Return true if the card number is valid
    public static boolean isValid(long number)
    {
       return (getSize(number) >= 13 &&
               getSize(number) <= 16) &&
               (prefixMatched(number, 4) ||
                prefixMatched(number, 5) ||
                prefixMatched(number, 37) ||
                prefixMatched(number, 6)) &&
              ((sumOfDoubleEvenPlace(number) +
                sumOfOddPlace(number)) % 10 == 0);
    }

    // Get the result from Step 2
    public static int sumOfDoubleEvenPlace(long number)
    {
        int sum = 0;
        String num = number + "";
        for (int i = getSize(number) - 2; i >= 0; i -= 2)
            sum += getDigit(Integer.parseInt(num.charAt(i) + "") * 2);

        return sum;
    }

    // Return this number if it is a single digit, otherwise,
    // return the sum of the two digits
    public static int getDigit(int number)
    {
        if (number < 9)
            return number;
        return number / 10 + number % 10;
    }

    // Return sum of odd-place digits in number
    public static int sumOfOddPlace(long number)
    {
        int sum = 0;
        String num = number + "";
        for (int i = getSize(number) - 1; i >= 0; i -= 2)
            sum += Integer.parseInt(num.charAt(i) + "");       
        return sum;
    }

    // Return true if the digit d is a prefix for number
    public static boolean prefixMatched(long number, int d)
    {
        return getPrefix(number, getSize(d)) == d;
    }

    // Return the number of digits in d
    public static int getSize(long d)
    {
        String num = d + "";
        return num.length();
    }

    // Return the first k number of digits from
    // number. If the number of digits in number
    // is less than k, return number.
    public static long getPrefix(long number, int k)
    {
        if (getSize(number) > k) {
            String num = number + "";
            return Long.parseLong(num.substring(0, k));
        }
        return number;
    }
}
```

## C#

```
// C# program to check if a given
// credit card is valid or not.
using System;

class CreditCard {

    // Main Method
    public static void Main()
    {
        long number = 5196081888500645L;
        Console.Write(number + " is " +
                     (isValid(number) ?
                     "valid" : "invalid"));
    }

    // Return true if the card number is valid
    public static bool isValid(long number)
    {
    return (getSize(number) >= 13 &&
            getSize(number) <= 16) &&
            (prefixMatched(number, 4) ||
            prefixMatched(number, 5) ||
            prefixMatched(number, 37) ||
            prefixMatched(number, 6)) &&
            ((sumOfDoubleEvenPlace(number) +
            sumOfOddPlace(number)) % 10 == 0);
    }

    // Get the result from Step 2
    public static int sumOfDoubleEvenPlace(long number)
    {
        int sum = 0;
        String num = number + "";
        for (int i = getSize(number) - 2; i >= 0; i -= 2)
            sum += getDigit(int.Parse(num[i] + "") * 2);

        return sum;
    }

    // Return this number if it is a
    // single digit, otherwise, return
    // the sum of the two digits
    public static int getDigit(int number)
    {
        if (number < 9)
            return number;
        return number / 10 + number % 10;
    }

    // Return sum of odd-place digits in number
    public static int sumOfOddPlace(long number)
    {
        int sum = 0;
        String num = number + "";
        for (int i = getSize(number) - 1; i >= 0; i -= 2)
            sum += int.Parse(num[i] + "");    
        return sum;
    }

    // Return true if the digit d
    // is a prefix for number
    public static bool prefixMatched(long number, int d)
    {
        return getPrefix(number, getSize(d)) == d;
    }

    // Return the number of digits in d
    public static int getSize(long d)
    {
        String num = d + "";
        return num.Length;
    }

    // Return the first k number of digits from
    // number. If the number of digits in number
    // is less than k, return number.
    public static long getPrefix(long number, int k)
    {
        if (getSize(number) > k)
        {
            String num = number + "";
            return long.Parse(num.Substring(0, k));
        }
        return number;
    }
}

// This code is contributed by nitin mittal.
```

输出:

```
5196081888500645 is valid
```

本文由**维沙尔·库马尔·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。