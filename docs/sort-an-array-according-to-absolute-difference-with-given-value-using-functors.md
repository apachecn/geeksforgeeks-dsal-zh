# 使用函子

根据与给定值的绝对差对数组进行排序

> 原文:[https://www . geeksforgeeks . org/使用函子按给定值的绝对差对数组进行排序/](https://www.geeksforgeeks.org/sort-an-array-according-to-absolute-difference-with-given-value-using-functors/)

给定 n 个不同元素和一个数 x 的数组，根据与 x 的绝对差排列数组元素，即具有最小差的元素排在第一位，依此类推。
**注意:**如果两个或多个元素距离相等，则按照给定数组中的相同顺序排列它们。

**示例:**

> **输入:** x = 7，arr[] = {10，5，3，9，2}
> **输出:** arr[] = {5，9，10，3，2 }
> 7–10 = 3(ABS)
> 7–5 = 2
> 7–3 = 4
> 7–9 = 2(ABS)
> 7–2 = 5
> 所以根据与 x 的区别，
> 元素排列为 5，9，11
> 
> **输入:** x = 6，arr[] = {1，2，3，4，5}
> **输出:** arr[] = {5，4，3，2，1}
> 
> **输入:** x = 5，arr[] = {2，6，8，3}
> **输出:** arr[] = {6，3，2，8}

**处理方式:**
上面的问题已经在下面的帖子里解释过了:
[根据给定值的绝对差排序数组](https://www.geeksforgeeks.org/sort-an-array-according-to-absolute-difference-with-given-value/)
[根据给定值的绝对差排序数组【使用常量额外空间】](https://www.geeksforgeeks.org/sort-array-according-absolute-difference-given-value-using-constant-extra-space/)

上述解的时间复杂度分别为 O(n)的辅助空间的 O(nlogn)和 O(1)的辅助空间的 O(n^2。本文提出了一种利用 O(1)辅助空间的时间复杂度为 O(nlogn)的解决方案。

解决方案基于[函子](https://www.geeksforgeeks.org/functors-in-cpp/)。将给定数字 k 之差的绝对值与数组值 arr[i]进行比较，如果第一个对象的值小于第二个对象的值，则返回 true。使用[稳定 _ 排序](https://www.geeksforgeeks.org/stable_sort-c-stl/)保留等值顺序。

下面是上述方法的实现:

```
// C++ program to sort an array according
// absolute difference with x.
#include <bits/stdc++.h>
using namespace std;

// Functor class to perform comparison
class compare {
private:
    int num;

public:
    compare(int n)
    {
        num = n;
    }

    // Overloads () operator to perform
    // the desired comparison
    int operator()(int arr_num1, int arr_num2)
    {
        return abs(num - arr_num1) <
                          abs(num - arr_num2);
    }
};

// Function to sort an array according to
// absolute difference with x.
void rearrange(int arr[], int n, int k)
{
    // stable_sort sorts all the values in
    // non-decreasing order and preserves the
    // order of elements with equal values
    stable_sort(arr, arr + n, compare(k));
}

// Function to print the array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 10, 5, 3, 9, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 7;

    rearrange(arr, n, k);

    printArray(arr, n);

    return 0;
}
```

**Output:**

```
5 9 10 3 2

```

**时间复杂度:**O(n Log n)
T3】辅助空间: O(1)