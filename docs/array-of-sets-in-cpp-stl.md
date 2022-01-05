# c++ STL 中的集合数组

> 原文:[https://www.geeksforgeeks.org/array-of-sets-in-cpp-stl/](https://www.geeksforgeeks.org/array-of-sets-in-cpp-stl/)

一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)是存储在[连续存储位置](https://www.geeksforgeeks.org/difference-between-contiguous-and-noncontiguous-memory-allocation/)的项目集合。它是将同一类型的多个项目存储在一起。这使得通过每个元素的位置来访问存储在其中的元素变得更加容易。

[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)是一种关联容器，其中每个元素必须是唯一的，因为元素的值标识了它。元素的值一旦添加到集合中就不能修改，尽管可以移除和添加该元素的修改值。

因此，**集合的数组**是具有固定行数的[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，其中每行是一组可变长度。数组的每个索引存储一个集合，可以使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)遍历和访问该集合。

**语法:**

> 设置 <data_type>S【尺寸】；</data_type>

**示例:**

> 集合< int > S[5]，其中 S 是大小为 5 的 int 集合的数组

**集合数组中的插入:**每个集合中元素的插入是使用 [insert()](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) 函数完成的。下面的示例演示了集合数组中的插入操作:

## C++

```
// C++ program to demonstrate the
// insertion in the array of sets
#include <bits/stdc++.h>
using namespace std;
#define ROW 4
#define COL 5

// Driver Code
int main()
{
    // Declaring array of sets
    set<int> s[ROW];

    // Elements to insert
    // in set
    int num = 10;

    // Inserting elements
    // into sets
    for (int i = 0; i < ROW; i++) {
        // Insert the column elements
        for (int j = 0; j < COL; j++) {
            s[i].insert(num);
            num += 5;
        }
    }

    // Display the array of sets
    for (int i = 0; i < ROW; i++) {
        cout << "Elements at index " << i << ": ";

        // Print the array of sets
        for (auto x : s[i])
            cout << x << " ";

        cout << endl;
    }

    return 0;
}
```

**Output:**

```
Elements at index 0: 10 15 20 25 30 
Elements at index 1: 35 40 45 50 55 
Elements at index 2: 60 65 70 75 80 
Elements at index 3: 85 90 95 100 105

```

**删除集合数组中的元素:**使用 [**erase()**](https://www.geeksforgeeks.org/seterase-c-stl/) 功能删除每个集合中的元素。下面是演示集合数组中删除操作的示例:

## C++

```
// C++ program to demonstrate the
// deletion in the array of sets
#include <bits/stdc++.h>
using namespace std;

// Defining the length of array
// and number of elements in
// each set
#define ROW 4
#define COL 5

// Driver Code
int main()
{
    // Declaring array of sets
    set<int> s[ROW];
    int num = 10;

    // Inserting elements in the set
    // at each index of array
    for (int i = 0; i < ROW; i++) {

        // insert the column elements
        for (int j = 0; j < COL; j++) {
            s[i].insert(num);
            num += 5;
        }
    }

    cout << "Before removal elements are:"
         << endl;

    // Display the array of sets
    for (int i = 0; i < ROW; i++) {
        cout << "Elements at index "
             << i << ": ";
        for (auto x : s[i])
            cout << x << " ";
        cout << endl;
    }

    // Erase 70 from 3rd set
    s[2].erase(70);

    // Erase 55 from 2nd set
    s[1].erase(55);

    // Display the array of sets
    // after removal of elements
    cout << endl
         << "After removal elements are:"
         << endl;

    for (int i = 0; i < ROW; i++) {
        cout << "Elements at index "
             << i << ": ";

        // Print the current set
        for (auto x : s[i])
            cout << x << " ";

        cout << endl;
    }

    return 0;
}
```

**Output:**

```
Before removal elements are:
Elements at index 0: 10 15 20 25 30 
Elements at index 1: 35 40 45 50 55 
Elements at index 2: 60 65 70 75 80 
Elements at index 3: 85 90 95 100 105 

After removal elements are:
Elements at index 0: 10 15 20 25 30 
Elements at index 1: 35 40 45 50 
Elements at index 2: 60 65 75 80 
Elements at index 3: 85 90 95 100 105

```

**集合数组中的遍历:**借助数组[索引]从集合数组中遍历每个集合，并且使用 [**迭代器**](https://www.geeksforgeeks.org/iterators-c-stl/) 执行集合中的遍历。下面是说明集合数组遍历的程序:

## C++

```
// C++ program to demonstrate the
// traversal in the array of sets
#include <bits/stdc++.h>
using namespace std;
#define ROW 2

// Driver Code
int main()
{
    // Declaring array of sets
    set<int> s[ROW];

    // Inserting elements into sets
    // Insert 10, 15, and 35 in 1st set
    s[0].insert(10);
    s[0].insert(15);
    s[0].insert(35);

    // Insert 20 and 30 in 2nd set
    s[1].insert(20);
    s[1].insert(30);

    // Traversing of sets s to print
    // elements stored in it
    for (int i = 0; i < ROW; i++) {
        cout << "Elements at index "
             << i << ": ";

        // Traversing and printing
        // element  at each column,
        // begin() is the starting
        // iterator, end() is the
        // ending iterator
        for (auto it = s[i].begin();
             it != s[i].end();
             it++) {

            // (*it) is used to get the
            // value at iterator is pointing
            cout << *it << ' ';
        }

        cout << endl;
    }

    return 0;
}
```

**Output:**

```
Elements at index 0: 10 15 35 
Elements at index 1: 20 30

```