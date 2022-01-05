# 使用 Stringstream 删除字符串中的空格

> 原文:[https://www . geesforgeks . org/remove-spaces-string-using-string stream/](https://www.geeksforgeeks.org/removing-spaces-string-using-stringstream/)

删除字符串中空格的解决方案已经在这里发布了。本文讨论了另一种使用 **stringstream** 的解决方案。

**算法:**

```
1\. Enter the whole string into stringstream.
2\. Empty the string.
3\. Extract word by word and concatenate to the string.
```

**程序 1:** 使用 [EOF](https://www.geeksforgeeks.org/eof-and-feof-in-c/) 。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to remove spaces using stringstream
#include <bits/stdc++.h>
using namespace std;

// Function to remove spaces
string removeSpaces(string str)
{
    stringstream ss;
    string temp;

    // Storing the whole string
    // into string stream
    ss << str;

    // Making the string empty
    str = "";

    // Running loop till end of stream
    while (!ss.eof()) {

        // Extracting word by word from stream
        ss >> temp;

        // Concatenating in the string to be
        // returned
        str = str + temp;
    }
    return str;
}

// Driver function
int main()
{
    // Sample Inputs
    string s = "This is a test";
    cout << removeSpaces(s) << endl;

    s = "geeks for geeks";
    cout << removeSpaces(s) << endl;

    s = "geeks quiz is awesome!";
    cout << removeSpaces(s) << endl;

    s = "I love     to     code";
    cout << removeSpaces(s) << endl;

    return 0;
}
```

**Output**

```
Thisisatest
geeksforgeeks
geeksquizisawesome!
Ilovetocode
```