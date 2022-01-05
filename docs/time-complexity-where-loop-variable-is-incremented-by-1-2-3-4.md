# 循环变量递增 1、2、3、4 的时间复杂度..

> 原文:[https://www . geesforgeks . org/time-complexity-where-loop-variable-递增-1-2-3-4/](https://www.geeksforgeeks.org/time-complexity-where-loop-variable-is-incremented-by-1-2-3-4/)

下面代码的时间复杂度是多少？

```
void fun(int n)
{
   int j = 1, i = 0;
   while (i < n)
   {
       // Some O(1) task
       i = i + j;
       j++;
   }
}
```

循环变量' I '递增 1，2，3，4，…，直到 I 变得大于或等于 n。

在 x 次迭代后，I 的值为 x(x+1)/2。所以如果循环运行 x 次，那么 x(x+1)/2 < n. Therefore time complexity can be written as Θ(√n).

本文由**比于什·古普塔**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论