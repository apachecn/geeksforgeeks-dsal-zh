# 如何在 C++中存储非常多的超过 100 位的数字

> 原文:[https://www . geeksforgeeks . org/如何存储超过 100 位数的非常大量的 c/](https://www.geeksforgeeks.org/how-to-store-a-very-large-number-of-more-than-100-digits-in-c/)

给定一个由 100 多个数字组成的字符串形式的整数 **N** ，任务是存储用于执行算术运算的值并打印给定的整数。
**例:**

> **输入:**str = " 54326789013892014531903492543267890138920145319034925432678901389201 "
> **输出:**54326789013892014531903492543267901

**方法:**
在 [C++](https://www.geeksforgeeks.org/c-plus-plus/) 中不存在数据类型来存储 **10 <sup>100</sup>** 。所以，想法是使用 get 输入作为 [**字符串**](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) (因为字符串可以是任意长度的)，然后将这个字符串转换成长度与字符串长度相同的 [**数字数组**](https://www.geeksforgeeks.org/adding-one-to-number-represented-as-array-of-digits/) 。将大整数存储到整数数组中将有助于对该数字执行一些基本运算。
以下是步骤:

1.  [将大数字作为输入](https://www.geeksforgeeks.org/basic-input-output-c/)存储成字符串。
2.  创建一个长度与字符串大小相同的整数[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** 。
3.  逐个迭代字符串**串**所有字符(数字)，并将数字存储在数组的相应索引中 **arr**

> arr[I]= str[I]–“0”；
> //这里‘0’代表数字 0，
> //str[I]–‘0’= ASCII(str[I])–ASCII(‘0’)= ASCII(str[I]–48

2.  使用上面的步骤，我们可以存储非常非常大的数字来进行任何算术运算。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to return dynamic allocated
// array consisting integers individually
int* GetBigInteger(string str)
{
    int x = str.size(), a = 0;

    // Create an array to store the big
    // integer into it.

    // Make the array size same as the
    // size of string str
    int* arr = new int[str.size()];

    // Loop to extract string elements
    // into the array one by one
    while (a != x) {

        // Subtracting '0' to convert
        // each character into digit

        // str[a] - '0'
        // = ASCII(str[a]) - ASCII('0')
        // = ASCII(str[a] - 48
        arr[a] = str[a] - '0';
        a++;
    }

    // Return the reference of the array
    return arr;
}

// Driver Code
int main()
{
    // Big Integer in form of string str
    string str = "12345678098765431234567809876543";

    // Function Call
    int* arr = GetBigInteger(str);

    // Print the digits in the arr[]
    for (int i = 0; i < str.size(); i++) {
        cout << arr[i];
    }
    return 0;
}
```

**Output:** 

```
12345678098765431234567809876543
```

**时间复杂度:** *O(K)* ，K 是数字
中的位数**辅助空间:** *O(K)* ，K 是数字
中的位数