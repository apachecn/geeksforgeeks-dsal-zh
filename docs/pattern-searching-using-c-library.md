# 使用 C++库进行模式搜索

> 原文:[https://www . geesforgeks . org/pattern-search-use-c-library/](https://www.geeksforgeeks.org/pattern-searching-using-c-library/)

给定文本 txt[0..n-1]和模式 pat[0..m-1]，编写一个函数，打印所有出现在 txt[]中的 pat[]。你可以假设 n > m
个例子:

```
Input : txt[] = "geeks for geeks"
        pat[] = "geeks"
Output : Pattern found at index 0
         Pattern found at index 10

Input : txt[] = "aaaa"
        pat[] = "aa"
Output : Pattern found at index 0
         Pattern found at index 1
         Pattern found at index 2
```

想法是在 C++字符串类中使用 [find()。](https://www.geeksforgeeks.org/c-string-class-and-its-applications/)

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to print all occurrences of a pattern
// in a text
#include <bits/stdc++.h>
using namespace std;

void printOccurrences(string txt, string pat)
{
    int found = txt.find(pat);
    while (found != string::npos) {
        cout << "Pattern found at index " << found << endl;
        found = txt.find(pat, found + 1);
    }
}

int main()
{
    string txt = "aaaa", pat = "aa";
    printOccurrences(txt, pat);
    return 0;
}
```

**Output:** 

```
Pattern found at index 0
Pattern found at index 1
Pattern found at index 2
```