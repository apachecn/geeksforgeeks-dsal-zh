# 检查通过交换 0 之前出现的 1 是否可以使两个二进制字符串相等

> 原文:[https://www . geeksforgeeks . org/check-if-two-binary-strings-可以通过交换-1s-0s 前出现来使其相等/](https://www.geeksforgeeks.org/check-if-two-binary-strings-can-be-made-equal-by-swapping-1s-occurring-before-0s/)

给定两个长度相同的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **str1** 和 **str2** ，任务是通过交换二进制字符串 **str1** 中出现在小于 **0** s 索引的索引处的所有 **1** s，来确定是否有可能使两个二进制字符串 **str1** 和 **str2** 相等。

**示例:**

> **输入:**str1 =“0110”，str 2 =“0011”
> **输出:**可能
> **解释:**
> 用 str1[3]交换 str1[2]二进制字符串 str 1 变成“0101”。
> 将 str1[1]替换为 str1[2]，二进制字符串 str1 变为“0011”。
> 二进制字符串 str1 变得等于二进制字符串 str2，因此，所需的输出是可能的。
> 
> **输入:**str 1 =“101”，str 2 =“010”
> T3】输出:不可能

**进场:**思路是统计 **str1** 和 **str2** 中 **1s** 和 **0s** 的数量，然后进行相应的处理。按照以下步骤解决问题:

*   如果 **str1** 和 **str2** 中 **1** 和 **0** 的计数不相等，则无法转换。
*   [穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
*   从第一个字符开始，逐一比较每个字符。对于 **i** 处的每个不同字符，执行以下步骤:
    *   检查字符串 **str1** 的当前字符是否为 **'0'** ，**curstr 1 one(**存储字符串 **str1)** 的 **1 的当前计数是否大于 **0** 。如果发现为真，则用**‘1’**交换字符，并将**光标 1 的值减**为 **1** 。**
    *   检查字符串 **str1** 的字符是否为**‘0’****curstr 1 one**等于 **0** 。如果发现为真，则将**标志**的值增加 **1** 并断开回路。
    *   检查字符串 **str1** 的字符是否为**“1”**，字符串 **str2** 的字符是否为**“0”**。如果发现为真，则将 **str1** 的字符换成 **'0'** ，并将**curst 1 的值增加 **1** 。**
*   最后，如果**标志**为 **0** ，则打印“可能”，否则打印“不可能”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to make
// two binary strings equal by given operations
void isBinaryStringsEqual(string str1, string str2)
{

    // Stores count of 1's and 0's
    // of the string str1
    int str1Zeros = 0, str1Ones = 0;

    // Stores count of 1's and 0's
    // of the string str2
    int str2Zeros = 0, str2Ones = 0;

    int flag = 0;

    // Stores current count of 1's
    // presenty in the string str1
    int curStr1Ones = 0;

    // Count the number of 1's and 0's
    // present in the strings str1 and str2
    for (int i = 0; i < str1.length(); i++) {

        if (str1[i] == '1') {
            str1Ones++;
        }

        else if (str1[i] == '0') {
            str1Zeros++;
        }

        if (str2[i] == '1') {
            str2Ones++;
        }

        else if (str2[i] == '0') {
            str2Zeros++;
        }
    }

    // If the number of 1's and 0's
    // are not same of the strings str1
    // and str2 then print not possible
    if (str1Zeros != str2Zeros && str1Ones != str2Ones) {
        cout << "Not Possible";
    }

    else {

        // Traversing through the
        // strings str1 and str2
        for (int i = 0; i < str1.length(); i++) {

            // If the str1 character not
            // equals to str2 character
            if (str1[i] != str2[i]) {

                // Swaps 0 with 1 of the
                // string str1
                if (str1[i] == '0' && curStr1Ones > 0) {
                    str1[i] = '1';
                    curStr1Ones--;
                }

                // Breaks the loop as the count
                // of 1's is zero. Hence, no swaps possible
                if (str1[i] == '0' && curStr1Ones == 0) {

                    flag++;
                    break;
                }

                // Swaps 1 with 0 in the string str1
                if (str1[i] == '1' && str2[i] == '0') {

                    str1[i] = '0';
                    curStr1Ones++;
                }
            }
        }

        if (flag == 0) {
            cout << "Possible";
        }

        // Print not possible
        else {
            cout << "Not Possible";
        }
    }
}

// Driver Code
int main()
{
    // Given Strings
    string str1 = "0110";
    string str2 = "0011";

    // Function Call
    isBinaryStringsEqual(str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

  // Function to check if it is possible to make
  // two binary strings equal by given operations
  static void isBinaryStringsEqual(String str1,
                                   String str2)
  {

    // Stores count of 1's and 0's
    // of the string str1
    int str1Zeros = 0, str1Ones = 0;

    // Stores count of 1's and 0's
    // of the string str2
    int str2Zeros = 0, str2Ones = 0;
    int flag = 0;

    // Stores current count of 1's
    // presenty in the string str1
    int curStr1Ones = 0;

    // Count the number of 1's and 0's
    // present in the strings str1 and str2
    for (int i = 0; i < str1.length(); i++)
    {

      if (str1.charAt(i) == '1')
      {
        str1Ones++;
      }

      else if (str1.charAt(i) == '0')
      {
        str1Zeros++;
      }

      if (str2.charAt(i) == '1')
      {
        str2Ones++;
      }

      else if (str2.charAt(i) == '0')
      {
        str2Zeros++;
      }
    }

    // If the number of 1's and 0's
    // are not same of the strings str1
    // and str2 then print not possible
    if (str1Zeros != str2Zeros
        && str1Ones != str2Ones)
    {
      System.out.println("Not Possible");
    }

    else {

      // Traversing through the
      // strings str1 and str2
      for (int i = 0; i < str1.length(); i++)
      {

        // If the str1 character not
        // equals to str2 character
        if (str1.charAt(i) != str2.charAt(i))
        {

          // Swaps 0 with 1 of the
          // string str1
          if (str1.charAt(i) == '0'
              && curStr1Ones > 0)
          {
            str1 = str1.substring(0, i) + '1'
              + str1.substring(i + 1);
            curStr1Ones--;
          }

          // Breaks the loop as the count
          // of 1's is zero. Hence, no swaps
          // possible
          if (str1.charAt(i) == '0'
              && curStr1Ones == 0)
          {
            flag++;
            break;
          }

          // Swaps 1 with 0 in the string str1
          if (str1.charAt(i) == '1'
              && str2.charAt(i) == '0')
          {
            str1 = str1.substring(0, i) + '0'
              + str1.substring(i+1);
            curStr1Ones++;
          }
        }
      }

      if (flag == 0) {
        System.out.println("Possible");
      }

      // Print not possible
      else {
        System.out.println("Not Possible");
      }
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given Strings
    String str1 = "0110";
    String str2 = "0011";

    // Function Call
    isBinaryStringsEqual(str1, str2);
  }
}

// This code is contributed by dharanendralv23
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if it is possible to make
# two binary strings equal by given operations
def isBinaryStringsEqual(list1, list2) :

    str1 = list(list1)
    str2 = list(list2)

    # Stores count of 1's and 0's
    # of the string str1
    str1Zeros = 0
    str1Ones = 0

    # Stores count of 1's and 0's
    # of the string str2
    str2Zeros = 0
    str2Ones = 0
    flag = 0

    # Stores current count of 1's
    # presenty in the string str1
    curStr1Ones = 0

    # Count the number of 1's and 0's
    # present in the strings str1 and str2
    for i in range(len(str1)):
        if (str1[i] == '1') :
            str1Ones += 1
        elif (str1[i] == '0') :
            str1Zeros += 1
        if (str2[i] == '1') :
            str2Ones += 1
        elif (str2[i] == '0') :
            str2Zeros += 1

    # If the number of 1's and 0's
    # are not same of the strings str1
    # and str2 then prnot possible
    if (str1Zeros != str2Zeros and str1Ones != str2Ones) :
        print("Not Possible")
    else :

        # Traversing through the
        # strings str1 and str2
        for i in range(len(str1)):

            # If the str1 character not
            # equals to str2 character
            if (str1[i] != str2[i]) :

                # Swaps 0 with 1 of the
                # string str1
                if (str1[i] == '0' and curStr1Ones > 0) :              
                    str1[i] = '1'
                    curStr1Ones -= 1

                # Breaks the loop as the count
                # of 1's is zero. Hence, no swaps possible
                if (str1[i] == '0' and curStr1Ones == 0) :
                    flag += 1
                    break

                # Swaps 1 with 0 in the string str1
                if (str1[i] == '1' and str2[i] == '0') :
                    str1[i] = '0'
                    curStr1Ones += 1

        if (flag == 0) :
            print("Possible")

        # Prnot possible
        else :
           print("Not Possible")

# Driver Code

# Given Strings
str1 = "0110"
str2 = "0011"

# Function Call
isBinaryStringsEqual(str1, str2)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Text;
class GFG
{

  // Function to check if it is possible to make
  // two binary strings equal by given operations
  static void isBinaryStringsEqual(string str1,
                                   string str2)
  {

    // Stores count of 1's and 0's
    // of the string str1
    int str1Zeros = 0, str1Ones = 0;

    // Stores count of 1's and 0's
    // of the string str2
    int str2Zeros = 0, str2Ones = 0;
    int flag = 0;

    // Stores current count of 1's
    // presenty in the string str1
    int curStr1Ones = 0;

    // Count the number of 1's and 0's
    // present in the strings str1 and str2
    for (int i = 0; i < str1.Length; i++)
    {
      if (str1[i] == '1')
      {
        str1Ones++;
      }

      else if (str1[i] == '0')
      {
        str1Zeros++;
      }

      if (str2[i] == '1')
      {
        str2Ones++;
      }

      else if (str2[i] == '0')
      {
        str2Zeros++;
      }
    }

    // If the number of 1's and 0's
    // are not same of the strings str1
    // and str2 then print not possible
    if (str1Zeros != str2Zeros
        && str1Ones != str2Ones)
    {
      Console.WriteLine("Not Possible");
    }

    else
    {

      // Traversing through the
      // strings str1 and str2
      for (int i = 0; i < str1.Length; i++)
      {

        // If the str1 character not
        // equals to str2 character
        if (str1[i] != str2[i])
        {

          // Swaps 0 with 1 of the
          // string str1
          if (str1[i] == '0' && curStr1Ones > 0)
          {
            StringBuilder sb
              = new StringBuilder(str1);
            sb[i] = '1';
            str1 = sb.ToString();
            curStr1Ones--;
          }

          // Breaks the loop as the count
          // of 1's is zero. Hence, no swaps
          // possible
          if (str1[i] == '0'
              && curStr1Ones == 0)
          {
            flag++;
            break;
          }

          // Swaps 1 with 0 in the string str1
          if (str1[i] == '1' && str2[i] == '0')
          {
            StringBuilder sb
              = new StringBuilder(str1);
            sb[i] = '0';
            str1 = sb.ToString();
            curStr1Ones++;
          }
        }
      }

      if (flag == 0)
      {
        Console.WriteLine("Possible");
      }

      // Print not possible
      else
      {
        Console.WriteLine("Not Possible");
      }
    }
  }

  // Driver Code
  static public void Main()
  {

    // Given Strings
    string str1 = "0110";
    string str2 = "0011";

    // Function Call
    isBinaryStringsEqual(str1, str2);
  }
}

// This code is contributed by dharanendralv23
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to check if it is possible to make
      // two binary strings equal by given operations
      function isBinaryStringsEqual(list1, list2) {
        var str1 = list1.split("");
        var str2 = list2.split("");
        // Stores count of 1's and 0's
        // of the string str1
        var str1Zeros = 0,
          str1Ones = 0;

        // Stores count of 1's and 0's
        // of the string str2
        var str2Zeros = 0,
          str2Ones = 0;
        var flag = 0;

        // Stores current count of 1's
        // presenty in the string str1
        var curStr1Ones = 0;

        // Count the number of 1's and 0's
        // present in the strings str1 and str2
        for (var i = 0; i < str1.length; i++) {
          if (str1[i] === "1") {
            str1Ones++;
          } else if (str1[i] === "0") {
            str1Zeros++;
          }

          if (str2[i] === "1") {
            str2Ones++;
          } else if (str2[i] === "0") {
            str2Zeros++;
          }
        }

        // If the number of 1's and 0's
        // are not same of the strings str1
        // and str2 then print not possible
        if (str1Zeros !== str2Zeros && str1Ones !== str2Ones) {
          document.write("Not Possible");
        } else {
          // Traversing through the
          // strings str1 and str2
          for (var i = 0; i < str1.length; i++) {
            // If the str1 character not
            // equals to str2 character
            if (str1[i] !== str2[i]) {
              // Swaps 0 with 1 of the
              // string str1
              if (str1[i] === "0" && curStr1Ones > 0) {
                str1[i] = "1";

                curStr1Ones--;
              }

              // Breaks the loop as the count
              // of 1's is zero. Hence, no swaps
              // possible
              if (str1[i] === "0" && curStr1Ones === 0) {
                flag++;
                break;
              }

              // Swaps 1 with 0 in the string str1
              if (str1[i] === "1" && str2[i] === "0") {
                str1[i] = "0";
                curStr1Ones++;
              }
            }
          }

          if (flag === 0) {
            document.write("Possible");
          }

          // Print not possible
          else {
            document.write("Not Possible");
          }
        }
      }

      // Driver Code
      // Given Strings
      var str1 = "0110";
      var str2 = "0011";

      // Function Call
      isBinaryStringsEqual(str1, str2);

</script>
```

**Output**

```
Possible
```

***时间复杂度:** O(|str1|)*
***辅助空间:** O(1)*