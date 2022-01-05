# 找到最多换 K 位可以组成的最大数字

> 原文:[https://www . geeksforgeeks . org/find-最多改变 k 位数可以形成的最大数字/](https://www.geeksforgeeks.org/find-the-largest-number-that-can-be-formed-by-changing-at-most-k-digits/)

给定代表一个数的字符串 **str** 和一个整数 **K** ，任务是找出给定数中最多改变 **K** 位可以构成的最大数。

**示例:**

> **输入:** str = "569431 "，K = 3
> **输出:** 999931
> 将第一、二、四位数字替换为 9。
> **输入:** str = "5687 "，K = 2
> **输出:** 9987

**方法:**为了得到可能的最大数字，最左边的数字必须替换为 9s。对于从最左边的数字开始的数字的每一个数字，如果它还不是 9，并且 K 大于 0，那么用 9 替换它，并将 K 减 1。当 K 大于 0 时，对每个数字重复这些步骤。最后，打印更新后的号码。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the maximum number
// that can be formed by changing
// at most k digits in str
string findMaximumNum(string str, int n, int k)
{

    // For every digit of the number
    for (int i = 0; i < n; i++) {

        // If no more digits can be replaced
        if (k < 1)
            break;

        // If current digit is not already 9
        if (str[i] != '9') {

            // Replace it with 9
            str[i] = '9';

            // One digit has been used
            k--;
        }
    }

    return str;
}

// Driver code
int main()
{
    string str = "569431";
    int n = str.length();
    int k = 3;

    cout << findMaximumNum(str, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to return the maximum number
    // that can be formed by changing
    // at most k digits in str
    static StringBuilder findMaximumNum(StringBuilder str,
                                             int n, int k)
    {

        // For every digit of the number
        for (int i = 0; i < n; i++)
        {

            // If no more digits can be replaced
            if (k < 1)
                break;

            // If current digit is not already 9
            if (str.charAt(i) != '9')
            {

                // Replace it with 9
                str.setCharAt(i, '9');

                // One digit has been used
                k--;
            }
        }
        return str;
    }

    // Driver code
    public static void main (String [] args)
    {
        StringBuilder str = new StringBuilder("569431");

        int n = str.length();
        int k = 3;

        System.out.println(findMaximumNum(str, n, k));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum number
# that can be formed by changing
# at most k digits in str
def findMaximumNum(st, n, k):

    # For every digit of the number
    for i in range(n):

        # If no more digits can be replaced
        if (k < 1):
            break

        # If current digit is not already 9
        if (st[i] != '9'):

            # Replace it with 9
            st = st[0:i] + '9' + st[i + 1:]

            # One digit has been used
            k -= 1

    return st

# Driver code
st = "569431"
n = len(st)
k = 3
print(findMaximumNum(st, n, k))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the approach
using System;
using System.Text;

class GFG
{
    // Function to return the maximum number
    // that can be formed by changing
    // at most k digits in str
    static StringBuilder findMaximumNum(StringBuilder str,
                                        int n, int k)
    {

        // For every digit of the number
        for (int i = 0; i < n; i++)
        {

            // If no more digits can be replaced
            if (k < 1)
                break;

            // If current digit is not already 9
            if (str[i] != '9')
            {

                // Replace it with 9
                str[i] = '9';

                // One digit has been used
                k--;
            }
        }
        return str;
    }

    // Driver code
    public static void Main ()
    {
        StringBuilder str = new StringBuilder("569431");

        int n = str.Length;
        int k = 3;

        Console.WriteLine(findMaximumNum(str, n, k));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the maximum number
      // that can be formed by changing
      // at most k digits in str
      function findMaximumNum(str, n, k) {
        // For every digit of the number
        for (var i = 0; i < n; i++) {
          // If no more digits can be replaced
          if (k < 1) break;

          // If current digit is not already 9
          if (str[i] !== "9") {
            // Replace it with 9
            str[i] = "9";

            // One digit has been used
            k--;
          }
        }
        return str.join("");
      }

      // Driver code
      var str = "569431";
      var n = str.length;
      var k = 3;

      document.write(findMaximumNum(str.split(""), n, k));
    </script>
```

**Output:** 

```
999931
```