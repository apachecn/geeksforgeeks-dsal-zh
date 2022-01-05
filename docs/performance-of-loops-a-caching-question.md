# 循环性能(缓存问题)

> 原文:[https://www . geeksforgeeks . org/performance-of-loops-a-cache-question/](https://www.geeksforgeeks.org/performance-of-loops-a-caching-question/)

考虑下面两个计算 2D 数组元素和的 C 语言函数。忽略编译器优化，两者中哪一个更好的实现 sum？

```
// Function 1
int fun1(int arr[R][C])
{
    int sum = 0;
    for (int i=0; i<R; i++)
      for (int j=0; j<C; j++)
          sum += arr[i][j];
}

// Function 2
int fun2(int arr[R][C])
{
    int sum = 0;
    for (int j=0; j<C; j++)
      for (int i=0; i<R; i++)
          sum += arr[i][j];
}
```

在 C/C++中，元素以行主顺序存储。因此第一个实现具有更好的空间局部性(在连续迭代中引用附近的内存位置)。因此，对于迭代多维数组，第一个实现应该总是首选的。

如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论