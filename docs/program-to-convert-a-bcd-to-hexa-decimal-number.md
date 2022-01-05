# 将二进制数转换为六进制数的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-a-BCD-to-hexa-decimal-number/](https://www.geeksforgeeks.org/program-to-convert-a-bcd-to-hexa-decimal-number/)

给定一个二进制数，任务是将这个二进制数转换成其等价的[六进制数](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)。
**例:**

> **输入:** 100000101111
> **输出:** 82F
> **解释:**
> 将数字分成 4 的组块，就变成了 **1000 0010 1111** 。
> 这里 **1000** 相当于 **8** 、
> **0010** 相当于 **2** 、
> T22**1111**相当于 **F**
> 因此，数字变成了 **82F**
> **输入:** 10101101 【T32
> 这里 **1010** 相当于**A**
> **1101**相当于 **D** 。
> 因此，编号成为 **AD** 。

**进场:**

1.  将给定的二进制数分成 4 块，开始计算其等价的**十六进制形式**。
2.  把这个数字存储在一个向量中。
3.  对给定的**二进制数**的所有数字重复该过程。
4.  以相反的顺序打印矢量中存储的数字。

下面是上述方法的实现:

## C++

```
// C++ code to convert Binary to its
// HexaDecimal number(base 16).

// Including Header Files
#include <bits/stdc++.h>
using namespace std;

// Function to convert
// Binary to HexaDecimal
void bToHexaDecimal(string s)
{
    int len = s.length(), check = 0;
    int num = 0, sum = 0, mul = 1;
    vector<char> ans;

    // Iterating through
    // the bits backwards
    for (int i = len - 1; i >= 0; i--) {
        sum += (s[i] - '0') * mul;
        mul *= 2;
        check++;

        // Computing the HexaDecimal
        // Number formed so far
        // and storing it in a vector.
        if (check == 4 || i == 0) {
            if (sum <= 9)
                ans.push_back(sum + '0');
            else
                ans.push_back(sum + 55);

            // Reinitializing all
            // variables for next group.
            check = 0;
            sum = 0;
            mul = 1;
        }
    }

    len = ans.size();

    // Printing the Hexadecimal
    // number formed so far.
    for (int i = len - 1; i >= 0; i--)
        cout << ans[i];
}

// Driver Code
int main()
{
    string s = "100000101111";

    // Function Call
    bToHexaDecimal(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to convert BCD to its
// HexaDecimal number(base 16).
// Including Header Files
import java.util.*;
class GFG{

// Function to convert
// BCD to HexaDecimal
static void bcdToHexaDecimal(char []s)
{
  int len = s.length, check = 0;
  int num = 0, sum = 0, mul = 1;
  Vector<Character> ans =
         new Vector<Character>();

  // Iterating through
  // the bits backwards
  for (int i = len - 1; i >= 0; i--)
  {
    sum += (s[i] - '0') * mul;
    mul *= 2;
    check++;

    // Computing the HexaDecimal
    // Number formed so far
    // and storing it in a vector.
    if (check == 4 || i == 0)
    {
      if (sum <= 9)
        ans.add((char) (sum + '0'));
      else
        ans.add((char) (sum + 55));

      // Reinitializing all
      // variables for next group.
      check = 0;
      sum = 0;
      mul = 1;
    }
  }

  len = ans.size();

  // Printing the Hexadecimal
  // number formed so far.
  for (int i = len - 1; i >= 0; i--)
    System.out.print(ans.get(i));
}

// Driver Code
public static void main(String[] args)
{
  String s = "100000101111";

  // Function Call
  bcdToHexaDecimal(s.toCharArray());
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 code to convert BCD to its
# hexadecimal number(base 16).

# Function to convert BCD to hexadecimal
def bcdToHexaDecimal(s):

    len1 = len(s)
    check = 0
    num = 0
    sum = 0
    mul = 1
    ans = []

    # Iterating through the bits backwards
    i = len1 - 1

    while(i >= 0):
        sum += (ord(s[i]) - ord('0')) * mul
        mul *= 2
        check += 1

        # Computing the hexadecimal number formed
        # so far and storing it in a vector.
        if (check == 4 or i == 0):

            if (sum <= 9):
                ans.append(chr(sum + ord('0')))
            else:
                ans.append(chr(sum + 55));

            # Reinitializing all variables
            # for next group.
            check = 0
            sum = 0
            mul = 1

        i -= 1

    len1 = len(ans)

    # Printing the hexadecimal
    # number formed so far.
    i = len1 - 1

    while(i >= 0):
        print(ans[i], end = "")
        i -= 1

# Driver Code
if __name__ == '__main__':

    s = "100000101111"

    # Function Call
    bcdToHexaDecimal(s)

# This code is contributed by Samarth
```

## C#

```
// C# code to convert BCD to its
// HexaDecimal number(base 16).
// Including Header Files
using System;
using System.Collections.Generic;
class GFG{

// Function to convert
// BCD to HexaDecimal
static void bcdToHexaDecimal(char []s)
{
  int len = s.Length, check = 0;
  int num = 0, sum = 0, mul = 1;
  List<char> ans =
       new List<char>();

  // Iterating through
  // the bits backwards
  for (int i = len - 1; i >= 0; i--)
  {
    sum += (s[i] - '0') * mul;
    mul *= 2;
    check++;

    // Computing the HexaDecimal
    // Number formed so far
    // and storing it in a vector.
    if (check == 4 || i == 0)
    {
      if (sum <= 9)
        ans.Add((char) (sum + '0'));
      else
        ans.Add((char) (sum + 55));

      // Reinitializing all
      // variables for next group.
      check = 0;
      sum = 0;
      mul = 1;
    }
  }

  len = ans.Count;

  // Printing the Hexadecimal
  // number formed so far.
  for (int i = len - 1; i >= 0; i--)
    Console.Write(ans[i]);
}

// Driver Code
public static void Main(String[] args)
{
  String s = "100000101111";

  // Function Call
  bcdToHexaDecimal(s.ToCharArray());
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript code to convert Binary to its
// HexaDecimal number(base 16).

// Including Header Files

// Function to convert
// Binary to HexaDecimal
function bToHexaDecimal(s) {
    let len = s.length, check = 0;
    let num = 0, sum = 0, mul = 1;
    let ans = new Array();

    // Iterating through
    // the bits backwards
    for (let i = len - 1; i >= 0; i--) {
        sum += (s[i].charCodeAt(0) - '0'.charCodeAt(0)) * mul;
        mul *= 2;
        check++;

        // Computing the HexaDecimal
        // Number formed so far
        // and storing it in a vector.
        if (check == 4 || i == 0) {
            if (sum <= 9)
                ans.push(String.fromCharCode(sum + '0'.charCodeAt(0)));
            else
                ans.push(String.fromCharCode(sum + 55));

            // Reinitializing all
            // variables for next group.
            check = 0;
            sum = 0;
            mul = 1;
        }
    }

    len = ans.length;

    // Printing the Hexadecimal
    // number formed so far.
    for (let i = len - 1; i >= 0; i--)
        document.write(ans[i]);
}

// Driver Code

let s = "100000101111";

// Function Call
bToHexaDecimal(s);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
82F
```