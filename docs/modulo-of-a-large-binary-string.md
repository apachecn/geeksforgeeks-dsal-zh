# 大二进制串的模

> 原文:[https://www . geeksforgeeks . org/大二进制字符串模/](https://www.geeksforgeeks.org/modulo-of-a-large-binary-string/)

给定一个大的二进制字符串 **str** 和一个整数 **K** ，任务是找到 **str % K** 的值。
**举例:**

> **输入:** str = "1101 "，K = 45
> **输出:** 13
> 十进制(1101) % 45 = 13 % 45 = 13
> **输入:** str = "11010101 "，K = 112
> **输出:** 101
> 十进制(11010101)% 112 = 213% 112 = 213

**方法:**已知 **str** 为二进制字符串的 **(str % K)** 可以写成**((str[n–1]* 2<sup>0</sup>)+(str[n–2]* 2<sup>1</sup>)+…+(str[0]* 2<sup>n–1</sup>))% K**又可以写成**((str[T0 +((str[n–2]* 2<sup>1</sup>)% K)+…+((str[0]* 2<sup>n–1</sup>)% K)% K**。 这可以用来找到所需的答案，而无需实际将给定的二进制字符串转换为其十进制等价物。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the value of (str % k)
int getMod(string str, int n, int k)
{

    // pwrTwo[i] will store ((2^i) % k)
    int pwrTwo[n];
    pwrTwo[0] = 1 % k;
    for (int i = 1; i < n; i++)
    {
        pwrTwo[i] = pwrTwo[i - 1] * (2 % k);
        pwrTwo[i] %= k;
    }

    // To store the result
    int res = 0;
    int i = 0, j = n - 1;
    while (i < n)
    {

        // If current bit is 1
        if (str[j] == '1')
        {

            // Add the current power of 2
            res += (pwrTwo[i]);
            res %= k;
        }
        i++;
        j--;
    }
    return res;
}

// Driver code
int main()
{
    string str = "1101";
    int n = str.length();
    int k = 45;

    cout << getMod(str, n, k) << endl;
}

// This code is contributed by ashutosh450
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the value of (str % k)
    static int getMod(String str, int n, int k)
    {

        // pwrTwo[i] will store ((2^i) % k)
        int pwrTwo[] = new int[n];
        pwrTwo[0] = 1 % k;
        for (int i = 1; i < n; i++) {
            pwrTwo[i] = pwrTwo[i - 1] * (2 % k);
            pwrTwo[i] %= k;
        }

        // To store the result
        int res = 0;
        int i = 0, j = n - 1;
        while (i < n) {

            // If current bit is 1
            if (str.charAt(j) == '1') {

                // Add the current power of 2
                res += (pwrTwo[i]);
                res %= k;
            }
            i++;
            j--;
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "1101";
        int n = str.length();
        int k = 45;

        System.out.print(getMod(str, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the value of (str % k)
def getMod(_str, n, k) :

    # pwrTwo[i] will store ((2^i) % k)
    pwrTwo = [0] * n
    pwrTwo[0] = 1 % k
    for i in range(1, n):
        pwrTwo[i] = pwrTwo[i - 1] * (2 % k)
        pwrTwo[i] %= k

    # To store the result
    res = 0
    i = 0
    j = n - 1
    while (i < n) :

        # If current bit is 1
        if (_str[j] == '1') :

            # Add the current power of 2
            res += (pwrTwo[i])
            res %= k

        i += 1
        j -= 1

    return res

# Driver code
_str = "1101"
n = len(_str)
k = 45

print(getMod(_str, n, k))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the value of (str % k)
    static int getMod(string str, int n, int k)
    {
        int i;

        // pwrTwo[i] will store ((2^i) % k)
        int []pwrTwo = new int[n];

        pwrTwo[0] = 1 % k;

        for (i = 1; i < n; i++)
        {
            pwrTwo[i] = pwrTwo[i - 1] * (2 % k);
            pwrTwo[i] %= k;
        }

        // To store the result
        int res = 0;
        i = 0;
        int j = n - 1;
        while (i < n)
        {

            // If current bit is 1
            if (str[j] == '1')
            {

                // Add the current power of 2
                res += (pwrTwo[i]);
                res %= k;
            }
            i++;
            j--;
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
        string str = "1101";
        int n = str.Length;
        int k = 45;

        Console.Write(getMod(str, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the value of (str % k)
function getMod(str, n, k)
{

    // pwrTwo[i] will store ((2^i) % k)
    var pwrTwo = Array(n);
    pwrTwo[0] = 1 % k;
    for (var i = 1; i < n; i++)
    {
        pwrTwo[i] = pwrTwo[i - 1] * (2 % k);
        pwrTwo[i] %= k;
    }

    // To store the result
    var res = 0;
    var i = 0, j = n - 1;
    while (i < n)
    {

        // If current bit is 1
        if (str[j] == '1')
        {

            // Add the current power of 2
            res += (pwrTwo[i]);
            res %= k;
        }
        i++;
        j--;
    }
    return res;
}

// Driver code
var str = "1101";
var n = str.length;
var k = 45;
document.write( getMod(str, n, k));

</script>
```

**Output:** 

```
13
```