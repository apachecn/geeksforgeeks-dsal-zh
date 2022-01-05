# 检查任意字符的频率是否超过字符串长度的一半

> 原文:[https://www . geesforgeks . org/check-如果任何字符的频率超过字符串长度的一半/](https://www.geeksforgeeks.org/check-if-the-frequency-of-any-character-is-more-than-half-the-length-of-the-string/)

给定一个字符串 **str** ，任务是检查任何字符的频率是否超过给定字符串长度的一半。字符可以是小写或大写字母、数字和特殊字符。

**示例:**

> **输入:**str = " AAa * 2aaa "
> T3】输出:是
> A 的频率超过了字符串长度的一半。
> 
> **输入:**str = " abB @ 2a "
> T3】输出:否

**方法:**使用长度为 2 <sup>8</sup> 的频率数组，即 256，可以很容易地解决这个问题，因为有 256 个不同的字符。遍历字符串，并在每次遇到该字符串时，将频率数组中的字符数增加 1。最后，遍历频率数组，检查任何字符的频率是否超过字符串长度的一半。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAXN 256

// Function that returns true if the frequency
// of any character is more than half the
// length of the string
bool checkHalfFrequency(string str)
{

    // Length of the string
    int L = str.size();

    // Initialize a frequency array
    int fre[MAXN] = { 0 };

    // Iterate the string and update the
    // frequency of each of the character
    for (int i = 0; i < L; i++)
        fre[str[i]]++;

    // Iterate the frequency array
    for (int i = 0; i < MAXN; i++)

        // If condition is satisfied
        if (fre[i] > L / 2)
            return true;

    return false;
}

// Driver code
int main()
{
    string str = "GeeksforGeeks";

    if (checkHalfFrequency(str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    static int MAXN = 256;

    // Function that returns true if the frequency
    // of any character is more than half the
    // length of the string
    static boolean checkHalfFrequency(String str)
    {

        // Length of the string
        int L = str.length();

        // Initialize a frequency array
        int fre[] = new int[MAXN];

        // Iterate the string and update the
        // frequency of each of the character
        for (int i = 0; i < L; i++)
        {
            fre[str.charAt(i)]++;
        }

        // Iterate the frequency array
        for (int i = 0; i < MAXN; i++) // If condition is satisfied
        {
            if (fre[i] > L / 2)
            {
                return true;
            }
        }

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "GeeksforGeeks";

        if (checkHalfFrequency(str))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAXN = 256

# Function that returns true if the frequency
# of any character is more than half the
# length of the String
def checkHalfFrequency(Str):

    # Length of the String
    L = len(Str)

    # Initialize a frequency array
    fre = [0 for i in range(MAXN)]

    # Iterate the and update the
    # frequency of each of the character
    for i in range(L):
        fre[ord(Str[i])] += 1

    # Iterate the frequency array
    for i in range(MAXN):

        # If condition is satisfied
        if (fre[i] > L // 2):
            return True

    return False

# Driver code
Str = "GeeksforGeeks"

if (checkHalfFrequency(Str)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAXN = 256;

    // Function that returns true if the frequency
    // of any character is more than half the
    // length of the string
    static bool checkHalfFrequency(string str)
    {

        // Length of the string
        int L = str.Length;

        // Initialize a frequency array
        int[] fre = new int[MAXN];

        // Iterate the string and update the
        // frequency of each of the character
        for (int i = 0; i < L; i++)
        {
            fre[str[i]]++;
        }

        // Iterate the frequency array
        for (int i = 0; i < MAXN; i++) // If condition is satisfied
        {
            if (fre[i] > L / 2)
            {
                return true;
            }
        }

        return false;
    }

    // Driver code
    public static void Main()
    {
        string str = "GeeksforGeeks";

        if (checkHalfFrequency(str))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

/* This code contributed by Code_Mech */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if the frequency
// of any character is more than half the
// length of the string
function checkHalfFrequency($str)
{
    $MAXN = 256;

    // Length of the string
    $L = strlen($str);

    // Initialize a frequency array
    $fre = array_fill(0, $MAXN, 0 );

    // Iterate the string and update the
    // frequency of each of the character
    for ($i = 0; $i < $L; $i++)
    {
        $fre[ord($str[$i])]++;
    }

    // Iterate the frequency array
    for ($i = 0; $i < $MAXN; $i++) // If condition is satisfied
    {
        if ($fre[$i] > (int)($L / 2))
        {
            return true;
        }
    }

    return false;
}

// Driver code
$str = "GeeksforGeeks";

if (checkHalfFrequency($str))
{
    echo("Yes");
}
else
{
    echo("No");
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var MAXN = 256

// Function that returns true if the frequency
// of any character is more than half the
// length of the string
function checkHalfFrequency(str)
{

    // Length of the string
    var L = str.length;

    // Initialize a frequency array
    var fre = Array(MAXN);

    // Iterate the string and update the
    // frequency of each of the character
    for(var i = 0; i < L; i++)
        fre[str[i]]++;

    // Iterate the frequency array
    for(var i = 0; i < MAXN; i++)

        // If condition is satisfied
        if (fre[i] > L / 2)
            return true;

    return false;
}

// Driver code
var str = "GeeksforGeeks";

if (checkHalfFrequency(str))
    document.write( "Yes");
else
    document.write( "No");

// This code is contributed by itsok

</script>
```

**Output:** 

```
No
```

**时间复杂度:** O(N)，N =字符串长度

**辅助空间:** O(1)