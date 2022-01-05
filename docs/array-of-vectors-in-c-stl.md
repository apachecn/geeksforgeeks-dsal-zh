# c++ STL 中的向量数组

> 原文:[https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/](https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/)

**先决条件:**[c++中的数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)[c++ STL 中的向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)

一个[](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**数组是存储在连续存储位置的项目的集合。它是将同一类型的多个项目存储在一起。这使得通过每个元素的位置来访问存储在其中的元素变得更加容易。**

**[](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**向量被称为[动态数组](https://www.geeksforgeeks.org/how-do-dynamic-arrays-work/)，能够在插入或删除元素时自动调整自身大小，其存储由容器自动处理。****

****因此，**[](https://www.geeksforgeeks.org/introduction-to-arrays/)[向量的数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**是固定行数的二维数组，其中每行是可变长度的向量。数组的每个索引存储一个向量，可以使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)遍历和访问该向量。****

******语法:******

```
**vector <data_type> V[size];** 
```

******示例:******

```
**vector <int> A[5];
where A is the array of vectors of int of size 5** 
```

****<u>**插入:**</u> 向量数组中的插入是使用 **[push_back()](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)** 函数完成的。****

******例如:******

```
**for i in [0, n) {
  A[i].push_back(35)
}** 
```

****上面的伪代码在**向量<int>A【n】**的每个索引处插入元素 35。****

****<u>**遍历:**</u> 使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)执行向量数组中遍历。****

******例如:******

```
**for i in [0, n) {
   for(iterator it = A[i].begin(); 
       it!=A[i].end(); it++) {
      print(*it)
    }
}** 
```

****以上伪代码使用起始迭代器 **A[i]在每个索引处遍历**向量< int > A[n]** 。begin()** 和 end 迭代器 **A[i]。end()** 。为了访问元素，它使用 **(*it)** 作为迭代器，迭代器是指向**向量<int>A【n】**中元素的指针。****

****下面是说明向量数组插入的程序。****

```
**// C++ program to illustrate
// array of vectors

#include <iostream>
#include <vector>
using namespace std;

// Declaring array of vectors
// globally
vector<int> v[5];

// Function for inserting elements
// in array of vectors
void insertionInArrayOfVectors()
{

    for (int i = 0; i < 5; i++) {

        // Inserting elements at every
        // row i using push_back()
        // function in vector
        for (int j = i + 1; j < 5; j++) {
            v[i].push_back(j);
        }
    }
}

// Function to print elements in array
// of vectors
void printElements()
{

    // Traversing of vectors v to print
    // elements stored in it
    for (int i = 0; i < 5; i++) {

        cout << "Elements at index "
             << i << ": ";

        // Displaying element at each column,
        // begin() is the starting iterator,
        // end() is the ending iterator
        for (auto it = v[i].begin();
             it != v[i].end(); it++) {

            // (*it) is used to get the
            // value at iterator is
            // pointing
            cout << *it << ' ';
        }
        cout << endl;
    }
}

// Function to illustrate array
// of vectors
void arrayOfVectors()
{
    // Inserting elements in array
    // of vectors
    insertionInArrayOfVectors();

    // Print elements stored in array
    // of vectors
    printElements();
}

// Driver code
int main()
{
    arrayOfVectors();
    return 0;
}**
```

******Output:**

```
Elements at index 0: 1 2 3 4 
Elements at index 1: 2 3 4 
Elements at index 2: 3 4 
Elements at index 3: 4 
Elements at index 4:

```****