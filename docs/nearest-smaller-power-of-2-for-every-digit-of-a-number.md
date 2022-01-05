# 一个数字的每一个数字最接近的 2 的小次方

> 原文:[https://www . geeksforgeeks . org/number 的每一位都是最近的 2 的小次方/](https://www.geeksforgeeks.org/nearest-smaller-power-of-2-for-every-digit-of-a-number/)

给定一个整数**数**，这个数的每个数字的任务是找到 2 的最高[幂，不超过那个数字。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

**示例:**

> **输入:** num = 4317
> **输出:** 4214
> **说明:**
> 2≤4 的最高幂是 4。
> 2≤3 的最高幂是 2。
> 2≤1 的最高幂为 1。
> 2≤7 的最高幂为 4。
> 
> **输入:**num = 8015
> T3】输出: 8014

**方法:**按照以下步骤解决问题:

1.  [将数字转换为其等价字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)。
2.  [穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
3.  如果数字是**‘0’**，打印 **0** 。
4.  否则，对于每一个数字 **x** ，计算 **2 <sup>(日志</sup>T5<sup>2</sup>T8<sup>(x)</sup>T11】。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest power of
// two for every digit of a given number
void highestPowerOfTwo(int num)
{
    // Converting number to string
    string s = to_string(num);

    // Traverse the array
    for (int i = 0; i < (int)s.size();
         i++) {

        if (s[i] == '0') {
            cout << "0";
            continue;
        }

        // Calculate log base 2
        // of the current digit s[i]
        int lg = log2(int(s[i]) - 48);

        // Highest power of 2 <= s[i]
        int p = pow(2, lg);

        // ASCII conversion
        cout << char(p + 48);
    }
}

// Driver Code
int main()
{
    int num = 4317;
    highestPowerOfTwo(num);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find the nearest power of
  // two for every digit of a given number
  static void highestPowerOfTwo(int num)
  {

    // Converting number to string
    String s = Integer.toString(num);

    // Traverse the array
    for (int i = 0; i < (int)s.length(); i++)
    {

      if (s.charAt(i) == '0')
      {
        System.out.print("0");
        continue;
      }

      // Calculate log base 2
      // of the current digit s[i]
      int lg
        = (int)(Math.log(s.charAt(i) - '0') / Math.log(2));

      // Highest power of 2 <= s[i]
      int p = (int)Math.pow(2, lg);

      // ASCII conversion
      System.out.print((char)(p + 48));
    }
  }

  // Driver Code
  public static void main(String args[])
  {
    int num = 4317;
    highestPowerOfTwo(num);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import math

# Function to find the nearest power of
# two for every digit of a given number
def highestPowerOfTwo(num) :

    # Converting number to string
    s = str(num)

    # Traverse the array
    for i in range(len(s)):
        if (s[i] == '0') :
            print("0")
            continue

        # Calculate log base 2
        # of the current digit s[i]
        lg = int(math.log2(ord(s[i]) - 48))

        # Highest power of 2 <= s[i]
        p = pow(2, lg)

        # ASCII conversion
        print(chr(p + 48), end = "")

# Driver Code
num = 4317
highestPowerOfTwo(num)

# This code is contributed by code_hunt.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to find the nearest power of
    // two for every digit of a given number
    static void highestPowerOfTwo(int num)
    {
        // Converting number to string
        String s = num.ToString();

        // Traverse the array
        for (int i = 0; i < (int)s.Length; i++)
        {

            if (s[i] == '0')
            {
                Console.Write("0");
                continue;
            }

            // Calculate log base 2
            // of the current digit s[i]
            int lg
                = (int)(Math.Log(s[i] - '0') / Math.Log(2));

            // Highest power of 2 <= s[i]
            int p = (int)Math.Pow(2, lg);

            // ASCII conversion
            Console.Write((char)(p + 48));
        }
    }

    // Driver Code
    public static void Main()
    {
        int num = 4317;
        highestPowerOfTwo(num);
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach

      // Function to find the nearest power of
      // two for every digit of a given number
      function highestPowerOfTwo(num) {
        // Converting number to string
        var s = num.toString();

        // Traverse the array
        for (var i = 0; i < s.length; i++) {
          if (s[i] === "0") {
            document.write("0");
            continue;
          }

          // Calculate log base 2
          // of the current digit s[i]
          var lg = parseInt(Math.log2(s[i].charCodeAt(0) - 48));

          // Highest power of 2 <= s[i]
          var p = Math.pow(2, lg);

          // ASCII conversion
          document.write(String.fromCharCode(p + 48));
        }
      }

      // Driver Code
      var num = 4317;
      highestPowerOfTwo(num);
    </script>
```

**Output:** 

```
4214
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*