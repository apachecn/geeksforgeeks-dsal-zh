# 对字符串子序列的查询

> 原文:[https://www.geeksforgeeks.org/queries-subsequence-string/](https://www.geeksforgeeks.org/queries-subsequence-string/)

给定一个字符串 **S** 和 **Q** 查询，每个查询包含一个字符串 **T** 。任务是如果 T 是 S 的子序列，则打印“是”，否则打印“否”。
**示例:**

```
Input : S = "geeksforgeeks"
Query 1: "gg"
Query 2: "gro"
Query 3: "gfg"
Query 4: "orf"

Output :
Yes
No
Yes
No
```

对于每个查询，使用**蛮力**，开始迭代 S 寻找 T 的第一个字符，一旦找到第一个字符，继续迭代 S 现在寻找 T 的第二个字符，以此类推(详见[本](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/))。如果设法找到所有的字符，打印“是”，否则打印“否”。时间复杂度为 O(Q*N)，N 为 s 的长度
**高效的方法**可以是如果我们知道 T 的下一个字符在 s 中的位置，那么简单地跳过当前和下一个字符位置之间的所有字符，跳到那个位置。这可以通过制作|S| x 26 大小的矩阵并从 S 的每个位置存储每个字符的下一个位置来实现。
下面是上述思想的实现:

## C++

```
// C++ program to answer subsequence queries for a
// given string.
#include <bits/stdc++.h>
#define MAX 10000
#define CHAR_SIZE 26
using namespace std;

// Precompute the position of each character from
// each position of String S
void precompute(int mat[MAX][CHAR_SIZE], char str[],
                                           int len)
{
    for (int i = 0; i < CHAR_SIZE; ++i)
        mat[len][i] = len;

    // Computing position of each character from
    // each position of String S
    for (int i = len-1; i >= 0; --i)
    {
        for (int j = 0; j < CHAR_SIZE; ++j)
            mat[i][j] = mat[i+1][j];

        mat[i][str[i]-'a'] = i;
    }
}

// Print "Yes" if T is subsequence of S, else "No"
bool query(int mat[MAX][CHAR_SIZE], const char *str,
                                          int len)
{
    int pos = 0;

    // Traversing the string T
    for (int i = 0; i < strlen(str); ++i)
    {
        // If next position is greater than
        // length of S set flag to false.
        if (mat[pos][str[i] - 'a'] >= len)
            return false;

        // Setting position of next character
        else
            pos = mat[pos][str[i] - 'a'] + 1;
    }
    return true;
}

// Driven Program
int main()
{
    char S[]= "geeksforgeeks";
    int len = strlen(S);

    int mat[MAX][CHAR_SIZE];
    precompute(mat, S, len);

    query(mat, "gg", len)?  cout << "Yes\n" :
                            cout << "No\n";
    query(mat, "gro", len)? cout << "Yes\n" :
                            cout << "No\n";
    query(mat, "gfg", len)? cout << "Yes\n" :
                            cout << "No\n";
    query(mat, "orf", len)? cout << "Yes\n" :
                            cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to answer subsequence queries for
// a given string.
public class Query_Subsequence {

    static final int MAX = 10000;
    static final int CHAR_SIZE = 26;

    // Precompute the position of each character from
    // each position of String S
    static void precompute(int mat[][], String str, int len)
    {
        for (int i = 0; i < CHAR_SIZE; ++i)
            mat[len][i] = len;

        // Computing position of each character from
        // each position of String S
        for (int i = len-1; i >= 0; --i)
        {
            for (int j = 0; j < CHAR_SIZE; ++j)
                mat[i][j] = mat[i+1][j];

            mat[i][str.charAt(i)-'a'] = i;
        }
    }

    // Print "Yes" if T is subsequence of S, else "No"
    static boolean query(int mat[][], String str, int len)
    {
        int pos = 0;

        // Traversing the string T
        for (int i = 0; i < str.length(); ++i)
        {
            // If next position is greater than
            // length of S set flag to false.
            if (mat[pos][str.charAt(i) - 'a'] >= len)
                return false;

            // Setting position of next character
            else
                pos = mat[pos][str.charAt(i) - 'a'] + 1;
        }
        return true;
    }

    // Driven Program
    public static void main(String args[])
    {
        String S= "geeksforgeeks";
        int len = S.length();

        int[][] mat = new int[MAX][CHAR_SIZE];
        precompute(mat, S, len);

        String get = query(mat, "gg", len)? "Yes" :"No";
        System.out.println(get);
        get = query(mat, "gro", len)? "Yes" :"No";
        System.out.println(get);
        get = query(mat, "gfg", len)? "Yes" :"No";
        System.out.println(get);
        get = query(mat, "orf", len)? "Yes" :"No";
        System.out.println(get);

    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to answer
# subsequence queries for
# a given string.
MAX = 10000
CHAR_SIZE = 26

# Precompute the position of
# each character from
# each position of String S
def precompute(mat, str, Len):

    for i in range(CHAR_SIZE):
        mat[Len][i] = Len

    # Computing position of each
    # character from each position
    # of String S
    for i in range(Len - 1, -1, -1):
        for j in range(CHAR_SIZE):
            mat[i][j] = mat[i + 1][j]
        mat[i][ord(str[i]) -
               ord('a')] = i

# Print "Yes" if T is
# subsequence of S, else "No"
def query(mat, str, Len):
    pos = 0

    # Traversing the string T
    for i in range(len(str)):

        # If next position is greater than 
        # length of S set flag to false.
        if(mat[pos][ord(str[i]) -
                    ord('a')] >= Len):
            return False

        # Setting position of next character
        else:
            pos = mat[pos][ord(str[i]) -
                           ord('a')] + 1
    return True

# Driven code
S = "geeksforgeeks"
Len = len(S)
mat = [[0 for i in range(CHAR_SIZE)]
          for j in range(MAX)]
precompute(mat, S, Len)

get = "No"
if(query(mat, "gg", Len)):
    get = "Yes"
print(get)

get = "No"
if(query(mat, "gro", Len)):
    get = "Yes"
print(get)

get = "No"
if(query(mat, "gfg", Len)):
    get = "Yes"
print(get)

get = "No"
if(query(mat, "orf", Len)):
    get = "Yes"
print(get)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to answer subsequence
// queries for a given string
using System;
public class Query_Subsequence
{

    static int MAX = 10000;
    static int CHAR_SIZE = 26;

    // Precompute the position of each
    // character from each position
    // of String S
    static void precompute(int [,]mat,
                        string str,
                        int len)
    {

        for (int i = 0; i < CHAR_SIZE; ++i)
            mat[len, i] = len;

        // Computing position of each
        // character from each position
        // of String S
        for (int i = len - 1; i >= 0; --i)
        {
            for (int j = 0; j < CHAR_SIZE;
                ++j)
                mat[i, j] = mat[i + 1, j];

            mat[i, str[i] - 'a'] = i;
        }
    }

    // Print "Yes" if T is subsequence
    // of S, else "No"
    static bool query(int [,]mat,
                    string str,
                    int len)
    {
        int pos = 0;

        // Traversing the string T
        for (int i = 0; i < str.Length; ++i)
        {
            // If next position is greater than
            // length of S set flag to false.
            if (mat[pos,str[i] - 'a'] >= len)
                return false;

            // Setting position of next character
            else
                pos = mat[pos,str[i] - 'a'] + 1;
        }
        return true;
    }

    // Driver Code
    public static void Main()
    {
        string S= "geeksforgeeks";
        int len = S.Length;

        int[,] mat = new int[MAX,CHAR_SIZE];
        precompute(mat, S, len);

        string get = query(mat, "gg", len)?
                           "Yes" :"No";
        Console.WriteLine(get);
        get = query(mat, "gro", len)?
                         "Yes" :"No";
        Console.WriteLine(get);
        get = query(mat, "gfg", len)?
                         "Yes" :"No";
        Console.WriteLine(get);
        get = query(mat, "orf", len)?
                         "Yes" :"No";
        Console.WriteLine(get);

    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
    // Javascript program to answer subsequence queries for
    // a given string.

    let MAX = 10000;
    let CHAR_SIZE = 26;

    // Precompute the position of each character from
    // each position of String S
    function precompute(mat, str, len)
    {
        for (let i = 0; i < CHAR_SIZE; ++i)
            mat[len][i] = len;

        // Computing position of each character from
        // each position of String S
        for (let i = len-1; i >= 0; --i)
        {
            for (let j = 0; j < CHAR_SIZE; ++j)
                mat[i][j] = mat[i+1][j];

            mat[i][str[i].charCodeAt()-'a'.charCodeAt()] = i;
        }
    }

    // Print "Yes" if T is subsequence of S, else "No"
    function query(mat, str, len)
    {
        let pos = 0;

        // Traversing the string T
        for (let i = 0; i < str.length; ++i)
        {
            // If next position is greater than
            // length of S set flag to false.
            if (mat[pos][str[i].charCodeAt() - 'a'.charCodeAt()] >= len)
                return false;

            // Setting position of next character
            else
                pos = mat[pos][str[i].charCodeAt() - 'a'.charCodeAt()] + 1;
        }
        return true;
    }

    let S= "geeksforgeeks";
    let len = S.length;

    let mat = new Array(MAX);
    for(let i = 0; i < MAX; i++)
    {
        mat[i] = new Array(CHAR_SIZE);
        for(let j = 0; j < CHAR_SIZE; j++)
        {
            mat[i][j] = 0;
        }
    }
    precompute(mat, S, len);

    let get = query(mat, "gg", len)? "Yes" :"No";
    document.write(get + "</br>");
    get = query(mat, "gro", len)? "Yes" :"No";
    document.write(get + "</br>");
    get = query(mat, "gfg", len)? "Yes" :"No";
    document.write(get + "</br>");
    get = query(mat, "orf", len)? "Yes" :"No";
    document.write(get + "</br>");

</script>
```

**输出:**

```
Yes
No
Yes
No
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。