# c++ |集合 2 中对的排序向量(按第一个和第二个降序排序)

> 原文:[https://www . geesforgeks . org/sorting-c-set-2 中的成对向量-按第一和第二降序排序/](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-2-sort-in-descending-order-by-first-and-second/)

我们在下面的集合 1 中讨论了排序向量对的一些情况。
[c++中对向量的排序|集合 1(按第一个和第二个排序)](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
更多情况在本文中讨论
有时我们要求对向量进行逆序排序。在这些情况下，不是首先对向量进行排序，然后使用“反向”函数，而是增加代码的时间复杂性。因此，为了避免这种情况，我们直接按降序对向量进行排序。
**情况 3:以对的第一个元素为基础，按降序对向量元素进行排序。**
这种类型的排序以降序排列向量中选定的行对。这是通过使用“sort()”并传递 1D 向量的迭代器作为参数来实现的。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate sorting in vector of
// pair according to 1st element of pair in
// descending order
#include<bits/stdc++.h>
using namespace std;

int main()
{
    // declaring vector of pairs
    vector< pair <int,int> > vect;

    // initializing 1st and 2nd element of
    // pairs with array values
    int arr[] = {5, 20, 10, 40 };
    int arr1[] = {30, 60, 20, 50};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Entering values in vector of pairs
    for (int i=0; i<n; i++)
        vect.push_back( make_pair(arr[i],arr1[i]) );

    // Printing the original vector(before sort())
    cout << "The vector before applying sort is:\n" ;
    for (int i=0; i<n; i++)
    {
        // "first" and "second" are used to access
        // 1st and 2nd element of pair respectively
        cout << vect[i].first << " "
             << vect[i].second << endl;

    }

    // using modified sort() function to sort
    sort(vect.rbegin(), vect.rend());

    // Printing the sorted vector(after using sort())
    cout << "The vector after applying sort is:\n" ;
    for (int i=0; i<n; i++)
    {
        // "first" and "second" are used to access
        // 1st and 2nd element of pair respectively
        cout << vect[i].first << " "
             << vect[i].second << endl;
    }
    return 0;
}
```

输出:

```
The vector before applying sort is:
5 30
20 60
10 20
40 50
The vector after applying sort is:
40 50
20 60
10 20
5 30

```

**情况 4:以对的第二个元素为基础，按降序对向量元素进行排序。**
这些实例也可以通过修改“sort()”函数并再次传递对用户定义函数的调用来处理。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate sorting/in vector of
// pair according to 2nd element of pair in
// descending order
#include<bits/stdc++.h>
using namespace std;

// Driver function to sort the vector elements by
// second element of pair in descending order
bool sortbysecdesc(const pair<int,int> &a,
                   const pair<int,int> &b)
{
       return a.second>b.second;
}

int main()
{
    // Declaring vector of pairs
    vector< pair <int,int> > vect;

    // Initializing 1st and 2nd element of
    // pairs with array values
    int arr[] = {5, 20, 10, 40 };
    int arr1[] = {30, 60, 20, 50};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Entering values in vector of pairs
    for (int i=0; i<n; i++)
        vect.push_back( make_pair(arr[i],arr1[i]) );

    // Printing the original vector(before sort())
    cout << "The vector before sort operation is:\n" ;
    for (int i=0; i<n; i++)
    {
        // "first" and "second" are used to access
        // 1st and 2nd element of pair respectively
        cout << vect[i].first << " "
            << vect[i].second << endl;
    }

    // using modified sort() function to sort
    sort(vect.begin(), vect.end(), sortbysecdesc);

    // Printing the sorted vector(after using sort())
    cout << "The vector after applying sort operation is:\n" ;
    for (int i=0; i<n; i++)
    {
        // "first" and "second" are used to access
        // 1st and 2nd element of pair respectively
        cout << vect[i].first << " "
             << vect[i].second << endl;
    }
    return 0;
}
```

输出:

```
The vector before sort operation is:
5 30
20 60
10 20
40 50
The vector after applying sort operation is:
20 60
40 50
5 30
10 20

```

本文由**曼吉特·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。