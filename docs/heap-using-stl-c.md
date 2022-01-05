# c++ STL 中的堆| make_heap()，push_heap()，pop_heap()，sort_heap()，is_heap，is _ heap _ 直到()

> 原文:[https://www.geeksforgeeks.org/heap-using-stl-c/](https://www.geeksforgeeks.org/heap-using-stl-c/)

堆数据结构可以在一个范围内使用 STL 实现，STL 允许更快地输入堆，检索一个数字总是得到最大的数字，即每次弹出剩余数字的最大数字。堆的其他数量根据实现进行排列。

**堆上操作**:

**1。make_heap()** :-此函数用于**将容器**中的范围**转换为堆。**

**2。front()** :-该功能显示堆的**第一个元素**，这是**最大数量**。

```
// C++ code to demonstrate the working of 
// make_heap(), front()
#include<bits/stdc++.h> 
using namespace std;
int main()
{

    // Initializing a vector
    vector<int> v1 = {20, 30, 40, 25, 15};

    // Converting vector into a heap
    // using make_heap()
    make_heap(v1.begin(), v1.end());

    // Displaying the maximum element of heap
    // using front()
    cout << "The maximum element of heap is : ";
    cout << v1.front() << endl;

    return 0;
}
```

输出:

```
The maximum element of heap is : 40

```

**3。push_heap()** :-该功能用于**将**元素插入堆中。堆的大小增加了 1。新元素被适当地放置在堆中。

**4。pop_heap()** :-该功能用于**删除堆的最大元素**。堆的大小减少 1。在此操作之后，堆元素会相应地重新组织。

```
// C++ code to demonstrate the working of 
// push_heap() and pop_heap()
#include<bits/stdc++.h> 
using namespace std;
int main()
{

    // Initializing a vector
    vector<int> v1 = {20, 30, 40, 25, 15};

    // Converting vector into a heap
    // using make_heap()
    make_heap(v1.begin(), v1.end());

    // Displaying the maximum element of heap
    // using front()
    cout << "The maximum element of heap is : ";
    cout << v1.front() << endl;

    // using push_back() to enter element
    // in vector
    v1.push_back(50);

    // using push_heap() to reorder elements
    push_heap(v1.begin(), v1.end());

    // Displaying the maximum element of heap
    // using front()
    cout << "The maximum element of heap after push is : ";
    cout << v1.front() << endl;

     // using pop_heap() to delete maximum element
    pop_heap(v1.begin(), v1.end());
    v1.pop_back();

    // Displaying the maximum element of heap
    // using front()
    cout << "The maximum element of heap after pop is : ";
    cout << v1.front() << endl;

    return 0;
}
```

输出:

```
The maximum element of heap is : 40
The maximum element of heap after push is : 50
The maximum element of heap after pop is : 40

```

**5。sort_heap()** :-该功能用于**对**堆进行排序。这次操作之后，集装箱就不再是**一堆**了。

```
// C++ code to demonstrate the working of 
// sort_heap()
#include<bits/stdc++.h> 
using namespace std;
int main()
{

    // Initializing a vector
    vector<int> v1 = {20, 30, 40, 25, 15};

    // Converting vector into a heap
    // using make_heap()
    make_heap(v1.begin(), v1.end());

    // Displaying heap elements 
    cout << "The heap elements are : ";
    for (int &x : v1) 
       cout << x << " ";
    cout << endl;

    // sorting heap using sort_heap()
    sort_heap(v1.begin(), v1.end());

     // Displaying heap elements 
    cout << "The heap elements after sorting are : ";
    for (int &x : v1) 
       cout << x << " ";

    return 0;
}
```

输出:

```
The heap elements are : 40 30 20 25 15 
The heap elements after sorting are : 15 20 25 30 40 

```

**6。is_heap()** :-该功能用于**检查**集装箱是否为**堆**。通常，在大多数实现中，**反向排序容器**被认为是堆。如果容器是堆，则返回 true，否则返回 false。

**6。is _ heap _ 直到()** :-这个函数将迭代器返回到位置**，直到容器成为堆。**一般来说，在大多数实现中，**反向排序容器**被认为是堆。

```
// C++ code to demonstrate the working of 
// is_heap() and is_heap_until()
#include<bits/stdc++.h> 
using namespace std;
int main()
{

    // Initializing a vector
    vector<int> v1 = {40, 30, 25, 35, 15};

    // Declaring heap iterator
    vector<int>::iterator it1;

    // Checking if container is heap
    // using is_heap()
    is_heap(v1.begin(), v1.end())?
    cout << "The container is heap ":
    cout << "The container is not heap";
    cout << endl;

    // using is_heap_until() to check position 
    // till which container is heap
    auto it = is_heap_until(v1.begin(), v1.end());

    // Displaying heap range elements
    cout << "The heap elements in container are : ";
    for (it1=v1.begin(); it1!=it; it1++)
       cout << *it1 << " ";

    return 0;
}
```

输出:

```
The container is not heap
The heap elements in container are : 40 30 25 

```

本文由供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。