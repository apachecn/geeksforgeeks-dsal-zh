# std::sort()在 C++ STL 中

> 哎哎哎:# t0]https://www . geeksforgeeks . org/sort-c-STL/

我们已经在 C 语言中讨论了[qsort()。c++ STL 提供了一个类似的函数排序，对向量或数组(具有随机访问的项)进行排序。](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/)

它通常需要两个参数，第一个参数是数组/向量需要开始排序的点，第二个参数是数组/向量需要排序的长度。第三个参数是可选的，可以在我们想要按字典顺序对元素进行排序的情况下使用。

默认情况下，sort()函数按升序对元素进行排序。

下面是一个简单的程序来展示 sort()的工作原理。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate default behaviour of
// sort() in STL.
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    /*Here we take two parameters, the beginning of the
    array and the length n upto which we want the array to
    be sorted*/
    sort(arr, arr + n);

    cout << "\nArray after sorting using "
            "default sort is : \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

**输出:**

```
Array after sorting using default sort is : 
0 1 2 3 4 5 6 7 8 9 
```

**如何降序排序？**
sort()采用第三个参数，用于指定元素的排序顺序。我们可以通过“greater()”函数进行降序排序。这个函数的比较方式是将更大的元素放在前面。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate descending order sort using
// greater<>().
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sort(arr, arr + n, greater<int>());

    cout << "Array after sorting : \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

**输出:**

```
Array after sorting : 
9 8 7 6 5 4 3 2 1 0 
```

**如何按照** **的特定顺序排序？**
我们也可以编写自己的比较器函数，作为第三个参数传递。这个“比较器”函数返回一个值；可转换为 bool，它基本上告诉我们传递的“第一个”参数是否应该放在传递的“第二个”参数之前。
例如:在下面的代码中，假设间隔{6，8}和{1，9}作为参数在“compareInterval”函数(比较器函数)中传递。现在作为 i1.first (=6) > i2.first (=1)，所以我们的函数返回“false”，这告诉我们“first”参数不应该放在“second”参数之前，因此排序将按照{1，9}优先，然后{6，8}作为下一个的顺序进行。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A C++ program to demonstrate
// STL sort() using
// our own comparator
#include <bits/stdc++.h>
using namespace std;

// An interval has a start
// time and end time
struct Interval {
    int start, end;
};

// Compares two intervals
// according to starting times.
bool compareInterval(Interval i1, Interval i2)
{
    return (i1.start < i2.start);
}

int main()
{
    Interval arr[]
        = { { 6, 8 }, { 1, 9 }, { 2, 4 }, { 4, 7 } };
    int n = sizeof(arr) / sizeof(arr[0]);

    // sort the intervals in increasing order of
    // start time
    sort(arr, arr + n, compareInterval);

    cout << "Intervals sorted by start time : \n";
    for (int i = 0; i < n; i++)
        cout << "[" << arr[i].start << "," << arr[i].end
             << "] ";

    return 0;
}
```

**输出:**

```
Intervals sorted by start time : 
[1,9] [2,4] [4,7] [6,8] 
```

std::sort()的时间复杂度为:
1。最佳情况–氧(氮对数氮)
2。平均病例–O(N 对数 N)
3。最差情况–0(对数 N)

空间复杂性–它可能使用 O(对数 N)个辅助空间。

？list = plqm 7 alhxfysgg 6 gsrme 2 ini 4k 8 fph 5 qvb

本文由 **Shubham Agrawal** 供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论