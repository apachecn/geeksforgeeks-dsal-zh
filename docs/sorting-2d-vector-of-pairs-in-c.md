# 在 C++中对 2D 向量进行排序

> 原文:[https://www . geesforgeks . org/sorting-2d-c 对向量/](https://www.geeksforgeeks.org/sorting-2d-vector-of-pairs-in-c/)

一个 [2D 向量](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)也被称为向量的向量，是一个向量，其中每个元素都是一个向量。换句话说，它是一个借助向量实现的矩阵。

**<u>什么是对的 2D 向量？</u>T3】**

一个[对的 2D 向量](https://www.geeksforgeeks.org/2d-vector-of-pairs-in-c-with-examples/)是一个向量，其中每个元素都是一个单独的[对的向量](https://www.geeksforgeeks.org/pair-in-cpp-stl/)。换句话说，它是一个借助成对向量实现的矩阵。

**示例:**下面是实现 2D 向量对的 C++程序。

## C++

```
// C++ program to demonstrate the
// working of vector of vectors
// of pairs
#include <bits/stdc++.h>
using namespace std;

// Function to print 2D vector elements
void print(vector<vector<pair<int, int> > >& myContainer)
{
    // Iterating over 2D vector elements
    for (auto currentVector : myContainer) 
    {
        // Each element of the 2D vector is
        // a vector itself
        vector<pair<int, int> > myVector = 
                                currentVector;

        // Iterating over the the vector
        // elements
        cout << "[  ";
        for (auto pr : myVector) 
         {
            // Print the element
            cout << "{";
            cout << pr.first << ", " << 
                    pr.second;
            cout << "}  ";
        }
        cout << "]\n";
    }
}

// Driver code
int main()
{
    // Declaring a 2D vector of pairs
    // Pairs are of type {char, bool}
    vector<vector<pair<int, int> > > myContainer;

    // Initializing vectors of pairs
    vector<pair<int, int> > vect1 = 
    {{1, 2}, {3, 4}, {5, 6}, {7, 8}};
    vector<pair<int, int> > vect2 = 
    {{9, 10}, {11, 12}, {13, 14}, {15, 16}};
    vector<pair<int, int> > vect3 = 
    {{17, 18}, {19, 20}, {21, 22}, {23, 24}};
    vector<pair<int, int> > vect4 = 
    {{25, 26}, {27, 28}, {29, 30}, {31, 32}};

    // Inserting vectors in the 2D vector
    myContainer.push_back(vect1);
    myContainer.push_back(vect2);
    myContainer.push_back(vect3);
    myContainer.push_back(vect4);

    print(myContainer);

    return 0;
}
```

**Output**

> [ {1，2} {3，4} {5，6} {7，8} ]
> [ {9，10} {11，12} {13，14} {15，16} ]
> [ {17，18} {19，20} {21，22} {23，24} ]
> [ {25，26} {27，28} {29，30} {31，32} ]

本文重点讨论用于对 2D 向量对进行排序的不同技术。

**情况 1:对 2D 向量的特定行进行排序:**

*   **基于对的第一个值:**这种类型的排序按照对的第一个值的升序排列 2D 向量的选定行。这是通过使用“sort()”并传递 1D 向量的迭代器作为参数来实现的。

**示例:**

> **输入:**
> (4，1) (1，9) (7，2)
> (3，2) (4，5) (8，1)
> (1，6) (3，2) (1，4)
> 
> **输出:**
> (1，9) (4，1) (7，2)
> (3，2) (4，5) (8，1)
> (1，6) (3，2) (1，4)

下面是上述方法的实现:

## C++

```
// C++ program to demonstrate the
// working of sorting vector of vectors
// of pairs
#include <bits/stdc++.h>
using namespace std;

// Function to print 2D vector elements
void print(vector<vector<pair<int, int> > >
           & myContainer)
{
    // Iterating over 2D vector elements
    for (auto currentVector : myContainer) 
    {
        // Each element of the 2D vector is
        // a vector itself
        vector<pair<int, int> > myVector = 
                                currentVector;

        // Iterating over the the vector
        // elements
        cout << "[  ";
        for (auto pr : myVector) 
        {
            // Print the element
            cout << "{";
            cout << pr.first << ", " << 
                    pr.second;
            cout << "}  ";
        }
        cout << "]\n";
    }
}

// Driver code
int main()
{
    // Declaring a 2D vector of pairs
    // Pairs are of type {char, bool}
    vector<vector<pair<int, int> > > myContainer;

    // Initializing vectors of pairs
    vector<pair<int, int> > vect1 = 
    {{2, 1}, {1, 9}, {4, 3}, {8, 1}};
    vector<pair<int, int> > vect2 = 
    {{19, 10}, {11, 2}, {12, 14}, {14, 6}};
    vector<pair<int, int> > vect3 = 
    {{17, 18}, {19, 20}, {21, 22}, {23, 24}};
    vector<pair<int, int> > vect4 = 
    {{25, 26}, {27, 28}, {29, 30}, {31, 32}};

    // Inserting vectors in the 2D vector
    myContainer.push_back(vect1);
    myContainer.push_back(vect2);
    myContainer.push_back(vect3);
    myContainer.push_back(vect4);

    // Print the vector elements 
    // before sorting
    cout << "Before sorting, ";
    print(myContainer);

    // Sorting the first row of 2D vector 
    // of pairs on the basis of first 
    // element of pairs
    sort(myContainer[0].begin(), 
         myContainer[0].end());

    cout << "\n\n After sorting the first row " << 
            "on the basis of first element of pairs, ";
    print(myContainer);

    return 0;
}
```

**Output**

> 排序前，我的容器元素:
> 
> [ {2，1} {1，9} {4，3} {8，1} ]
> [ {19，10} {11，2} {12，14} {14，6} ]
> [ {17，18} {19，20} {21，22} {23，24} ]
> [ {25，26} {27，28} {29，30} {31，32} ]
> 
> 根据第一对元素对对第一行进行排序后，myContainer 元素:
> 
> [ {1，9} {2，1} {4，3} {8，1} ]
> [ {19，10} {11，2} {12，14} {14，6} ]
> [ {17，18} {19，20} {21，22} {23，24} ]
> [ {25，26} {27，28} {29，30} {31，32} ]

*   **基于对的第二个值:**这种类型的排序按照对的第二个值的升序排列 2D 向量的选定行。这是通过使用“sort()”并传递 1D 向量的迭代器作为参数来实现的。在这种情况下，需要传递一个自定义比较器作为第三个参数，实现基于第二个值对进行排序的逻辑。

**示例:**

> **输入:**
> (4，1) (1，9) (7，2)
> (3，2) (4，5) (8，1)
> (1，6) (3，2) (1，4)
> 
> **输出:**
> (4，1) (7，2) (1，9)
> (3，2) (4，5) (8，1)
> (1，6) (3，2) (1，4)

下面是上述方法的实现:

## C++

```
// C++ program to demonstrate the
// working of sorting vector of vectors
// of pairs
#include <bits/stdc++.h>
using namespace std;

// Custom comparator function
bool myComparator(pair<int, int>& pair1, 
                  pair<int, int>& pair2)
{
    return pair1.second < pair2.second;
}

// Function to print 2D vector elements
void print(vector<vector<pair<int, int> > >
           & myContainer)
{
    // Iterating over 2D vector elements
    for (auto currentVector : myContainer) 
    {
        // Each element of the 2D vector is
        // a vector itself
        vector<pair<int, int> > myVector = 
                                currentVector;

        // Iterating over the the vector
        // elements
        cout << "[  ";
        for (auto pr : myVector) 
        {
            // Print the element
            cout << "{";
            cout << pr.first << ", " << 
                    pr.second;
            cout << "}  ";
        }
        cout << "]\n";
    }
}

// Driver code
int main()
{
    // Declaring a 2D vector of pairs
    // Pairs are of type {char, bool}
    vector<vector<pair<int, int> > > myContainer;

    // Initializing vectors of pairs
    vector<pair<int, int> > vect1 = 
    {{2, 1}, {1, 9}, {4, 3}, {8, 1}};
    vector<pair<int, int> > vect2 = 
    {{19, 10}, {11, 2}, {12, 14}, {14, 6}};
    vector<pair<int, int> > vect3 = 
    {{17, 18}, {19, 20}, {21, 22}, {23, 24}};
    vector<pair<int, int> > vect4 = 
    {{25, 26}, {27, 28}, {29, 30}, {31, 32}};

    // Inserting vectors in the 2D vector
    myContainer.push_back(vect1);
    myContainer.push_back(vect2);
    myContainer.push_back(vect3);
    myContainer.push_back(vect4);

    // Print the vector elements before sorting
    cout << "Before sorting, ";
    print(myContainer);

    // Sorting first row of 2D vector of pairs
    // on the basis of second element of pairs
    // By passing a custom comparator as a 
    // third argument
    sort(myContainer[0].begin(), 
         myContainer[0].end(), myComparator);

    cout << "\n\n After sorting the first row on " << 
            "the basis of second element of pairs, ";
    print(myContainer);

    return 0;
}
```

**Output**

> 排序前，我的容器元素:
> 
> [ {2，1} {1，9} {4，3} {8，1} ]
> [ {19，10} {11，2} {12，14} {14，6} ]
> [ {17，18} {19，20} {21，22} {23，24} ]
> [ {25，26} {27，28} {29，30} {31，32} ]
> 
> 根据第二对元素对对第一行进行排序后，myContainer 元素:
> 
> [ {2，1} {8，1} {4，3} {1，9} ]
> [ {19，10} {11，2} {12，14} {14，6} ]
> [ {17，18} {19，20} {21，22} {23，24} ]
> [ {25，26} {27，28} {29，30} {31，32} ]