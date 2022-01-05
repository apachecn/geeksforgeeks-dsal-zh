# c++中的数组和字符串

> 原文:[https://www.geeksforgeeks.org/arrays-and-strings-in-c/](https://www.geeksforgeeks.org/arrays-and-strings-in-c/)

**<u>阵列</u>**

[C](https://www.geeksforgeeks.org/c/) 或 [C++](https://www.geeksforgeeks.org/c-plus-plus/) 中的数组是存储在连续内存位置的项目集合，可以使用数组的索引随机访问元素。它们用于存储类似类型的元素，因为所有元素的数据类型必须相同。它们可以用来存储原始数据类型的集合，例如任何特定类型的 **int、float、double、char 等**。另外，C 或 C++中的数组可以存储派生的数据类型，如结构、指针等。
有两种类型的阵列:

*   一维数组
*   多维数组

**一维数组:**一维数组是相同数据类型的集合。一维数组声明为:

```
data_type variable_name[size]

data_type is the type of array, like int, float, char, etc.
variable_name is the name of the array.
size is the length of the array which is fixed.

```

**注意:**数组元素的位置取决于我们使用的数据类型。

下图为阵列示意图:
[![](img/71dffc4422d3df10ce0e40467820d96b.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200507091006/Arrays3.png)

下面是演示数组遍历的程序:

```
// C++ program to illustrate the traversal
// of the array
#include "iostream"
using namespace std;

// Function to illustrate traversal in arr[]
void traverseArray(int arr[], int N)
{

    // Iterate from [1, N-1] and print
    // the element at that index
    for (int i = 0; i < N; i++) {
        cout << arr[i] << ' ';
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    traverseArray(arr, N);
}
```

**Output:**

```
1 2 3 4

```

**多维数组:**多维数组也称为数组的数组。通常，我们使用二维数组。它也被称为矩阵。我们使用两个索引来遍历 2D 数组的行和列。声明如下:

```
data_type variable_name[N][M]

data_type is the type of array, like int, float, char, etc.
variable_name is the name of the array.
N is the number of rows.
M is the number of columns.

```

下面是演示 2D 数组遍历的程序:

```
// C++ program to illustrate the traversal
// of the 2D array
#include "iostream"
using namespace std;

const int N = 2;
const int M = 2;

// Function to illustrate traversal in arr[][]
void traverse2DArray(int arr[][M], int N)
{

    // Iterate from [1, N-1] and print
    // the element at that index
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            cout << arr[i][j] << ' ';
        }
        cout << endl;
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[][M] = { { 1, 2 }, { 3, 4 } };

    // Function call
    traverse2DArray(arr, N);

    return 0;
}
```

**Output:**

```
1 2 
3 4

```

**<u>琴弦</u>**

C++字符串类在内部使用字符数组来存储字符，但是所有的内存管理、分配和空终止都是由字符串类本身处理的，这就是它易于使用的原因。例如，它被声明为:

```
char str[] = "GeeksforGeeks"

```

下面是说明字符串遍历的程序:

```
// C++ program to illustrate the
// traversal of string
#include "iostream"
using namespace std;

// Function to illustrate traversal
// in string
void traverseString(char str[])
{
    int i = 0;

    // Iterate till we found '\0'
    while (str[i] != '\0') {
        printf("%c ", str[i]);
        i++;
    }
}

// Driver Code
int main()
{

    // Given string
    char str[] = "GeekforGeeks";

    // Function call
    traverseString(str);

    return 0;
}
```

**Output:**

```
G e e k f o r G e e k s

```

C++中的字符串数据类型提供了各种字符串操作功能。它们是:

1.  **strcpy()** :用于将字符从一个字符串复制到另一个字符串。
2.  **strcat()** :用于给定的两个字符串相加。
3.  **strlen()** :用于求给定字符串的长度。
4.  **strcmp()** :用于比较两个给定的字符串。

下面是说明上述功能的程序:

```
// C++ program to illustrate functions
// of string manipulation
#include "iostream"
#include "string.h"
using namespace std;

// Driver Code
int main()
{

    // Given two string
    char str1[100] = "GeekforGeeks";
    char str2[100] = "HelloGeek";

    // To get the length of the string
    // use strlen() function
    int x = strlen(str1);

    cout << "Length of string " << str1
         << " is " << x << endl;

    cout << endl;

    // To compare the two string str1
    // and str2 use strcmp() function
    int result = strcmp(str1, str2);

    // If result is 0 then str1 and str2
    // are equals
    if (result == 0) {
        cout << "String " << str1
             << " and String " << str2
             << " are equal." << endl;
    }
    else {

        cout << "String " << str1
             << " and String " << str2
             << " are not equal." << endl;
    }

    cout << endl;

    cout << "String str1 before: "
         << str1 << endl;

    // Use strcpy() to copy character
    // from one string to another
    strcpy(str1, str2);

    cout << "String str1 after: "
         << str1 << endl;

    cout << endl;

    return 0;
}
```

**Output:**

```
Length of string GeekforGeeks is 12

String GeekforGeeks and String HelloGeek are not equal.

String str1 before: GeekforGeeks
String str1 after: HelloGeek

```