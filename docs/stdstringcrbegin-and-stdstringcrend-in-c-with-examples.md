# c++中的 std::string::crbegin()和 std::string::crend()，示例

> 原文:[https://www . geeksforgeeks . org/stdstringrbegin-and-stdstringtrend-in-c-with-examples/](https://www.geeksforgeeks.org/stdstringcrbegin-and-stdstringcrend-in-c-with-examples/)

<u>**STD::string::crbegin()**T3】</u>

**std::string::crbegin()** 是一个字符串类内置函数，返回一个引用字符串中最后一个元素的常量反向迭代器。使用这个迭代器从字符串的末尾开始遍历字符串。

**头文件:**

```
#include <string>

```

**模板类:**

```
template <class C>
auto crbegin( const C& c ) 
        -> decltype(std::rbegin(c));

```

**语法:**

```
string_name.crbegin()

```

**参数:**该功能不需要任何参数。

**返回值:**这个函数 **std::string::crbegin()** 返回一个引用字符串中最后一个元素的常量反向迭代器。

下面是说明**字符串的程序:**

**程序 1:**

```
// C++ program to illustrate
// std::string:crbegin()

#include <iostream>
#include <string>
using namespace std;

// Driver Code
int main()
{

    // Given string
    string str("GeeksForGeeks");

    // Traverse the given string using
    // reverse iterator crbegin()
    for (auto it = str.crbegin();
         it != str.crend(); it++) {

        // Print the elements
        cout << *it;
    }
    return 0;
}
```

**Output:**

```
skeeGroFskeeG

```

<u>**STD::string::crend()**T3】</u>

**std::string::crend()** 是一个字符串类内置函数，它返回一个常量反向迭代器，指向字符串中第一个元素之前的理论元素。这个迭代器用于在以相反的顺序遍历字符串时到达字符串的起点。

**模板类:**

```
template <class C>
auto crend( const C& c ) 
      -> decltype(std::rend(c));

```

**语法:**

```
string_name.crend()

```

**参数:**该功能不需要任何参数。

**返回值:**这个函数 **std::string::crend()** 返回一个常量反向迭代器，指向字符串中第一个元素之前的元素。

下面是说明**字符串的程序::crend()** :

**程序 2:**

```
// C++ program to illustrate
// std::string:crend()

#include <iostream>
#include <string>
using namespace std;

// Driver Code
int main()
{
    // Given string
    string str("GeeksForGeeks");

    // Find string length
    int N = str.length();

    // Given character
    char ch = 'k';

    // To check whether the char is
    // present or not
    bool a = true;

    // Traverse the given string using
    // reverse iterator crbegin() and
    // check if ch is present or not
    for (auto it = str.crbegin();
         it != str.crend(); it++) {

        if (*it == ch) {
            cout << "The last index is "
                 << N - (it - str.crbegin() + 1)
                 << endl;
            a = false;
            break;
        }
    }

    if (a) {
        cout << "Character is not present";
    }

    return 0;
}
```

**Output:**

```
The last index is 11

```