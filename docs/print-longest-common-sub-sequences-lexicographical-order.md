# 按照字典顺序打印所有最长的公共子序列

> 原文:[https://www . geesforgeks . org/print-最长-常见-子序列-词典编纂-顺序/](https://www.geeksforgeeks.org/print-longest-common-sub-sequences-lexicographical-order/)

你有两条绳子。现在你必须按照字典顺序打印所有最长的公共子序列？
示例:

```
Input : str1 = "abcabcaa", str2 = "acbacba"
Output: ababa
        abaca
        abcba
        acaba
        acaca
        acbaa
        acbca
```

这个问题是[最长公共子序列](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)的扩展。我们首先找到 LCS 的长度，并使用内存化(或动态编程)将所有 LCS 存储在 2D 表中。然后，我们在两个字符串中搜索从“a”到“z”(以输出排序顺序)的所有字符。如果在字符串中发现一个字符，并且该字符的当前位置指向 LCS，我们递归搜索当前 LCS 长度加 1 的所有出现。
下面是算法的实现。

## C++

```
// C++ program to find all LCS of two strings in
// sorted order.
#include<bits/stdc++.h>
#define MAX 100
using namespace std;

// length of lcs
int lcslen = 0;

// dp matrix to store result of sub calls for lcs
int dp[MAX][MAX];

// A memoization based function that returns LCS of
// str1[i..len1-1] and str2[j..len2-1]
int lcs(string str1, string str2, int len1, int len2,
                                      int i, int j)
{
    int &ret = dp[i][j];

    // base condition
    if (i==len1 || j==len2)
        return ret = 0;

    // if lcs has been computed
    if (ret != -1)
        return ret;

    ret = 0;

    // if characters are same return previous + 1 else
    // max of two sequences after removing i'th and j'th
    // char one by one
    if (str1[i] == str2[j])
        ret = 1 + lcs(str1, str2, len1, len2, i+1, j+1);
    else
        ret = max(lcs(str1, str2, len1, len2, i+1, j),
                  lcs(str1, str2, len1, len2, i, j+1));
    return ret;
}

// Function to print all routes common sub-sequences of
// length lcslen
void printAll(string str1, string str2, int len1, int len2,
              char data[], int indx1, int indx2, int currlcs)
{
    // if currlcs is equal to lcslen then print it
    if (currlcs == lcslen)
    {
        data[currlcs] = '\0';
        puts(data);
        return;
    }

    // if we are done with all the characters of both string
    if (indx1==len1 || indx2==len2)
        return;

    // here we have to print all sub-sequences lexicographically,
    // that's why we start from 'a'to'z' if this character is
    // present in both of them then append it in data[] and same
    // remaining part
    for (char ch='a'; ch<='z'; ch++)
    {
        // done is a flag to tell that we have printed all the
        // subsequences corresponding to current character
        bool done = false;

        for (int i=indx1; i<len1; i++)
        {
            // if character ch is present in str1 then check if
            // it is present in str2
            if (ch==str1[i])
            {
              for (int j=indx2; j<len2; j++)
              {
                // if ch is present in both of them and
                // remaining length is equal to remaining
                // lcs length then add ch in sub-sequence
                if (ch==str2[j] &&
                  dp[i][j] == lcslen-currlcs)
                {
                  data[currlcs] = ch;
                  printAll(str1, str2, len1, len2, data, i+1, j+1, currlcs+1);
                  done = true;
                  break;
                }
              }
            }

            // If we found LCS beginning with current character.
            if (done)
                break;
        }
    }
}

// This function prints all LCS of str1 and str2
// in lexicographic order.
void prinlAllLCSSorted(string str1, string str2)
{
    // Find lengths of both strings
    int len1 = str1.length(), len2 = str2.length();

    // Find length of LCS
    memset(dp, -1, sizeof(dp));
    lcslen = lcs(str1, str2, len1, len2, 0, 0);

    // Print all LCS using recursive backtracking
    // data[] is used to store individual LCS.
    char data[MAX];
    printAll(str1, str2, len1, len2, data, 0, 0, 0);
}

// Driver program to run the case
int main()
{
    string str1 = "abcabcaa", str2 = "acbacba";
    prinlAllLCSSorted(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all LCS of two strings in
// sorted order.
class GFG
{
  static int MAX = 100;

  // length of lcs
  static int lcslen = 0;

  // dp matrix to store result of sub calls for lcs
  static int[][] dp = new int[MAX][MAX];

  // A memoization based function that returns LCS of
  // str1[i..len1-1] and str2[j..len2-1]
  static int lcs(String str1, String str2,
                 int len1, int len2, int i, int j)
  {
    int ret = dp[i][j];

    // base condition
    if (i == len1 || j == len2)
      return ret = 0;

    // if lcs has been computed
    if (ret != -1)
      return ret;      
    ret = 0;

    // if characters are same return previous + 1 else
    // max of two sequences after removing i'th and j'th
    // char one by one
    if (str1.charAt(i) == str2.charAt(j))
      ret = 1 + lcs(str1, str2, len1, len2, i + 1, j + 1);
    else
      ret = Math.max(lcs(str1, str2, len1, len2, i + 1, j),
                     lcs(str1, str2, len1, len2, i, j + 1));
    return ret;
  }

  // Function to print all routes common sub-sequences of
  // length lcslen
  static void printAll(String str1, String str2, int len1, int len2,
                       char[] data, int indx1, int indx2, int currlcs)
  {

    // if currlcs is equal to lcslen then print it
    if (currlcs == lcslen)
    {
      data[currlcs] = '\0';
      System.out.println(new String(data));
      return;
    }

    // if we are done with all the characters of both string
    if (indx1 == len1 || indx2 == len2)
      return;

    // here we have to print all sub-sequences lexicographically,
    // that's why we start from 'a'to'z' if this character is
    // present in both of them then append it in data[] and same
    // remaining part
    for (char ch ='a'; ch <='z'; ch++)
    {

      // done is a flag to tell that we have printed all the
      // subsequences corresponding to current character
      boolean done = false;

      for (int i = indx1; i < len1; i++)
      {

        // if character ch is present in str1 then check if
        // it is present in str2
        if (ch == str1.charAt(i))
        {
          for (int j = indx2; j < len2; j++)
          {

            // if ch is present in both of them and
            // remaining length is equal to remaining
            // lcs length then add ch in sub-sequence
            if (ch == str2.charAt(j) &&
                dp[i][j] == lcslen - currlcs)
            {
              data[currlcs] = ch;
              printAll(str1, str2, len1, len2,
                       data, i + 1, j + 1, currlcs + 1);
              done = true;
              break;
            }
          }
        }

        // If we found LCS beginning with current character. 
        if (done)
          break;
      }
    }
  }

  // This function prints all LCS of str1 and str2
  // in lexicographic order.
  static void prinlAllLCSSorted(String str1, String str2)
  {

    // Find lengths of both strings
    int len1 = str1.length(), len2 = str2.length();

    // Find length of LCS
    for(int i = 0; i < MAX; i++)
    {
      for(int j = 0; j < MAX; j++)
      {
        dp[i][j] = -1;
      }
    }
    lcslen = lcs(str1, str2, len1, len2, 0, 0);

    // Print all LCS using recursive backtracking
    // data[] is used to store individual LCS.
    char[] data = new char[MAX];
    printAll(str1, str2, len1, len2, data, 0, 0, 0);
  }

  // Driver code
  public static void main(String[] args)
  {
    String str1 = "abcabcaa", str2 = "acbacba";
    prinlAllLCSSorted(str1, str2);
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program to find all LCS of two strings in
# sorted order.
MAX=100
lcslen = 0

# dp matrix to store result of sub calls for lcs
dp=[[-1 for i in range(MAX)] for i in range(MAX)]

# A memoization based function that returns LCS of
# str1[i..len1-1] and str2[j..len2-1]
def lcs(str1, str2, len1, len2, i, j):

    # base condition
    if (i == len1 or j == len2):
        dp[i][j] = 0
        return dp[i][j]

    # if lcs has been computed
    if (dp[i][j] != -1):
        return dp[i][j]

    ret = 0

    # if characters are same return previous + 1 else
    # max of two sequences after removing i'th and j'th
    # char one by one
    if (str1[i] == str2[j]):
        ret = 1 + lcs(str1, str2, len1, len2, i + 1, j + 1)
    else:
        ret = max(lcs(str1, str2, len1, len2, i + 1, j),
                  lcs(str1, str2, len1, len2, i, j + 1))
    dp[i][j] = ret
    return ret

# Function to prall routes common sub-sequences of
# length lcslen
def printAll(str1, str2, len1, len2,data, indx1, indx2, currlcs):

    # if currlcs is equal to lcslen then print
    if (currlcs == lcslen):
        print("".join(data[:currlcs]))
        return

    # if we are done with all the characters of both string
    if (indx1 == len1 or indx2 == len2):
        return

    # here we have to prall sub-sequences lexicographically,
    # that's why we start from 'a'to'z' if this character is
    # present in both of them then append it in data[] and same
    # remaining part
    for ch in range(ord('a'),ord('z') + 1):

        # done is a flag to tell that we have printed all the
        # subsequences corresponding to current character
        done = False

        for i in range(indx1,len1):
            # if character ch is present in str1 then check if
            # it is present in str2
            if (chr(ch)==str1[i]):
              for j in range(indx2, len2):

                # if ch is present in both of them and
                # remaining length is equal to remaining
                # lcs length then add ch in sub-sequence
                if (chr(ch) == str2[j] and dp[i][j] == lcslen-currlcs):
                  data[currlcs] = chr(ch)
                  printAll(str1, str2, len1, len2, data, i + 1, j + 1, currlcs + 1)
                  done = True
                  break

            # If we found LCS beginning with current character.
            if (done):
                break

# This function prints all LCS of str1 and str2
# in lexicographic order.
def prinlAllLCSSorted(str1, str2):
    global lcslen
    # Find lengths of both strings
    len1,len2 = len(str1),len(str2)

    lcslen = lcs(str1, str2, len1, len2, 0, 0)

    # Prall LCS using recursive backtracking
    # data[] is used to store individual LCS.
    data = ['a' for i in range(MAX)]
    printAll(str1, str2, len1, len2, data, 0, 0, 0)

# Driver program to run the case
if __name__ == '__main__':
    str1 = "abcabcaa"
    str2 = "acbacba"
    prinlAllLCSSorted(str1, str2)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find all LCS of two strings in
// sorted order.
using System;
class GFG
{   
    static int MAX = 100;

    // length of lcs
    static int lcslen = 0;

    // dp matrix to store result of sub calls for lcs
    static int[,] dp = new int[MAX,MAX];

    // A memoization based function that returns LCS of
    // str1[i..len1-1] and str2[j..len2-1]
    static int lcs(string str1, string str2,
                   int len1, int len2, int i, int j)
    {
        int ret = dp[i, j];

        // base condition
        if (i == len1 || j == len2)
            return ret = 0;

        // if lcs has been computed
        if (ret != -1)
            return ret;

        ret = 0;

        // if characters are same return previous + 1 else
        // max of two sequences after removing i'th and j'th
        // char one by one
        if (str1[i] == str2[j])
            ret = 1 + lcs(str1, str2, len1, len2, i + 1, j + 1);
        else
            ret = Math.Max(lcs(str1, str2, len1, len2, i + 1, j),
                      lcs(str1, str2, len1, len2, i, j + 1));
        return ret;
    }

    // Function to print all routes common sub-sequences of
    // length lcslen
    static void printAll(string str1, string str2, int len1, int len2,
                  char[] data, int indx1, int indx2, int currlcs)
    {
        // if currlcs is equal to lcslen then print it
        if (currlcs == lcslen)
        {
            data[currlcs] = '\0';
            Console.WriteLine(new string(data));
            return;
        }

        // if we are done with all the characters of both string
        if (indx1 == len1 || indx2 == len2)
            return;

        // here we have to print all sub-sequences lexicographically,
        // that's why we start from 'a'to'z' if this character is
        // present in both of them then append it in data[] and same
        // remaining part
        for (char ch='a'; ch<='z'; ch++)
        {
            // done is a flag to tell that we have printed all the
            // subsequences corresponding to current character
            bool done = false;

            for (int i = indx1; i < len1; i++)
            {
                // if character ch is present in str1 then check if
                // it is present in str2
                if (ch == str1[i])
                {
                  for (int j = indx2; j < len2; j++)
                  {
                    // if ch is present in both of them and
                    // remaining length is equal to remaining
                    // lcs length then add ch in sub-sequence
                    if (ch == str2[j] &&
                      lcs(str1, str2, len1, len2, i, j) == lcslen-currlcs)
                    {
                      data[currlcs] = ch;
                      printAll(str1, str2, len1, len2, data, i+1, j+1, currlcs+1);
                      done = true;
                      break;
                    }
                  }
                }

                // If we found LCS beginning with current character. 
                if (done)
                    break;
            }
        }
    }

    // This function prints all LCS of str1 and str2
    // in lexicographic order.
    static void prinlAllLCSSorted(string str1, string str2)
    {
        // Find lengths of both strings
        int len1 = str1.Length, len2 = str2.Length;

        // Find length of LCS
        for(int i = 0; i < MAX; i++)
        {
            for(int j = 0; j < MAX; j++)
            {
                dp[i, j] = -1;
            }
        }
        lcslen = lcs(str1, str2, len1, len2, 0, 0);

        // Print all LCS using recursive backtracking
        // data[] is used to store individual LCS.
        char[] data = new char[MAX];
        printAll(str1, str2, len1, len2, data, 0, 0, 0);
    }

  // Driver code
  static void Main()
  {
    string str1 = "abcabcaa", str2 = "acbacba";
    prinlAllLCSSorted(str1, str2);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript program to find all LCS of two strings in
// sorted order.

    let  MAX = 100;
    // length of lcs
    let lcslen = 0;

    // dp matrix to store result of sub calls for lcs
    let dp = new Array(MAX);

    // A memoization based function that returns LCS of
  // str1[i..len1-1] and str2[j..len2-1]
    function lcs(str1,str2,len1,len2,i,j)
    {
        let ret = dp[i][j];

    // base condition
    if (i == len1 || j == len2)
      return ret = 0;

    // if lcs has been computed
    if (ret != -1)
      return ret;     
    ret = 0;

    // if characters are same return previous + 1 else
    // max of two sequences after removing i'th and j'th
    // char one by one
    if (str1[i] == str2[j])
      ret = 1 + lcs(str1, str2, len1, len2, i + 1, j + 1);
    else
      ret = Math.max(lcs(str1, str2, len1, len2, i + 1, j),
                     lcs(str1, str2, len1, len2, i, j + 1));
    return ret;
    }

    // Function to print all routes common sub-sequences of
  // length lcslen
    function printAll(str1,str2,len1,len2,data,indx1,indx2,currlcs)
    {
        // if currlcs is equal to lcslen then print it
    if (currlcs == lcslen)
    {
      data[currlcs] = null;
      document.write(data.join("")+"<br>");
      return;
    }

    // if we are done with all the characters of both string
    if (indx1 == len1 || indx2 == len2)
      return;

    // here we have to print all sub-sequences lexicographically,
    // that's why we start from 'a'to'z' if this character is
    // present in both of them then append it in data[] and same
    // remaining part
    for (let ch ='a'.charCodeAt(0); ch <='z'.charCodeAt(0); ch++)
    {

      // done is a flag to tell that we have printed all the
      // subsequences corresponding to current character
      let done = false;

      for (let i = indx1; i < len1; i++)
      {

        // if character ch is present in str1 then check if
        // it is present in str2
        if (ch == str1[i].charCodeAt(0))
        {
          for (let j = indx2; j < len2; j++)
          {

            // if ch is present in both of them and
            // remaining length is equal to remaining
            // lcs length then add ch in sub-sequence
            if (ch == str2[j].charCodeAt(0) &&
                lcs(str1, str2, len1, len2, i, j) == lcslen - currlcs)
            {
              data[currlcs] = String.fromCharCode(ch);
              printAll(str1, str2, len1, len2,
                       data, i + 1, j + 1, currlcs + 1);
              done = true;
              break;
            }
          }
        }

        // If we found LCS beginning with current character.
        if (done)
          break;
      }
    }
    }

    // This function prints all LCS of str1 and str2
  // in lexicographic order.
    function prinlAllLCSSorted(str1,str2)
    {
        // Find lengths of both strings
    let len1 = str1.length, len2 = str2.length;

    // Find length of LCS
    for(let i = 0; i < MAX; i++)
    {
        dp[i]=new Array(MAX);
      for(let j = 0; j < MAX; j++)
      {
        dp[i][j] = -1;
      }
    }
    lcslen = lcs(str1, str2, len1, len2, 0, 0);

    // Print all LCS using recursive backtracking
    // data[] is used to store individual LCS.
    let data = new Array(MAX);
    printAll(str1, str2, len1, len2, data, 0, 0, 0);
    }

    // Driver code
    let str1 = "abcabcaa", str2 = "acbacba";
    prinlAllLCSSorted(str1, str2);

    // This code is contributed by unknown2108
</script>
```

**Output**

```
ababa
abaca
abcba
acaba
acaca
acbaa
acbca
```

本文由 [**沙沙克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。