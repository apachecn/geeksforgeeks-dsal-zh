# 使用 stringstream

查找大于给定长度 k 的单词

> 原文:[https://www . geeksforgeeks . org/find-words-what-大于给定长度-k-use-string stream/](https://www.geeksforgeeks.org/find-words-which-are-greater-than-given-length-k-using-stringstream/)

给定一个包含空格分隔的单词和数字 K 的字符串。任务是使用 C++中的[string stream](https://www.geeksforgeeks.org/stringstream-c-applications/)查找并打印所有长度大于 K 的单词。

在[之前的文章](https://www.geeksforgeeks.org/find-words-greater-given-length-k/)中讨论了使用循环来解决这个问题的一般解决方案。在本文中，将讨论在 C++中使用 stringstream 的解决方案。

**示例** :

```
Input : str = "hello geeks for geeks 
          is computer science portal" 
        K = 4
Output : hello geeks geeks computer 
         science portal

Input : str = "string is fun in python"
        K = 3
Output : string python

```

其思想是使用 stringstream 通过将给定的字符串拆分成标记来创建流，然后处理该流并打印长度大于 k 的单词。

下面是上面思路的实现:

```
// C++ program to find all string 
// which are greater than given length k
// using stringstream

#include <bits/stdc++.h>
using namespace std;

// Function to find all string 
// which are greater than given length k
// using stringstream
void findWords(string str, int K)
{
    string word;

    // using stringstream to break
    // the string into tokens
    stringstream ss(str); 

    int count = 0;
    while (ss >> word) { // reading words
        if (word.size() > K) {
            cout << word << " ";
            count++;
        }
    }
}

// Driver code
int main()
{
    string str = "geeks for geeks";

    int k = 4;

    findWords(str, k);

    return 0;
}
```

**输出:**

```
geeks geeks

```