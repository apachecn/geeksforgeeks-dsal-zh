# 可以由给定的弦形成的任何长度的所有可能的弦

> 原文:[https://www . geesforgeks . org/可能-字符串-长度-可形成-给定-字符串/](https://www.geeksforgeeks.org/possible-strings-length-can-formed-given-string/)

给定一串不同的字符，打印由给定字符串组成的任何长度的所有可能的字符串。

示例:

```
Input: abc
Output: a b c abc ab ac bc bac bca 
         cb ca ba cab cba acb

Input: abcd
Output: a b ab ba c ac ca bc cb abc acb bac
         bca cab cba d ad da bd db abd adb bad 
         bda dab dba cd dc acd adc cad cda dac 
         dca bcd bdc cbd cdb dbc dcb abcd abdc 
         acbd acdb adbc adcb bacd badc bcad bcda 
         bdac bdca cabd cadb cbad cbda cdab cdba 
         dabc dacb dbac dbca dcab dcba 

```

所有字符串的生成包括以下步骤。
1) [生成给定字符串的所有子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。
2)对于每个子序列“子序列”，打印“子序列”的所有排列

下面是 C++实现。它使用 C++中的[next _ 置换函数](https://www.geeksforgeeks.org/find-the-next-lexicographically-greater-word-than-a-given-word/)。

## C/C++

```
/*  C++ code to generate all possible strings
    that can be formed from given string */
#include<bits/stdc++.h>
using namespace std;

void printAll(string str)
{
    /* Number of subsequences is (2**n -1)*/
    int n = str.length();
    unsigned int opsize = pow(2, n);

    /* Generate all subsequences of a given string.
       using counter 000..1 to 111..1*/
    for (int counter = 1; counter < opsize; counter++)
    {
        string subs = "";
        for (int j = 0; j < n; j++)
        {
            /* Check if jth bit in the counter is set
                If set then print jth element from arr[] */
            if (counter & (1<<j))
                subs.push_back(str[j]);
        }

        /* Print all permutations of current subsequence */
        do
        {
            cout << subs << " ";
        }
        while (next_permutation(subs.begin(), subs.end()));
    }
}

// Driver program
int main()
{
    string str = "abc";
    printSubsequences(str);
    return 0;
}
```