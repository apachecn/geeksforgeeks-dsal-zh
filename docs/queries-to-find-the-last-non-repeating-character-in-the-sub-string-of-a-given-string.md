# 在给定字符串的子字符串中查找最后一个非重复字符的查询

> 原文:[https://www . geesforgeks . org/query-to-find-给定字符串的子字符串中最后一个非重复字符/](https://www.geeksforgeeks.org/queries-to-find-the-last-non-repeating-character-in-the-sub-string-of-a-given-string/)

给定一个字符串 **str** ，任务是回答 **Q** 查询，其中每个查询由两个整数 **L** 和 **R** 组成，我们必须找到子字符串**str【L…R】**中最后一个不重复的字符。如果没有不重复字符，则打印 **-1** 。
**示例:**

> **输入:** str = "GeeksForGeeks "，q[] = {{2，9}，{2，3}，{0，12}}
> **输出:**
> G
> k
> r
> 查询的子字符串分别为“eksForGe”、“ek”和“GeeksForGeeks”，它们最后的非重复字符分别为“G”、“k”和“r”。
> “G”是给定频率范围内从末尾开始的第一个字符。
> **输入:**str = " xxyxx "，q[] = {{2，3}，{3，4}}
> **输出:**
> -1
> x

**方法:**创建一个频率数组 **freq[][]** ，其中 **freq[i][j]** 存储子字符串 **str[0…j]** 中字符的频率，其 ASCII 值为 **i** 。现在，ASCII 值为 **x** 的子串**字符串【I…j】**中任意字符的出现频率可以计算为**freq[x][j]= freq[x][I–1]**。
现在对于每个查询，开始遍历给定范围内的字符串，即**字符串【L…R】**，对于每个字符，如果其频率为 **1** ，则这是所需子字符串中最后一个不重复的字符。如果所有字符的频率都大于 **1** ，则打印 **-1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Maximum distinct characters possible
int MAX = 256;

// To store the frequency of the characters
int freq[256][1000] = {0};

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
int getFrequency(char ch, int l, int r)
{

    if (l == 0)
        return freq[(int)ch][r];
    else
        return (freq[(int)ch][r] - freq[(int)ch][l - 1]);
}

string getString(char x)
{

    // string class has a constructor
    // that allows us to specify size of
    // string as first parameter and character
    // to be filled in given size as second
    // parameter.
    string s(1, x);

    return s;
}

// Function to return the last non-repeating character
string lastNonRepeating(string str, int n, int l, int r)
{

    // Starting from the last character
    for (int i = r; i >= l; i--)
    {

        // Current character
        char ch = str[i];

        // If frequency of the current character is 1
        // then return the character
        if (getFrequency(ch, l, r) == 1)
            return getString(ch);
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

    int queries[3][2] = { { 2, 9 }, { 2, 3 }, { 0, 12 } };
    int q =3;

    // Pre-calculate the frequency array

    preCalculate(str, n);

    for (int i = 0; i < q; i++)
    {
        cout << (lastNonRepeating(str, n,
                            queries[i][0],
                            queries[i][1]))<<endl;;
    }
}

// This code is contributed by Arnab Kundu
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

    // Function to return the last non-repeating character
    static String lastNonRepeating(String str, int n, int l, int r)
    {

        // Starting from the last character
        for (int i = r; i >= l; i--) {

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

        int queries[][] = { { 2, 9 }, { 2, 3 }, { 0, 12 } };
        int q = queries.length;

        // Pre-calculate the frequency array
        freq = new int[MAX][n];
        preCalculate(str, n);

        for (int i = 0; i < q; i++) {
            System.out.println(lastNonRepeating(str, n,
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
freq = [[0 for i in range(256)]
           for j in range(1000)]

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

# Function to return the
# last non-repeating character
def lastNonRepeating(string, n, l, r):

    # Starting from the last character
    for i in range(r, l - 1, -1):

        # Current character
        ch = string[i]

        # If frequency of the current character is 1
        # then return the character
        if getFrequency(ch, l, r) == 1:
            return ch

    # All the characters of the
    # sub-string are repeating
    return "-1"

# Driver Code
if __name__ == "__main__":
    string = "GeeksForGeeks"
    n = len(string)

    queries = [(2, 9), (2, 3), (0, 12)]
    q = len(queries)

    # Pre-calculate the frequency array
    preCalculate(string, n)

    for i in range(q):
        print(lastNonRepeating(string, n,
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
    static int [,]freq;

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
                    freq[j, i] = freq[j, i - 1] + 1;
                else
                    freq[j, i] = freq[j, i - 1];
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

    // Function to return the last non-repeating character
    static String lastNonRepeating(string str, int n, int l, int r)
    {

        // Starting from the last character
        for (int i = r; i >= l; i--)
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

        int [,]queries = { { 2, 9 }, { 2, 3 }, { 0, 12 } };
        int q = queries.Length;

        // Pre-calculate the frequency array
        freq = new int[MAX,n];
        preCalculate(str, n);

        for (int i = 0; i < q; i++)
        {
            Console.WriteLine(lastNonRepeating(str, n,
                                                queries[i,0],
                                                queries[i,1]));
        }
    }
}

// This code is contributed by AnkitRai01
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Maximum distinct characters possible
$MAX = 256;

// To store the frequency of the characters
$freq = array_fill(0, 256, array_fill(0, 1000, 0));

// Function to pre-calculate the frequency array
function preCalculate($str, $n)
{

    global $freq;
    global $MAX;

    // Only the first character has
    // frequency 1 till index 0
    $freq[ord($str[0])][0] = 1;

    // Starting from the second
    // character of the string
    for ($i = 1; $i < $n; $i++)
    {
        $ch = $str[$i];

        // For every possible character
        for ($j = 0; $j < $MAX; $j++)
        {

            // Current character under consideration
            $charToUpdate = chr($j);

            // If it is equal to the character
            // at the current index
            if ($charToUpdate == $ch)
                $freq[$j][$i] = $freq[$j][$i - 1] + 1;
            else
                $freq[$j][$i] = $freq[$j][$i - 1];
        }
    }
}

// Function to return the frequency of the
// given character in the sub-string $str[$l...$r]
function getFrequency($ch, $l, $r)
{

    global $freq;
    if ($l == 0)
        return $freq[ord($ch)][$r];
    else
        return ($freq[ord($ch)][$r] - $freq[ord($ch)][$l - 1]);
}

// Function to return the last non-repeating character
function lastNonRepeating($str, $n, $l, $r)
{

    // Starting from the last character
    for ($i = $r; $i >= $l; $i--)
    {

        // Current character
        $ch = $str[$i];

        // If frequency of the current character is 1
        // then return the character
        if (getFrequency($ch, $l, $r) == 1)
             return $ch;
    }

    // All the characters of the
    // sub-string are repeating
    return "-1";
}

// Driver code

$str = "GeeksForGeeks";
$n = strlen($str);

$queries = array( array( 2, 9 ), array( 2, 3 ), array( 0, 12 ) );

$q =3;

// Pre-calculate the frequency array

preCalculate($str, $n);

for ($i = 0; $i < $q; $i++)
{
    echo (lastNonRepeating($str, $n,
                        $queries[$i][0],
                        $queries[$i][1])), "\n";
}

// This code is contributed by ihritik

?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Maximum distinct characters possible
    let MAX = 256;

     // To store the frequency of the characters
    let freq;

    // Function to pre-calculate the frequency array

    function preCalculate(str,n)
    {
        // Only the first character has
        // frequency 1 till index 0
        freq[str[0].charCodeAt(0)][0] = 1;

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
    function getFrequency(ch,l,r)
    {
        if (l == 0)
            return freq[ch.charCodeAt(0)][r];
        else
            return (freq[ch.charCodeAt(0)][r] -
            freq[ch.charCodeAt(0)][l - 1]);
    }

    // Function to return the last non-repeating character
    function lastNonRepeating(str,n,l,r)
    {
        // Starting from the last character
        for (let i = r; i >= l; i--) {

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

    // Driver code
    let str = "GeeksForGeeks";
    let n = str.length;
    let queries = [[ 2, 9 ], [ 2, 3 ], [ 0, 12 ]];
    let q = queries.length;

        // Pre-calculate the frequency array
        freq = new Array(MAX);
        for(let i=0;i<MAX;i++)
        {
            freq[i]=new Array(n);
            for(let j=0;j<n;j++)
            {
                freq[i][j]=0;
            }
        }
        preCalculate(str, n);

        for (let i = 0; i < q; i++) {
            document.write(
            lastNonRepeating(str, n,queries[i][0],queries[i][1])+
            "<br>");}

// This code is contributed by rag2127

</script>
```

**Output:** 

```
G
k
r
```