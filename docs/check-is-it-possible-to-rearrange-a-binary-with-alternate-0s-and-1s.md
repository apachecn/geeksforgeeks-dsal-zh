# 检查是否可以用交替的 0 和 1 重新排列二进制字符串

> 原文:[https://www . geeksforgeeks . org/check-有没有可能用 0 和 1 交替来重新排列二进制文件/](https://www.geeksforgeeks.org/check-is-it-possible-to-rearrange-a-binary-with-alternate-0s-and-1s/)

给定长度的二进制字符串，至少两个。我们需要检查是否有可能重新排列二进制字符串，使 0 和 1 交替出现。如果可能，则输出为是，否则输出为否。

**示例**:

> **输入** : 1011
> **输出**:否
> 我们不能把字符串重新排列成 0 和 1 交替出现。
> 
> **输入** : 1100
> **输出**:是
> 重新排列字符串正好有两种方式，分别是 0101 或者 1010。

我们可以将所有 0 放在偶数位置，将所有 1 放在奇数位置，或者将所有 0 放在奇数位置，将所有 1 放在偶数位置。如果字符串的长度是偶数，那么为了满足给定的条件，1 和 0 的计数必须相等。如果字符串的长度是奇数，那么为了满足给定的条件，1 和 0 的计数
的绝对差值必须是 1。

下面是上述方法的实现:

## C++

```
// CPP program to check if we can rearrange a
// string such that it has alternate 0s and 1s.
#include <bits/stdc++.h>
using namespace std;

// function to check the binary string
bool is_possible(string s)
{
    // length of string
    int l = s.length();

    int one = 0, zero = 0;

    for (int i = 0; i < l; i++) {

        // count zero's
        if (s[i] == '0')
            zero++;

        // count one's
        else
            one++;
    }

    // if length is even
    if (l % 2 == 0)
        return (one == zero);

    // if length is odd
    else
        return (abs(one - zero) == 1);
}

// Driver code
int main()
{
    string s = "100110";
    if (is_possible(s))
      cout << "Yes";
    else
      cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if we can rearrange a
// string such that it has alternate 0s and 1s.
import java.lang.Math;

public class GfG{

    // function to check the binary string
    public static boolean is_possible(String s)
    {
        // length of string
        int l = s.length();

        int one = 0, zero = 0;

        for (int i = 0; i < l; i++) {

            // count zero's
            if (s.charAt(i) == '0')
                zero++;

            // count one's
            else
                one++;
        }

        // if length is even
        if (l % 2 == 0) 
            return (one == zero);

        // if length is odd
        else
            return (Math.abs(one - zero) == 1);
    }

    public static void main(String []args){

        String s = "100110";
        if (is_possible(s))
          System.out.println("Yes");
        else
          System.out.println("No");
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 program to check if
# we can rearrange a
# string such that it has alternate
# 0s and 1s.

# function to check the binary string
def is_possible(s):

    # length of string
    l = len(s)

    one = 0
    zero = 0

    for i in range(0,l) :

        # count zero's
        if (s[i] == '0'):
            zero += 1

        # count one's
        else:
            one += 1

    # if length is even
    if (l % 2 == 0) :
        return (one == zero)

    # if length is odd
    else:
        return (abs(one - zero) == 1)

# Driver code
if __name__ == "__main__":
    s = "100110"
    if (is_possible(s)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to check if we can rearrange a
// string such that it has alternate 0s and 1s.
using System;

class GfG
{

    // function to check the binary string
    public static bool is_possible(String s)
    {
        // length of string
        int l = s.Length;

        int one = 0, zero = 0;

        for (int i = 0; i < l; i++)
        {

            // count zero's
            if (s[i] == '0')
                zero++;

            // count one's
            else
                one++;
        }

        // if length is even
        if (l % 2 == 0)
            return (one == zero);

        // if length is odd
        else
            return (Math.Abs(one - zero) == 1);
    }

    // Driver code
    public static void Main(String []args)
    {

        String s = "100110";
        if (is_possible(s))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if we can rearrange a
// string such that it has alternate 0s and 1s.

// function to check the binary string
function is_possible($s)
{
    // length of string
    $l = strlen($s);

    $one = 0;
    $zero = 0;

    for ($i = 0; $i < $l; $i++)
    {

        // count zero's
        if ($s[$i] == '0')
            $zero++;

        // count one's
        else
            $one++;
    }

    // if length is even
    if ($l % 2 == 0)
        return ($one == $zero);

    // if length is odd
    else
        return (abs($one - $zero) == 1);
}

// Driver code
$s = "100110";
if (is_possible($s))
    echo("Yes");
else
    echo("No");

// This code is contributed by
// Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to check if we can rearrange a
// string such that it has alternate 0s and 1s.

    // function to check the binary string
    function is_possible(s)
    {
        // length of string
        let l = s.length;

        let one = 0, zero = 0;

        for (let i = 0; i < l; i++) {

            // count zero's
            if (s[i] == '0')
                zero++;

            // count one's
            else
                one++;
        }

        // if length is even
        if (l % 2 == 0) 
            return (one == zero);

        // if length is odd
        else
            return (Math.abs(one - zero) == 1);
    }

    let s = "100110";
        if (is_possible(s))
          document.write("Yes");
        else
          document.write("No");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(l)，其中 l 为二进制字符串的长度。