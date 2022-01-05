# 通过包含给定字符串的字符或字符的 ASCII 值生成的子序列

> 原文:[https://www . geesforgeks . org/subseries-由给定字符串的包含字符或 ascii 字符值生成/](https://www.geeksforgeeks.org/subsequences-generated-by-including-characters-or-ascii-value-of-characters-of-given-string/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是打印给定字符串的所有可能的非空[子序列，使得子序列包含给定字符串中的字符或字符](https://www.geeksforgeeks.org/print-subsequences-string/)的 [ASCII 值。](https://www.geeksforgeeks.org/program-print-ascii-value-character/)

**示例:**

> **输入:** str = "ab"
> **输出:** b 98 a ab a98 97 97b 9798
> **解释:**
> 字符串的可能子序列是{ b，a，ab }。
> 通过包含给定字符串中的字符或字符的 ASCII 值而生成的字符串的可能子序列是{ 98，b，a，97，ab，97b，a98，9798 }。
> 因此，需要的输出是{ b，98，a，ab，a98，97，97b，9798 }。
> 
> **输入:**str = " a "
> T3】输出: a 97

**方法:**按照以下步骤解决问题:

*   [使用变量 **i**](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) 到[迭代给定字符串的每个字符，生成字符串的所有可能的子序列](https://www.geeksforgeeks.org/print-subsequences-string/)。
*   对于第 i <sup>个</sup>字符，可以执行以下三个操作:
    *   在子序列中包含**字符串**的第**I<sup>T3【字符。</sup>**
    *   不要在子序列中包含**字符串**的 **i <sup>th</sup>** 字符。
    *   在子序列中包含**字符串**的**I<sup>th</sup>T3【字符的 ASCII 值。**
*   因此，解决这个问题的递推关系如下:

> FindSub(str，res，i) = { FindSub(str，res，i + 1)，FindSub(str，res + str[i]，i + 1)，FindSub(str，res + ASCII(str[i])，i + 1) }
> res =字符串的子序列
> i =字符串中某个字符的索引

*   使用上面的递归关系，根据给定的条件打印所有可能的子序列。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print subsequences containing
// ASCII value of the characters or the
// the characters of the given string
void FindSub(string str, string res,
             int i)
{

    // Base Case
    if (i == str.length())
    {

        // If length of the
        // subsequence exceeds 0
        if (res.length() > 0)
        {

            // Print the subsequence
           cout << res << " ";
        }
        return;
    }

    // Stores character present at
    // i-th index of str
    char ch = str[i];

    // If the i-th character is not
    // included in the subsequence
    FindSub(str, res, i + 1);

    // Including the i-th character
    // in the subsequence
    FindSub(str, res + ch, i + 1);

    // Include the ASCII value of the
    // ith character in the subsequence
    FindSub(str, res + to_string(int(ch)), i + 1);
}

// Driver Code
int main()
{
    string str = "ab";
    string res = "";

    // Stores length of str
    int N = str.length();

    FindSub(str, res, 0);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG {

    // Function to print subsequences containing
    // ASCII value of the characters or the
    // the characters of the given string
    static void FindSub(String str, String res,
                        int i)
    {
        // Base Case
        if (i == str.length()) {

            // If length of the
            // subsequence exceeds 0
            if (res.length() > 0) {

                // Print the subsequence
                System.out.print(res + " ");
            }
            return;
        }

        // Stores character present at
        // i-th index of str
        char ch = str.charAt(i);

        // If the i-th character is not
        // included in the subsequence
        FindSub(str, res, i + 1);

        // Including the i-th character
        // in the subsequence
        FindSub(str, res + ch, i + 1);

        // Include the ASCII value of the
        // ith character in the subsequence
        FindSub(str, res + (int)ch, i + 1);
        ;
    }

    // Driver Code
    public static void main(String[] args)
    {

        String str = "ab";

        String res = "";

        // Stores length of str
        int N = str.length();

        FindSub(str, res, 0);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print subsequences containing
# ASCII value of the characters or the
# the characters of the given string
def FindSub(string , res, i) :

    # Base Case
    if (i == len(string)):

        # If length of the
        # subsequence exceeds 0
        if (len(res) > 0) :

            # Print the subsequence
            print(res, end=" ");

        return;

    # Stores character present at
    # i-th index of str
    ch = string[i];

    # If the i-th character is not
    # included in the subsequence
    FindSub(string, res, i + 1);

    # Including the i-th character
    # in the subsequence
    FindSub(string, res + ch, i + 1);

    # Include the ASCII value of the
    # ith character in the subsequence
    FindSub(string, res + str(ord(ch)), i + 1);

# Driver Code
if __name__ == "__main__" :

    string = "ab";

    res = "";

    # Stores length of str
    N = len(string);

    FindSub(string, res, 0);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print subsequences containing
// ASCII value of the characters or the
// the characters of the given string
static void FindSub(string str, string res,
                    int i)
{

    // Base Case
    if (i == str.Length)
    {

        // If length of the
        // subsequence exceeds 0
        if (res.Length > 0)
        {

            // Print the subsequence
            Console.Write(res + " ");
        }
        return;
    }

    // Stores character present at
    // i-th index of str
    char ch = str[i];

    // If the i-th character is not
    // included in the subsequence
    FindSub(str, res, i + 1);

    // Including the i-th character
    // in the subsequence
    FindSub(str, res + ch, i + 1);

    // Include the ASCII value of the
    // ith character in the subsequence
    FindSub(str, res + (int)ch, i + 1);
}

// Driver Code
public static void Main(String[] args)
{
    string str = "ab";
    string res = "";

    // Stores length of str
    int N = str.Length;

    FindSub(str, res, 0);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to print subsequences containing
// ASCII value of the characters or the
// the characters of the given string
function FindSub(str, res, i)
{

    // Base Case
    if (i === str.length)
    {

        // If length of the
        // subsequence exceeds 0
        if (res.length > 0)
        {

            // Print the subsequence
            document.write(res + " ");
        }
        return;
    }

    // Stores character present at
    // i-th index of str
    var ch = str[i];

    // If the i-th character is not
    // included in the subsequence
    FindSub(str, res, i + 1);

    // Including the i-th character
    // in the subsequence
    FindSub(str, res + ch, i + 1);

    // Include the ASCII value of the
    // ith character in the subsequence
    FindSub(str, res + ch.charCodeAt(0), i + 1);
}

// Driver Code
var str = "ab";
var res = "";

// Stores length of str
var N = str.length;

FindSub(str, res, 0);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
b 98 a ab a98 97 97b 9798
```

***时间复杂度:**O(3<sup>N</sup>)*
***辅助空间:** O(N)*