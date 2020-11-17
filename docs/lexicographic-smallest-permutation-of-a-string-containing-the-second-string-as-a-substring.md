# 字符串的最小词典排列，它包含第二个字符串作为子字符串

> 原文：[https://www.geeksforgeeks.org/lexicographic-smallest-permutation-of-a-string-containing-the-second-string-as-a-substring/](https://www.geeksforgeeks.org/lexicographic-smallest-permutation-of-a-string-containing-the-second-string-as-a-substring/)

给定两个字符串`str1`和`str2`，任务是查找包含`str2`作为子字符串的`str1`的词典最小排列。

**注意**：假定解决方案始终存在。

**示例**：

> **输入**：`str1 = "abab", str2 = "ab"`
>
> **输出**：`"aabb"`
>
> **解释**：字符串`str1`的词法最小排列是`"aabb"`，由于`"aabb"`包含字符串`"ab"`作为替换，因此，`"aabb"`是所需的答案。
>
> **输入**：`str1 = "geeksforgeeks", str2 = "for"`
>
> **输出**：`"eeeeforggkkss"`

**方法**：可以使用[频率计数](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)技术的概念来解决此问题。 请按照以下步骤解决此问题。

1.  存储字符串`str1`和`str2`的所有字符的频率。

2.  用子字符串初始化结果字符串。

3.  从第一个字符串的频率中减去第二个字符串的频率。

4.  现在，在结果字符串中，在字典上小于或等于子字符串的第一个字符的其余字符附加在子字符串之前。

5.  将其余字符按字典顺序追加到结果字符串中子字符串的后面。

6.  最后，打印结果字符串。

下面是上述方法的实现。

## C++

```cpp

// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the desired
// lexicographic smaller string
string findSmallestString(string str1,
                          string str2)
{

    int freq1[26], freq2[26];
    memset(freq1, 0, sizeof freq1);
    memset(freq2, 0, sizeof freq2);

    // Calculate length of the string
    int n1 = str1.length();
    int n2 = str2.length();

    // Stores the frequencies of
    // characters of string str1
    for (int i = 0; i < n1; ++i) {
        freq1[str1[i] - 'a']++;
    }

    // Stores the frequencies of
    // characters of string str2
    for (int i = 0; i < n2; ++i) {
        freq2[str2[i] - 'a']++;
    }

    // Decrease the frequency of
    // second string from that of
    // of the first string
    for (int i = 0; i < 26; ++i) {
        freq1[i] -= freq2[i];
    }

    // To store the resultant string
    string res = "";

    // To find the index of first
    // character of the string str2
    int minIndex = str2[0] - 'a';

    // Append the characters in
    // lexicographical order
    for (int i = 0; i < 26; ++i) {

        // Append all the current
        // character (i + 'a')
        for (int j = 0; j < freq1[i]; ++j) {
            res += (char)(i + 'a');
        }

        // If we reach first character
        // of string str2 append str2
        if (i == minIndex) {
            res += str2;
        }
    }

    // Return the resultant string
    return res;
}

// Driver Code
int main()
{
    string str1 = "geeksforgeeksfor";
    string str2 = "for";
    cout << findSmallestString(str1, str2);
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to print the desired
// lexicographic smaller String
static String findSmallestString(String str1,
                                 String str2)
{
    int []freq1 = new int[26];
    int []freq2 = new int[26];
    Arrays.fill(freq1, 0);
    Arrays.fill(freq2, 0);

    // Calculate length of the String
    int n1 = str1.length();
    int n2 = str2.length();

    // Stores the frequencies of
    // characters of String str1
    for(int i = 0; i < n1; ++i) 
    {
        freq1[str1.charAt(i) - 'a']++;
    }

    // Stores the frequencies of
    // characters of String str2
    for(int i = 0; i < n2; ++i)
    {
        freq2[str2.charAt(i) - 'a']++;
    }

    // Decrease the frequency of
    // second String from that of
    // of the first String
    for(int i = 0; i < 26; ++i)
    {
        freq1[i] -= freq2[i];
    }

    // To store the resultant String
    String res = "";

    // To find the index of first
    // character of the String str2
    int minIndex = str2.charAt(0) - 'a';

    // Append the characters in
    // lexicographical order
    for(int i = 0; i < 26; ++i)
    {

        // Append all the current
        // character (i + 'a')
        for(int j = 0; j < freq1[i]; ++j)
        {
            res += (char)(i + 'a');
        }

        // If we reach first character
        // of String str2 append str2
        if (i == minIndex) 
        {
            res += str2;
        }
    }

    // Return the resultant String
    return res;
}

// Driver Code
public static void main(String[] args)
{
    String str1 = "geeksforgeeksfor";
    String str2 = "for";

    System.out.print(findSmallestString(str1, str2));
}
}

// This code is contributed by Amit Katiyar 

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to print the desired 
# lexicographic smaller string 
def findSmallestString(str1, str2):

    freq1 = [0] * 26
    freq2 = [0] * 26

    # Calculate length of the string
    n1 = len(str1)
    n2 = len(str2)

    # Stores the frequencies of 
    # characters of string str1 
    for i in range(n1):
        freq1[ord(str1[i]) - ord('a')] += 1

    # Stores the frequencies of 
    # characters of string str2 
    for i in range(n2):
        freq2[ord(str2[i]) - ord('a')] += 1

    # Decrease the frequency of 
    # second string from that of 
    # of the first string 
    for i in range(26):
        freq1[i] -= freq2[i]

    # To store the resultant string
    res = ""

    # To find the index of first 
    # character of the string str2
    minIndex = ord(str2[0]) - ord('a')

    # Append the characters in 
    # lexicographical order 
    for i in range(26):

        # Append all the current 
        # character (i + 'a') 
        for j in range(freq1[i]):
            res += chr(i+ ord('a'))

        # If we reach first character 
        # of string str2 append str2 
        if i == minIndex:
            res += str2

    # Return the resultant string 
    return res

# Driver code
str1 = "geeksforgeeksfor"
str2 = "for"

print(findSmallestString(str1, str2))

# This code is contributed by Stuti Pathak

```

## C#

```cs

// C# program to implement
// the above approach
using System;
class GFG{

    // Function to print the desired
    // lexicographic smaller String
    static String findSmallestString(String str1,
                                     String str2)
    {
        int[] freq1 = new int[26];
        int[] freq2 = new int[26];

        // Calculate length of the String
        int n1 = str1.Length;
        int n2 = str2.Length;

        // Stores the frequencies of
        // characters of String str1
        for (int i = 0; i < n1; ++i) 
        {
            freq1[str1[i] - 'a']++;
        }

        // Stores the frequencies of
        // characters of String str2
        for (int i = 0; i < n2; ++i) 
        {
            freq2[str2[i] - 'a']++;
        }

        // Decrease the frequency of
        // second String from that of
        // of the first String
        for (int i = 0; i < 26; ++i) 
        {
            freq1[i] -= freq2[i];
        }

        // To store the resultant String
        String res = "";

        // To find the index of first
        // character of the String str2
        int minIndex = str2[0] - 'a';

        // Append the characters in
        // lexicographical order
        for (int i = 0; i < 26; ++i) 
        {

            // Append all the current
            // character (i + 'a')
            for (int j = 0; j < freq1[i]; ++j) 
            {
                res += (char)(i + 'a');
            }

            // If we reach first character
            // of String str2 append str2
            if (i == minIndex) 
            {
                res += str2;
            }
        }

        // Return the resultant String
        return res;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str1 = "geeksforgeeksfor";
        String str2 = "for";
          Console.Write(findSmallestString(str1, str2));
    }
}

// This code is contributed by shikhasingrajput

```

**输出**： 

```
eeeefforggkkorss

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。



* * *

* * *



