# 对任何数据类型的变量进行排序的程序

> 原文:[https://www . geesforgeks . org/program-sorting-variables-data-type/](https://www.geeksforgeeks.org/program-sorting-variables-data-type/)

编写一个不使用 std::sort 对任何数据类型的变量进行排序的程序。

示例:

```
Input :  2000, 456, -10, 0
Output : -10   0   456   2000    

Input :  "We do nothing"
         "Hi I have something"
         "Hello Join something!"
         "(Why to do work)"
Output :(Why to do work)   
         Hello Join something!
         Hi I have something
         We do nothing   

```

上面的例子表明，我们可以将任何数据类型元素作为输入呈现，并且输出将是输入数据的排序形式。
这里解决这个问题的思路是制作一个[模板](https://www.geeksforgeeks.org/templates-cpp/)。

**方法 1(编写自己的排序)**在下面的代码中，我们实现了[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)对数组进行排序。

```
// CPP program to sort array of any data types.
#include <bits/stdc++.h>
using namespace std;

// Template formed so that sorting of any 
// type variable is possible
template <class T>
void sortArray(T a[], int n)
{   
    // boolean variable to check that 
    // whether it is sorted or not
    bool b = true;
    while (b) {
        b = false;
        for (size_t i=0; i<n-1; i++) {

            // swapping the variable
            // for sorting order
            if (a[i] > a[i + 1]) {
                T temp = a[i];
                a[i] = a[i + 1];
                a[i + 1] = temp;
                b = true;
            }
        }
    }
}

// Template formed so that sorting of any 
// type variable is possible
template <class T>
void printArray(T a[], int n)
{
    for (size_t i = 0; i < n; ++i) 
        cout << a[i] << "   ";    
    cout << endl;
}

// Driver code
int main()
{
    int n = 4;
    int intArr[n] = { 2000, 456, -10, 0 };
    sortArray(intArr, n);
    printArray(intArr, n);

    string strArr[n] = { "We do nothing",
                         "Hi I have something",
                         "Hello Join something!",
                        "(Why to do work)" };
    sortArray(strArr, n);
    printArray(strArr, n);

    float floatArr[n] = { 23.4, 11.4, -9.7, 11.17 };
    sortArray(floatArr, n);
    printArray(floatArr, n);

    return 0;
}
```

**Output:**

```
-10   0   456   2000   
(Why to do work)   Hello Join something!   Hi I have something   We do nothing   
-9.7   11.17   11.4   23.4

```

**方法 2(使用库函数)**
我们可以在 C++中使用 [std::sort](https://www.geeksforgeeks.org/sort-c-stl/) 对任意数据类型的数组进行排序。

```
// CPP program to sort array of any data types.
#include <bits/stdc++.h>
using namespace std;

// Template formed so that sorting of any 
// type variable is possible
template <class T>
void printArray(T a[], int n)
{
    for (size_t i = 0; i < n; ++i) 
        cout << a[i] << "   ";    
    cout << endl;
}

// Driver code
int main()
{
    int n = 4;
    int intArr[n] = { 2000, 456, -10, 0 };
    sort(intArr, intArr + n);
    printArray(intArr, n);

    string strArr[n] = { "We do nothing",
                         "Hi I have something",
                         "Hello Join something!",
                        "(Why to do work)" };
    sort(strArr, strArr + n);
    printArray(strArr, n);

    float floatArr[n] = { 23.4, 11.4, -9.7, 11.17 };
    sort(floatArr, floatArr+n);
    printArray(floatArr, n);

    return 0;
}
```

**Output:**

```
-10   0   456   2000   
(Why to do work)   Hello Join something!   Hi I have something   We do nothing   
-9.7   11.17   11.4   23.4

```