# std::string::find_last_of 在 C++中带有示例

> 原文:[https://www . geesforgeks . org/stdstringfind _ last _ in-c-with-examples/](https://www.geeksforgeeks.org/stdstringfind_last_of-in-c-with-examples/)

**STD::string::find _ last _ of**是一个字符串类成员函数，用于查找字符串中任何字符最后一次出现的索引。如果字符串中存在该字符，则返回该字符在字符串中最后一次出现的索引，否则返回**字符串::npos** 。
**头文件:**

```
#include < string >
```

模板类

```
template < class T >
size_type
    find_last_of(const T& t, 
                 size_type pos = npos ) const noexcept();
```

**语法 1:**

```
find_last_of(char ch)
```

**参数:**该函数取一个给定的字符，并返回该字符最后一次出现的位置。
下面是说明**字符串的程序::find_last_of()** :

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate string::find_last_of
#include <cstddef>
#include <iostream>
#include <string>
using namespace std;

// Driver Code
int main()
{

    // Given String
    string str("Welcome to GeeksforGeeks!");

    // Character to be found
    char ch = 'e';

    // To store the index of last
    // character found
    size_t found;

    // Function to find the last
    // character ch in str
    found = str.find_last_of(ch);

    // If string doesn't have
    // character ch present in it
    if (found == string::npos) {
        cout << "Character " << ch
             << " is not present in"
             << " the given string.";
    }

    // Else print the last position
    // of the character
    else {
        cout << "Character " << ch
             << " is found at index: "
             << found << endl;
    }
}
```

**Output:** 

```
Character e is found at index: 21
```

**语法 2:**

```
find_last_of(char ch, size_t position)
```

**参数:**该函数获取给定的字符和索引，直到要执行搜索的位置。它返回该字符最后一次出现的位置。
下面是说明**字符串的程序::find_last_of()** :

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate string::find_last_of
#include <cstddef>
#include <iostream>
#include <string>
using namespace std;

// Driver Code
int main()
{

    // Given String
    string str("Welcome to GeeksforGeeks!");

    // Character to be found
    char ch = 'e';

    // To store the index of last
    // character found
    size_t found;

    // Position till search is performed
    int pos = 10;

    // Function to find the last
    // character ch in str[0, pos]
    found = str.find_last_of(ch, pos);

    // If string doesn't have
    // character ch present in it
    if (found == string::npos) {
        cout << "Character " << ch
             << " is not present in"
             << " the given string.";
    }

    // Else print the last position
    // of the character
    else {
        cout << "Character " << ch
             << " is found at index: "
             << found << endl;
    }
}
```

**Output:** 

```
Character e is found at index: 6
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。
**辅助空间:** O(1)。

**参考文献:**T2【http://www . cplusplus . com/reference/string/find _ last _ of/T4】