# 去掉数字后将数字减少到 4 的最小倍数

> 原文:[https://www . geeksforgeeks . org/将数字去掉数字后减少到 4 的最小倍数/](https://www.geeksforgeeks.org/reduce-the-number-to-minimum-multiple-of-4-after-removing-the-digits/)

给定一个整数 **N** ，任务是在去掉一些数字(可能没有)后，将该数减少到最小正整数 **X** ，使得 **X** 可以被 **4** 整除。打印 **-1** 如果不能减少到这样的倍数。
**举例:**

> **输入:**N = 7894566384
> **输出:** 4
> 删除除数字“4”的单个
> 出现以外的所有数字。
> **输入:** N = 17
> **输出:** -1

**方法:**因为结果数必须最小化。因此，检查数字中是否有任何数字等于 **'4'** 或 **'8'** ，因为这些数字在升序中可被 **4** 整除。如果没有这样的数字，则检查长度为 **2** 的所有数字子序列是否为 **4** 的任意倍数。如果仍然没有 **4** 的倍数，则该数是不可能的，因为任何超过 **2** 位数的数，即 **4** 的倍数，肯定会有一个可被 **4** 整除的子序列，位数少于 **3** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int TEN = 10;

// Function to return the minimum number
// that can be formed after removing
// the digits which is a multiple of 4
int minNum(string str, int len)
{
    int res = INT_MAX;

    // For every digit of the number
    for (int i = 0; i < len; i++) {

        // Check if the current digit
        // is divisible by 4
        if (str[i] == '4' || str[i] == '8') {
            res = min(res, str[i] - '0');
        }
    }

    for (int i = 0; i < len - 1; i++) {
        for (int j = i + 1; j < len; j++) {
            int num = (str[i] - '0') * TEN
                      + (str[j] - '0');

            // If any subsequence of two
            // digits is divisible by 4
            if (num % 4 == 0) {
                res = min(res, num);
            }
        }
    }

    return ((res == INT_MAX) ? -1 : res);
}

// Driver code
int main()
{
    string str = "17";
    int len = str.length();

    cout << minNum(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int TEN = 10;

// Function to return the minimum number
// that can be formed after removing
// the digits which is a multiple of 4
static int minNum(char[] str, int len)
{
    int res = Integer.MAX_VALUE;

    // For every digit of the number
    for (int i = 0; i < len; i++)
    {

        // Check if the current digit
        // is divisible by 4
        if (str[i] == '4' || str[i] == '8')
        {
            res = Math.min(res, str[i] - '0');
        }
    }

    for (int i = 0; i < len - 1; i++)
    {
        for (int j = i + 1; j < len; j++)
        {
            int num = (str[i] - '0') * TEN
                    + (str[j] - '0');

            // If any subsequence of two
            // digits is divisible by 4
            if (num % 4 == 0)
            {
                res = Math.min(res, num);
            }
        }
    }

    return ((res == Integer.MAX_VALUE) ? -1 : res);
}

// Driver code
public static void main(String[] args)
{
    String str = "17";
    int len = str.length();

    System.out.print(minNum(str.toCharArray(), len));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys
TEN = 10

# Function to return the minimum number
# that can be formed after removing
# the digits which is a multiple of 4
def minNum(str, len1):
    res = sys.maxsize

    # For every digit of the number
    for i in range(len1):

        # Check if the current digit
        # is divisible by 4
        if (str[i] == '4' or str[i] == '8'):
            res = min(res, ord(str[i]) - ord('0'))

    for i in range(len1 - 1):
        for j in range(i + 1, len1, 1):
            num = (ord(str[i]) - ord('0')) * TEN + \
                  (ord(str[j]) - ord('0'))

            # If any subsequence of two
            # digits is divisible by 4
            if (num % 4 == 0):
                res = min(res, num)

    if (res == sys.maxsize):
        return -1
    else:
        return res

# Driver code
if __name__ == '__main__':
    str = "17"
    len1 = len(str)

    print(minNum(str, len1))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int TEN = 10;

// Function to return the minimum number
// that can be formed after removing
// the digits which is a multiple of 4
static int minNum(char[] str, int len)
{
    int res = int.MaxValue;

    // For every digit of the number
    for (int i = 0; i < len; i++)
    {

        // Check if the current digit
        // is divisible by 4
        if (str[i] == '4' || str[i] == '8')
        {
            res = Math.Min(res, str[i] - '0');
        }
    }

    for (int i = 0; i < len - 1; i++)
    {
        for (int j = i + 1; j < len; j++)
        {
            int num = (str[i] - '0') * TEN
                    + (str[j] - '0');

            // If any subsequence of two
            // digits is divisible by 4
            if (num % 4 == 0)
            {
                res = Math.Min(res, num);
            }
        }
    }
    return ((res == int.MaxValue) ? -1 : res);
}

// Driver code
public static void Main(String[] args)
{
    String str = "17";
    int len = str.Length;

    Console.Write(minNum(str.ToCharArray(), len));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
var TEN = 10;

    // Function to return the minimum number
    // that can be formed after removing
    // the digits which is a multiple of 4
    function minNum( str , len) {
        var res = Number.MAX_VALUE;

        // For every digit of the number
        for (var i = 0; i < len; i++) {

            // Check if the current digit
            // is divisible by 4
            if (str[i] == '4' || str[i] == '8') {
                res = Math.min(res, str[i] - '0');
            }
        }

        for (i = 0; i < len - 1; i++) {
            for (j = i + 1; j < len; j++) {
                var num = (str[i] - '0') * TEN + (str[j] - '0');

                // If any subsequence of two
                // digits is divisible by 4
                if (num % 4 == 0) {
                    res = Math.min(res, num);
                }
            }
        }

        return ((res == Number.MAX_VALUE) ? -1 : res);
    }

    // Driver code
        var str = "17";
        var len = str.length;

        document.write(minNum(str, len));

// This code is contributed by umadevi9616.
</script>
```

**Output:** 

```
-1
```