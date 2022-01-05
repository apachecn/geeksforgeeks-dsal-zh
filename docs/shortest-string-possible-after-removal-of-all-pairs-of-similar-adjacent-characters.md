# 移除所有相似相邻字符对后的最短字符串

> 原文:[https://www . geesforgeks . org/移除所有相似相邻字符对后的最短字符串/](https://www.geeksforgeeks.org/shortest-string-possible-after-removal-of-all-pairs-of-similar-adjacent-characters/)

给定一个[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** ，任务是找到可能的最小合成字符串，该字符串是通过重复删除相等的相邻字符对而形成的。

**示例:**

> **输入:**S =“aabccddd”
> T3】输出: abd
> **解释:**按照去除相邻字符对的顺序，使字符串的长度最小化:
> aabccddd→abcddd→abddd→Abd。
> 
> **输入:** S = aa
> **输出:**空字符串
> **解释:**移除相邻字符对的以下顺序使字符串的长度最小化:
> aa →" "。

**方法:**解决给定问题的主要思路是[递归](https://www.geeksforgeeks.org/recursion/)逐个删除所有相等的相邻字符对。按照以下步骤解决给定的问题:

*   初始化一个空字符串，比如**和**，在删除所有相等的相邻字符对后，存储最小长度的字符串。
*   初始化一个字符串，比如说 **pre** ，以便在每次删除相等的相邻字符后存储更新的字符串。
*   现在，迭代直到字符串**和**以及**不相等，并执行以下步骤:**
    *   使用函数**移除相邻的第一个相同字符来更新字符串**和**的值。**
    *   如果字符串**和**的值与字符串**在**之前相同，则[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将字符串 **pre** 的值更新为字符串 **ans** 。
*   完成上述步骤后，打印字符串**和**作为结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to delete pair of adjacent
// characters which are equal
string removeAdjacent(string s)
{

    // Base Case
    if (s.length() == 1)
        return s;

    // Stores the update string
    string sb = "";

    // Traverse the string s
    for(int i = 0; i < s.length() - 1; i++)
    {
        char c = s[i];
        char d = s[i + 1];

        // If two unequal pair of
        // adjacent characters are found
        if (c != d)
        {
            sb = sb + c;

            if (i == s.length() - 2)
            {
                sb = sb + d;
            }
        }

        // If two equal pair of adjacent
        // characters are found
        else
        {
            for(int j = i + 2;
                    j < s.length(); j++)

                // Append the remaining string
                // after removing the pair
                sb = sb + s[j];

            return sb;
        }
    }

    // Return the final String
    return sb;
}

// Function to find the shortest string
// after repeatedly removing pairs of
// adjacent characters which are equal
void reduceString(string s)
{

    // Stores the resultant String
    string result = "";

    // Keeps track of previously
    // iterated string
    string pre = s;

    while (true)
    {

        // Update the result after
        // deleting adjacent pair of
        // characters which are similar
        result = removeAdjacent(pre);

        // Termination Conditions
        if (result == pre)
            break;

        // Update pre variable with
        // the value of result
        pre = result;
    }

    if (result.length() != 0)
        cout << (result) << endl;

    // Case for "Empty String"
    else
        cout << "Empty String" << endl;
}

// Driver code   
int main()
{
    string S = "aaabccddd";

    reduceString(S);

    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to delete pair of adjacent
    // characters which are equal
    static String removeAdjacent(String s)
    {
        // Base Case
        if (s.length() == 1)
            return s;

        // Stores the update string
        StringBuilder sb = new StringBuilder("");

        // Traverse the string s
        for (int i = 0;
             i < s.length() - 1; i++) {
            char c = s.charAt(i);
            char d = s.charAt(i + 1);

            // If two unequal pair of
            // adjacent characters are found
            if (c != d) {
                sb.append(c);

                if (i == s.length() - 2) {
                    sb.append(d);
                }
            }

            // If two equal pair of adjacent
            // characters are found
            else {
                for (int j = i + 2;
                     j < s.length(); j++)

                    // Append the remaining string
                    // after removing the pair
                    sb.append(s.charAt(j));

                return sb.toString();
            }
        }

        // Return the final String
        return sb.toString();
    }

    // Function to find the shortest string
    // after repeatedly removing pairs of
    // adjacent characters which are equal
    public static void reduceString(String s)
    {
        // Stores the resultant String
        String result = "";

        // Keeps track of previously
        // iterated string
        String pre = s;

        while (true) {
            // Update the result after
            // deleting adjacent pair of
            // characters which are similar
            result = removeAdjacent(pre);

            // Termination Conditions
            if (result.equals(pre))
                break;

            // Update pre variable with
            // the value of result
            pre = result;
        }

        if (result.length() != 0)
            System.out.println(result);

        // Case for "Empty String"
        else
            System.out.println("Empty String");
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "aaabccddd";
        reduceString(S);
    }
}
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to delete pair of adjacent
    // characters which are equal
    static string removeAdjacent(string s)
    {

        // Base Case
        if (s.Length == 1)
            return s;

        // Stores the update string
        string sb = "";

        // Traverse the string s
        for(int i = 0; i < s.Length - 1; i++)
        {
            char c = s[i];
            char d = s[i + 1];

            // If two unequal pair of
            // adjacent characters are found
            if (c != d)
            {
                sb = sb + c;

                if (i == s.Length - 2)
                {
                    sb = sb + d;
                }
            }

            // If two equal pair of adjacent
            // characters are found
            else
            {
                for(int j = i + 2;
                        j < s.Length; j++)

                    // Append the remaining string
                    // after removing the pair
                    sb = sb + s[j];

                return sb;
            }
        }

        // Return the final String
        return sb;
    }

    // Function to find the shortest string
    // after repeatedly removing pairs of
    // adjacent characters which are equal
    static void reduceString(string s)
    {

        // Stores the resultant String
        string result = "";

        // Keeps track of previously
        // iterated string
        string pre = s;

        while (true)
        {

            // Update the result after
            // deleting adjacent pair of
            // characters which are similar
            result = removeAdjacent(pre);

            // Termination Conditions
            if (result == pre)
                break;

            // Update pre variable with
            // the value of result
            pre = result;
        }

        if (result.Length != 0)
            Console.WriteLine(result);

        // Case for "Empty String"
        else
            Console.WriteLine("Empty String");
    }

  static void Main() {
    string S = "aaabccddd";

    reduceString(S);
  }
}
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to delete pair of adjacent
    // characters which are equal
    function removeAdjacent(s)
    {

        // Base Case
        if (s.length == 1)
            return s;

        // Stores the update string
        let sb = "";

        // Traverse the string s
        for(let i = 0; i < s.length - 1; i++)
        {
            let c = s[i];
            let d = s[i + 1];

            // If two unequal pair of
            // adjacent characters are found
            if (c != d)
            {
                sb = sb + c;

                if (i == s.length - 2)
                {
                    sb = sb + d;
                }
            }

            // If two equal pair of adjacent
            // characters are found
            else
            {
                for(let j = i + 2; j < s.length; j++)

                    // Append the remaining string
                    // after removing the pair
                    sb = sb + s[j];

                return sb;
            }
        }

        // Return the final String
        return sb;
    }

    // Function to find the shortest string
    // after repeatedly removing pairs of
    // adjacent characters which are equal
    function reduceString(s)
    {

        // Stores the resultant String
        let result = "";

        // Keeps track of previously
        // iterated string
        let pre = s;

        while (true)
        {

            // Update the result after
            // deleting adjacent pair of
            // characters which are similar
            result = removeAdjacent(pre);

            // Termination Conditions
            if (result == pre)
                break;

            // Update pre variable with
            // the value of result
            pre = result;
        }

        if (result.length != 0)
            document.write(result);

        // Case for "Empty String"
        else
            document.write("Empty String");
    }

    let S = "aaabccddd";

    reduceString(S);

  // This code is contributed by suresh07
</script>
```

**Output:** 

```
abd
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助** **空间:** O(N)*