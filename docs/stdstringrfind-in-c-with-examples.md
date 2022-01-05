# std::string::rfind 在 C++中带有示例

> 原文:[https://www . geesforgeks . org/stdstringfind-in-c-with-examples/](https://www.geeksforgeeks.org/stdstringrfind-in-c-with-examples/)

**std::string::rfind** 是一个字符串类成员函数，用于搜索字符串中任何字符的最后一次出现。如果该字符出现在字符串中，则它返回该字符在字符串中最后一次出现的索引，否则它将返回**字符串::npos** ，表示指针在字符串的末尾。

**头文件:**

```
#include < string >

```

<u>**语法 1:**</u>

```
rfind(char ch)
rfind(string str)

```

**参数:**该函数以给定的**字符**或**字符串**为参数，其索引将被找到。

**返回值:**该方法返回该字符最后一次出现的**位置或字符串最后一次出现的第一个索引。**

**程序 1:**

下面是说明**字符串的程序::rfind(char ch)**:

```
// C++ program to demonstrate
// rfind() method

#include <cstddef>
#include <iostream>
#include <string>
using namespace std;

// Function to return last occurrence
// of character in a string
void findLastOccurernce(string str, char ch)
{

    // To store the index of the result
    size_t found;

    // Function to find the last
    // occurence of character ch
    // in string str
    found = str.rfind(ch);

    // If string doesn't have
    // character ch present in it
    if (found == string::npos) {
        cout << "Character " << ch
             << " is not present in"
             << " the given string.";
    }

    // Else print the position
    else {
        cout << "The last occurence of '"
             << ch << "' is found at index: "
             << found << endl;
    }
}

// Driver Code
int main()
{
    // Given String
    string str("Welcome to GeeksforGeeks!");

    // Character to be found
    char ch = 'e';

    findLastOccurernce(str, ch);
}
```

**Output:**

> 最后一次出现“e”是在索引处:21

**程序 2:**

下面是程序说明**字符串::rfind(字符串字符串)** :

```
// C++ program to demonstrate
// rfind() method

#include <cstddef>
#include <iostream>
#include <string>
using namespace std;

// Function to return last occurrence
// of string in a string
void findLastOccurernce(string str, string s)
{

    // To store the index of the result
    size_t found;

    // Function to find the first index
    // of last occurence of string s in str
    found = str.rfind(s);

    // If string doesn't have
    // string s present in it
    if (found == string::npos) {
        cout << "String '" << s
             << "' is not present in"
             << " the given string.";
    }

    // Else print the position
    else {
        cout << "The first index of last "
             << "occurence of '" << s
             << "' is found at index: "
             << found << endl;
    }
}

// Driver Code
int main()
{
    // Given String
    string str("Welcome to GeeksforGeeks!");

    // string to be found
    string s = "to";

    findLastOccurernce(str, s);
}
```

**输出:**

> 上次出现“to”的第一个索引位于索引:8