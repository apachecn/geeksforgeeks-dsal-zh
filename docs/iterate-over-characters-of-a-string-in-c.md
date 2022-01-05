# 在 C++中迭代字符串的字符

> 原文:[https://www . geesforgeks . org/iterate-over-characters-of-a-string-in-c/](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并打印给定字符串的所有字符。

**示例:**

> **输入:**str = " geeks forgeeks "
> T3】输出: G e e k s f o r G e e k s
> 
> **输入:**str = " Coder "
> T3】输出: C o d e r

**天真方法:**解决这个问题最简单的方法是在**【0，N–1】**范围内迭代一个循环，其中 **N** 表示字符串的长度，使用变量 **i** 并打印 **str[i]** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to traverse the string and
// print the characters of the string
void TraverseString(string &str, int N)
{ 
    // Traverse the string
    for (int i = 0; i < N; i++) {

        // Print current character
        cout<< str[i]<< " ";
    }

}

// Driver Code
int main()
{
    string str = "GeeksforGeeks";

    // Stores length of the string
    int N = str.length();

    TraverseString(str, N);
}
```

**Output:**

```
G e e k s f o r G e e k s

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**[自动关键字](https://www.geeksforgeeks.org/type-inference-in-c-auto-and-decltype/)–基于方法:**可以使用[自动](https://www.geeksforgeeks.org/type-inference-in-c-auto-and-decltype/)迭代器遍历字符串。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to traverse the string and
// print the elements of the string
void TraverseString(string &str, int N)
{
    // Traverse the string
    for (auto &ch : str) {

        // Print current character
        cout<< ch<< " ";
    }
}
// Driver Code
int main()
{
    string str = "GeeksforGeeks";

    // Stores length of the string
    int N = str.length();

    TraverseString(str, N);
}
```

**Output:**

```
G e e k s f o r G e e k s

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**[迭代器](https://www.geeksforgeeks.org/introduction-iterators-c/)–基于方法:**可以使用[迭代器](https://www.geeksforgeeks.org/introduction-iterators-c/)遍历字符串。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to traverse the string and
// print the elements of the string
void TraverseString(string &str, int N)
{

    // Stores address of 
    // a character of str
    string:: iterator it;

    // Traverse the string
    for (it = str.begin(); it != str.end();
                                   it++) {
        // Print current character
        cout<< *it<< " ";
    }
}

// Driver Code
int main()
{
    string str = "GeeksforGeeks";

    // Stores length of the string
    int N = str.length();
    TraverseString(str, N);
}
```

**Output:**

```
G e e k s f o r G e e k s

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)