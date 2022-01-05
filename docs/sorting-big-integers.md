# 大整数排序

> 原文:[https://www.geeksforgeeks.org/sorting-big-integers/](https://www.geeksforgeeks.org/sorting-big-integers/)

给定一个由 **n** 个正整数组成的数组，其中每个整数最多可以有 10 位 <sup>6</sup> ，以升序打印数组元素。

```
Input: arr[] = {54, 724523015759812365462, 870112101220845, 8723} 
Output: 54 8723 870112101220845 724523015759812365462
Explanation:
All elements of array are sorted in non-descending(i.e., ascending)
order of their integer value

Input: arr[] = {3643641264874311, 451234654453211101231,
                4510122010112121012121}
Output: 3641264874311 451234654453211101231 4510122010112121012121

```

一种**天真的方法**是使用任意精度的数据类型，比如 python 中的 **int** 或者 Java 中的 **Biginteger** 类。但是这种方法不会有成效，因为将字符串内部转换为 int，然后执行排序会导致二进制数系统中加法和乘法的计算速度变慢。

**高效解决方案:**由于整数的大小非常大，甚至无法适合 C/C++的**长**数据类型，所以我们只需要将所有数字输入为字符串，并使用比较函数进行排序。以下是比较功能的要点:-

1.  如果两个字符串的长度不同，那么我们需要比较长度来决定排序顺序。
2.  如果长度相同，那么我们只需要按照字典顺序比较这两个字符串。

假设:没有前导零。

## C++

```
// Below is C++ code to sort the Big integers in
// ascending order
#include<bits/stdc++.h>
using namespace std;

// comp function to perform sorting
bool comp(const string &left, const string &right)
{
    // if length of both string are equals then sort
    // them in lexicographically order
    if (left.size() == right.size())
        return left < right;

    // Otherwise sort them according to the length
    // of string in ascending order
    else
        return left.size() < right.size();
}

// Function to sort arr[] elements according
// to integer value
void SortingBigIntegers(string arr[], int n)
{
    // Copy the arr[] elements to sortArr[]
    vector<string> sortArr(arr, arr + n);

    // Inbuilt sort function using function as comp
    sort(sortArr.begin(), sortArr.end(), comp);

    // Print the final sorted array
    for (auto &ele : sortArr)
        cout << ele << " ";
}

// Driver code of above implementation
int main()
{
    string arr[] = {"54", "724523015759812365462",
                    "870112101220845", "8723"};
    int n = sizeof(arr) / sizeof(arr[0]);

    SortingBigIntegers(arr, n);

    return 0;
}
```

## 计算机编程语言

```
# Below is Python code to sort the Big integers
# in ascending order
def SortingBigIntegers(arr, n):

  # Direct sorting using lamda operator
  # and length comparison
  arr.sort(key = lambda x: (len(x), x))

# Driver code of above implementation
arr = ["54", "724523015759812365462",
        "870112101220845", "8723"]
n = len(arr)

SortingBigIntegers(arr, n)

# Print the final sorted list using 
# join method
print " ".join(arr)
```

```
Output: 54 8723 870112101220845 724523015759812365462

```

**时间复杂度:** O(sum * log(n))其中 sum 是所有字符串长度的总和，n 是数组的大小
**辅助空间:** O(n)

**类似帖子:**
[整理一大堆数字](https://www.geeksforgeeks.org/sort-array-large-numbers/)

本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。