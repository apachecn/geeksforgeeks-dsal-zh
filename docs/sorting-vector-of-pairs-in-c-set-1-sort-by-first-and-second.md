# c++中对的排序向量|集合 1(按第一个和第二个排序)

> 原文:[https://www . geesforgeks . org/sorting-c-set-1 中的成对向量-按第一和第二排序/](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)

**什么是对的向量？**
一个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)是一个存储相互映射的两个值的容器，一个包含多个这样的对的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)被称为一个对向量。

```
// C++ program to demonstrate vector of pairs
#include<bits/stdc++.h>
using namespace std;

int main()
{
    //declaring vector of pairs
    vector< pair <int,int> > vect;

    // initialising 1st and 2nd element of
    // pairs with array values
    int arr[] = {10, 20, 5, 40 };
    int arr1[] = {30, 60, 20, 50};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Entering values in vector of pairs
    for (int i=0; i<n; i++)
        vect.push_back( make_pair(arr[i],arr1[i]) );

    // Printing the vector
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
10 30
20 60
5 20
40 50

```

**情况 1:以对的第一个元素为基础，按升序对向量元素进行排序。**
这种类型的排序可以使用简单的“sort()”函数来实现。默认情况下，排序函数根据第一个元素对向量元素进行排序。

```
// C++ program to demonstrate sorting in
// vector of pair according to 1st element
// of pair
#include<bits/stdc++.h>
using namespace std;

int main()
{
    // Declaring vector of pairs
    vector< pair <int,int> > vect;

    // Initializing 1st and 2nd element of
    // pairs with array values
    int arr[] = {10, 20, 5, 40 };
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

    // Using simple sort() function to sort
    sort(vect.begin(), vect.end());

     // Printing the sorted vector(after using sort())
    cout << "The vector after sort operation is:\n" ;
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
The vector before applying sort operation is:
10 30
20 60
5 20
40 50
The vector after applying sort operation is:
5 20
10 30
20 60
40 50

```

**情况 2:以对的第二个元素为基础，按升序对向量元素进行排序。**
有时我们需要根据第二对元素对向量的元素进行排序。为此，我们修改了 sort()函数，并传递了第三个参数，即对 sort()函数中用户定义的显式函数的调用。

```
// C++ program to demonstrate sorting in vector
// of pair according to 2nd element of pair
#include<bits/stdc++.h>
using namespace std;

// Driver function to sort the vector elements
// by second element of pairs
bool sortbysec(const pair<int,int> &a,
              const pair<int,int> &b)
{
    return (a.second < b.second);
}

int main()
{
    // declaring vector of pairs
    vector< pair <int, int> > vect;

    // Initialising 1st and 2nd element of pairs
    // with array values
    int arr[] = {10, 20, 5, 40 };
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

    // Using sort() function to sort by 2nd element
    // of pair
    sort(vect.begin(), vect.end(), sortbysec);

    // Printing the sorted vector(after using sort())
    cout << "The vector after sort operation is:\n" ;
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

The vector before applying sort operation is:
10 30
20 60
5 20
40 50
The vector after applying sort operation is:
5 20
10 30
40 50
20 60

```

C++中对的排序向量|集合 2 [(按第一和第二降序排序)](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-2-sort-in-descending-order-by-first-and-second/)

本文由**曼吉特·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。