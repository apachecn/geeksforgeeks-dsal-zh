# 使用指针反转数组的程序

> 原文:[https://www . geesforgeks . org/program-reverse-array-use-pointers/](https://www.geeksforgeeks.org/program-reverse-array-using-pointers/)

**先决条件:**[C/c++](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)中的指针

给定一个数组，编写一个程序使用指针来反转它。

在这个程序中，我们使用*运算符。*(星号)运算符表示变量值。声明时的*运算符表示这是一个指针，否则它表示指针所指向的内存位置的值。

*   **反转功能:**用于通过指针反转数组
*   **交换功能:**用于交换两个内存内容
*   **打印功能:**将打印数组

**方法:**在反函数中，我们取两个指针，一个指向数组的开头，另一个指向数组的结尾。这两个指针指向的内存位置的内容被交换，然后第一个指针的值增加，第二个指针的值减少。

示例:

```
Input : array = 2, 4, -6, 5, 8, -1
Output : reverse_array = -1, 8, 5, -6, 4, 2

Input : array = 1, 4, -6, 8, -10, -12
Output : reverse_array = -12, -10, 8, -6, 4, 1

```

```
// CPP program to reverse array
// using pointers
#include <iostream>
using namespace std;

// Function to swap two memory contents
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to reverse the array through pointers
void reverse(int array[], int array_size)
{

    // pointer1 pointing at the beginning of the array
    int *pointer1 = array,

        // pointer2 pointing at end of the array
        *pointer2 = array + array_size - 1;
    while (pointer1 < pointer2) {
        swap(pointer1, pointer2);
        pointer1++;
        pointer2--;
    }
}

// Function to print the array
void print(int* array, int array_size)
{

    // Length pointing at end of the array
    int *length = array + array_size,

        // Position pointing to the beginning of the array
        *position = array;
    cout << "Array = ";
    for (position = array; position < length; position++)
        cout << *position << " ";
}

// Driver function
int main()
{

    // Array to hold the values
    int array[] = { 2, 4, -6, 5, 8, -1 };

    cout << "Original ";
    print(array, 6);

    cout << "Reverse ";
    reverse(array, 6);
    print(array, 6);
    return 0;
}
```

输出:

```
reverse array = -1  8  5  -6  4  2

```