# 给定一个数字作为字符串，求递归加起来等于 9 的连续子序列的数目

> 原文:[https://www . geesforgeks . org/给定-数字-查找-数字-连续-子序列-递归-添加-9/](https://www.geeksforgeeks.org/given-number-find-number-contiguous-subsequences-recursively-add-9/)

给定一个数字作为字符串，编写一个函数来查找给定字符串的子字符串(或连续子序列)的数量，这些子字符串递归加起来等于 9。
例如 729 的数字递归加到 9，
7 + 2 + 9 = 18
递归 18
1+8 = 9
T5】示例:

```

Input: 4189
Output: 3
There are three substrings which recursively add to 9.
The substrings are 18, 9 and 189.

Input: 999
Output: 6
There are 6 substrings which recursively add to 9.
9, 99, 999, 9, 99, 9
```

一个数字的所有数字递归加起来是 9，如果这个数字是 9 的倍数。我们基本上需要检查所有子字符串的 s%9。下面程序中使用的一个技巧是进行模块化运算，以避免大字符串溢出。
下面是基于这种方法的简单实现。该实现假设输入数字中没有前导 0。

## C++

```
// C++ program to count substrings with recursive sum equal to 9
#include <iostream>
#include <cstring>
using namespace std;

int count9s(char number[])
{
    int count = 0; // To store result
    int n = strlen(number);

    // Consider every character as beginning of substring
    for (int i = 0; i < n; i++)
    {
        int sum = number[i] - '0';  //sum of digits in current substring

        if (number[i] == '9') count++;

        // One by one choose every character as an ending character
        for (int j = i+1; j < n; j++)
        {
            // Add current digit to sum, if sum becomes multiple of 5
            // then increment count. Let us do modular arithmetic to
            // avoid overflow for big strings
            sum = (sum + number[j] - '0')%9;

            if (sum == 0)
               count++;
        }
    }
    return count;
}

// driver program to test above function
int main()
{
    cout << count9s("4189") << endl;
    cout << count9s("1809");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// substrings with
// recursive sum equal to 9
import java.io.*;

class GFG
{
static int count9s(String number)
{
    // To store result
    int count = 0;
    int n = number.length();

    // Consider every character
    // as beginning of substring
    for (int i = 0; i < n; i++)
    {
        // sum of digits in
        // current substring
        int sum = number.charAt(i) - '0';

        if (number.charAt(i) == '9')
            count++;

        // One by one choose
        // every character as
        // an ending character
        for (int j = i + 1;
                 j < n; j++)
        {
            // Add current digit to
            // sum, if sum becomes
            // multiple of 5 then
            // increment count. Let
            // us do modular arithmetic
            // to avoid overflow for
            // big strings
            sum = (sum +
                   number.charAt(j) -
                            '0') % 9;

            if (sum == 0)
            count++;
        }
    }
    return count;
}

// Driver Code
public static void main (String[] args)
{
    System.out.println(count9s("4189"));
    System.out.println(count9s("1809"));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to count substrings
# with recursive sum equal to 9

def count9s(number):

    count = 0 # To store result
    n = len(number)

    # Consider every character as
    # beginning of substring
    for i in range(n):

        # sum of digits in current substring
        sum = ord(number[i]) - ord('0')    

        if (number[i] == '9'):
            count += 1

        # One by one choose every character
        # as an ending character
        for j in range(i + 1, n):

            # Add current digit to sum, if
            # sum becomes multiple of 5 then
            # increment count. Let us do
            # modular arithmetic to avoid
            # overflow for big strings
            sum = (sum + ord(number[j]) -
                         ord('0')) % 9

            if (sum == 0):
                count += 1
    return count

# Driver Code
if __name__ == "__main__":

    print(count9s("4189"))
    print(count9s("1809"))

# This code is contributed by ita_c
```

## C#

```
// C# program to count
// substrings with
// recursive sum equal to 9
using System;
class GFG
{
static int count9s(String number)
{
    // To store result
    int count = 0;
    int n = number.Length;

    // Consider every character
    // as beginning of substring
    for (int i = 0; i < n; i++)
    {
        // sum of digits in
        // current substring
        int sum = number[i] - '0';

        if (number[i] == '9')
            count++;

        // One by one choose
        // every character as
        // an ending character
        for (int j = i + 1;
                 j < n; j++)
        {
            // Add current digit to
            // sum, if sum becomes
            // multiple of 5 then
            // increment count. Let
            // us do modular arithmetic
            // to avoid overflow for
            // big strings
            sum = (sum + number[j] -
                           '0') % 9;

            if (sum == 0)
            count++;
        }
    }
    return count;
}

// Driver Code
public static void Main ()
{
    Console.WriteLine(count9s("4189"));
    Console.WriteLine(count9s("1809"));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count substrings
// with recursive sum equal to 9

function count9s($number)
{
    // To store result
    $count = 0;
    $n = strlen($number);

    // Consider every character as
    // beginning of substring
    for ($i = 0; $i < $n; $i++)
    {
        //sum of digits in
        // current substring
        $sum = $number[$i] - '0';

        if ($number[$i] == '9') $count++;

        // One by one choose every character
        // as an ending character
        for ($j = $i + 1; $j < $n; $j++)
        {

            // Add current digit to sum,
            // if sum becomes multiple of 5
            // then increment count. Let us
            // do modular arithmetic to
            // avoid overflow for big strings
            $sum = ($sum + $number[$j] - '0') % 9;

            if ($sum == 0)
            $count++;
        }
    }
    return $count;
}

    // Driver Code
    echo count9s("4189"),"\n";
    echo count9s("1809");

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to count substrings
// with recursive sum equal to 9

  function count9s(number){
      // To store result
      let count = 0;
      let n = (number.length);
      // Consider every character as beginning of substring
      for (let i = 0; i < n; i++)
      {
          //sum of digits in current substring
          let sum = number[i] - '0'; 

          if (number[i] == '9'){ count++;}

          // One by one choose every character
          // as an ending character
          for (let j = i+1; j < n; j++)
          {
              // Add current digit to sum,
              // if sum becomes multiple of 5
              // then increment count.
              // Let us do modular arithmetic to
              // avoid overflow for big strings
              sum = (sum + number[j] - '0')%9;

              if (sum == 0){
                 count++;
              }
          }
      }
      return count;
  }

  // driver program to test above function

  document.write( count9s("4189") );
  document.write("</br>");
  document.write( count9s("1809"));

</script>
```

**输出:**

```
3
5
```

上述程序的时间复杂度为 O(n <sup>2</sup> )。如果有更好的解决办法，请告诉我。
[给定一个数字作为字符串，求递归加起来等于 9 的连续子序列的个数|集合 2](https://www.geeksforgeeks.org/given-number-string-find-number-contiguous-subsequences-recursively-add-9-set-2/)
本文由 **Abhishek** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息