# c++中数组的排序向量

> 原文:[https://www . geesforgeks . org/sorting-向量数组 in-c/](https://www.geeksforgeeks.org/sorting-vector-of-arrays-in-c/)

给定一个数组向量，任务是对它们进行排序。

**示例:**

> **输入:** [[1，2，3]，[10，20，30]，[30，60，90]，[10，20，10]]
> **输出:** [[1，2，3]，[10，20，10]，[10，20，30]，[30，60，90]]
> 
> **输入:** [[7，2，9]，[5，20，11]，[6，16，19]]
> **输出:** [[5，20，11]，[6，16，19]，[7，2，9]]

**进场:**

要使用 C++中内置的 [**【排序】(**](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) )对**数组的**向量**进行排序，需要一个在增强库中定义的数组模板来存储数组的**向量。

> **STD::vector<STD::array>T1】**
> 
> 其中，std::array 是**封装**固定大小数组的**容器**。

在这个问题中，sort()函数接受两个参数，第一个参数(向量的开始位置)，第二个参数(向量的结束位置)来对数组向量(随机访问的项目)进行排序。下面是一个简单的程序来展示 sort()的工作原理。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to sort the vector
// of array by sort() function
// using STL in c++

#include <algorithm>
#include <array>
#include <iostream>
#include <vector>
using namespace std;

#define N 3

// Function to print vector of arrays
void print(vector<array<int, N> > vect)
{

    // Displaying the vector of arrays
    // ranged for loop is supported
    for (array<int, N> i : vect) {
        for (auto x : i)
            cout << x << " ";
        cout << endl;
    }
}

// Driver code
int main()
{
    // std::array is a container that
    // encapsulates fixed size arrays.
    vector<array<int, N> > vect;
    vect.push_back({ 1, 2, 3 });
    vect.push_back({ 10, 20, 30 });
    vect.push_back({ 30, 60, 90 });
    vect.push_back({ 10, 20, 10 });

    cout << "Vector of arrays"
         << " before sorting: \n";
    print(vect);

    // Sorting the vector using built-in sort()
    // defined in algorithm header in C++ STL
    sort(vect.begin(), vect.end());

    cout << "Vector of arrays"
         << " after sorting: \n";
    print(vect);

    // End of program
    return 0;
}
```

**Output:**

```
Vector of arrays before sorting: 
1 2 3 
10 20 30 
30 60 90 
10 20 10 

Vector of arrays after sorting: 
1 2 3 
10 20 10 
10 20 30 
30 60 90

```