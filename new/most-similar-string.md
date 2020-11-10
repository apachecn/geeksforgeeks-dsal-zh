# 最相似的字符串

> 原文：[https://www.geeksforgeeks.org/most-similar-string/](https://www.geeksforgeeks.org/most-similar-string/)

给定字符串`str`和[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，大小为`N`，任务是打印`arr`中与`str`匹配最多字符的字符串。

**示例**：

> **输入**：`str = "vikas", N = 3, arr[] = ["preeti", "khusbu", "katherina"]`
> **输出**：`"katherina"`
> **解释**：
> `Str`和`D[]`中每个字符串之间相似字符的数量为：
>
> ```
> "preeti" = 1
> "khusbu" = 2
> "katherina" = 3
> ```
> 
> 因此，`"katherina"`具有最大匹配字符。
> 
> **输入**：`str = "gfg", N = 3, arr [] = ["goal", "fog", "abc"]`
> **输出**：`"fog"`
> **说明**：
> `Str`和`D[]`中每个字符串之间相似字符的数量为：
> 
> ```
> "goal" = 1
> "fog" = 2
> "abc = 0
> ```
> 因此，`"fog"`具有最大匹配字符。

**方法**：想法是考虑数组`arr[]`的每个字符串，并将其每个字符与给定的字符串`str`进行比较。 跟踪匹配字符和相应字符串的最大数量。 另外，请确保从每个字符串中删除重复项。 步骤如下：

1.  创建变量`maxVal`和变量`val`，以分别跟踪匹配字符和相应字符串的最大数目。

2.  遍历数组`arr[]`，并从每个字符串中删除重复项。 另外，从`Str`中删除重复项。

3.  对于`arr[]`的每个字符串，将其与给定的字符串`Str`比较，并计算匹配字符的数量。

4.  继续使用最大匹配字符数更新`maxVal`，并使用相应的字符串更新`val`。

5.  最后，在执行上述操作后，打印`val`的值。

下面是上述方法的实现：

## Java

```java

// Java program for the above appraoch
import java.util.*;
import java.io.*;

public class GFG {

    // Function that print string which
    // has maximum similar characters
    private static void
    maxMatchingChar(ArrayList<String> list,
                    int n, char ch[])
    {

        String val = "";

        int maxVal = Integer.MIN_VALUE;

        for (String s : list) {

            // Count matching characters
            int matchingchar = matchingChar(
                s.toLowerCase(), ch);

            // Update maxVal if needed
            if (matchingchar > maxVal) {
                maxVal = matchingchar;
                val = s;
            }
        }

        System.out.print(val + " ");
    }

    // Function that returns the count
    // of number of matching characters
    private static int matchingChar(
        String s, char[] ch)
    {

        int freq = 0, c = ch.length;

        // Traverse the character array
        for (int i = 0; i < c; i++) {

            // If character matches
            // then increment the count
            if (s.contains(
                    String.valueOf(ch[i]))) {
                freq++;
            }
        }

        return freq;
    }

    // Function to remove duplicate
    // characters
    private static char[] removeDuplicate(String str)
    {
        // To keep unique character only
        HashSet<Character> set
            = new HashSet<Character>();

        int c = str.length();

        // Inserting character in hashset
        for (int i = 0; i < c; i++) {

            set.add(str.charAt(i));
        }

        char arr[] = new char[set.size()];
        int index = 0;

        // Update string with unique characters
        for (char s : set) {

            arr[index] = s;
            index++;
        }

        // Return the char array
        return arr;
    }

    // Driver Code
    public static void main(
        String[] args) throws Exception
    {
        int n = 3;
        String str = "Vikas";
        String D[] = { "preeti", "khusbu", "katherina" };

        // Removing duplicate and
        // convert to lowercase
        char ch[]
            = removeDuplicate(str.toLowerCase());

        ArrayList<String> list
            = new ArrayList<String>();

        // Insert each string in the list
        for (int i = 0; i < n; i++) {

            list.add(D[i]);
        }

        // Function Call
        maxMatchingChar(list, n, ch);
    }
}

```

## Python3

```py

# Python3 program for the above appraoch
import sys

# Function that print string which 
# has maximum similar characters
def maxMatchingChar(list, n, ch):

    val = ""
    maxVal = -sys.maxsize - 1

    for s in list:

        # Count matching characters
        matchingchar = matchingChar(s.lower(), ch)

        # Update maxVal if needed
        if (matchingchar > maxVal):
            maxVal = matchingchar
            val = s

    print(val, end = " ")

# Function that returns the count 
# of number of matching characters
def matchingChar(s, ch):

    freq = 0
    c = len(ch)

    # Traverse the character array 
    for i in range(c):

        # If character matches 
        # then increment the count
        if ch[i] in s:
            freq += 1

    return freq

# Driver Code 
n = 3
str = "Vikas"
D = [ "preeti", "khusbu", "katherina" ]

# Remove duplicate characters and
# convert to lowercase 
ch = list(set(str.lower()))
List = []

# Insert each string in the list
for i in range(n):
    List.append(D[i])

# Function call 
maxMatchingChar(List, n, ch)

# This code is contributed by avanitrachhadiya2155

```

## C#

```cs

// C# program for the above appraoch
using System;
using System.Collections.Generic;

class GFG{

// Function that print string which
// has maximum similar characters
private static void maxMatchingChar(List<String> list,
                                    int n, char []ch)
{
    String val = "";

    int maxVal = int.MinValue;

    foreach(String s in list) 
    {

        // Count matching characters
        int matchingchar = matchingChar(
                           s.ToLower(), ch);

        // Update maxVal if needed
        if (matchingchar > maxVal)
        {
            maxVal = matchingchar;
            val = s;
        }
    }
    Console.Write(val + " ");
}

// Function that returns the count
// of number of matching characters
private static int matchingChar(String s, char[] ch)
{
    int freq = 0, c = ch.Length;

    // Traverse the character array
    for(int i = 0; i < c; i++)
    {

        // If character matches
        // then increment the count
        if (s.Contains(String.Join("", ch[i])))
        {
            freq++;
        }
    }
    return freq;
}

// Function to remove duplicate
// characters
private static char[] removeDuplicate(String str)
{

    // To keep unique character only
    HashSet<char> set = new HashSet<char>();

    int c = str.Length;

    // Inserting character in hashset
    for(int i = 0; i < c; i++)
    {
        set.Add(str[i]);
    }

    char []arr = new char[set.Count];
    int index = 0;

    // Update string with unique characters
    foreach(char s in set) 
    {
        arr[index] = s;
        index++;
    }

    // Return the char array
    return arr;
}

// Driver Code
public static void Main(String[] args) 
{
    int n = 3;
    String str = "Vikas";
    String []D = { "preeti", "khusbu", 
                   "katherina" };

    // Removing duplicate and
    // convert to lowercase
    char []ch = removeDuplicate(str.ToLower());

    List<String> list = new List<String>();

    // Insert each string in the list
    for(int i = 0; i < n; i++)
    {
        list.Add(D[i]);
    }

    // Function call
    maxMatchingChar(list, n, ch);
}
}

// This code is contributed by Rohit_ranjan 

```

**输出**： 

```
katherina

```

**时间复杂度**：`O(N * M)`，其中`M`是字符串的最大长度。

**辅助空间**：`O(M)`



* * *

* * *



