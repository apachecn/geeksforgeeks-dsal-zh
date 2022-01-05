# 将一个字符串分割成长度至少为 2 的回文字符串，每个字符出现在一个字符串中

> 原文:[https://www . geesforgeks . org/partition-a-string-in-回文-至少长度为 2 的字符串，每个字符都出现在单个字符串中/](https://www.geeksforgeeks.org/partition-a-string-into-palindromic-strings-of-at-least-length-2-with-every-character-present-in-a-single-string/)

给定一个由 **N** 个小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查**个至少长度为 2** 的所有字符串是否都是[回文](https://www.geeksforgeeks.org/string-palindrome/)的，所述字符串是通过选择字符串 **S** 的每个字符仅一次而形成的。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**S = " abb badzcz "
> **输出:**是
> **说明:**长度大于 1 的回文串为{“aa”、“bbb”、“dd”、“zcz”}，给定串中的所有字符只使用一次。因此，打印“是”。
> 
> **输入:**S = " ABCD "
> T3】输出:否

**做法:**思路是将字符串拆分成偶数长度的回文串，如果存在有频率的字符 **1** ，则将其与偶数长度的回文串配对。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如 **freq[]** ，大小为 **26** ，以[存储字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)中出现的每个字符的频率。
*   [迭代给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并更新数组中每个字符的频率 **freq[]** 。
*   初始化两个变量，比如 **O** 和 **E** ，分别存储唯一字符和偶次字符的个数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **freq[]** ，如果 **freq[i]** 等于 **1** ，那么将 **O** 递增 **1** 。否则，将 **E** 增加 **1** 。
*   检查 **E ≥ O** ，然后打印**“是”**。否则，请执行以下步骤:
    *   将 **O** 更新为**O–E**，存储配对后剩余的唯一字符。
    *   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**freq【】**如果 **O** 的值最多为 **0** ，则[破环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将 **O** 更新为**O –( freq[I]/2)**，然后将 **O** 增加 **1** 。
*   完成上述步骤后，如果**0≤0**的值，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to check if  a string can be
// split into palindromic strings of at
// least length 2 by including every
// character exactly once
void checkPalindrome(string& s)
{
    // Stores the frequency
    // of each character
    int a[26] = { 0 };

    // Store the frequency of
    // characters with frequencies
    // 1 and even respectively
    int o = 0, e = 0;

    // Traverse the string s
    for (int i = 0; s[i] != '\0'; i++)
        a[(int)s[i] - 97]++;

    // Iterate over all the characters
    for (int i = 0; i < 26; i++) {

        // If the frequency is 1
        if (a[i] == 1)
            o++;

        // If frequency is even
        else if (a[i] % 2 == 0
                 and a[i] != 0)
            e += (a[i] / 2);
    }

    // Print the result
    if (e >= o)
        cout << "Yes";

    else {

        // Stores the number of characters
        // with frequency equal to 1 that
        // are not part of a palindromic string
        o = o - e;

        // Iterate over all the characters
        for (int i = 0; i < 26; i++) {

            // If o becomes less than 0,
            // then break out of the loop
            if (o <= 0)
                break;

            // If frequency of the current
            // character is > 2 and is odd
            if (o > 0
                and a[i] % 2 == 1
                and a[i] > 2) {

                int k = o;

                // Update the value of o
                o = o - a[i] / 2;

                // If a single character
                // is still remaining
                if (o > 0 or 2 * k + 1 == a[i]) {

                    // Increment o by 1
                    o++;

                    // Set a[i] to 1
                    a[i] = 1;
                }
            }
        }

        // Print the result
        if (o <= 0)
            cout << "Yes";
        else
            cout << "No";
    }
}

// Driver Code
int main()
{
    string S = "abbbaddzcz";
    checkPalindrome(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if  a string can be
// split into palindromic strings of at
// least length 2 by including every
// character exactly once
static void checkPalindrome(String s)
{

    // Stores the frequency
    // of each character
    int a[] = new int[26];

    // Store the frequency of
    // characters with frequencies
    // 1 and even respectively
    int o = 0, e = 0;

    // Traverse the string s
    for(int i = 0; i < s.length(); i++)
        a[s.charAt(i) - 'a']++;

    // Iterate over all the characters
    for(int i = 0; i < 26; i++)
    {

        // If the frequency is 1
        if (a[i] == 1)
            o++;

        // If frequency is even
        else if (a[i] % 2 == 0 && a[i] != 0)
            e += (a[i] / 2);
    }

    // Print the result
    if (e >= o)
        System.out.println("Yes");

    else
    {

        // Stores the number of characters
        // with frequency equal to 1 that
        // are not part of a palindromic string
        o = o - e;

        // Iterate over all the characters
        for(int i = 0; i < 26; i++)
        {

            // If o becomes less than 0,
            // then break out of the loop
            if (o <= 0)
                break;

            // If frequency of the current
            // character is > 2 and is odd
            if (o > 0 && a[i] % 2 == 1 && a[i] > 2)
            {
                int k = o;

                // Update the value of o
                o = o - a[i] / 2;

                // If a single character
                // is still remaining
                if (o > 0 || 2 * k + 1 == a[i])
                {

                    // Increment o by 1
                    o++;

                    // Set a[i] to 1
                    a[i] = 1;
                }
            }
        }

        // Print the result
        if (o <= 0)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// Driver Code
public static void main(String[] args)
{
    String S = "abbbaddzcz";

    checkPalindrome(S);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if  a string can be
# split into palindromic strings of at
# least length 2 by including every
# character exactly once
def checkPalindrome(s):

    # Stores the frequency
    # of each character
    a = [0] * 26

    # Store the frequency of
    # characters with frequencies
    # 1 and even respectively
    o, e = 0, 0

    # Traverse the string s
    for i in s:
        a[ord(i) - 97] += 1

    # Iterate over all the characters
    for i in range(26):

        # If the frequency is 1
        if (a[i] == 1):
            o += 1

        # If frequency is even
        elif (a[i] % 2 == 0 and a[i] != 0):
            e += (a[i] // 2)

    # Print the result
    if (e >= o):
        print("Yes")
    else:

        # Stores the number of characters
        # with frequency equal to 1 that
        # are not part of a palindromic string
        o = o - e

        # Iterate over all the characters
        for i in range(26):

            # If o becomes less than 0,
            # then break out of the loop
            if (o <= 0):
                break

            # If frequency of the current
            # character is > 2 and is odd
            if (o > 0 and a[i] % 2 == 1 and a[i] > 2):
                k = o

                # Update the value of o
                o = o - a[i] // 2

                # If a single character
                # is still remaining
                if (o > 0 or 2 * k + 1 == a[i]):

                    # Increment o by 1
                    o += 1

                    # Set a[i] to 1
                    a[i] = 1

        # Print the result
        if (o <= 0):
            print("Yes")
        else:
            print("No")

# Driver Code
if __name__ == '__main__':

    S = "abbbaddzcz"

    checkPalindrome(S)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if  a string can be
// split into palindromic strings of at
// least length 2 by including every
// character exactly once
static void checkPalindrome(string s)
{

    // Stores the frequency
    // of each character
    int[] a = new int[26];

    // Store the frequency of
    // characters with frequencies
    // 1 and even respectively
    int o = 0, e = 0;

    // Traverse the string s
    for(int i = 0; i < s.Length; i++)
        a[s[i] - 'a']++;

    // Iterate over all the characters
    for(int i = 0; i < 26; i++)
    {

        // If the frequency is 1
        if (a[i] == 1)
            o++;

        // If frequency is even
        else if (a[i] % 2 == 0 && a[i] != 0)
            e += (a[i] / 2);
    }

    // Print the result
    if (e >= o)
        Console.WriteLine("Yes");

    else
    {

        // Stores the number of characters
        // with frequency equal to 1 that
        // are not part of a palindromic string
        o = o - e;

        // Iterate over all the characters
        for(int i = 0; i < 26; i++)
        {

            // If o becomes less than 0,
            // then break out of the loop
            if (o <= 0)
                break;

            // If frequency of the current
            // character is > 2 and is odd
            if (o > 0 && a[i] % 2 == 1 && a[i] > 2)
            {
                int k = o;

                // Update the value of o
                o = o - a[i] / 2;

                // If a single character
                // is still remaining
                if (o > 0 || 2 * k + 1 == a[i])
                {

                    // Increment o by 1
                    o++;

                    // Set a[i] to 1
                    a[i] = 1;
                }
            }
        }

        // Print the result
        if (o <= 0)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// Driver code
static void Main()
{
    string S = "abbbaddzcz";

    checkPalindrome(S);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

        // Javascript program for the above approach

        // Function to check if  a string can be
        // split into palindromic strings of at
        // least length 2 by including every
        // character exactly once
        function checkPalindrome( s )
        {
            // Stores the frequency
            // of each character
            let a = [0]

            // Store the frequency of
            // characters with frequencies
            // 1 and even respectively
            let o = 0, e = 0;

            // Traverse the string s
            for (let i = 0; i<s.length; i++)
                a[s.charCodeAt(i) - 97]++;

            // Iterate over all the characters
            for (let i = 0; i < 26; i++) {

                // If the frequency is 1
                if (a[i] == 1)
                    o++;

                // If frequency is even
                else if (a[i] % 2 == 0 && a[i] != 0)
                    e += (a[i] / 2);
            }

            // Print the result
            if (e >= o)
                document.write("Yes")

            else {

                // Stores the number of characters
                // with frequency equal to 1 that
                // are not part of a palindromic string
                o = o - e;

                // Iterate over all the characters
                for (let i = 0; i < 26; i++)
                {

                    // If o becomes less than 0,
                    // then break out of the loop
                    if (o <= 0)
                        break;

                    // If frequency of the current
                    // character is > 2 and is odd
                    if (o > 0 && a[i] % 2 == 1 && a[i] > 2)
                    {

                        let k = o;

                        // Update the value of o
                        o = o - a[i] / 2;

                        // If a single character
                        // is still remaining
                        if (o > 0 || 2 * k + 1 == a[i])
                        {

                            // Increment o by 1
                            o++;

                            // Set a[i] to 1
                            a[i] = 1;
                        }
                    }
                }

                // Print the result
                if (o <= 0)
                document.write("Yes")
                else
                document.write("No")
            }
        }

        // Driver Code

        let S = "abbbaddzcz";
        checkPalindrome(S);

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)