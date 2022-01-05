# 代表一个数的字符串的所有子串的和|集合 1

> 原文:[https://www . geesforgeks . org/代表数字的字符串的所有子字符串之和/](https://www.geeksforgeeks.org/sum-of-all-substrings-of-a-string-representing-a-number/)

给定一个表示为字符串的整数，我们需要得到这个字符串所有可能的子字符串之和。

**示例:**

```
Input  : num = “1234”
Output : 1670
Sum = 1 + 2 + 3 + 4 + 12 + 23 +
       34 + 123 + 234 + 1234 
    = 1670

Input  : num = “421”
Output : 491
Sum = 4 + 2 + 1 + 42 + 21 + 421 = 491
```

我们可以用动态规划来解决这个问题。在这种情况下，我们可以根据所有子字符串的结束数字来写一个总和，
所有子字符串的总和= sumofdigit[0]+sumofdigit[1]+sumofdigit[2]…+sumofdigit[n-1]，其中 n 是字符串的长度。
其中 sumofdigit[i]存储以第一个索引数字结束的所有子字符串的总和，在上面的示例中，

```
Example : num = "1234"
sumofdigit[0] = 1 = 1
sumofdigit[1] = 2 + 12  = 14
sumofdigit[2] = 3 + 23  + 123 = 149
sumofdigit[3] = 4 + 34  + 234 + 1234  = 1506
Result = 1670
```

现在我们可以得到 sumofdigit 值之间的关系，并且可以迭代地解决这个问题。每个 sumofdigit 可以用如下所示的前一个值来表示，

```
For above example,
sumofdigit[3] = 4 + 34 + 234 + 1234
           = 4 + 30 + 4 + 230 + 4 + 1230 + 4
           = 4*4 + 10*(3 + 23 +123)
           = 4*4 + 10*(sumofdigit[2])
In general, 
sumofdigit[i]  =  (i+1)*num[i] + 10*sumofdigit[i-1]
```

利用上述关系，我们可以在线性时间内解决这个问题。在下面的代码中，使用一个完整的数组来存储 sumofdigit，因为每个 sumofdigit 值只需要前一个值，所以我们可以在不分配完整数组的情况下解决这个问题。

## C++

```
// C++ program to print sum of all substring of
// a number represented as a string
#include <bits/stdc++.h>
using namespace std;

// Utility method to convert character digit to
// integer digit
int toDigit(char ch)
{
    return (ch - '0');
}

// Returns sum of all substring of num
int sumOfSubstrings(string num)
{
    int n = num.length();

    // allocate memory equal to length of string
    int sumofdigit[n];

    // initialize first value with first digit
    sumofdigit[0] = toDigit(num[0]);
    int res = sumofdigit[0];

    // loop over all digits of string
    for (int i = 1; i < n; i++) {
        int numi = toDigit(num[i]);

        // update each sumofdigit from previous value
        sumofdigit[i] = (i + 1) * numi + 10 * sumofdigit[i - 1];

        // add current value to the result
        res += sumofdigit[i];
    }

    return res;
}

// Driver code to test above methods
int main()
{
    string num = "1234";
    cout << sumOfSubstrings(num) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print sum of all substring of
// a number represented as a string
import java.util.Arrays;

class GFG {

    // Returns sum of all substring of num
    public static int sumOfSubstrings(String num)
    {
        int n = num.length();

        // allocate memory equal to length of string
        int sumofdigit[] = new int[n];

        // initialize first value with first digit
        sumofdigit[0] = num.charAt(0) - '0';
        int res = sumofdigit[0];

        // loop over all digits of string
        for (int i = 1; i < n; i++) {
            int numi = num.charAt(i) - '0';

            // update each sumofdigit from previous value
            sumofdigit[i] = (i + 1) * numi + 10 * sumofdigit[i - 1];

            // add current value to the result
            res += sumofdigit[i];
        }

        return res;
    }

    // Driver code to test above methods
    public static void main(String[] args)
    {
        String num = "1234";

        System.out.println(sumOfSubstrings(num));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python program to print
# sum of all substring of
# a number represented as
# a string

# Returns sum of all
# substring of num
def sumOfSubstrings(num):
    n = len(num)

    # allocate memory equal
    # to length of string
    sumofdigit = []

    # initialize first value
    # with first digit
    sumofdigit.append(int(num[0]))
    res = sumofdigit[0]

    # loop over all
    # digits of string
    for i in range(1, n):
        numi = int(num[i])

        # update each sumofdigit
        # from previous value
        sumofdigit.append((i + 1) *
                        numi + 10 * sumofdigit[i - 1])

        # add current value
        # to the result
        res += sumofdigit[i]

    return res

# Driver code
num = "1234"
print(sumOfSubstrings(num))

# This code is contributed
# by Sanjit_Prasad
```

## C#

```
// C# program to print sum of
// all substring of a number
// represented as a string
using System;

class GFG {

    // Returns sum of all
    // substring of num
    public static int sumOfSubstrings(String num)
    {
        int n = num.Length;

        // allocate memory equal to
        // length of string
        int[] sumofdigit = new int[n];

        // initialize first value
        // with first digit
        sumofdigit[0] = num[0] - '0';
        int res = sumofdigit[0];

        // loop over all digits
        // of string
        for (int i = 1; i < n; i++) {
            int numi = num[i] - '0';

            // update each sumofdigit
            // from previous value
            sumofdigit[i] = (i + 1) * numi + 10 * sumofdigit[i - 1];

            // add current value
            // to the result
            res += sumofdigit[i];
        }

        return res;
    }

    // Driver code
    public static void Main()
    {
        String num = "1234";

        Console.Write(sumOfSubstrings(num));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print sum of all
// substring of a number represented
// as a string

// Method to convert character
// digit to integer digit
function toDigit($ch)
{
    return ($ch - '0');
}

// Returns sum of all
// substring of num
function sumOfSubstrings($num)
{
    $n = strlen($num);

    // allocate memory equal to
    // length of string
    $sumofdigit[$n] = 0;

    // initialize first value
    // with first digit
    $sumofdigit[0] = toDigit($num[0]);
    $res = $sumofdigit[0];

    // loop over all digits of string
    for($i = 1; $i < $n; $i++)
    {
        $numi = toDigit($num[$i]);

        // update each sumofdigit
        // from previous value
        $sumofdigit[$i] = ($i + 1) * $numi + 10 *
                              $sumofdigit[$i - 1];

        // add current value to the result
        $res += $sumofdigit[$i];
    }

    return $res;
}

    // Driver Code
    $num = "1234";
    echo sumOfSubstrings($num) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

    // Javascript program to print sum of
    // all substring of a number
    // represented as a string

    // Returns sum of all
    // substring of num
    function sumOfSubstrings(num)
    {
        let n = num.length;

        // allocate memory equal to
        // length of string
        let sumofdigit = new Array(n);

        // initialize first value
        // with first digit
        sumofdigit[0] = num[0].charCodeAt() - '0'.charCodeAt();
        let res = sumofdigit[0];

        // loop over all digits
        // of string
        for (let i = 1; i < n; i++) {
            let numi = num[i].charCodeAt() - '0'.charCodeAt();

            // update each sumofdigit
            // from previous value
            sumofdigit[i] = (i + 1) * numi + 10 * sumofdigit[i - 1];

            // add current value
            // to the result
            res += sumofdigit[i];
        }

        return res;
    }

    let num = "1234";

      document.write(sumOfSubstrings(num));

</script>
```

**Output:** 

```
1670
```

**时间复杂度:** O(n)，其中 n 为输入字符串的长度。
**辅助空间:** O(n)

[代表一个数的字符串的所有子串之和|集合 2(恒定额外空间)](https://www.geeksforgeeks.org/sum-substrings-string-representing-number-set-2-constant-extra-space/)
本文由 [**乌特卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
**O(1)空间进场**
进场与上述相同。我们观察到的是，在当前索引处，我们依赖于当前和+先前的索引和，因此我们可以将它存储在两个变量 current 和 prev 中，而不是存储在 dp 数组中。

## C++14

```
// C++ program to print sum of all substring of
// a number represented as a string
#include <bits/stdc++.h>
using namespace std;

// Utility method to convert character digit to
// integer digit
int toDigit(char ch)
{
    return (ch - '0');
}

// Returns sum of all substring of num
int sumOfSubstrings(string num)
{
    int n = num.length();

    // storing prev value
    int prev = toDigit(num[0]);

    int res = prev; // ans

    int current = 0;

    // substrings sum upto current index
    // loop over all digits of string
    for (int i = 1; i < n; i++) {
        int numi = toDigit(num[i]);

        // update each sumofdigit from previous value
        current = (i + 1) * numi + 10 * prev;

        // add current value to the result
        res += current;
        prev = current; // update previous
    }

    return res;
}

// Driver code to test above methods
int main()
{
    string num = "1234";
    cout << sumOfSubstrings(num) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// sum of all subString of
// a number represented as a String
import java.util.*;
class GFG{

// Utility method to
// convert character
// digit to integer digit
static int toDigit(char ch)
{
  return (ch - '0');
}

// Returns sum of all subString of num
static int sumOfSubStrings(String num)
{
  int n = num.length();

  // Storing prev value
  int prev = toDigit(num.charAt(0));

  int res = prev;

  int current = 0;

  // SubStrings sum upto current index
  // loop over all digits of String
  for (int i = 1; i < n; i++)
  {
    int numi = toDigit(num.charAt(i));

    // Update each sumofdigit
    // from previous value
    current = (i + 1) * numi + 10 * prev;

    // Add current value to the result
    res += current;

    // Update previous
    prev = current;
  }
  return res;
}

// Driver code to test above methods
public static void main(String[] args)
{
  String num = "1234";
  System.out.print(sumOfSubStrings(num) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to print sum of all substring of
# a number represented as a string

# Returns sum of all substring of num
def sumOfSubstrings(num) :

    n = len(num)

    # storing prev value
    prev = int(num[0])

    res = prev # ans

    current = 0

    # substrings sum upto current index
    # loop over all digits of string
    for i in range(1, n) :
        numi = int(num[i])

        # update each sumofdigit from previous value
        current = (i + 1) * numi + 10 * prev

        # add current value to the result
        res += current
        prev = current # update previous

    return res

num = "1234"
print(sumOfSubstrings(num))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to print sum of all substring of
// a number represented as a string
using System;
class GFG {

    // Utility method to
    // convert character
    // digit to integer digit
    static int toDigit(char ch)
    {
      return (ch - '0');
    }

    // Returns sum of all subString of num
    static int sumOfSubStrings(string num)
    {
      int n = num.Length;

      // Storing prev value
      int prev = toDigit(num[0]);

      int res = prev;

      int current = 0;

      // SubStrings sum upto current index
      // loop over all digits of String
      for (int i = 1; i < n; i++)
      {
        int numi = toDigit(num[i]);

        // Update each sumofdigit
        // from previous value
        current = (i + 1) * numi + 10 * prev;

        // Add current value to the result
        res += current;

        // Update previous
        prev = current;
      }
      return res;
    }

  static void Main() {
    string num = "1234";
    Console.WriteLine(sumOfSubStrings(num));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program to print
// sum of all subString of
// a number represented as a String

// Utility method to
// convert character
// digit to integer digit
function toDigit(ch)
{
  return (ch - '0');
}

// Returns sum of all subString of num
function sumOfSubStrings(num)
{
  let n = num.length;

  // Storing prev value
  let prev = toDigit(num[0]);

  let res = prev;

  let current = 0;

  // SubStrings sum upto current index
  // loop over all digits of String
  for (let i = 1; i < n; i++)
  {
    let numi = toDigit(num[i]);

    // Update each sumofdigit
    // from previous value
    current = (i + 1) * numi + 10 * prev;

    // Add current value to the result
    res += current;

    // Update previous
    prev = current;
  }
  return res;
}

// Driver Code

        let num = "1234";
  document.write(sumOfSubStrings(num) + "\n");

</script>
```

**Output:** 

```
1670
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。