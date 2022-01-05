# 查询给定字符串的子串中元音的计数

> 原文:[https://www . geesforgeks . org/query-to-find-给定字符串的子字符串中元音的计数/](https://www.geeksforgeeks.org/queries-to-find-the-count-of-vowels-in-the-substrings-of-the-given-string/)

给定长度为 **N** 和 **Q** 的字符串**字符串**，其中每个查询由两个整数 **L** 和 **R** 组成。对于每个查询，任务是找到子串**str【L…R】**中元音的计数。

**示例:**

> **输入:** str = "geeksforgeeks "，q[][] = {{1，3}，{2，4}，{1，9}}
> **输出:**
> 2
> 1
> 4
> 查询 1:“eek”有 2 个元音。
> 查询 2:“eks”有 1 个元音。
> 查询 3:“eeks forge”有 2 个元音。
> 
> **输入:** str = "aaaa "，q[][] = {{1，3}，{1，4}}
> **输出:**
> 3
> 3

**天真的方法:**对于每个查询，遍历从 **L <sup>第</sup>T5】字符到 **R <sup>第</sup>T9】字符的字符串，并找到元音的计数。
以下是上述方法的实施:****

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 2

// Function that returns true
// if ch is a vowel
bool isVowel(char ch)
{

    return (ch == 'a' || ch == 'e'
            || ch == 'i' || ch == 'o'
            || ch == 'u');
}

// Function to return the count of vowels
// in the substring str[l...r]
int countVowels(string str, int l, int r)
{

    // To store the count of vowels
    int cnt = 0;

    // For every character in
    // the index range [l, r]
    for (int i = l; i <= r; i++) {

        // If the current character
        // is a vowel
        if (isVowel(str[i]))
            cnt++;
    }
    return cnt;
}

void performQueries(string str, int queries[][N], int q)
{

    // For every query
    for (int i = 0; i < q; i++) {

        // Find the count of vowels
        // for the current query
        cout << countVowels(str, queries[i][0],
                            queries[i][1]) << "\n";
    }
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int queries[][N] = { { 1, 3 }, { 2, 4 }, { 1, 9 } };
    int q = (sizeof(queries)
             / sizeof(queries[0]));

    performQueries(str, queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int N = 2;

// Function that returns true
// if ch is a vowel
static boolean isVowel(char ch)
{

    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// Function to return the count of vowels
// in the substring str[l...r]
static int countVowels(String str,
                       int l, int r)
{

    // To store the count of vowels
    int cnt = 0;

    // For every character in
    // the index range [l, r]
    for (int i = l; i <= r; i++)
    {

        // If the current character
        // is a vowel
        if (isVowel(str.charAt(i)))
            cnt++;
    }
    return cnt;
}

static void performQueries(String str,
                           int queries[][],
                           int q)
{

    // For every query
    for (int i = 0; i < q; i++)
    {

        // Find the count of vowels
        // for the current query
        System.out.println(countVowels(str, queries[i][0],
                                            queries[i][1]));
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int queries[][] = { { 1, 3 }, { 2, 4 },
                                  { 1, 9 } };
    int q = queries.length;

    performQueries(str, queries, q);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 2;

# Function that returns true
# if ch is a vowel
def isVowel(ch) :

    return (ch == 'a' or ch == 'e' or
            ch == 'i' or ch == 'o' or
            ch == 'u');

# Function to return the count of vowels
# in the substring str[l...r]
def countVowels(string, l, r) :

    # To store the count of vowels
    cnt = 0;

    # For every character in
    # the index range [l, r]
    for i in range(l, r + 1) :

        # If the current character
        # is a vowel
        if (isVowel(string[i])) :
            cnt += 1;

    return cnt;

def performQueries(string, queries, q) :

    # For every query
    for i in range(q) :

        # Find the count of vowels
        # for the current query
        print(countVowels(string, queries[i][0],
                                  queries[i][1]));

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";
    queries = [ [ 1, 3 ],
                [ 2, 4 ],
                [ 1, 9 ] ];
    q = len(queries)

    performQueries(string, queries, q);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int N = 2;

// Function that returns true
// if ch is a vowel
static Boolean isVowel(char ch)
{

    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// Function to return the count of vowels
// in the substring str[l...r]
static int countVowels(String str,
                       int l, int r)
{

    // To store the count of vowels
    int cnt = 0;

    // For every character in
    // the index range [l, r]
    for (int i = l; i <= r; i++)
    {

        // If the current character
        // is a vowel
        if (isVowel(str[i]))
            cnt++;
    }
    return cnt;
}

static void performQueries(String str,
                           int [,]queries,
                           int q)
{

    // For every query
    for (int i = 0; i < q; i++)
    {

        // Find the count of vowels
        // for the current query
        Console.WriteLine(countVowels(str, queries[i, 0],
                                           queries[i, 1]));
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int [,]queries = { { 1, 3 }, { 2, 4 },
                                 { 1, 9 } };
    int q = queries.GetLength(0);

    performQueries(str, queries, q);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let N = 2;

    // Function that returns true
    // if ch is a vowel
    function isVowel(ch)
    {

        return (ch == 'a' || ch == 'e' ||
                ch == 'i' || ch == 'o' ||
                ch == 'u');
    }

    // Function to return the count of vowels
    // in the substring str[l...r]
    function countVowels(str, l, r)
    {

        // To store the count of vowels
        let cnt = 0;

        // For every character in
        // the index range [l, r]
        for (let i = l; i <= r; i++)
        {

            // If the current character
            // is a vowel
            if (isVowel(str[i]))
                cnt++;
        }
        return cnt;
    }

    function performQueries(str, queries, q)
    {

        // For every query
        for (let i = 0; i < q; i++)
        {

            // Find the count of vowels
            // for the current query
            document.write(countVowels(str, queries[i][0],
                                                queries[i][1]) + "</br>");
        }
    }

    let str = "geeksforgeeks";
    let queries = [ [ 1, 3 ], [ 2, 4 ], [ 1, 9 ] ];
    let q = queries.length;

    performQueries(str, queries, q);

</script>
```

**Output:** 

```
2
1
4
```

**时间复杂度:** O(N * Q)，其中 N 为字符串长度，Q 为查询次数。

**有效方法:**创建前缀数组 **pre[]** ，其中 **pre[i]** 将存储子串 **str[0…i]** 中的计数元音。现在**【L，R】**范围内的元音数可以很容易地在 O(1)中计算为**pre[R]–pre[L–1]**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 2

// Function that returns true
// if ch is a vowel
bool isVowel(char ch)
{

    return (ch == 'a' || ch == 'e'
            || ch == 'i' || ch == 'o'
            || ch == 'u');
}

void performQueries(string str, int len,
                    int queries[][N], int q)
{

    // pre[i] will store the count of
    // vowels in the substring str[0...i]
    int pre[len];

    if (isVowel(str[0]))
        pre[0] = 1;
    else
        pre[0] = 0;

    // Fill the pre[] array
    for (int i = 1; i < len; i++) {

        // If current character is a vowel
        if (isVowel(str[i]))
            pre[i] = 1 + pre[i - 1];

        // If its a consonant
        else
            pre[i] = pre[i - 1];
    }

    // For every query
    for (int i = 0; i < q; i++) {

        // Find the count of vowels
        // for the current query
        if (queries[i][0] == 0) {
            cout << pre[queries[i][1]] << "\n";
        }
        else {
            cout << (pre[queries[i][1]]
                     - pre[queries[i][0] - 1])
                 << "\n";
        }
    }
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int len = str.length();
    int queries[][N] = { { 1, 3 }, { 2, 4 }, { 1, 9 } };
    int q = (sizeof(queries)
             / sizeof(queries[0]));

    performQueries(str, len, queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static final int N = 2;

// Function that returns true
// if ch is a vowel
static Boolean isVowel(char ch)
{

    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

static void performQueries(String str, int len,
                      int queries[][], int q)
{

    // pre[i] will store the count of
    // vowels in the subString str[0...i]
    int []pre = new int[len];

    if (isVowel(str.charAt(0)))
        pre[0] = 1;
    else
        pre[0] = 0;

    // Fill the pre[] array
    for (int i = 1; i < len; i++)
    {

        // If current character is a vowel
        if (isVowel(str.charAt(i)))
            pre[i] = 1 + pre[i - 1];

        // If its a consonant
        else
            pre[i] = pre[i - 1];
    }

    // For every query
    for (int i = 0; i < q; i++)
    {

        // Find the count of vowels
        // for the current query
        if (queries[i][0] == 0)
        {
            System.out.println(pre[queries[i][1]]);
        }
        else
        {
            System.out.println((pre[queries[i][1]] -
                                pre[queries[i][0] - 1]));
        }
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int len = str.length();
    int queries[][] = { { 1, 3 },
                        { 2, 4 }, { 1, 9 } };
    int q = queries.length;

    performQueries(str, len, queries, q);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
N = 2

# Function that returns true
# if ch is a vowel
def isVowel(ch):
    return (ch == 'a' or ch == 'e' or
            ch == 'i' or ch == 'o' or
            ch == 'u')

def performQueries(str1, len1, queries, q):

    # pre[i] will store the count of
    # vowels in the substring str[0...i]
    pre = [0 for i in range(len1)]

    if (isVowel(str1[0])):
        pre[0] = 1
    else:
        pre[0] = 0

    # Fill the pre[] array
    for i in range(0, len1, 1):

        # If current character is a vowel
        if (isVowel(str1[i])):
            pre[i] = 1 + pre[i - 1]

        # If its a consonant
        else:
            pre[i] = pre[i - 1]

    # For every query
    for i in range(q):

        # Find the count of vowels
        # for the current query
        if (queries[i][0] == 0):
            print(pre[queries[i][1]])
        else:
            print(pre[queries[i][1]] -
                  pre[queries[i][0] - 1])

# Driver code
if __name__ == '__main__':
    str1 = "geeksforgeeks"
    len1 = len(str1)
    queries = [[1, 3], [2, 4], [1, 9]]
    q = len(queries)

    performQueries(str1, len1, queries, q)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static readonly int N = 2;

// Function that returns true
// if ch is a vowel
static Boolean isVowel(char ch)
{

    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

static void performQueries(String str, int len,
                       int [,]queries, int q)
{

    // pre[i] will store the count of
    // vowels in the subString str[0...i]
    int []pre = new int[len];

    if (isVowel(str[0]))
        pre[0] = 1;
    else
        pre[0] = 0;

    // Fill the pre[] array
    for (int i = 1; i < len; i++)
    {

        // If current character is a vowel
        if (isVowel(str[i]))
            pre[i] = 1 + pre[i - 1];

        // If its a consonant
        else
            pre[i] = pre[i - 1];
    }

    // For every query
    for (int i = 0; i < q; i++)
    {

        // Find the count of vowels
        // for the current query
        if (queries[i, 0] == 0)
        {
            Console.WriteLine(pre[queries[i, 1]]);
        }
        else
        {
            Console.WriteLine((pre[queries[i, 1]] -
                               pre[queries[i, 0] - 1]));
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int len = str.Length;
    int [,]queries = { { 1, 3 },
                       { 2, 4 }, { 1, 9 } };
    int q = queries.GetLength(0);

    performQueries(str, len, queries, q);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var N = 2;

// Function that returns true
// if ch is a vowel
function isVowel(ch)
{

    return (ch == 'a' || ch == 'e'
            || ch == 'i' || ch == 'o'
            || ch == 'u');
}

function performQueries(str, len, queries, q)
{

    // pre[i] will store the count of
    // vowels in the substring str[0...i]
    var pre = Array(len);

    if (isVowel(str[0]))
        pre[0] = 1;
    else
        pre[0] = 0;

    // Fill the pre[] array
    for (var i = 1; i < len; i++) {

        // If current character is a vowel
        if (isVowel(str[i]))
            pre[i] = 1 + pre[i - 1];

        // If its a consonant
        else
            pre[i] = pre[i - 1];
    }

    // For every query
    for (var i = 0; i < q; i++) {

        // Find the count of vowels
        // for the current query
        if (queries[i][0] == 0) {
            document.write( pre[queries[i][1]] + "<br>");
        }
        else {
            document.write(pre[queries[i][1]]
                     - pre[queries[i][0] - 1]
                  +  "<br>");
        }
    }
}

// Driver code
var str = "geeksforgeeks";
var len = str.length;
var queries = [ [ 1, 3 ], [ 2, 4 ], [ 1, 9 ] ];
var q = queries.length
performQueries(str, len, queries, q);

</script>
```

**Output:** 

```
2
1
4
```

**时间复杂度:** O(N)用于预计算，O(1)用于每个查询。