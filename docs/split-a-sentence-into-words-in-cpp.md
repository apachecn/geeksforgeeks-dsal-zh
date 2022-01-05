# 在 C++中将一个句子拆分成单词

> 原文:[https://www . geeksforgeeks . org/split-a-a-句子-in-word-CPP/](https://www.geeksforgeeks.org/split-a-sentence-into-words-in-cpp/)

给出一个句子，打印出不同的单词。单词用空格隔开。

**示例:**

```
Input : str = "Geeks for Geeks"
Output : Geeks
         for
         Geeks  
Explanation : All space separated words 
are printed line by line.

Input : str = "a computer science portal"
Output : a
         computer
         science
         portal

```

**方法 1(书写我们自己的逻辑)**
我们遍历所有字符。如果当前字符是空格，我们已经到达一个单词的末尾，我们打印当前单词并将其重置为空。否则我们将当前字符附加到单词上。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print words in a sentence
#include <bits/stdc++.h>
using namespace std;

void removeDupWord(string str)
{
    string word = "";
    for (auto x : str) 
    {
        if (x == ' ')
        {
            cout << word << endl;
            word = "";
        }
        else {
            word = word + x;
        }
    }
    cout << word << endl;
}

// Driver code
int main()
{
    string str = "Geeks for Geeks";
    removeDupWord(str);
    return 0;
}
```

**Output**

```
Geeks
for
Geeks

```