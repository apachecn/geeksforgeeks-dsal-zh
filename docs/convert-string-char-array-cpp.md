# 在 C++中将字符串转换为字符数组

> 原文:[https://www . geesforgeks . org/convert-string-char-array-CPP/](https://www.geeksforgeeks.org/convert-string-char-array-cpp/)

我们很多人都遇到过错误**'无法将 std::string 转换为 char[]或 char*数据类型'**。
例子:

```
Input : string s = "geeksforgeeks" ;
Output : char s[] = { 'g', 'e', 'e', 'k', 's', 'f', 'o',
                     'r', 'g', 'e', 'e', 'k', 's' } ;
Input : string s = "coding" ;
Output : char s[] = { 'c', 'o', 'd', 'i', 'n', 'g' } ;
```

**方法 1**
一种方法是将字符串的内容复制到 char 数组中。这可以在库 cstring 的 c_str()和 strcpy()函数的帮助下完成。
函数的作用是:返回一个指向数组的指针，该数组包含一个空终止的字符序列，该序列代表字符串的当前值。
语法:

```
const char* c_str() const ;
```

如果抛出异常，则字符串中没有任何更改。但是当我们需要查找或访问单个元素时，我们使用 strcpy()函数将其复制到 char 数组中。复制后，我们可以像使用简单数组一样使用它。
所取字符数组的长度不应小于输入字符串的长度。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to convert string
// to char array
#include <iostream>
#include <cstring>

using namespace std;

// driver code
int main()
{
    // assigning value to string s
    string s = "geeksforgeeks";

    int n = s.length();

    // declaring character array
    char char_array[n + 1];

    // copying the contents of the
    // string to char array
    strcpy(char_array, s.c_str());

    for (int i = 0; i < n; i++)
        cout << char_array[i];

    return 0;
}
```

**Output**

```
geeksforgeeks
```