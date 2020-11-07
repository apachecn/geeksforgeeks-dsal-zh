# 不使用指针在 C++ STL 中实现单独链接的程序

> 原文：[https://www.geeksforgeeks.org/program-to-implement-separate-chaining-in-c-stl-without-the-use-of-pointers/](https://www.geeksforgeeks.org/program-to-implement-separate-chaining-in-c-stl-without-the-use-of-pointers/)

**先决条件**：[独立链接](https://www.geeksforgeeks.org/hashing-set-2-separate-chaining/)和 [STL in C++](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)

本文借助 C++ 中的 STL 实现了哈希中的单独链接，而无需使用[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)。

**方法**：制作矢量的数组，以获得每个哈希索引的动态（可调整大小）数组，而不是[，使用链接列表执行相同的](https://www.geeksforgeeks.org/c-program-hashing-chaining/)。 现在，无需使用链表就可以更轻松地处理数据集。 这个简单的技巧更容易实现，效率更高。 在这种方法中：

1.  哈希的大小由类的构造函数初始化。

2.  The elements are inserted in the Hash according to the expression:

    ```
    Vector[i % n].push_back(i);
    where:
        Vector = the array of vectors used for hash
        i = current element to be hashed
        n = size of the hash

    ```

    [![](img/9bf222b917ac1f2a6903a3706d83f577.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200227131935/Separate-Chaining-without-pointers.png)

    使用 STL 的单独链接

    **算法**：该方法的算法如下：

    1.  初始化向量的大小（例如`n`）。

    2.  添加元素时，请执行以下步骤：

        1.  获得`x = [value] MOD n`的值。

        2.  在`v[x]`中推回该元素的值。

    3.  对于删除，我们按照以下步骤操作：

        1.  获得`x = [value] MOD n`的值。

        2.  扫描要在`v[x]`中删除的元素。

        3.  如果找到，请使用[`delete()`](https://www.geeksforgeeks.org/vector-erase-and-clear-in-cpp/)方法删除该元素。

        4.  如果找不到要删除的元素，则打印`No Element Found!`。

    4.  打印哈希。

    **实现**

    ```
    // C++ Program to implement Separate
    // Chaining in C++ STL without
    // the use of pointers
    #include <bits/stdc++.h>
    using namespace std;
    // Container for our data-set
    class SeperateHash {
    HTG263]
    // Data members are kept private
    // since they are accessed using methods
    private :
    int n;
    vector<vector< int > > v;
    // Methods are kept public
    public : ]
    // Initialising constructors as the
    // minimum required memory will be
    // allocated after which compiler
    // will not report flag error
    SeperateHash( int n)
    {
    // Constructor to initialize
    // the vector of vectors
    [HT G296]          v = vector<vector< int > >(n);
    // Here, we will allocate
    // memory of the unnamed_memory
    // to the object. This snippet
    // of code won't work for now.
    // Program will work whenever
    // constructor gets initialized
    this ->n = n;
    }
    int getHashIndex( int x)
    {
    return x % n;
    }
    void add( int x)
    {
    // Adding the element according
    // to hash index
    v[getHashIndex(x)].push_back(x);
    }
    [
    [ void del( int x)
    {
    int i = getHashIndex(x);
    // Scan for the element to be removed
    for ( int j = 0; j < v[i].size(); j++) {
    // Erase if present otherwise
    // print no element found!
    if (v[i][j] == x) {
    v[i].erase(v[i].begin() + j);
    cout << x << " deleted!" << endl;
    return ;
    }
    }
    cout << "No Element Found!" << endl;
    }
    void displayHash()
    {
    // Display the contents
    for ( int i = 0; i < v.size(); i++) {
    cout << i;
    for ( int j = 0; j < v[i].size(); j++)
    cout << " -> " << v[i][j];
    cout << endl;
    }
    }
    };
    // Driver Code
    int main()
    {
    // Array to be used
    ]
    int arr[] = { 12, 3, 23, 4, 11,
    32, 26, 33, 17, 19 };
    // Sending the size
    // for separate chaining
    SeperateHash obj(10);
    // Inserting elements in
    // the container accordingly
    for ( int i = 0; i < 10; i++)
    obj.add(arr[i]);
    [HT G432]
    // Display the initial hash
    cout << "Initial Hash:\n" ;
    obj.displayHash();
    // Removing the element
    // from the container
    cout << "\nRemoving 23 from Hash: " ;
    obj.del(23);
    cout << endl;
    // Display the final hash
    cout << "Final Hash:\n" ;
    obj.displayHash();
    return 0;
    }
    ```

    **Output:**

    ```
    Initial Hash:
    0
    1 -> 11
    2 -> 12 -> 32
    3 -> 3 -> 23 -> 33
    4 -> 4
    5
    6 -> 26
    7 -> 17
    8
    9 -> 19

    Removing 23 from Hash: 23 deleted!

    Final Hash:
    0
    1 -> 11
    2 -> 12 -> 32
    3 -> 3 -> 33
    4 -> 4
    5
    6 -> 26
    7 -> 17
    8
    9 -> 19

    ```

    **使用此方法的优势**：

    1.  我们不需要像访问链接列表那样遍历条目。

    2.  简化代码调试。

    3.  由于传统方法具有标记具有较小逻辑错误的分段错误的机会，因此更易于实现。

    4.  在数据上应用 STL 方法的强大功能在竞争性编程中提供了优势。

    注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

    * * *

    * * *

    如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

    如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。