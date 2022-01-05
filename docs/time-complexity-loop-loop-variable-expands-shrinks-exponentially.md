# 当循环变量指数“膨胀或收缩”时循环的时间复杂度

> 原文:[https://www . geesforgeks . org/时间-复杂性-循环-循环-变量-扩展-收缩-指数级/](https://www.geeksforgeeks.org/time-complexity-loop-loop-variable-expands-shrinks-exponentially/)

对于这种情况，循环的时间复杂度为 O(log(log(n))。以下案例分析了问题的不同方面。

**案例 1 :**

```
for (int i = 2; i <=n; i = pow(i, k)) 
{ 
    // some O(1) expressions or statements
}
```

在这种情况下，我取值 2，2 <sup>k</sup> ，(2<sup>k</sup>)<sup>k</sup>= 2<sup>k<sup>2</sup>T9】，(2<sup>k<sup>2</sup></sup>)<sup>k</sup>= 2<sup>k<sup>3</sup></sup>，…，2<sup>k</sup>T22<sup>log<sub>k 最后一项必须小于等于 n，我们有 2<sup>k</sup><sup><sup>log<sub>k</sub>(log(n))</sup></sup>= 2<sup>log(n)</sup>= n，完全符合我们最后一项的数值。所以总共有 log <sub>k</sub> (log(n))多次迭代，每次迭代需要恒定的运行时间，因此总时间复杂度为 O(log(log(n))。</sub></sup></sup>

**案例 2 :**

```
// func() is any constant root function
for (int i = n; i > 1; i = func(i)) 
{ 
   // some O(1) expressions or statements
}
```

在这种情况下，我取值 n，n <sup>1/k</sup> ，(n<sup>1/k</sup>)<sup>1/k</sup>= n<sup>1/k<sup>2</sup></sup>，n <sup>1/k <sup>3</sup></sup> ，…，n<sup>1/k<sup>log<sub>k</sub>(log(n))</sup></sup>，所以总共有【log

有关不同类型循环的分析，请参考下面的文章。
[https://www . geeksforgeeks . org/算法集分析-4-循环分析/](https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/)

本文由**里沙夫·拉吉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。