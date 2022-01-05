# 打印字符排列位置制作回文

> 原文:[https://www . geeksforgeeks . org/print-将字符的排列位置转换为回文/](https://www.geeksforgeeks.org/print-the-arranged-positions-of-characters-to-make-palindrome/)

给你一个长度为 n 的字符串 s(只有小写字母)。打印它必须获得的字符串的每个字符的位置，这样它将形成一个回文字符串。

**示例:**

```
Input  : c b b a a
Output : 3 1 5 2 4
To make string palindrome 'c' must be at position 3,
'b' at 1 and 5, 'a' at 2 and 4.

Input : a b c
Output : Not Possible
Any permutation of string cannot form palindrome. 
```

其思想是创建一个向量数组(或动态大小数组)，存储每个字符的所有位置。在存储位置之后，我们检查奇数字符的计数是否超过 1。如果是，我们返回“不可能”。否则，我们首先打印数组的前半部分位置，然后打印奇数字符的一个位置(如果存在)，最后打印后半部分位置。

## C++

```
// CPP program to print original
// positions of characters in a
// string after rearranging and
// forming a palindrome
#include <bits/stdc++.h>
using namespace std;

// Maximum number of characters
const int MAX = 256;

void printPalindromePos(string &str)
{
    // Insert all positions of every
    // character in the given string.
    vector<int> pos[MAX];
    int n = str.length();
    for (int i = 0; i < n; i++)
        pos[str[i]].push_back(i+1);

    /* find the number of odd elements.
       Takes O(n) */
    int oddCount = 0;
    char oddChar;
    for (int i=0; i<MAX; i++) {
        if (pos[i].size() % 2 != 0) {
            oddCount++;
            oddChar = i;
        }
    }

    /* A palindrome cannot contain more than 1
       odd characters */
    if (oddCount > 1)
        cout << "NO PALINDROME";

    /* Print positions in first half
       of palindrome */
    for (int i=0; i<MAX; i++)
    {
        int mid = pos[i].size()/2;
        for (int j=0; j<mid; j++)
            cout << pos[i][j] << " ";
    }

    // Consider one instance odd character
    if (oddCount > 0)
    {
        int last = pos[oddChar].size() - 1;
        cout << pos[oddChar][last] << " ";
        pos[oddChar].pop_back();
    }

    /* Print positions in second half
       of palindrome */
    for (int i=MAX-1; i>=0; i--)
    {
        int count = pos[i].size();
        for (int j=count/2; j<count; j++)
            cout << pos[i][j] << " ";
    }
}

// Driver code
int main()
{
    string s = "geeksgk";
    printPalindromePos(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to print original
// positions of characters in a
// String after rearranging and
// forming a palindrome
import java.util.*;

class GFG
{

// Maximum number of characters
static int MAX = 256;

static void printPalindromePos(String str)
{
    // Insert all positions of every
    // character in the given String.
    Vector<Integer> []pos = new Vector[MAX];
    for (int i = 0; i < MAX; i++)
        pos[i] = new Vector<Integer>();
    int n = str.length();
    for (int i = 0; i < n; i++)
        pos[str.charAt(i)].add(i + 1);

    /* find the number of odd elements.
    Takes O(n) */
    int oddCount = 0;
    char oddChar = 0;
    for (int i = 0; i < MAX; i++)
    {
        if (pos[i].size() % 2 != 0)
        {
            oddCount++;
            oddChar = (char) i;
        }
    }

    /* A palindrome cannot contain more than 1
    odd characters */
    if (oddCount > 1)
        System.out.print("NO PALINDROME");

    /* Print positions in first half
    of palindrome */
    for (int i = 0; i < MAX; i++)
    {
        int mid = pos[i].size() / 2;
        for (int j = 0; j < mid; j++)
            System.out.print(pos[i].get(j) + " ");
    }

    // Consider one instance odd character
    if (oddCount > 0)
    {
        int last = pos[oddChar].size() - 1;
        System.out.print(pos[oddChar].get(last) + " ");
        pos[oddChar].remove(pos[oddChar].size() - 1);
    }

    /* Print positions in second half
    of palindrome */
    for (int i = MAX - 1; i >= 0; i--)
    {
        int count = pos[i].size();
        for (int j = count / 2; j < count; j++)
            System.out.print(pos[i].get(j) + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    String s = "geeksgk";
    printPalindromePos(s);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program to print original
// positions of characters in a
// String after rearranging and
// forming a palindrome
using System;
using System.Collections.Generic;

class GFG
{

// Maximum number of characters
static int MAX = 256;

static void printPalindromePos(String str)
{
    // Insert all positions of every
    // character in the given String.
    List<int> []pos = new List<int>[MAX];
    for (int i = 0; i < MAX; i++)
        pos[i] = new List<int>();
    int n = str.Length;
    for (int i = 0; i < n; i++)
        pos[str[i]].Add(i + 1);

    /* find the number of odd elements.
    Takes O(n) */
    int oddCount = 0;
    char oddChar = (char)0;
    for (int i = 0; i < MAX; i++)
    {
        if (pos[i].Count % 2 != 0)
        {
            oddCount++;
            oddChar = (char) i;
        }
    }

    /* A palindrome cannot contain more than 1
    odd characters */
    if (oddCount > 1)
        Console.Write("NO PALINDROME");

    /* Print positions in first half
    of palindrome */
    for (int i = 0; i < MAX; i++)
    {
        int mid = pos[i].Count / 2;
        for (int j = 0; j < mid; j++)
            Console.Write(pos[i][j] + " ");
    }

    // Consider one instance odd character
    if (oddCount > 0)
    {
        int last = pos[oddChar].Count - 1;
        Console.Write(pos[oddChar][last] + " ");
        pos[oddChar].RemoveAt(pos[oddChar].Count - 1);
    }

    /* Print positions in second half
    of palindrome */
    for (int i = MAX - 1; i >= 0; i--)
    {
        int count = pos[i].Count;
        for (int j = count / 2; j < count; j++)
            Console.Write(pos[i][j] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    String s = "geeksgk";
    printPalindromePos(s);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to print original
// positions of characters in a
// string after rearranging and
// forming a palindrome

// Maximum number of characters
var MAX = 256;

function printPalindromePos(str)
{
    // Insert all positions of every
    // character in the given string.
    var pos = Array.from(Array(MAX), ()=>Array());
    var n = str.length;
    for (var i = 0; i < n; i++)
        pos[str[i].charCodeAt(0)].push(i+1);

    /* find the number of odd elements.
       Takes O(n) */
    var oddCount = 0;
    var oddChar;
    for (var i=0; i<MAX; i++) {
        if (pos[i].length % 2 != 0) {
            oddCount++;
            oddChar = i;
        }
    }

    /* A palindrome cannot contain more than 1
       odd characters */
    if (oddCount > 1)
        document.write( "NO PALINDROME");

    /* Print positions in first half
       of palindrome */
    for (var i=0; i<MAX; i++)
    {
        var mid = pos[i].length/2;
        for (var j=0; j<mid; j++)
            document.write( pos[i][j] + " ");
    }

    // Consider one instance odd character
    if (oddCount > 0)
    {
        var last = pos[oddChar].length - 1;
        document.write( pos[oddChar][last] + " ");
        pos[oddChar].pop();
    }

    /* Print positions in second half
       of palindrome */
    for (var i=MAX-1; i>=0; i--)
    {
        var count = pos[i].length;
        for (var j=count/2; j<count; j++)
            document.write( pos[i][j] + " ");
    }
}

// Driver code
var s = "geeksgk";
printPalindromePos(s);

</script>
```

**Output:** 

```
2 1 4 5 7 6 3 
```

**时间复杂度** : O ( n )