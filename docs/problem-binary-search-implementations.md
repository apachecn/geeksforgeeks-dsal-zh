# 许多二分搜索法实现中的一个问题

> 原文:[https://www . geesforgeks . org/problem-binary-search-implements/](https://www.geeksforgeeks.org/problem-binary-search-implementations/)

考虑下面 C 实现的[二分搜索法](http://geeksquiz.com/binary-search/)功能，这里面有什么不对吗？

```
// A iterative binary search function. It returns location of x in
// given array arr[l..r] if present, otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
    while (l <= r)
    {
        // find index of middle element
        int m = (l+r)/2;

        // Check if x is present at mid
        if (arr[m] == x) return m;

        // If x greater, ignore left half
        if (arr[m] < x) l = m + 1;

        // If x is smaller, ignore right half
        else r = m - 1;
    }

    // if we reach here, then element was not present
    return -1;
}
```

上面看起来很好，除了一个微妙的东西，表达式“m = (l+r)/2”。对于较大的 l 和 r 值，它会失败。具体来说，如果低和高的总和大于最大正 int 值(2<sup>31</sup>–1)，它会失败。总和溢出为负值，该值除以 2 后仍为负值。在 C 语言中，这会导致数组索引超出界限，并产生不可预测的结果。

**解决这个问题的方法是什么？**
以下是一种方式:

```
        int mid = low + ((high - low) / 2); 
```

可能更快，可以说很清楚(只在 Java 中起作用，参考[这个](https://www.geeksforgeeks.org/bitwise-shift-operators-in-java/)):

```
        int mid = (low + high) >>> 1; 
```

在 C 和 C++中(这里没有>>>运算符)，您可以这样做:

```
        mid = ((unsigned int)low + (unsigned int)high)) >> 1 
```

类似的问题也出现在[合并排序](http://geeksquiz.com/merge-sort/)中。

以上内容摘自[谷歌研究博客](http://googleresearch.blogspot.in/2006/06/extra-extra-read-all-about-it-nearly.html)。

也请参考[这个](http://locklessinc.com/articles/binary_search/)，它指出上述解决方案可能并不总是有效的。

当数组长度为 2 <sup>30</sup> 或更大，并且搜索重复移动到数组的后半部分时，会出现上述问题。这么大的数组不太可能在大多数时候出现。例如，当我们用 32 位[代码块](http://www.codeblocks.org/)编译器尝试下面的程序时，我们会得到编译器错误。

```
int main()
{
    int arr[1<<30];
    return 0;
}
```

输出:

```
error: size of array 'arr' is too large
```

即使我们尝试布尔数组，程序也能很好地编译，但是在 Windows 7.0 和[代码块](http://www.codeblocks.org/) 32 位编译器中运行时会崩溃

```
#include <stdbool.h>
int main()
{
    bool arr[1<<30];
    return 0;
}
```

输出:没有编译器错误，但在运行时崩溃。

**来源:**
[http://googleresearch . blogspot . in/2006/06/extra-extra-read-all-it-near . html](http://googleresearch.blogspot.in/2006/06/extra-extra-read-all-about-it-nearly.html)
[http://locklessinc.com/articles/binary_search/](http://locklessinc.com/articles/binary_search/)

本文由**阿沛·拉提**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论