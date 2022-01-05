# 在 C++中实现 strtok()函数

> 原文:[https://www . geeksforgeeks . org/implementing-of-strtok-function-in-c/](https://www.geeksforgeeks.org/implementing-of-strtok-function-in-c/)

[strtok()函数](https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/)用于根据分隔符标记字符串。它存在于[头文件](https://www.geeksforgeeks.org/header-files-in-c-cpp-and-its-uses/)“**string . h”**中，并返回一个[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)到下一个令牌(如果存在)，如果下一个令牌不存在，则返回空值。为了获得所有的标记，我们的想法是在一个循环中调用这个函数。

**头文件:**

```
#include <string.h>
```

**语法:**

```
char *strtok(char *s1, const char *s2);
```

在本文中，我们将讨论这个函数的实现，其中必须考虑两件事:

*   维护字符串的状态，以确保我们已经提取了多少令牌。
*   其次，在数组中维护提取的令牌列表以返回它。

**步骤:**

*   创建一个函数 **strtok()** ，该函数接受字符串和分隔符作为参数并返回字符指针。
*   创建一个[静态变量](https://www.geeksforgeeks.org/static-variables-in-c/) **输入**来维持字符串的状态。
*   检查是否第一次提取代币，然后用其初始化**输入**。
*   如果**输入**为空，并且提取了所有令牌，则返回空。
*   在此步骤中，开始提取代币并将其存储在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **结果【】**中。
*   现在，迭代一个循环，直到出现**空值**或分隔符，然后通过包含 [**'\0'**](https://www.geeksforgeeks.org/difference-between-null-pointer-null-character-0-and-0-in-c-with-examples/) 返回结果。
*   当到达字符串的末尾时，如果需要，则手动添加一个 **'\0** ，并在末尾包含此角例。

下面是同样的实现:

## C++

```
// C++ program to demonstrate the function
// strtok() to tokenized the string
#include <bits/stdc++.h>
using namespace std;
char* mystrtok(char* s, char d)
{
    // Stores the state of string
    static char* input = NULL;

    // Initialize the input string
    if (s != NULL)
        input = s;

    // Case for final token
    if (input == NULL)
        return NULL;

    // Stores the extracted string
    char* result = new char[strlen(input) + 1];
    int i = 0;

    // Start extracting string and
    // store it in array
    for (; input[i] != '\0'; i++) {

        // If delimiter is not reached
        // then add the current character
        // to result[i]
        if (input[i] != d)
            result[i] = input[i];

        // Else store the string formed
        else {
            result[i] = '\0';
            input = input + i + 1;
            return result;
        }
    }

    // Case when loop ends
    result[i] = '\0';
    input = NULL;

    // Return the resultant pointer
    // to the string
    return result;
}

// Driver Code
int main()
{
    // Given string str
    char str[90] = "It, is my, day";

    // Tokenized the first string
    char* ptr = mystrtok(str, ' ');

    // Print current tokenized string
    cout << ptr << endl;

    // While ptr is not NULL
    while (ptr != NULL) {
        // Tokenize the string
        ptr = mystrtok(NULL, ' ');

        // Print the string
        cout << ptr << endl;
    }
    return 0;
}
```

**Output:** 

```
It,
is
my,
day
```