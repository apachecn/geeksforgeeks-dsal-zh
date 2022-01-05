# 查询字符串子字符串中的第一个非重复字符

> 原文:[https://www . geesforgeks . org/query-to-find-字符串中第一个非重复字符子字符串/](https://www.geeksforgeeks.org/queries-to-find-the-first-non-repeating-character-in-the-sub-string-of-a-string/)

给定一个字符串 **str** ，任务是回答 **Q** 查询，其中每个查询由两个整数 **L** 和 **R** 组成，我们必须找到子字符串**str【L…R】**中的第一个非重复字符。如果没有不重复字符，则打印 **-1** 。

**示例:**

> **输入:** str = "GeeksForGeeks "，q[] = {{0，3}、{2，3}、{5，12}}
> **输出:**
> G
> e
> F
> 查询的子串分别为“Geek”、“ek”和“ForGeeks”，它们的第一个非重复字符分别为“G”、“e”和“F”。
> 
> **输入:**str = " xxyxx "，q[] = {{2，3}，{3，4}}
> **输出:**
> -1
> y

**方法:**创建一个频率数组 **freq[][]** ，其中 **freq[i][j]** 存储子字符串 **str[0…j]** 中字符的频率，其 ASCII 值为 **i** 。现在，ASCII 值为 **x** 的子串**字符串【I…j】**中任意字符的出现频率可以计算为**freq[x][j]= freq[x][I–1]**。
现在对于每个查询，开始遍历给定范围内的字符串，即**字符串【L…R】**，对于每个字符，如果其频率为 **1** ，则这是所需子字符串中的第一个非重复字符。如果所有字符的频率都大于 **1** ，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Maximum distinct characters possible
#define MAX 256

// To store the frequency of the characters
int freq[MAX][MAX];

// Function to pre-calculate the frequency array
void preCalculate(string str, int n)
{
    // Only the first character has
    // frequency 1 till index 0
    freq[(int)str[0]][0] = 1;

    // Starting from the second
    // character of the string
    for (int i = 1; i < n; i++)
    {
        char ch = str[i];

        // For every possible character
        for (int j = 0; j < MAX; j++)
        {
            // Current character under consideration
            char charToUpdate = j;

            // If it is equal to the character
            // at the current index
            if (charToUpdate == ch)
                freq[j][i] = freq[j][i - 1] + 1;
            else
                freq[j][i] = freq[j][i - 1];
        }
    }
}

// Function to return the frequency of the
// given character in the sub-string str[l...r]
int getFrequency(char ch, int l, int r)
{
    if (l == 0)
        return freq[(int)ch][r];
    else
        return (freq[(int)ch][r] -
                freq[(int)ch][l - 1]);
}

// Function to return the first
// non-repeating character in range[l..r]
string firstNonRepeating(string str, int n,
                              int l, int r)
{
    char t[2] = "";

    // Starting from the first character
    for (int i = l; i < r; i++)
    {
        // Current character
        char ch = str[i];

        // If frequency of the current character is 1
        // then return the character
        if (getFrequency(ch, l, r) == 1)
        {
            t[0] = ch;
            return t;
        }
    }

    // All the characters of the
    // sub-string are repeating
    return "-1";
}

// Driver code
int main()
{
    string str = "GeeksForGeeks";
    int n = str.length();

    int queries[][2] = {{0, 3}, {2, 3}, {5, 12}};
    int q = sizeof(queries) /
            sizeof(queries[0]);

    // Pre-calculate the frequency array
    freq[MAX][n] = {0};
    preCalculate(str, n);

    for (int i = 0; i < q; i++)
        cout << firstNonRepeating(str, n, queries[i][0],
                                          queries[i][1])
                                                << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Maximum distinct characters possible
    static final int MAX = 256;

    // To store the frequency of the characters
    static int freq[][];

    // Function to pre-calculate the frequency array
    static void preCalculate(String str, int n)
    {

        // Only the first character has
        // frequency 1 till index 0
        freq[(int)str.charAt(0)][0] = 1;

        // Starting from the second
        // character of the string
        for (int i = 1; i < n; i++) {
            char ch = str.charAt(i);

            // For every possible character
            for (int j = 0; j < MAX; j++) {

                // Current character under consideration
                char charToUpdate = (char)j;

                // If it is equal to the character
                // at the current index
                if (charToUpdate == ch)
                    freq[j][i] = freq[j][i - 1] + 1;
                else
                    freq[j][i] = freq[j][i - 1];
            }
        }
    }

    // Function to return the frequency of the
    // given character in the sub-string str[l...r]
    static int getFrequency(char ch, int l, int r)
    {

        if (l == 0)
            return freq[(int)ch][r];
        else
            return (freq[(int)ch][r] - freq[(int)ch][l - 1]);
    }

    // Function to return the first non-repeating character in range[l..r]
    static String firstNonRepeating(String str, int n, int l, int r)
    {

        // Starting from the first character
        for (int i = l; i < r; i++) {

            // Current character
            char ch = str.charAt(i);

            // If frequency of the current character is 1
            // then return the character
            if (getFrequency(ch, l, r) == 1)
                return ("" + ch);
        }

        // All the characters of the
        // sub-string are repeating
        return "-1";
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "GeeksForGeeks";
        int n = str.length();

        int queries[][] = { { 0, 3 }, { 2, 3 }, { 5, 12 } };
        int q = queries.length;

        // Pre-calculate the frequency array
        freq = new int[MAX][n];
        preCalculate(str, n);

        for (int i = 0; i < q; i++) {
            System.out.println(firstNonRepeating(str, n,
                                                 queries[i][0],
                                                 queries[i][1]));
        }
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Maximum distinct characters possible
MAX = 256

# To store the frequency of the characters
freq = [[0 for i in range(MAX)]
           for j in range(MAX)]

# Function to pre-calculate
# the frequency array
def preCalculate(string, n):

    # Only the first character has
    # frequency 1 till index 0
    freq[ord(string[0])][0] = 1

    # Starting from the second
    # character of the string
    for i in range(1, n):
        ch = string[i]

        # For every possible character
        for j in range(MAX):

            # Current character under consideration
            charToUpdate = chr(j)

            # If it is equal to the character
            # at the current index
            if charToUpdate == ch:
                freq[j][i] = freq[j][i - 1] + 1
            else:
                freq[j][i] = freq[j][i - 1]

# Function to return the frequency of the
# given character in the sub-string str[l...r]
def getFrequency(ch, l, r):
    if l == 0:
        return freq[ord(ch)][r]
    else:
        return (freq[ord(ch)][r] -
                freq[ord(ch)][l - 1])

# Function to return the first
# non-repeating character in range[l..r]
def firstNonRepeating(string, n, l, r):
    t = [""] * 2

    # Starting from the first character
    for i in range(l, r):

        # Current character
        ch = string[i]

        # If frequency of the current character is 1
        # then return the character
        if getFrequency(ch, l, r) == 1:
            t[0] = ch
            return t[0]

    # All the characters of the
    # sub-string are repeating
    return "-1"

# Driver Code
if __name__ == "__main__":
    string = "GeeksForGeeks"
    n = len(string)

    queries = [(0, 3), (2, 3), (5, 12)]
    q = len(queries)

    # Pre-calculate the frequency array
    preCalculate(string, n)

    for i in range(q):
        print(firstNonRepeating(string, n,
                                queries[i][0],
                                queries[i][1]))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Maximum distinct characters possible
    static int MAX = 256;

    // To store the frequency of the characters
    static int [,]freq ;

    // Function to pre-calculate the frequency array
    static void preCalculate(string str, int n)
    {

        // Only the first character has
        // frequency 1 till index 0
        freq[(int)str[0],0] = 1;

        // Starting from the second
        // character of the string
        for (int i = 1; i < n; i++)
        {
            char ch = str[i];

            // For every possible character
            for (int j = 0; j < MAX; j++)
            {

                // Current character under consideration
                char charToUpdate = (char)j;

                // If it is equal to the character
                // at the current index
                if (charToUpdate == ch)
                    freq[j,i] = freq[j,i - 1] + 1;
                else
                    freq[j,i] = freq[j,i - 1];
            }
        }
    }

    // Function to return the frequency of the
    // given character in the sub-string str[l...r]
    static int getFrequency(char ch, int l, int r)
    {

        if (l == 0)
            return freq[(int)ch, r];
        else
            return (freq[(int)ch, r] - freq[(int)ch, l - 1]);
    }

    // Function to return the first non-repeating character in range[l..r]
    static string firstNonRepeating(string str, int n, int l, int r)
    {

        // Starting from the first character
        for (int i = l; i < r; i++)
        {

            // Current character
            char ch = str[i];

            // If frequency of the current character is 1
            // then return the character
            if (getFrequency(ch, l, r) == 1)
                return ("" + ch);
        }

        // All the characters of the
        // sub-string are repeating
        return "-1";
    }

    // Driver code
    public static void Main()
    {
        string str = "GeeksForGeeks";
        int n = str.Length;

        int [,]queries = { { 0, 3 }, { 2, 3 }, { 5, 12 } };
        int q = queries.Length;

        // Pre-calculate the frequency array
        freq = new int[MAX,n];
        preCalculate(str, n);

        for (int i = 0; i < q; i++)
        {
            Console.WriteLine(firstNonRepeating(str, n,
                                                queries[i,0],
                                                queries[i,1]));
        }
    }

}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Maximum distinct characters possible
    let MAX = 256;

    // To store the frequency of the characters
    let freq;

    // Function to pre-calculate the frequency array
    function preCalculate(str, n)
    {

        // Only the first character has
        // frequency 1 till index 0
        freq[str[0].charCodeAt()][0] = 1;

        // Starting from the second
        // character of the string
        for (let i = 1; i < n; i++) {
            let ch = str[i];

            // For every possible character
            for (let j = 0; j < MAX; j++) {

                // Current character under consideration
                let charToUpdate = String.fromCharCode(j);

                // If it is equal to the character
                // at the current index
                if (charToUpdate == ch)
                    freq[j][i] = freq[j][i - 1] + 1;
                else
                    freq[j][i] = freq[j][i - 1];
            }
        }
    }

    // Function to return the frequency of the
    // given character in the sub-string str[l...r]
    function getFrequency(ch, l, r)
    {

        if (l == 0)
            return freq[ch.charCodeAt()][r];
        else
            return (freq[ch.charCodeAt()][r] - freq[ch.charCodeAt()][l - 1]);
    }

    // Function to return the first non-repeating character in range[l..r]
    function firstNonRepeating(str, n, l, r)
    {

        // Starting from the first character
        for (let i = l; i < r; i++) {

            // Current character
            let ch = str[i];

            // If frequency of the current character is 1
            // then return the character
            if (getFrequency(ch, l, r) == 1)
                return ("" + ch);
        }

        // All the characters of the
        // sub-string are repeating
        return "-1";
    }

    let str = "GeeksForGeeks";
    let n = str.length;

    let queries = [ [ 0, 3 ], [ 2, 3 ], [ 5, 12 ] ];
    let q = queries.length;

    // Pre-calculate the frequency array
    freq = new Array(MAX);
    for (let i = 0; i < MAX; i++)
    {
        freq[i] = new Array(n);
        for (let j = 0; j < n; j++)
        {
            freq[i][j] = 0;
        }
    }

    preCalculate(str, n);

    for (let i = 0; i < q; i++) {
      document.write(firstNonRepeating(str, n,
                                           queries[i][0],
                                           queries[i][1]) + "</br>");
    }

</script>
```

**Output:** 

```
G
e
F
```