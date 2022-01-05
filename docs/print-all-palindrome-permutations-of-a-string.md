# 打印一个字符串的所有回文排列

> 原文:[https://www . geesforgeks . org/print-all-回文-字符串排列/](https://www.geeksforgeeks.org/print-all-palindrome-permutations-of-a-string/)

给定一个字符串，我们需要打印所有可能的回文，这些回文可以使用该字符串的字母生成。

示例:

```
Input:  str = "aabcb"
Output: abcba bacab

Input:  str = "aabbcadad"
Output: aabdcdbaa aadbcbdaa abadcdaba
        abdacadba adabcbada adbacabda
        baadcdaab badacadab bdaacaadb
        daabcbaad dabacabad dbaacaabd

```

回文的生成可以通过以下步骤完成，

1.  First, we need to check whether the letters of the string can form palindromes, and if not, return.
2.  After the above inspection, we can make half of the first palindrome string (the smallest in dictionary order) by taking half of the frequency of each letter of a given string.
3.  Now traverse all possible permutations of this half string, add the reverse order of this part at the end each time, and if the string is of odd length, add odd frequency characters in the middle to form palindromes.

下面是 C++实现。

## C

```
// C++ program to print all palindrome permutations of
// a string.
#include <bits/stdc++.h>
using namespace std;
#define M 26

/* Utility function to count frequencies and checking
    whether letter can make a palindrome or not */
bool isPalin(string str, int* freq)
{
    /* Initialising frequency array with all zeros */
    memset(freq, 0, M * sizeof(int));
    int l = str.length();

    /* Updating frequency according to given string */
    for (int i = 0; i < l; i++)
        freq[str[i] - 'a']++;

    int odd = 0;

    /* Loop to count total letter with odd frequency */
    for (int i = 0; i < M; i++)
        if (freq[i] % 2 == 1)
            odd++;

    /* Palindrome condition :
    if length is odd then only one letter's frequency must be odd
    if length is even no letter should have odd frequency */
    if ((l % 2 == 1 && odd == 1 ) || (l %2 == 0 && odd == 0))
        return true;
    else
        return false;
}

/* Utility function to reverse a string */
string reverse(string str)
{
    string rev = str;
    reverse(rev.begin(), rev.end());
    return rev;
}

/* Function to print all possible palindromes by letter of
    given string */
void printAllPossiblePalindromes(string str)
{
    int freq[M];

    // checking whether letter can make palindrome or not
    if (!isPalin(str, freq))
        return;

    int l = str.length();

    // half will contain half part of all palindromes,
    // that is why pushing half freq of each letter
    string half = "";
    char oddC;
    for (int i = 0; i < M; i++)
    {
        /* This condition will be true at most once */
        if(freq[i] % 2 == 1)
            oddC = i + 'a';

        half += string(freq[i] / 2, i + 'a');
    }

    /* palin will store the possible palindromes one by one */
    string palin;

    // Now looping through all permutation of half, and adding
    // reverse part at end.
    // if length is odd, then pushing oddCharacter also in mid
    do
    {
        palin = half;
        if (l % 2 == 1)
            palin += oddC;
        palin += reverse(half);
        cout << palin << endl;
    }
    while (next_permutation(half.begin(), half.end()));
}

// Driver Program to test above function
int main()
{
    string str = "aabbcadad";
    cout << "All palindrome permutations of " << str << endl;
    printAllPossiblePalindromes(str);
    return 0;
}
```

Output:

```
All palindrome permutations of aabbcadad
aabdcdbaa
aadbcbdaa
abadcdaba
abdacadba
adabcbada
adbacabda
baadcdaab
badacadab
bdaacaadb
daabcbaad
dabacabad
dbaacaabd
```

**插图:**

```
Let given string is "aabbcadad"

Letters have following frequencies : 
 a(4), b(2), c(1), d(2).

As all letter has even frequency except one we can 
make palindromes with the letter of this string.

Now half part is – aabd

So traversing through all possible permutations of 
this half string and adding odd frequency character 
and reverse of string at the end we get following 
possible palindrome as final result : 
aabdcdbaa   aadbcbdaa   abadcdaba   abdacadba
adabcbada   adbacabda   baadcdaab   badacadab
bdaacaadb   daabcbaad   dabacabad   dbaacaabd
```

本文由乌卡什·特里维迪供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论