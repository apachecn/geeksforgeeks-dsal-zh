# c++ STL 中的向量集，示例

> 原文:[https://www . geeksforgeeks . org/c-STL-in-vectors-set-with-examples/](https://www.geeksforgeeks.org/set-of-vectors-in-c-stl-with-examples/)

**[集合在 STL 中](https://www.geeksforgeeks.org/set-in-cpp-stl/)** 集合是一种关联容器，其中每个元素必须是唯一的，因为元素的值标识了它。元素的值一旦添加到集合中就不能修改，尽管可以移除和添加该元素的修改值。

**[STL 中的向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)** 向量与动态数组相同，能够在插入或删除元素时自动调整自身大小，其存储由容器自动处理。向量元素被放在连续的存储中，这样就可以使用迭代器访问和遍历它们。

**STL 中的向量集:**向量集在设计复杂的数据结构时非常有效。

**语法:**

```
set<vector<datatype>> set_of_vector;

```

**例如**:考虑一个简单的问题，我们必须打印所有的唯一向量。

```
// C++ program to demonstrate
// use of set for vectors

#include <bits/stdc++.h>
using namespace std;

set<vector<int> > set_of_vectors;

// Print elements of Vector
void Print_Vector(vector<int> Vec)
{
    for (int i = 0; i < Vec.size(); i++) {
        cout << Vec[i] << " ";
    }
    cout << endl;
    return;
}

// Driver code
int main()
{
    // Initializing some vectors
    vector<int> data_1{ 10, 20, 30, 40 };
    vector<int> data_2{ 5, 10, 15 };
    vector<int> data_3{ 1, 3, 5, 7, 9, 11, 13 };
    vector<int> data_4{ 5, 10, 15 };
    vector<int> data_5{ 10, 20, 30, 40 };

    // Inserting vectors into set
    set_of_vectors.insert(data_1);
    set_of_vectors.insert(data_2);
    set_of_vectors.insert(data_3);
    set_of_vectors.insert(data_4);
    set_of_vectors.insert(data_5);

    // printing all the unique vectors in set
    cout << "Set of Vectors: \n";
    for (auto it = set_of_vectors.begin();
         it != set_of_vectors.end();
         it++) {

        Print_Vector(*it);
    }

    return 0;
}
```

**Output:**

```
Set of Vectors: 
1 3 5 7 9 11 13 
5 10 15 
10 20 30 40

```