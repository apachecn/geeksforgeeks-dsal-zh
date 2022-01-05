# 除以二进制数的 2 的最高幂

> 原文:[https://www . geeksforgeeks . org/二进制数除以二的最高幂/](https://www.geeksforgeeks.org/highest-power-of-2-that-divides-a-number-represented-in-binary/)

给定二进制字符串 **str** ，任务是求 2 的最大幂，除以给定二进制数的十进制等效值。

**示例:**

> **输入:** str = "100100"
> **输出:** 2
> 2 <sup>2</sup> = 4 是 2 除以 36 (100100)的最高幂。
> **输入:** str = "10010"
> **输出:** 1

**逼近:**从右边开始，计算二进制表示中的 0 的个数，这是 2 的最高幂，它将除以这个数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the highest power of 2
// which divides the given binary number
int highestPower(string str, int len)
{

    // To store the highest required power of 2
    int ans = 0;

    // Counting number of consecutive zeros
    // from the end in the given binary string
    for (int i = len - 1; i >= 0; i--) {
        if (str[i] == '0')
            ans++;
        else
            break;
    }

    return ans;
}

// Driver code
int main()
{
    string str = "100100";
    int len = str.length();
    cout << highestPower(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the highest power of 2
// which divides the given binary number
static int highestPower(String str, int len)
{

    // To store the highest required power of 2
    int ans = 0;

    // Counting number of consecutive zeros
    // from the end in the given binary string
    for (int i = len - 1; i >= 0; i--)
    {
        if (str.charAt(i) == '0')
            ans++;
        else
            break;
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    String str = "100100";
    int len = str.length();
    System.out.println(highestPower(str, len));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the highest power of 2
# which divides the given binary number
def highestPower(str, length):

    # To store the highest required power of 2
    ans = 0;

    # Counting number of consecutive zeros
    # from the end in the given binary string
    for i in range(length-1,-1,-1):
        if (str[i] == '0'):
            ans+=1;
        else:
            break;
    return ans;

# Driver code
def main():
    str = "100100";
    length = len(str);
    print(highestPower(str, length));

if __name__ == '__main__':
    main()

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the highest power of 2
// which divides the given binary number
static int highestPower(String str, int len)
{

    // To store the highest required power of 2
    int ans = 0;

    // Counting number of consecutive zeros
    // from the end in the given binary string
    for (int i = len - 1; i >= 0; i--)
    {
        if (str[i] == '0')
            ans++;
        else
            break;
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String str = "100100";
    int len = str.Length;
    Console.WriteLine(highestPower(str, len));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the highest power of 2
// which divides the given binary number
function highestPower($str, $len)
{

    // To store the highest required power of 2
    $ans = 0;

    // Counting number of consecutive zeros
    // from the end in the given binary string
    for ($i = $len - 1; $i >= 0; $i--)
    {
        if ($str[$i] == '0')
            $ans++;
        else
            break;
    }

    return $ans;
}

// Driver code
$str = "100100";
$len = strlen($str);
echo highestPower($str, $len);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the highest power of 2
// which divides the given binary number
function highestPower(str, len)
{

    // To store the highest required power of 2
    let ans = 0;

    // Counting number of consecutive zeros
    // from the end in the given binary string
    for (let i = len - 1; i >= 0; i--) {
        if (str[i] == '0')
            ans++;
        else
            break;
    }

    return ans;
}

// Driver code
    let str = "100100";
    let len = str.length;
    document.write(highestPower(str, len));

</script>
```

**Output**

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(1)