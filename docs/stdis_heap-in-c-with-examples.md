# std::is_heap()在 C++中有示例

> 原文:[https://www . geesforgeks . org/stdis _ heap-in-c-with-examples/](https://www.geeksforgeeks.org/stdis_heap-in-c-with-examples/)

[C++标准模板库](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)中的 **std::is_heap()** 函数用于检查给定范围的元素是否形成[最大堆](https://www.geeksforgeeks.org/heap-data-structure/)。当给定的元素范围形成最大堆时，它返回真，否则返回假。

**头文件:**

```
#include <algorithm>

```

**语法:**

```
is_heap(first, last)

```

**参数:**它取两个参数，迭代器指向范围的第一个**和最后一个**元素。****

******返回值:**该函数返回以下值:****

*****   **True:** If the elements in the range **[the first and last]** form the largest heap.*   **False:** If the elements within the range of **[first, last]** do not form the largest heap.****

****下面是说明 **std::is_heap()** 的程序:****

******程序 1:******

```
**// C++ program to illustrate
// the std::is_heap()

#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

// Driver Code
int main()
{

    // Given list of numbers
    vector<int> arr = { 3, 1, 5, 1, 9, 8 };

    // Check if arr[] forms max-heap or not
    bool isHeap = is_heap(arr.begin(),
                          arr.end());

    if (isHeap) {
        cout << "Forms a Max Heap";
    }
    else {
        cout << "Doesn't forms a Max Heap";
    }
}**
```

******输出:**

```
Doesn't forms a Max Heap

```

**程序二:**

```
// C++ program to illustrate the std::is_heap()

#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

// Driver Code
int main()
{

    // Given list of numbers
    vector<int> arr = { 3, 1, 5, 1, 9, 8 };

    // Check if arr[] forms max-heap or not
    bool isHeap = is_heap(arr.begin(),
                          arr.end());

    // isHeap is false then make Max Heap
    // using in built function make_heap
    if (!isHeap) {
        make_heap(arr.begin(), arr.end());
    }

    // Else already a heap
    else {
        cout << "Already Max Heap\n";
    }

    // Print all the elements of arr
    // after make Max Heap
    for (auto& it : arr) {
        cout << it << ' ';
    }
    return 0;
}
```

**输出:**

```
9 3 8 1 1 5

```

**参考:**T2】http://www.cplusplus.com/reference/algorithm/is_heap/****