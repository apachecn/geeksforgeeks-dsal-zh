# 按字母顺序找出子串的个数

> 原文:[https://www . geesforgeks . org/find-按字母顺序计算子字符串的数量/](https://www.geeksforgeeks.org/find-the-count-of-substrings-in-alphabetic-order/)

给定一串由小写字母组成的长度![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")。任务是找到字符按字母顺序出现的子字符串的数量。子字符串的最小允许长度为 2。
**示例** :

```
Input : str = "refjhlmnbv"
Output : 2
Substrings are: "ef", "mn"

Input : str = "qwertyuiopasdfghjklzxcvbnm"
Output : 3
```

对于按字母顺序排列的子串，其字符的顺序与英文字母相同。此外，此类子字符串中连续字符的 ASCII 值相差 1。为了找到按字母顺序排列的子字符串的总数，遍历给定的字符串并比较两个相邻的字符，如果它们按字母顺序排列，则递增结果，然后找到字符串中与前一个字符不按字母顺序排列的下一个字符。
**算法:**
迭代字符串长度:

*   如果 str[i]+1 == str[i+1] ->将结果增加 1，并重复该字符串直到下一个不按字母顺序的字符
*   否则继续

以下是上述方法的实现:

## C++

```
// CPP to find the number of substrings
// in alphabetical order

#include <bits/stdc++.h>
using namespace std;

// Function to find number of substrings
int findSubstringCount(string str)
{
    int result = 0;
    int n = str.size();

    // Iterate over string length
    for (int i = 0; i < n - 1; i++) {
        // if any two chars are in alphabetic order
        if (str[i] + 1 == str[i + 1]) {
            result++;
            // find next char not in order
            while (str[i] + 1 == str[i + 1]) {
                i++;
            }
        }
    }

    // return the result
    return result;
}

// Driver function
int main()
{
    string str = "alphabet";

    cout << findSubstringCount(str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to find the number of substrings
// in alphabetical order
import java.util.*;
class Solution
{

// Function to find number of substrings
static int findSubstringCount(String str)
{
    int result = 0;
    int n = str.length();

    // Iterate over string length
    for (int i = 0; i < n - 1; i++) {
        // if any two chars are in alphabetic order
        if (str.charAt(i) + 1 == str.charAt(i+1)) {
            result++;
            // find next char not in order
            while (str.charAt(i) + 1 == str.charAt(i+1)) {
                i++;
            }
        }
    }

    // return the result
    return result;
}

// Driver function
public static void main(String args[])
{
    String str = "alphabet";

    System.out.println(findSubstringCount(str));

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 to find the number of substrings
# in alphabetical order

# Function to find number of substrings
def findSubstringCount(str):

    result = 0
    n = len (str)

    # Iterate over string length
    for i in range (n - 1) :

        # if any two chars are in alphabetic order
        if (ord(str[i]) + 1 == ord(str[i + 1])) :
            result += 1

            # find next char not in order
            while (ord(str[i]) + 1 == ord(str[i + 1])) :
                i += 1

    # return the result
    return result

# Driver Code
if __name__ == "__main__":

    str = "alphabet"

    print(findSubstringCount(str))

# This code is contributed by ChitraNayal
```

## C#

```
using System;

// C# to find the number of substrings 
// in alphabetical order 
public class Solution
{

// Function to find number of substrings 
public static int findSubstringCount(string str)
{
    int result = 0;
    int n = str.Length;

    // Iterate over string length 
    for (int i = 0; i < n - 1; i++)
    {
        // if any two chars are in alphabetic order 
        if ((char)(str[i] + 1) == str[i + 1])
        {
            result++;
            // find next char not in order 
            while ((char)(str[i] + 1) == str[i + 1])
            {
                i++;
            }
        }
    }

    // return the result 
    return result;
}

// Driver function 
public static void Main(string[] args)
{
    string str = "alphabet";

    Console.WriteLine(findSubstringCount(str));

}

}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// javascript to find the number of substrings
// in alphabetical order

// Function to find number of substrings
function findSubstringCount(str)
{
    var result = 0;
    var n = str.length;

    // Iterate over string length
    for (var i = 0; i < n - 1; i++) {
        // if any two chars are in alphabetic order
        if (String.fromCharCode(str[i].charCodeAt(0) + 1) == str[i + 1]) {
            result++;
            // find next char not in order
            while (String.fromCharCode(str[i].charCodeAt(0) + 1) === str[i + 1]) {
                i++;
            }
        }
    }

    // return the result
    return result;
}

// Driver function
var str = "alphabet";
document.write( findSubstringCount(str));

</script>
```

**Output:** 

```
1
```