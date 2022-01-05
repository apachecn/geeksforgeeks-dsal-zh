# c++中的数组类

> 原文:[https://www.geeksforgeeks.org/array-class-c/](https://www.geeksforgeeks.org/array-class-c/)

从 C++11 引入数组类为 C 风格的数组提供了一个更好的选择。数组类相对于 C 风格数组的优势是:-

*   数组类知道自己的大小，而 C 风格的数组缺少这个属性。因此，当传递给函数时，我们不需要将数组的大小作为一个单独的参数传递。
*   使用 C 型数组时，[数组更有可能衰减成指针](https://www.geeksforgeeks.org/what-is-array-decay-in-c-how-can-it-be-prevented/)。数组类不会衰减成指针
*   数组类通常比 C 风格的数组更高效、轻量和可靠。

**阵前作战**:-
T4【1】。at() :-该函数用于访问数组的元素。
**2。get()** :-这个函数也用来访问数组的元素。此函数不是数组类的成员，而是类元组中的重载函数。
**3。运算符[]** :-这类似于 C 风格的数组。此方法也用于访问数组元素。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ code to demonstrate working of array,
// at() and get()
#include<iostream>
#include<array> // for array, at()
#include<tuple> // for get()
using namespace std;
int main()
{
    // Initializing the array elements
    array<int,6> ar = {1, 2, 3, 4, 5, 6};

    // Printing array elements using at()
    cout << "The array elements are (using at()) : ";
    for ( int i=0; i<6; i++)
    cout << ar.at(i) << " ";
    cout << endl;

    // Printing array elements using get()
    cout << "The array elements are (using get()) : ";
    cout << get<0>(ar) << " " << get<1>(ar) << " ";
    cout << get<2>(ar) << " " << get<3>(ar) << " ";
    cout << get<4>(ar) << " " << get<5>(ar) << " ";
    cout << endl;

    // Printing array elements using operator[]
    cout << "The array elements are (using operator[]) : ";
    for ( int i=0; i<6; i++)
    cout << ar[i] << " ";
    cout << endl;

    return 0;

}
```

输出:

```
The array elements are (using at()) : 1 2 3 4 5 6 
The array elements are (using get()) : 1 2 3 4 5 6 
The array elements are (using operator[]) : 1 2 3 4 5 6 
```

**4。front()** :-返回数组的第一个元素。
T4【5】。back() :-这将返回数组的最后一个元素。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ code to demonstrate working of
// front() and back()
#include<iostream>
#include<array> // for front() and back()
using namespace std;
int main()
{
    // Initializing the array elements
    array<int,6> ar = {1, 2, 3, 4, 5, 6};

    // Printing first element of array
    cout << "First element of array is : ";
    cout << ar.front() << endl;

    // Printing last element of array
    cout << "Last element of array is : ";
    cout << ar.back() << endl;

    return 0;

}
```

输出:

```
First element of array is : 1
Last element of array is : 6
```

**6。size()** :-返回数组中的元素个数。这是 C 风格数组所缺乏的属性。
**7。max_size()** :-返回数组可以容纳的最大元素数，即声明数组的大小。size()和 max_size()返回相同的值。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ code to demonstrate working of
// size() and max_size()
#include<iostream>
#include<array> // for size() and max_size()
using namespace std;
int main()
{
    // Initializing the array elements
    array<int,6> ar = {1, 2, 3, 4, 5, 6};

    // Printing number of array elements
    cout << "The number of array elements is : ";
    cout << ar.size() << endl;

    // Printing maximum elements array can hold
    cout << "Maximum elements array can hold is : ";
    cout << ar.max_size() << endl;

    return 0;

}
```

输出:

```
The number of array elements is : 6
Maximum elements array can hold is : 6
```

**8。swap()**:-swap()将一个数组的所有元素与另一个数组交换。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ code to demonstrate working of swap()
#include<iostream>
#include<array> // for swap() and array
using namespace std;
int main()
{

    // Initializing 1st array
    array<int,6> ar = {1, 2, 3, 4, 5, 6};

    // Initializing 2nd array
    array<int,6> ar1 = {7, 8, 9, 10, 11, 12};

    // Printing 1st and 2nd array before swapping
    cout << "The first array elements before swapping are : ";
    for (int i=0; i<6; i++)
    cout << ar[i] << " ";
    cout << endl;
    cout << "The second array elements before swapping are : ";
    for (int i=0; i<6; i++)
    cout << ar1[i] << " ";
    cout << endl;

    // Swapping ar1 values with ar
    ar.swap(ar1);

    // Printing 1st and 2nd array after swapping
    cout << "The first array elements after swapping are : ";
    for (int i=0; i<6; i++)
    cout << ar[i] << " ";
    cout << endl;
    cout << "The second array elements after swapping are : ";
    for (int i=0; i<6; i++)
    cout << ar1[i] << " ";
    cout << endl;

    return 0;

}
```

输出:

```
The first array elements before swapping are : 1 2 3 4 5 6 
The second array elements before swapping are : 7 8 9 10 11 12 
The first array elements after swapping are : 7 8 9 10 11 12 
The second array elements after swapping are : 1 2 3 4 5 6 
```

**9。empty()** :-当数组大小为零时，此函数返回 true，否则返回 false。
T4【10。fill() :-此函数用于用特定值填充整个数组。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ code to demonstrate working of empty()
// and fill()
#include<iostream>
#include<array> // for fill() and empty()
using namespace std;
int main()
{

    // Declaring 1st array
    array<int,6> ar;

    // Declaring 2nd array
    array<int,0> ar1;

    // Checking size of array if it is empty
    ar1.empty()? cout << "Array empty":
        cout << "Array not empty";
    cout << endl;

    // Filling array with 0
    ar.fill(0);

    // Displaying array after filling
    cout << "Array after filling operation is : ";
    for ( int i=0; i<6; i++)
        cout << ar[i] << " ";

    return 0;

}
```

输出:

```
Array empty
Array after filling operation is : 0 0 0 0 0 0 
```

本文由**曼吉特·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。