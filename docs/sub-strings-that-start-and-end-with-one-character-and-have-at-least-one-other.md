# 以一个字符开始和结束并且至少有一个其他字符的子字符串

> 原文:[https://www . geeksforgeeks . org/sub-strings-以一个字符开头和结尾并至少有一个其他字符/](https://www.geeksforgeeks.org/sub-strings-that-start-and-end-with-one-character-and-have-at-least-one-other/)

给定仅包含字符 **x** 和 **y** 的字符串 **str** ，任务是计算以 **x** 开始和结束的所有子字符串，并且至少有一个单独的 **y** 。

**示例:**

> **输入:**str = " xyyxx "
> T3】输出:2
> “xyyx”和“xyyxx”是唯一有效的子字符串。
> 
> **输入:**str = " xyy "
> T3】输出: 0

**进场:**

*   创建一个数组 **countX[]** ，其中 **countX[i]** 存储从 **i** 到**n–1**的总计 **x** 。
*   现在，对于字符串中的每一个 **x** ，找到在这个 **x** 之后出现的第一个 **y** 。
*   并更新**count = count+countX[index of(y)】**，因为以此 **x** 为起始索引，所有子字符串在找到 **y** 后，将在任意 **x** 处结束。
*   最后返回**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function that returns the index of next occurrence
// of the character c in string str starting from index start
int nextIndex(string str, int start, char c)
{

    // Starting from start
    for (int i = start; i < str.length(); i++) {

        // If current character = c
        if (str[i] == c)
            return i;
    }

    // Not found
    return -1;
}

// Function to return the count of required sub-strings
int countSubStrings(string str)
{
    int i, n = str.length();

    // Stores running count of 'x' starting from the end
    int countX[n];

    int count = 0;
    for (i = n - 1; i >= 0; i--) {
        if (str[i] == 'x')
            count++;
        countX[i] = count;
    }

    // Next index of 'x' starting from index 0
    int nextIndexX = nextIndex(str, 0, 'x');

    // Next index of 'y' starting from index 0
    int nextIndexY = nextIndex(str, 0, 'y');

    // To store the count of required sub-strings
    count = 0;
    while (nextIndexX != -1 && nextIndexY != -1) {

        // If 'y' appears before 'x'
        // it won't contribute to a valid sub-string
        if (nextIndexX > nextIndexY) {

            // Find next occurrence of 'y'
            nextIndexY = nextIndex(str, nextIndexY + 1, 'y');
            continue;
        }

        // If 'y' appears after 'x'
        // every sub-string ending at an 'x' appearing after this 'y'
        // and starting with the current 'x' is a valid sub-string
        else {
            count += countX[nextIndexY];

            // Find next occurrence of 'x'
            nextIndexX = nextIndex(str, nextIndexX + 1, 'x');
        }
    }

    // Return the count
    return count;
}

// Driver code
int main()
{

    string s = "xyyxx";

    cout << countSubStrings(s);
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function that returns the index of next occurrence
    // of the character c in string str starting from index start
    static int nextIndex(String str, int start, char c)
    {

        // Starting from start
        for (int i = start; i < str.length(); i++) {

            // If current character = c
            if (str.charAt(i) == c)
                return i;
        }

        // Not found
        return -1;
    }

    // Function to return the count of required sub-strings
    static int countSubStrings(String str)
    {
        int i, n = str.length();

        // Stores running count of 'x' starting from the end
        int countX[] = new int[n];

        int count = 0;
        for (i = n - 1; i >= 0; i--) {
            if (str.charAt(i) == 'x')
                count++;
            countX[i] = count;
        }

        // Next index of 'x' starting from index 0
        int nextIndexX = nextIndex(str, 0, 'x');

        // Next index of 'y' starting from index 0
        int nextIndexY = nextIndex(str, 0, 'y');

        // To store the count of required sub-strings
        count = 0;
        while (nextIndexX != -1 && nextIndexY != -1) {

            // If 'y' appears before 'x'
            // it won't contribute to a valid sub-string
            if (nextIndexX > nextIndexY) {

                // Find next occurrence of 'y'
                nextIndexY = nextIndex(str, nextIndexY + 1, 'y');
                continue;
            }

            // If 'y' appears after 'x'
            // every sub-string ending at an 'x' appearing after this 'y'
            // and starting with the current 'x' is a valid sub-string
            else {
                count += countX[nextIndexY];

                // Find next occurrence of 'x'
                nextIndexX = nextIndex(str, nextIndexX + 1, 'x');
            }
        }

        // Return the count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {

        String s = "xyyxx";

        System.out.println(countSubStrings(s));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the index of next occurrence
# of the character c in string str starting from index start
def nextIndex(str, start, c):

    # Starting from start
    for i in range(start,len(str)):

        # If current character = c
        if (str[i] == c):
            return i;

    # Not found
    return -1;

# Function to return the count of required sub-strings
def countSubStrings(str):

    n = len(str)

    # Stores running count of 'x' starting from the end
    countX=[0]*n;

    count = 0;
    for i in range(n-1,-1,-1):
        if (str[i] == 'x'):
            count=count+1
        countX[i] = count

    # Next index of 'x' starting from index 0
    nextIndexX = nextIndex(str, 0, 'x')

    # Next index of 'y' starting from index 0
    nextIndexY = nextIndex(str, 0, 'y')

    # To store the count of required sub-strings
    count = 0;
    while (nextIndexX != -1 and nextIndexY != -1):

        # If 'y' appears before 'x'
        # it won't contribute to a valid sub-string
        if (nextIndexX > nextIndexY):

            # Find next occurrence of 'y'
            nextIndexY = nextIndex(str, nextIndexY + 1, 'y')
            continue

        # If 'y' appears after 'x'
        # every sub-string ending at an 'x' appearing after this 'y'
        # and starting with the current 'x' is a valid sub-string
        else :
            count += countX[nextIndexY]

            # Find next occurrence of 'x'
            nextIndexX = nextIndex(str, nextIndexX + 1, 'x');

    # Return the count
    return count

# Driver code

s = "xyyxx";

print(countSubStrings(s));

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach

using System;

public class GFG {

    // Function that returns the index of next occurrence
    // of the character c in string str starting from index start
    static int nextIndex(string str, int start, char c)
    {

        // Starting from start
        for (int i = start; i < str.Length; i++) {

            // If current character = c
            if (str[i] == c)
                return i;
        }

        // Not found
        return -1;
    }

    // Function to return the count of required sub-strings
    static int countSubStrings(string str)
    {
        int i, n = str.Length ;

        // Stores running count of 'x' starting from the end
        int []countX = new int[n];

        int count = 0;
        for (i = n - 1; i >= 0; i--) {
            if (str[i] == 'x')
                count++;
            countX[i] = count;
        }

        // Next index of 'x' starting from index 0
        int nextIndexX = nextIndex(str, 0, 'x');

        // Next index of 'y' starting from index 0
        int nextIndexY = nextIndex(str, 0, 'y');

        // To store the count of required sub-strings
        count = 0;
        while (nextIndexX != -1 && nextIndexY != -1) {

            // If 'y' appears before 'x'
            // it won't contribute to a valid sub-string
            if (nextIndexX > nextIndexY) {

                // Find next occurrence of 'y'
                nextIndexY = nextIndex(str, nextIndexY + 1, 'y');
                continue;
            }

            // If 'y' appears after 'x'
            // every sub-string ending at an 'x' appearing after this 'y'
            // and starting with the current 'x' is a valid sub-string
            else {
                count += countX[nextIndexY];

                // Find next occurrence of 'x'
                nextIndexX = nextIndex(str, nextIndexX + 1, 'x');
            }
        }

        // Return the count
        return count;
    }

    // Driver code
    public static void Main()
    {

        string s = "xyyxx";

        Console.WriteLine(countSubStrings(s));
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns the index of next occurrence
// of the character c in string str starting from index start
function nextIndex($str, $start, $c)
{

    // Starting from start
    for ($i = $start; $i < strlen($str); $i++) {

        // If current character = c
        if ($str[$i] == $c)
            return $i;
    }

    // Not found
    return -1;
}

// Function to return the count of required sub-strings
function countSubStrings($str)
{
    $n = strlen($str);

    // Stores running count of 'x' starting from the end
    $countX = array(0,$n,NULL);

    $count = 0;
    for ($i = $n - 1; $i >= 0; $i--) {
        if ($str[$i] == 'x')
            $count++;
        $countX[$i] = $count;
    }

    // Next index of 'x' starting from index 0
    $nextIndexX = nextIndex($str, 0, 'x');

    // Next index of 'y' starting from index 0
    $nextIndexY = nextIndex($str, 0, 'y');

    // To store the count of required sub-strings
    $count = 0;
    while ($nextIndexX != -1 && $nextIndexY != -1) {

        // If 'y' appears before 'x'
        // it won't contribute to a valid sub-string
        if ($nextIndexX > $nextIndexY) {

            // Find next occurrence of 'y'
            $nextIndexY = nextIndex($str, $nextIndexY + 1, 'y');
            continue;
        }

        // If 'y' appears after 'x'
        // every sub-string ending at an 'x' appearing after this 'y'
        // and starting with the current 'x' is a valid sub-string
        else {
            $count += $countX[$nextIndexY];

            // Find next occurrence of 'x'
            $nextIndexX = nextIndex($str, $nextIndexX + 1, 'x');
        }
    }

    // Return the count
    return $count;
}

// Driver code

$s = "xyyxx";
echo countSubStrings($s);
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function that returns the index of next occurrence
    // of the character c in string str starting from index start
    function nextIndex(str,start,c)
    {
        // Starting from start
        for (let i = start; i < str.length; i++) {

            // If current character = c
            if (str[i] == c)
                return i;
        }

        // Not found
        return -1;
    }

    // Function to return the count of required sub-strings
    function countSubStrings(str)
    {
        let i, n = str.length;

        // Stores running count of 'x' starting from the end
        let countX = new Array(n);

        let count = 0;
        for (i = n - 1; i >= 0; i--) {
            if (str[i] == 'x')
                count++;
            countX[i] = count;
        }

        // Next index of 'x' starting from index 0
        let nextIndexX = nextIndex(str, 0, 'x');

        // Next index of 'y' starting from index 0
        let nextIndexY = nextIndex(str, 0, 'y');

        // To store the count of required sub-strings
        count = 0;
        while (nextIndexX != -1 && nextIndexY != -1) {

            // If 'y' appears before 'x'
            // it won't contribute to a valid sub-string
            if (nextIndexX > nextIndexY) {

                // Find next occurrence of 'y'
                nextIndexY = nextIndex(str, nextIndexY + 1, 'y');
                continue;
            }

            // If 'y' appears after 'x'
            // every sub-string ending at an 'x' appearing after this 'y'
            // and starting with the current 'x' is a valid sub-string
            else {
                count += countX[nextIndexY];

                // Find next occurrence of 'x'
                nextIndexX = nextIndex(str, nextIndexX + 1, 'x');
            }
        }

        // Return the count
        return count;
    }

    // Driver code
    let s = "xyyxx";
    document.write(countSubStrings(s));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```