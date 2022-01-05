# 检查字符串的第一个和最后一个 X 字符组成的字符串是否是回文

> 原文:[https://www . geesforgeks . org/check-if-string-formed-by-first-and-last-x-characters-of-string-is-a-回文/](https://www.geeksforgeeks.org/check-if-string-formed-by-first-and-last-x-characters-of-a-string-is-a-palindrome/)

给定一个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**和一个整数 **X** 。任务是查找[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **串**和[倒排](https://www.geeksforgeeks.org/reverse-a-string-in-java/) [串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **串**的前 **X** 字符是否相同。如果相等，则打印**真**，否则打印**假**。

**示例:**

> **输入** : str = abcdefba，X = 2
> **输出** : true
> **解释** :
> 两个字符串 **str** 和反转字符串 **str** 的前 2 个字符相同。
> 
> **输入**:str = geesforgeks，X = 3
> 输出 : false

**方法:**这个问题可以通过[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符来解决。按照以下步骤解决此问题:

*   初始化两个变量，将 **i** 设为 **0** ，将 **n** 设为**字符串**的长度，分别存储当前字符的位置和[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**的长度。
*   [迭代而](https://www.geeksforgeeks.org/java-while-loop-with-examples/)T2 I 小于 **n** 和 **x** :
    *   如果从开始的**和最后的**字符和最后的**和**不相等，则打印**假**和**返回**。
*   完成以上步骤后，打印**真**作为答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether the first
// x characters of both string str and
// reversed string str are same or not
void isEqualSubstring(string str, int x)
{
    // Length of the string str
    int n = str.length();
    int i = 0;

    // Traverse over the string while
    // first and last x characters are
    // not equal
    while (i < n && i < x) {

        // If the current and n-k-1 from last
        // character are not equal
        if (str[i] != str[n - i - 1]) {
            cout << "false";
            return;
        }
        i++;
    }

    // Finally, print true
    cout << "true";
}

// Driver Code
int main()
{
    // Given Input
    string str = "GeeksforGeeks";
    int x = 3;

    // Function Call
    isEqualSubstring(str, x);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
    // Function to check whether the first
    // x characters of both string str and
    // reversed string str are same or not
    public static void isEqualSubstring(String str, int x)
    {
        // Length of the string str
        int n = str.length();
        int i = 0;

        // Traverse over the string while
        // first and last x characters are
        // not equal
        while (i < n && i < x) {

            // If the current and n-k-1 from last
            // character are not equal
            if (str.charAt(i) != str.charAt(n - i - 1)) {
                System.out.println("false");
                return;
            }
            i++;
        }

        // Finally, print true
        System.out.println("true");
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        String str = "GeeksforGeeks";
        int x = 3;

        // Function Call
        isEqualSubstring(str, x);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check whether the first
# x characters of both string str and
# reversed string str are same or not
def isEqualSubstring(string, x):

    # Length of the string str
    n = len(string)
    i = 0

    # Traverse over the string while
    # first and last x characters are
    # not equal
    while i < n and i < x:

        # If the current and n-k-1 from last
        # character are not equal
        if (string[i] != string[n-i-1]):
            print("false")
            return

        i += 1

    # Finally, print true
    print("true")
    return

# Driver Code
if __name__ == '__main__':

    # Given input
    string = "GeeksforGeeks"
    x = 3

    # Function Call
    isEqualSubstring(string, x)

# This code is contributed by MuskanKalra1
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check whether the first
// x characters of both string str and
// reversed string str are same or not
static void isEqualSubstring(string str, int x)
{

    // Length of the string str
    int n = str.Length;
    int i = 0;

    // Traverse over the string while
    // first and last x characters are
    // not equal
    while (i < n && i < x) {

        // If the current and n-k-1 from last
        // character are not equal
        if (str[i] != str[n - i - 1]) {
            Console.Write("false");
            return;
        }
        i++;
    }

    // Finally, print true
    Console.Write("true");
}

// Driver Code
public static void Main()
{

    // Given Input
    string str = "GeeksforGeeks";
    int x = 3;

    // Function Call
    isEqualSubstring(str, x);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check whether the first
// x characters of both string str and
// reversed string str are same or not
function isEqualSubstring(str, x)
{
    // Length of the string str
    let n = str.length;
    let i = 0;

    // Traverse over the string while
    // first and last x characters are
    // not equal
    while (i < n && i < x) {

        // If the current and n-k-1 from last
        // character are not equal
        if (str[i] !== str[n - i - 1]) {
            document.write("false");
            return;
        }
        i++;
    }

    // Finally, print true
    document.write("true");
}

// Driver Code

    // Given Input
    let str = "GeeksforGeeks";
    let x = 3;

    // Function Call
    isEqualSubstring(str, x);

    // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
false
```

***时间复杂度:** O(min(n，k))*
***辅助空间:** O(1)*