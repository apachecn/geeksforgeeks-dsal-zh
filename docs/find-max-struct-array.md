# 在结构数组中找到最大值

> 原文:[https://www.geeksforgeeks.org/find-max-struct-array/](https://www.geeksforgeeks.org/find-max-struct-array/)

给定高度类型的结构数组，求最大值

```
struct Height{
  int feet;
  int inches;
}

```

**问题来源:** [微软面试体验集 127 |(IDC 校内)](https://www.geeksforgeeks.org/microsoft-interview-experience-set-127-campus-idc/)

想法很简单，遍历数组，跟踪数组元素的最大值
值(英寸)= 12 *英尺+英寸

```
// CPP program to return max
// in struct array
#include <iostream>
#include <climits>
using namespace std;

// struct Height
// 1 feet = 12 inches
struct Height {
    int feet;
    int inches;
};

// return max of the array
int findMax(Height arr[], int n)
{
    int mx = INT_MIN;
    for (int i = 0; i < n; i++) {
        int temp = 12 * (arr[i].feet) 
                     + arr[i].inches;
        mx = max(mx, temp);
    }
    return mx;
}

// driver program
int main()
{
    // initialize the array
    Height arr[] = {
        { 1, 3 },
        { 10, 5 },
        { 6, 8 },
        { 3, 7 },
        { 5, 9 }
    };
    int res = findMax(arr, 5);
    cout << "max :: " << res << endl;
    return 0;
}
```

输出:

```
max :: 125

```

本文由 **[曼德普·辛格](https://github.com/msdeep14)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。