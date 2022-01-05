# 快速排序算法在 C 语言中的通用实现

> 原文:[https://www . geeksforgeeks . org/generic-implementation-of-quick sort-algorithm-in-c/](https://www.geeksforgeeks.org/generic-implementation-of-quicksort-algorithm-in-c/)

编写一个函数来实现[快速排序](https://www.geeksforgeeks.org/quick-sort/)算法，该算法将适用于所有类型的数据，即整型、浮点型、字符型等。
它应该接受所有类型的数据，并将排序后的数据显示为输出。

注意:这个函数类似于 C 标准库函数 qsort()。

示例:

```
First Input as a string.
Input :abc cad bcd xyz bsd 
Output :abc bcd bsd cad xyz

Second input as integer
Input :5 6 4 2 3
Output :2 3 4 5 6

```

我们用 void*在 c 语言中实现通用快速排序函数，void*不知道它在内存空间中要占用多少字节的内存。在对其执行任何操作之前，必须将其转换为任何其他数据类型，如 int*、char*。
例:当我们声明 int var 时；编译器知道它已经占用了 4 字节的内存，但是 void 不知道它必须占用多少字节的内存。
我们还将使用指向函数的指针，该指针将指向依赖于不同类型数据的函数，即该函数将由用户根据需要定义。

下面是将 void*转换为任何特定数据类型之前和之后内存中 void *的图像表示，以便更好地理解。

内存中的空*点:

[![](img/ba61763943bec2010f9a86cb127c3ceb.png "Representation of void* in Memory without casting")](https://media.geeksforgeeks.org/wp-content/uploads/Generic_quickSort_in_C.png)

void* pt 铸造成 char*:

[![](img/32be744b23f4801675b08fcf40c6bf69.png "Representation of void* in Memory after casting")](https://media.geeksforgeeks.org/wp-content/uploads/Generic_quickSort-_in_C_2.png)

```
// C Program to illustrate Generic Quicksort Function
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// function for comparing two strings. This function
// is passed as a parameter to _quickSort() when we
// want to sort 
int cmpstr(void* v1, void* v2)
{
    // casting v1 to char** and then assigning it to
    // pointer to v1 as v1 is array of characters i.e
    // strings.
    char *a1 = *(char**)v1;
    char *a2 = *(char**)v2;
    return strcmp(a1, a2);
}

// function for comparing two strings
int cmpnum(void* s1, void* s2)
{
    // casting s1 to int* so it can be
    // copied in variable a.
    int *a = (int*)s1;
    int *b = (int*)s2;
    if ((*a) > (*b))
        return 1;
    else if ((*a) < (*b))
        return -1;
    else
        return 0;
}

/* you can also write compare function for floats,
    chars, double similarly as integer. */
// function for swap two elements
void swap(void* v1, void* v2, int size)
{
    // buffer is array of characters which will 
    // store element byte by byte
    char buffer[size];

    // memcpy will copy the contents from starting
    // address of v1 to length of size in buffer 
    // byte by byte.
    memcpy(buffer, v1, size);
    memcpy(v1, v2, size);
    memcpy(v2, buffer, size);
}

// v is an array of elements to sort.
// size is the number of elements in array
// left and right is start and end of array
//(*comp)(void*, void*) is a pointer to a function
// which accepts two void* as its parameter
void _qsort(void* v, int size, int left, int right,
                      int (*comp)(void*, void*))
{
    void *vt, *v3;
    int i, last, mid = (left + right) / 2;
    if (left >= right)
        return;

    // casting void* to char* so that operations 
    // can be done.
    void* vl = (char*)(v + (left * size));
    void* vr = (char*)(v + (mid * size));
    swap(vl, vr, size);
    last = left;
    for (i = left + 1; i <= right; i++) {

        // vl and vt will have the starting address 
        // of the elements which will be passed to 
        // comp function.
        vt = (char*)(v + (i * size));
        if ((*comp)(vl, vt) > 0) {
            ++last;
            v3 = (char*)(v + (last * size));
            swap(vt, v3, size);
        }
    }
    v3 = (char*)(v + (last * size));
    swap(vl, v3, size);
    _qsort(v, size, left, last - 1, comp);
    _qsort(v, size, last + 1, right, comp);
}

int main()
{
    // Your C Code
    char* a[] = {"bbc", "xcd", "ede", "def",
            "afg", "hello", "hmmm", "okay", "how" };

    int b[] = { 45, 78, 89, 65, 70, 23, 44 };
    int* p = b;
    _qsort(a, sizeof(char*), 0, 8, (int (*)(void*, void*))(cmpstr));
    _qsort(p, sizeof(int), 0, 6, (int (*)(void*, void*))(cmpnum));

    for (int i = 0; i < 9; i++)
        printf("%s ", a[i]);
    printf("\n");

    for (int i = 0; i < 7; i++)
        printf("%d ", b[i]);
    return 0;
}
```

**Output:**

```
afg bbc def ede hello hmmm how okay xcd 
23 44 45 65 70 78 89

```