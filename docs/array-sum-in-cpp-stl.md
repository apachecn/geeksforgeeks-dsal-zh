# c++ STL 中的数组和

> 原文:[https://www.geeksforgeeks.org/array-sum-in-cpp-stl/](https://www.geeksforgeeks.org/array-sum-in-cpp-stl/)

在 C++中，我们可以使用[累加()](https://www.geeksforgeeks.org/numeric-header-in-c-stl-set-1-accumulate-and-partial_sum/)

```
// C++ program to demonstrate working of accumulate()
#include <iostream> 
#include <numeric>     
using namespace std;

// User defined function that returns sum of
// arr[] using accumulate() library function.
int arraySum(int a[], int n) 
{
    int initial_sum  = 0; 
    return accumulate(a, a+n, initial_sum);
}

int main() 
{
    int a[] = {5 , 10 , 15} ;
    int n = sizeof(a)/sizeof(a[0]);
    cout << arraySum(a, n);
    return 0;
}
```

快速找到数组和

输出:

```
30

```

**矢量之和**

```
// C++ program to demonstrate working of accumulate()
#include <iostream> 
#include <vector> 
#include <numeric>     
using namespace std;

// User defined function that returns sum of
// arr[] using accumulate() library function.
int arraySum(vector<int> &v) 
{
    int initial_sum  = 0; 
    return accumulate(v.begin(), v.end(), initial_sum);
}

int main() 
{
    vector<int> v{5 , 10 , 15} ;
    cout << arraySum(v);
    return 0;
}
```

输出:

```
30

```

我们也可以在累加中使用自定义函数。详见 C++ STL | Set 1(累加()和 partial_sum()) 中的[数值表头。](https://www.geeksforgeeks.org/numeric-header-in-c-stl-set-1-accumulate-and-partial_sum/)

本文由[](https://auth.geeksforgeeks.org/profile.php?user=kartik)**kartik 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。**

**如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**