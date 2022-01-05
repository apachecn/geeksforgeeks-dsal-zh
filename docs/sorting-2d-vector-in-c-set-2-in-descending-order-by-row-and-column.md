# c++中 2D 向量排序|集合 2(按行和列降序排列)

> 原文:[https://www . geesforgeks . org/sorting-2d-vector-in-c-set-2-按行和列降序排列/](https://www.geeksforgeeks.org/sorting-2d-vector-in-c-set-2-in-descending-order-by-row-and-column/)

我们已经在下面的集合 1 中讨论了排序 2D 向量的一些情况。

[c++中 2D 向量排序|集合 1(按行和列)](https://www.geeksforgeeks.org/sorting-2d-vector-in-c-set-1-by-row-and-column/)

本文将讨论更多的案例

**情况 3:以降序排列 2D 向量的特定行**
这种排序方式以降序排列 2D 向量的选定行。这是通过使用“sort()”并传递 1D 向量的迭代器作为参数来实现的。

```
// C++ code to demonstrate sorting of a
// row of 2D vector in descending order
#include<iostream>
#include<vector> // for 2D vector
#include<algorithm> // for sort()
using namespace std;

int main()
{
    // Initializing 2D vector "vect" with
    // values
    vector< vector<int> > vect{{3, 5, 1},
                               {4, 8, 6},
                               {7, 2, 9}};
    // Number of rows;
    int m = vect.size();

    // Number of columns (Assuming all rows
    // are of same size).  We can have different
    // sizes though (like Java).
    int n = vect[0].size();

    // Displaying the 2D vector before sorting
    cout << "The Matrix before sorting 1st row is:\n";
    for (int i=0; i<m; i++)
    {
        for (int j=0; j<n ;j++)
           cout << vect[i][j] << " ";
        cout << endl;
    }

    // Use of "sort()" for sorting first row
    sort(vect[0].rbegin(), vect[0].rend());

    // Displaying the 2D vector after sorting
    cout << "The Matrix after sorting 1st row is:\n";
    for (int i=0; i<m; i++)
    {
        for (int j=0; j<n ;j++)
            cout << vect[i][j] << " ";
        cout << endl;
    }

    return 0;
}
```

输出:

```
The Matrix before sorting 1st row is:
3 5 1 
4 8 6 
7 2 9 
The Matrix after sorting 1st row is:
5 3 1 
4 8 6 
7 2 9 

```

**情况 4:根据特定的列，按降序对整个 2D 向量进行排序。**
在这种类型的排序中，2D 向量完全是根据选定的列按降序排序的。例如，如果选择的列是第二列，则第二列中具有最大值的行成为第一行，第二列中具有第二大值的行成为第二行，依此类推。

{3，5，1}，
{4，8，6}，
{7，2，9 }；

将这个矩阵按第二列排序后，我们得到

{4，8，6} //第二列中值最大的行
{3，5，1} //第二列中值第二大的行
{7，2，9}

这是通过在“sort()”中传递第三个参数作为对用户定义的显式函数的调用来实现的。

```
// C++ code to demonstrate sorting of a
// 2D vector on basis of a column in
// descending order
#include<iostream>
#include<vector> // for 2D vector
#include<algorithm> // for sort()
using namespace std;

// Driver function to sort the 2D vector
// on basis of a particular column in 
// descending order
bool sortcol( const vector<int>& v1,
               const vector<int>& v2 ) {
    return v1[1] > v2[1];
}

int main()
{
    // Initializing 2D vector "vect" with
    // values
    vector< vector<int> > vect{{3, 5, 1},
                                {4, 8, 6},
                                {7, 2, 9}};

    // Number of rows;
    int m = vect.size();

    // Number of columns (Assuming all rows
    // are of same size).  We can have different
    // sizes though (like Java).
    int n = vect[0].size();

    // Displaying the 2D vector before sorting
    cout << "The Matrix before sorting is:\n";
    for (int i=0; i<m; i++)
    {
        for (int j=0; j<n ;j++)
            cout << vect[i][j] << " ";
        cout << endl;
    }                               

    // Use of "sort()" for sorting on basis
    // of 2nd column in descending order
    sort(vect.begin(), vect.end(),sortcol);

    // Displaying the 2D vector after sorting
    cout << "The Matrix after sorting is:\n";
    for (int i=0; i<m; i++)
    {
        for (int j=0; j<n ;j++)
            cout << vect[i][j] << " ";
        cout << endl;
    }
    return 0;
}
```

输出:

```
The Matrix before sorting is:
3 5 1 
4 8 6 
7 2 9 
The Matrix after sorting is:
4 8 6 
3 5 1 
7 2 9 

```

本文由**曼吉特·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。