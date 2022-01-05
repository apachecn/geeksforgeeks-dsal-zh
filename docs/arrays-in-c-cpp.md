# C/c++

中的数组

> 原文:[https://www.geeksforgeeks.org/arrays-in-c-cpp/](https://www.geeksforgeeks.org/arrays-in-c-cpp/)

C/C++或任何编程语言中的数组都是存储在连续内存位置的相似数据项的集合，可以使用数组的索引随机访问元素。它们可以用来存储原始数据类型的集合，例如任何特定类型的 int、float、double、char 等。此外，C/C++中的数组可以存储派生的数据类型，如结构、指针等。下面给出了一个数组的图片表示。

![arrays](img/13b7429b646a58c1b6e67867ce0dab9c.png)

**为什么我们需要数组？**
我们可以用正态变量(v1，v2，v3，..)当我们有少量对象时，但是如果我们想要存储大量实例，那么用普通变量来管理它们就变得很困难。数组的思想是在一个变量中表示多个实例。
**C/c++中的数组声明:**

![](img/cd4c57042859fbd9af9970d0143f1c14.png)

**注:**上图中 int a[3]= {[0…1]= 3 }；自从 GCC 2.5 以来，这种声明已经过时了

有多种方法可以声明数组。可以通过指定它的类型和大小、初始化它或两者都初始化来完成。

**通过指定大小进行数组声明**

## C

```
// Array declaration by specifying size
int arr1[10];

// With recent C/C++ versions, we can also
// declare an array of user specified size
int n = 10;
int arr2[n];
```

**通过初始化元素进行数组声明**

## C

```
// Array declaration by initializing elements
int arr[] = { 10, 20, 30, 40 }

// Compiler creates an array of size 4.
// above is same as  "int arr[4] = {10, 20, 30, 40}"
```

**通过指定大小和初始化元素进行数组声明**

## C

```
// Array declaration by specifying size and initializing
// elements
int arr[6] = { 10, 20, 30, 40 }

// Compiler creates an array of size 6, initializes first
// 4 elements as specified by user and rest two elements as
// 0\. above is same as  "int arr[] = {10, 20, 30, 40, 0, 0}"
```

**C/c++中数组的优势:**

1.  使用数组索引随机访问元素。
2.  使用较少的代码行，因为它创建了多个元素的单个数组。
3.  轻松接触所有元素。
4.  使用单个循环遍历数组变得很容易。
5.  排序变得很容易，因为它可以通过编写更少的代码来完成。

**C/c++中数组的缺点:**

1.  允许输入固定数量的元素，这在声明时决定。与链表不同，C 语言中的数组不是动态的。
2.  元素的插入和删除可能是昂贵的，因为元素需要根据新的内存分配来管理。

**C/c++中关于数组的事实:**

*   **访问数组元素:**
    使用整数索引访问数组元素。数组索引从 0 开始，直到数组大小减 1。
*   数组的名称也是指向数组第一个元素的指针。

![](img/f638bc6d869bd54a01af33849b8a4661.png)

**示例:**

## C

```
#include <stdio.h>

int main()
{
    int arr[5];
    arr[0] = 5;
    arr[2] = -10;
    arr[3 / 2] = 2; // this is same as arr[1] = 2
    arr[3] = arr[0];

    printf("%d %d %d %d", arr[0], 
           arr[1], arr[2], arr[3]);

    return 0;
}
```

## C++

```
#include <iostream>
using namespace std;

int main()
{
    int arr[5];
    arr[0] = 5;
    arr[2] = -10;

    // this is same as arr[1] = 2
    arr[3 / 2] = 2;
    arr[3] = arr[0];

    cout << arr[0] << " " << arr[1] << " " << arr[2] << " "
         << arr[3];

    return 0;
}
```

**输出**

```
5 2 -10 5
```

**没有索引越界检查:**
在 C/C++中没有索引越界检查，例如，下面的程序编译良好，但运行时可能会产生意外的输出。

## C

```
// This C program compiles fine
// as index out of bound
// is not checked in C.

#include <stdio.h>

int main()
{
    int arr[2];

    printf("%d ", arr[3]);
    printf("%d ", arr[-2]);

    return 0;
}
```

## C++

```
// This C++ program compiles fine
// as index out of bound
// is not checked in C.

#include <iostream>
using namespace std;

int main()
{
    int arr[2];

    cout << arr[3] << " ";
    cout << arr[-2] << " ";

    return 0;
}
```

**Output**

```
-449684907 4195777 
```

在 C 语言中，用超过指定大小的元素初始化数组并不是编译器错误。例如，下面的程序编译良好，只显示警告。

## C

```
#include <stdio.h>
int main()
{

    // Array declaration by initializing it 
    // with more elements than specified size.
    int arr[2] = { 10, 20, 30, 40, 50 };

    return 0;
}
```

**警告:**

```
prog.c: In function 'main':
prog.c:7:25: warning: excess elements in array initializer
  int arr[2] = { 10, 20, 30, 40, 50 };
                         ^
prog.c:7:25: note: (near initialization for 'arr')
prog.c:7:29: warning: excess elements in array initializer
  int arr[2] = { 10, 20, 30, 40, 50 };
                             ^
prog.c:7:29: note: (near initialization for 'arr')
prog.c:7:33: warning: excess elements in array initializer
  int arr[2] = { 10, 20, 30, 40, 50 };
                                 ^
prog.c:7:33: note: (near initialization for 'arr')
```

*   **注意:**程序不会用 C++编译。如果我们将上述程序保存为. cpp，程序会生成编译器错误*“错误:int[2]”*的初始值设定项太多。

**元素存储在连续的存储位置**
**示例:**

## C

```
// C program to demonstrate that
// array elements are stored
// contiguous locations

#include <stdio.h>
int main()
{
    // an array of 10 integers.  
    // If arr[0] is stored at
    // address x, then arr[1] is
    // stored at x + sizeof(int)
    // arr[2] is stored at x + 
    // sizeof(int) + sizeof(int)
    // and so on.
    int arr[5], i;

    printf("Size of integer in this compiler is %lu\n",
           sizeof(int));

    for (i = 0; i < 5; i++)
        // The use of '&' before a variable name, yields
        // address of variable.
        printf("Address arr[%d] is %p\n", i, &arr[i]);

    return 0;
}
```

## C++

```
// C++ program to demonstrate that array elements
// are stored contiguous locations

#include <iostream>
using namespace std;

int main()
{
    // an array of 10 integers.  
    // If arr[0] is stored at
    // address x, then arr[1] is 
    // stored at x + sizeof(int)
    // arr[2] is stored at x + 
    // sizeof(int) + sizeof(int)
    // and so on.
    int arr[5], i;

    cout << "Size of integer in this compiler is "
         << sizeof(int) << "\n";

    for (i = 0; i < 5; i++)
        // The use of '&' before a variable name, yields
        // address of variable.
        cout << "Address arr[" << i << "] is " << &arr[i]
             << "\n";

    return 0;
}
```

**Output**

```
Size of integer in this compiler is 4
Address arr[0] is 0x7ffe75c32210
Address arr[1] is 0x7ffe75c32214
Address arr[2] is 0x7ffe75c32218
Address arr[3] is 0x7ffe75c3221c
Address arr[4] is 0x7ffe75c32220
```

遍历数组的另一种方法

## C++

```
#include<bits/stdc++.h>
using namespace std;

int main()
{
    int arr[6]={11,12,13,14,15,16};
    // Way -1
    for(int i=0;i<6;i++)
        cout<<arr[i]<<" ";

  cout<<endl;
      // Way 2
    cout<<"By Other Method:"<<endl;
    for(int i=0;i<6;i++)   
        cout<<i[arr]<<" ";

    cout<<endl;

    return 0;
}

// Contributed by Akshay Pawar ( Username - akshaypawar4)
```

**Output**

```
11 12 13 14 15 16 
By Other Method:
11 12 13 14 15 16 
```

**数组 vs 指针**
数组和指针是两回事(我们可以通过应用 sizeof 来检查)。之所以会出现这种混乱，是因为数组名称指示第一个元素的地址，数组总是作为指针传递(即使我们使用方括号)。请看[C 中指针和数组的区别？](https://www.geeksforgeeks.org/difference-pointer-array-c/)了解更多详情。
**什么是 C++中的 vector？**
c++中的向量是 STL 中表示数组的类。向量相对于普通数组的优点是，

*   当我们声明一个向量时，我们不需要传递大小作为额外的参数，即向量支持动态大小(我们不需要一开始就指定向量的大小)。我们也可以调整向量的大小。
*   向量有许多内置的功能，比如，移除一个元素等。

想要了解更多关于 vector 提供的功能，请参考 C++中的[vector](https://www.geeksforgeeks.org/vector-in-cpp-stl/)了解更多细节。

**Related Articles**: Please write comments if you find anything incorrect, or you want to share more information about the topic discussed above.