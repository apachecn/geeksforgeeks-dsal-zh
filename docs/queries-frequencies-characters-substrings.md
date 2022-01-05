# 查询子串中字符的频率

> 原文:[https://www . geesforgeks . org/query-frequency-characters-substrings/](https://www.geeksforgeeks.org/queries-frequencies-characters-substrings/)

给定字符串 s 和 Q 的查询数。每个查询 Q 由 l 和 r 以及一个字符 c 组成，在子串 l 到 r 中查找字符 c 的频率
**示例:**

```
Input : s = geeksforgeeks
        4
        0 5 e
        2 6 f
        4 7 m
        0 12 e
Output : 2
         1
         0
         4
Substring from 0 to 5 is geeksf.
Here e occurs 2 times.

Input : s = apple
        2
        0 4 e
        1 2 p        
Output : 1
         2 
```

**天真方法:**对 Q 个查询运行从 l 到 r 的循环。计算字符出现次数并返回计数。整体时间复杂度将为 Q * O(|s|)。
**高效方法:**我们可以预先计算每个角色的数量。二维数组中每个字符的存储计数。从 0 到 r 的字符返回频率减去 O(1)中 0 到 l 范围内的字符频率。总时间复杂度为 Q * O(1)。

## C++

```
// CPP program to find occurrence
// of character in substring l to r
#include <bits/stdc++.h>
#define MAX_LEN 1005
#define MAX_CHAR 26

using namespace std;

// To store count of all character
int cnt[MAX_LEN][MAX_CHAR];

// To pre-process string from
// 0 to size of string
void preProcess(string s)
{
    int n = s.length();

    // Initializing cnt with 0
    memset(cnt, 0, sizeof(cnt));

    // Store occurrence of
    // character i
    for (int i = 0; i < n; i++)
        cnt[i][s[i] - 'a']++;

    // Store occurrence o
    // all character upto i
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < 26; j++)
            cnt[i][j] += cnt[i - 1][j];
    }
}

// To return occurrence of
// character in range l to r
int findCharFreq(int l, int r, char c)
{
    // Return occurrence of character
    // from 0 to r minus its
    // occurrence from 0 to l
    int count = cnt[r][c-'a'];

    if (l != 0)
        count -= cnt[l - 1][c-'a'];
    return count;
}

// Driver program to test above functions
int main()
{
    string s = "geeksforgeeks";
    int Q = 4;
    preProcess(s);

    cout << findCharFreq(0, 5, 'e') << endl;
    cout << findCharFreq(2, 6, 'f') << endl;
    cout << findCharFreq(4, 7, 'm') << endl;
    cout << findCharFreq(0, 12, 'e') << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find occurrence
// of character in substring l to r
import java.util.*;

class GFG
{

static int MAX_LEN = 1005;
static int MAX_CHAR = 26;

// To store count of all character
static int [][]cnt = new int[MAX_LEN][MAX_CHAR];

// To pre-process string from
// 0 to size of string
static void preProcess(String s)
{
    int n = s.length();

    // Store occurrence of
    // character i
    for (int i = 0; i < n; i++)
        cnt[i][s.charAt(i) - 'a']++;

    // Store occurrence o
    // all character upto i
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j < 26; j++)
            cnt[i][j] += cnt[i - 1][j];
    }
}

// To return occurrence of
// character in range l to r
static int findCharFreq(int l, int r, char c)
{
    // Return occurrence of character
    // from 0 to r minus its
    // occurrence from 0 to l
    return (cnt[r][(c) - 97] - cnt[l][(c) - 97]);
}

// Driver Code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    int Q = 4;
    preProcess(s);

    System.out.println(findCharFreq(0, 5, 'e'));
    System.out.println(findCharFreq(2, 6, 'f'));
    System.out.println(findCharFreq(4, 7, 'm'));
    System.out.println(findCharFreq(0, 12, 'e'));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find occurrence
# of character in substring l to r
MAX_LEN, MAX_CHAR = 1005, 26

# To store count of all character
cnt = [[0 for i in range(MAX_CHAR)]
          for j in range(MAX_LEN)]

# To pre-process string from
# 0 to size of string
def preProcess(s):

    n = len(s)

    # Store occurrence of character i
    for i in range(0, n):
        cnt[i][ord(s[i]) - ord('a')] += 1

    # Store occurrence o
    # all character upto i
    for i in range(1, n):
        for j in range(0, 26):
            cnt[i][j] += cnt[i - 1][j]

# To return occurrence of
# character in range l to r
def findCharFreq(l, r, c):

    # Return occurrence of character
    # from 0 to r minus its
    # occurrence from 0 to l
    return (cnt[r][ord(c) - 97] -
            cnt[l - 1][ord(c) - 97])

# Driver Code
if __name__ == "__main__":

    s = "geeksforgeeks"
    Q = 4
    preProcess(s)

    print(findCharFreq(0, 5, 'e'))
    print(findCharFreq(2, 6, 'f'))
    print(findCharFreq(4, 7, 'm'))
    print(findCharFreq(0, 12, 'e'))

# This code is contributed by Rituraj Jain
# and Edited by Md Azharuddin
```

## C#

```
// C# program to find occurrence
// of character in substring l to r
using System;

class GFG
{
    static int MAX_LEN = 1005;
    static int MAX_CHAR = 26;

    // To store count of all character
    static int[,] cnt = new int[MAX_LEN,
                                MAX_CHAR];

    // To pre-process string from
    // 0 to size of string
    static void preProcess(string s)
    {
        int n = s.Length;

        // Store occurrence of
        // character i
        for (int i = 0; i < n; i++)
            cnt[i, s[i] - 'a']++;

        // Store occurrence o
        // all character upto i
        for (int i = 1; i < n; i++)
        {
            for (int j = 0; j < 26; j++)
                cnt[i, j] += cnt[i - 1, j];
        }
    }

    // To return occurrence of
    // character in range l to r
    static int findCharFreq(int l, int r, char c)
    {
        // Return occurrence of character
        // from 0 to r minus its
        // occurrence from 0 to l
        return (cnt[r, c - 97] - cnt[l, c - 97]);
    }

    // Driver code
    public static void Main(string[] args)
    {
        string s = "geeksforgeeks";
        int Q = 4;
        preProcess(s);

        Console.WriteLine(findCharFreq(0, 5, 'e'));
        Console.WriteLine(findCharFreq(2, 6, 'f'));
        Console.WriteLine(findCharFreq(4, 7, 'm'));
        Console.WriteLine(findCharFreq(0, 12, 'e'));
    }
}

// This code is contributed by
// sanjeev2552
```

**输出:**

```
2
1
0
4
```