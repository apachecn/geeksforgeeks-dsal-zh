# 给定操作的最小可能数量

> 原文:[https://www . geesforgeks . org/给定操作的最小可能数/](https://www.geeksforgeeks.org/minimum-possible-number-with-the-given-operation/)

给定一个正整数 **N** ，任务是通过改变数字将这个整数转换成最小可能的整数，而不用前导零。一个数字 **X** 只有在 **X + Y = 9** 的情况下才能变成一个数字 **Y** 。
**举例:**

> **输入:** N = 589
> **输出:** 410
> 更改 5 - > 4、8 - > 1 和 9 - > 0
> **输入:** N = 934
> **输出:** 934
> 934 不能最小化。

**方式:**只有大于等于 **5** 的数字需要更改，因为更改小于 **5** 的数字会导致数字变大。更新所有要求的数字后，检查结果数字是否有前导零，如果有，则将其更改为 **9** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum possible
// integer that can be obtained from the
// given integer after performing
// the given operations
string minInt(string str)
{
    // For every digit
    for (int i = 0; i < str.length(); i++) {

        // Digits less than 5 need not to be
        // changed as changing them will
        // lead to a larger number
        if (str[i] >= '5') {
            str[i] = ('9' - str[i]) + '0';
        }
    }

    // The resulting integer
    // cannot have leading zero
    if (str[0] == '0')
        str[0] = '9';

    return str;
}

// Driver code
int main()
{
    string str = "589";

    cout << minInt(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

// Function to return the minimum possible
// integer that can be obtained from the
// given integer after performing
// the given operations

import java.util.*;

class GFG{

static String minInt(String str)
{
    // For every digit
    String s = "";
    for (int i = 0; i < str.length(); i++)
    {

        // Digits less than 5 need not to be
        // changed as changing them will
        // lead to a larger number
        if (str.charAt(i) >= '5')
        {
            s += (char)(('9' - str.charAt(i)) + '0');
        }
        else
        {
            s += str.charAt(i);
        }

    }

    // The resulting integer
    // cannot have leading zero
    if (str.charAt(0) == '0')
        s += '9';

    return s;
}

// Driver code
public static void main(String []args)
{
    String str = "589";

    System.out.println(minInt(str));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum possible
# integer that can be obtained from the
# given integer after performing
# the given operations
def minInt(str1):

    # For every digit
    for i in range(len(str1)):

        # Digits less than 5 need not to be
        # changed as changing them will
        # lead to a larger number
        if (str1[i] >= 5):
            str1[i] = (9 - str1[i])

    # The resulting integer
    # cannot have leading zero
    if (str1[0] == 0):
        str1[0] = 9

    temp = ""

    for i in str1:
        temp += str(i)

    return temp

# Driver code
str1 = "589"
str1 = [int(i) for i in str1]

print(minInt(str1))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the minimum possible
    // integer that can be obtained from the
    // given integer after performing
    // the given operations
    static string minInt(char []str)
    {
        // For every digit
        for (int i = 0; i < str.Length; i++)
        {

            // Digits less than 5 need not to be
            // changed as changing them will
            // lead to a larger number
            if ((int)str[i] >= (int)('5'))
            {
                str[i] = (char)(((int)('9') -
                                 (int)(str[i])) +
                                 (int)('0'));
            }
        }

        // The resulting integer
        // cannot have leading zero
        if (str[0] == '0')
            str[0] = '9';

        string s = new string(str);
        return s;
    }

    // Driver code
    static public void Main ()
    {
        string str = "589";
        Console.WriteLine(minInt(str.ToCharArray()));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Function to return the minimum possible
    // integer that can be obtained from the
    // given integer after performing
    // the given operations
    function minInt(str)
    {
        // For every digit
        for (let i = 0; i < str.length; i++)
        {

            // Digits less than 5 need not to be
            // changed as changing them will
            // lead to a larger number
            if (str[i].charCodeAt() >= ('5').charCodeAt())
            {
                str[i] = String.fromCharCode((('9').charCodeAt() -
                                 (str[i]).charCodeAt()) +
                                 ('0').charCodeAt());
            }
        }

        // The resulting integer
        // cannot have leading zero
        if (str[0] == '0')
            str[0] = '9';

        let s = str.join("");
        return s;
    }

    let str = "589";
      document.write(minInt(str.split('')));

</script>
```

**Output:** 

```
410
```