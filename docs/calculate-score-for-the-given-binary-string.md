# 计算给定二进制字符串的分数

> 原文:[https://www . geeksforgeeks . org/计算给定二进制字符串的分数/](https://www.geeksforgeeks.org/calculate-score-for-the-given-binary-string/)

给定一个二进制字符串 **str** 。对于 **n 连片 1s** 来说，得分更新为**得分=得分+ n <sup>2</sup>** ，对于 **n 连片 0s** ，得分更新为**得分=得分–n<sup>2</sup>**。任务是找到完整的二进制字符串的分数。
**举例:**

> **输入:** str = 11011
> **输出:** 7
> 得分(“11”)–得分(“0”)+得分(“11”)= 2<sup>2</sup>–1<sup>2</sup>+2<sup>2</sup>= 7
> **输入:** str = 1100011
> **输出:** -1

**方法:**为了解决问题，迭代给定的字符串并计算连续的 **1s** 和 **0s** 的数量。对于 n 个 **1s** 的每个连续组块，将 **n 个 <sup>2 个</sup>** 添加到当前分数，同样，对于 n 个 **0s** 的每个连续组块，从当前分数中减去 **n 个 <sup>2 个</sup>** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the score for
// the given binary string
int calcScore(string str)
{
    int score = 0;
    int len = str.length();

    // Traverse through string character
    for (int i = 0; i < len;) {

        // Initialize current chunk's size
        int chunkSize = 1;

        // Get current character
        char currentChar = str[i++];

        // Calculate total chunk size
        // of same characters
        while (i < len && str[i] == currentChar) {
            chunkSize++;
            i++;
        }

        // Add/subtract pow(chunkSize, 2)
        // depending upon character
        if (currentChar == '1')
            score += pow(chunkSize, 2);
        else
            score -= pow(chunkSize, 2);
    }

    // Return the score
    return score;
}

// Driver code
int main()
{
    string str = "11011";
    cout << calcScore(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the score for
    // the given binary string
    public static int calcScore(String str)
    {
        int score = 0;
        int len = str.length();

        // Traverse through string character
        for (int i = 0; i < len;)
        {

            // Initialize current chunk's size
            int chunkSize = 1;

            // Get current character
            char currentChar = str.charAt(i++);

            // Calculate total chunk size
            // of same characters
            while (i < len && str.charAt(i) == currentChar)
            {
                chunkSize++;
                i++;
            }

            // Add/subtract pow(chunkSize, 2)
            // depending upon character
            if (currentChar == '1')
                score += Math.pow(chunkSize, 2);
            else
                score -= Math.pow(chunkSize, 2);
        }

        // Return the score
        return score;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "11011";
        System.out.println(calcScore(str));
    }
}

// This code is contributed by Naman_Garg
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the score for
# the given binary string
def calcScore(str):
    score = 0
    len1 = len(str)

    # Traverse through string character
    i = 0
    while(i < len1):

        # Initialize current chunk's size
        chunkSize = 1

        # Get current character
        currentChar = str[i]
        i += 1

        # Calculate total chunk size
        # of same characters
        while (i < len1 and str[i] == currentChar):
            chunkSize += 1
            i += 1

        # Add/subtract pow(chunkSize, 2)
        # depending upon character
        if (currentChar == '1'):
            score += pow(chunkSize, 2)
        else:
            score -= pow(chunkSize, 2)

    # Return the score
    return score

# Driver code
if __name__ == '__main__':
    str = "11011"
    print(calcScore(str))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the score for
    // the given binary string
    public static int calcScore(String str)
    {
        int score = 0;
        int len = str.Length;

        // Traverse through string character
        for (int i = 0; i < len;)
        {

            // Initialize current chunk's size
            int chunkSize = 1;

            // Get current character
            char currentChar = str[i++];

            // Calculate total chunk size
            // of same characters
            while (i < len && str[i] == currentChar)
            {
                chunkSize++;
                i++;
            }

            // Add/subtract pow(chunkSize, 2)
            // depending upon character
            if (currentChar == '1')
                score += (int)Math.Pow(chunkSize, 2);
            else
                score -= (int)Math.Pow(chunkSize, 2);
        }

        // Return the score
        return score;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "11011";
        Console.WriteLine(calcScore(str));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to return the score for
// the given binary string
function calcScore($str)
{
    $score = 0;
    $len = strlen($str);

    // Traverse through string character
    for ($i = 0; $i < $len😉
    {

        // Initialize current chunk's size
        $chunkSize = 1;

        // Get current character
        $currentChar = $str[$i++];

        // Calculate total chunk size
        // of same characters
        while ($i < $len && $str[$i] == $currentChar)
        {
            $chunkSize++;
            $i++;
        }

        // Add/subtract pow(chunkSize, 2)
        // depending upon character
        if ($currentChar == '1')
            $score += pow($chunkSize, 2);
        else
            $score -= pow($chunkSize, 2);
    }

    // Return the score
    return $score;
}

    // Driver code
    $str = "11011";
    echo calcScore($str);

    // This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the score for
// the given binary string
function calcScore(str)
{
    var score = 0;
    var len = str.length;

    // Traverse through string character
    for (var i = 0; i < len;) {

        // Initialize current chunk's size
        var chunkSize = 1;

        // Get current character
        var currentChar = str[i++];

        // Calculate total chunk size
        // of same characters
        while (i < len && str[i] == currentChar) {
            chunkSize++;
            i++;
        }

        // Add/subtract pow(chunkSize, 2)
        // depending upon character
        if (currentChar == '1')
            score += Math.pow(chunkSize, 2);
        else
            score -= Math.pow(chunkSize, 2);
    }

    // Return the score
    return score;
}

// Driver code
var str = "11011";
document.write( calcScore(str));

</script>
```

**Output:** 

```
7
```