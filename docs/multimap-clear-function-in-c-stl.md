# c++ STL 中的 multimap clear()函数

> 原文:[https://www . geesforgeks . org/multimap-clear-function-in-c-STL/](https://www.geeksforgeeks.org/multimap-clear-function-in-c-stl/)

multimap clear()函数是 C++ STL 中的一个内置函数，用于从 multimap 容器中移除所有元素(这些元素被销毁)，使容器的大小为 0。
**语法:**

```
mymultimap_name.clear()
```

**参数**:该函数不接受任何参数。
**返回值**:这个函数不返回任何东西。函数的返回类型是 void。它只是清空了整个容器。
下面的程序说明了 C++中的 multimap::clear()函数:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to illustrate the
// multimap::clear() function

#include <cstring>
#include <iostream>
#include <map>

using namespace std;

int main()
{
    // Creating multimap of string and int
    multimap<string, int> mymultimap;

    // Inserting 3 Items with their value
    // using insert function
    mymultimap.insert(pair<string, int>("Item1", 10));
    mymultimap.insert(pair<string, int>("Item2", 20));
    mymultimap.insert(pair<string, int>("Item3", 30));

    cout << "Size of the multimap before using "
         << "clear function : ";
    cout << mymultimap.size() << '\n';

    // Removing all the elements
    // present in the multimap
    mymultimap.clear();

    cout << "Size of the multimap after using"
         << " clear function : ";
    cout << mymultimap.size() << '\n';

    return 0;
}
```

**Output:** 

```
Size of the multimap before using clear function : 3
Size of the multimap after using clear function : 0
```

**时间复杂度:** O(N)，其中 N 是多 map 中元素的总数。