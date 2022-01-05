# 用 2^k 检查二进制串的可除性

> 原文:[https://www . geesforgeks . org/check-可分性-二进制-字符串-2k/](https://www.geeksforgeeks.org/check-divisibility-binary-string-2k/)

给定一个二进制字符串和一个数字 **k** ，任务是检查二进制字符串是否能被 2 <sup>k</sup> 整除。

示例:

```
Input : 11000  k = 2
Output : Yes
Explanation :
(11000)2 = (24)10
24 is evenly divisible by 2k i.e. 4.

Input : 10101  k = 3
Output : No
Explanation : 
(10101)2 = (21)10
21 is not evenly divisible by 2k i.e. 8.
```

**天真方法:**将二进制字符串计算成十进制，然后简单检查它是否能被 2 <sup>k</sup> 整除。但是，这种方法对于长二进制串是不可行的，因为从二进制串计算十进制数然后将其除以 2 <sup>k</sup> 的时间复杂度会很高。

**有效方法:**在二进制字符串中，检查最后 k 位。如果最后的 k 位都是 0，那么二进制数可以被 2 <sup>k</sup> 整除，否则不能整除。使用这种方法的时间复杂度为 0(k)。

**以下是实施办法。**

## C++

```
// C++ implementation to check whether
// given binary number is evenly
// divisible by 2^k or not
#include <bits/stdc++.h>
using namespace std;

// function to check whether
// given binary number is
// evenly divisible by 2^k or not
bool isDivisible(char str[], int k)
{
    int n = strlen(str);
    int c = 0;

    // count of number of 0 from last
    for (int i = 0; i < k; i++)   
        if (str[n - i - 1] == '0')        
            c++;

    // if count = k, number is evenly
    // divisible, so returns true else
    // false
    return (c == k);
}

// Driver program to test above
int main()
{
    // first example
    char str1[] = "10101100";
    int k = 2;
    if (isDivisible(str1, k))
        cout << "Yes" << endl;
    else
        cout << "No"
             << "\n";

    // Second example
    char str2[] = "111010100";
    k = 2;
    if (isDivisible(str2, k))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether
// given binary number is evenly
// divisible by 2^k or not
class GFG {

    // function to check whether
    // given binary number is
    // evenly divisible by 2^k or not
    static boolean isDivisible(String str, int k)
    {
        int n = str.length();
        int c = 0;

        // count of number of 0 from last
        for (int i = 0; i < k; i++)
            if (str.charAt(n - i - 1) == '0')        
                c++;

        // if count = k, number is evenly
        // divisible, so returns true else
        // false
        return (c == k);
    }

    // Driver program to test above
    public static void main(String args[])
    {

        // first example
        String str1 = "10101100";
        int k = 2;
        if (isDivisible(str1, k) == true)
            System.out.println("Yes");
        else
            System.out.println("No");

    // Second example
        String str2 = "111010100";
        k = 2;
        if (isDivisible(str2, k) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by JaideepPyne.
```

## 蟒蛇 3

```
# Python 3 implementation to check
# whether given binary number is
# evenly divisible by 2^k or not

# function to check whether
# given binary number is
# evenly divisible by 2^k or not
def isDivisible(str, k):
    n = len(str)
    c = 0

    # count of number of 0 from last
    for i in range(0, k):
        if (str[n - i - 1] == '0'):    
            c += 1

    # if count = k, number is evenly
    # divisible, so returns true else
    # false
    return (c == k)

# Driver program to test above
# first example
str1 = "10101100"
k = 2
if (isDivisible(str1, k)):
    print("Yes")
else:
    print("No")

# Second example
str2 = "111010100"
k = 2
if (isDivisible(str2, k)):
    print("Yes")
else:
    print("No")

# This code is contributed by Smitha
```

## C#

```
// C# implementation to check whether
// given binary number is evenly
// divisible by 2^k or not
using System;

class GFG {

    // function to check whether
    // given binary number is
    // evenly divisible by 2^k or not
    static bool isDivisible(String str, int k)
    {
        int n = str.Length;
        int c = 0;

        // count of number of 0 from last
        for (int i = 0; i < k; i++)
            if (str[n - i - 1] == '0')    
                c++;

        // if count = k, number is evenly
        // divisible, so returns true else
        // false
        return (c == k);
    }

    // Driver program to test above
    public static void Main()
    {

        // first example
        String str1 = "10101100";
        int k = 2;

        if (isDivisible(str1, k) == true)
            Console.Write("Yes\n");
        else
            Console.Write("No");

        // Second example
        String str2 = "111010100";
        k = 2;

        if (isDivisible(str2, k) == true)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check whether
// given binary number is evenly

// function to check whether
// given binary number is
// evenly divisible by 2^k or not
function isDivisible($str, $k)
{
    $n = strlen($str);
    $c = 0;

    // count of number
    // of 0 from last
    for ($i = 0; $i < $k; $i++)
        if ($str[$n - $i - 1] == '0')    
            $c++;

    // if count = k,
    // number is evenly
    // divisible, so
    // returns true else
    // false
    return ($c == $k);
}

    // Driver Code
    // first example
    $str1 = "10101100";
    $k = 2;
    if (isDivisible($str1, $k))
        echo "Yes", "\n";
    else
        echo "No", "\n";

    // Second example
    $str2= "111010100";
    $k = 2;
    if (isDivisible($str2, $k))
        echo "Yes", "\n";
    else
        echo "No", "\n";

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation to check whether
// given binary number is evenly
// divisible by 2^k or not

// Function to check whether
// given binary number is
// evenly divisible by 2^k or not
function isDivisible(str, k)
{
    let n = str.length;
    let c = 0;

    // Count of number of 0 from last
    for(let i = 0; i < k; i++)
        if (str[n - i - 1] == '0')    
            c++;

    // If count = k, number is evenly
    // divisible, so returns true else
    // false
    return (c == k);
}

// Driver code

// First example
let str1 = "10101100";
let k = 2;

if (isDivisible(str1, k) == true)
    document.write("Yes" + "</br>");
else
    document.write("No");

// Second example
let str2 = "111010100";
k = 2;

if (isDivisible(str2, k) == true)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
Yes
Yes
```

时间复杂度:O(k)