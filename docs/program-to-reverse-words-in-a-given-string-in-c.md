# 在 C++中对给定字符串中的单词进行倒排的程序

> 原文:[https://www . geesforgeks . org/program-to-reverse-word-in-给定字符串-in-c/](https://www.geeksforgeeks.org/program-to-reverse-words-in-a-given-string-in-c/)

以字符串 **str** 的形式给定一个句子，任务是在 C++中反转给定句子的每个单词。
**例:**

> **输入:** str = "天空是蓝色的"
> T3】输出:蓝色是天空
> T6】输入: str = "我爱编程"
> T9】输出:编程爱我

**<u>方法一:使用</u>** [**<u>STL 功能</u>**](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)

1.  [使用 STL 功能](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)[反向()](https://www.geeksforgeeks.org/stdreverse-in-c/)反向给定字符串 **字符串**。
2.  迭代反转的字符串，并且每当找到一个空格时[使用 STL 函数**反向()**反向该空格前的单词](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to reverse the given string
string reverseString(string str)
{

    // Reverse str using inbuilt function
    reverse(str.begin(), str.end());

    // Add space at the end so that the
    // last word is also reversed
    str.insert(str.end(), ' ');

    int n = str.length();

    int j = 0;

    // Find spaces and reverse all words
    // before that
    for (int i = 0; i < n; i++) {

        // If a space is encountered
        if (str[i] == ' ') {
            reverse(str.begin() + j,
                    str.begin() + i);

            // Update the starting index
            // for next word to reverse
            j = i + 1;
        }
    }

    // Remove spaces from the end of the
    // word that we appended
    str.pop_back();

    // Return the reversed string
    return str;
}

// Driver code
int main()
{
    string str = "I like this code";

    // Function call
    string rev = reverseString(str);

    // Print the reversed string
    cout << rev;
    return 0;
}
```

**Output:** 

```
code this like I
```

**<u>方法二:不使用内置函数</u> :** 我们可以创建 reverse()函数，用于反转给定的字符串。以下是步骤:

1.  最初反转给定字符串的每个单词。
2.  现在反转整个字符串，以期望的顺序得到结果字符串。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function used to reverse a string
// from index l to r
void reversed(string& s, int l, int r)
{

    while (l < r) {

        // Swap characters at l and r
        swap(s[l], s[r]);
        l++;
        r--;
    }
}

// Function to reverse the given string
string reverseString(string str)
{

    // Add space at the end so that the
    // last word is also reversed
    str.insert(str.end(), ' ');

    int n = str.length();

    int j = 0;

    // Find spaces and reverse all words
    // before that
    for (int i = 0; i < n; i++) {

        // If a space is encountered
        if (str[i] == ' ') {

            // Function call to our custom
            // reverse function()
            reversed(str, j, i - 1);

            // Update the starting index
            // for next word to reverse
            j = i + 1;
        }
    }

    // Remove spaces from the end of the
    // word that we appended
    str.pop_back();

    // Reverse the whole string
    reversed(str, 0, str.length() - 1);

    // Return the reversed string
    return str;
}

// Driver code
int main()
{
    string str = "I like this code";

    // Function call
    string rev = reverseString(str);

    // Print the reversed string
    cout << rev;
    return 0;
}
```

**Output:** 

```
code this like I
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)