# 算法分析|集合 4(求解递归)

> 原文:[https://www . geesforgeks . org/analysis-algorithm-set-4-master-method-solution-recurrences/](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)

在前一篇文章中，我们讨论了循环的[分析。许多算法本质上是递归的。当我们分析它们时，我们得到了时间复杂性的递归关系。我们得到大小为 n 的输入上的运行时间是 n 的函数，以及较小大小的输入上的运行时间。例如在](https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/)[合并排序](http://geeksquiz.com/merge-sort/)中，为了对给定的数组进行排序，我们将其分成两半，并递归地对两半重复该过程。最后我们合并结果。合并排序的时间复杂度可以写成 T(n) = 2T(n/2) + cn。还有很多其他的算法，比如二分搜索法、汉诺塔等等。

解决复发主要有三种方法。

**1)代入法**:我们对解进行猜想，然后用数学归纳法证明猜想的正确或不正确。

```
For example consider the recurrence T(n) = 2T(n/2) + n

We guess the solution as T(n) = O(nLogn). Now we use induction
to prove our guess.

We need to prove that T(n) <= cnLogn. We can assume that it is true
for values smaller than n.

T(n) = 2T(n/2) + n
    <= 2cn/2Log(n/2) + n
    =  cnLogn - cnLog2 + n
    =  cnLogn - cn + n
    <= cnLogn
```

**2)递归树方法:**在该方法中，我们绘制一个递归树，并计算每一级树所花费的时间。最后，我们总结了各级所做的工作。为了绘制循环树，我们从给定的循环开始，一直绘制，直到找到层次之间的模式。该模式通常是算术或几何级数。

```
For example consider the recurrence relation 
T(n) = T(n/4) + T(n/2) + cn2

           cn2
         /      \
     T(n/4)     T(n/2)

If we further break down the expression T(n/4) and T(n/2), 
we get following recursion tree.

                cn2
           /           \      
       c(n2)/16      c(n2)/4
      /      \          /     \
  T(n/16)     T(n/8)  T(n/8)    T(n/4) 
Breaking down further gives us following
                 cn2
            /            \      
       c(n2)/16          c(n2)/4
       /      \            /      \
c(n2)/256   c(n2)/64  c(n2)/64    c(n2)/16
 /    \      /    \    /    \       /    \  

To know the value of T(n), we need to calculate sum of tree 
nodes level by level. If we sum the above tree level by level, 
we get the following series
T(n)  = c(n^2 + 5(n^2)/16 + 25(n^2)/256) + ....
The above series is geometrical progression with ratio 5/16.

To get an upper bound, we can sum the infinite series. 
We get the sum as (n2)/(1 - 5/16) which is O(n2)
```

**3)大师法:**
大师法是直接得到解的方法。主方法仅适用于以下类型的循环或可转换为以下类型的循环。

```
T(n) = aT(n/b) + f(n) where a >= 1 and b > 1
```

有以下三种情况:
**1。**如果 f(n) = O(n <sup>c</sup> )其中 c < Log <sub>b</sub> a 则 T(n)=θ(n<sup>Log</sup>T9<sup>b</sup>T12<sup>a</sup>

**2。**如果 f(n)=θ(n<sup>c</sup>)其中 c =对数 <sub>b</sub> a，那么 T(n)=θ(n<sup>c</sup>对数 n)

**3。**如果 f(n)=ω(n<sup>c</sup>)其中 c > Log <sub>b</sub> a 则 T(n)=θ(f(n))

**这是如何工作的？**
大师法主要来源于递归树法。如果我们画出 T(n) = aT(n/b) + f(n)的递归树，我们可以看到根所做的功是 f(n)，所有叶所做的功是θ(n<sup>c</sup>，其中 c 是 Log <sub>b</sub> a，递归树的高度是 Log <sub>b</sub> n

![Master Theorem](img/7c9545d77618a1692eafee0d888c821e.png)

在递归树方法中，我们计算完成的总工作量。如果在叶子上做的功更多是多项式的，那么叶子就是主导部分，我们的结果就变成了在叶子上做的功(例 1)。如果在叶子和根上做的功是渐近相同的，那么我们的结果就变成了高度乘以在任何水平上做的功(例 2)。如果在根上做的功是渐近更多的，那么我们的结果变成在根上做的功(情况 3)。

**一些标准算法的例子，其时间复杂度可以使用主方法**
[合并排序](http://geeksquiz.com/merge-sort/):T(n)= 2T(n/2)+θ(n)。它属于情况 2，因为 c 为 1，Log <sub>b</sub> a】也为 1。所以解是θ(n Logn)

[二分搜索法](http://geeksquiz.com/binary-search/):T(n)= T(n/2)+θ(1)。它也属于情况 2，因为 c 是 0，而 Log <sub>b</sub> a 也是 0。所以解是θ(Logn)

**注:**
**1)** 形式的递推 T(n) = aT(n/b) + f(n)不一定能用 Master 定理求解。给定的三个案例之间有一些差距。比如递归 T(n) = 2T(n/2) + n/Logn 不能用 master 方法求解。

**2)** 情况 2 可以扩展为 f(n)=θ(n<sup>c</sup>Log<sup>k</sup>n)
如果 f(n)=θ(n<sup>c</sup>Log<sup>k</sup>n)对于某些常数 k > = 0 且 c = Log <sub>b</sub> a，那么 T(n)=θ(n<sup>c</sup>Log<sup>k+1</sup>

[练习掌握定理的问题及解决方法。](http://www.csd.uwo.ca/~moreno//CS424/Ressources/master.pdf)

下一步–[算法分析|第五集(摊销分析介绍)](https://www.geeksforgeeks.org/analysis-algorithm-set-5-amortized-analysis-introduction/)

**参考文献:**
[【http://en.wikipedia.org/wiki/Master_theorem】](http://en.wikipedia.org/wiki/Master_theorem)
[麻省理工学院渐进记号学视频讲座|重现|替换，主方法](http://www.youtube.com/watch?v=whjt_N9uYFI)
[算法导论第三版，作者:克利福德·斯坦、托马斯·h·科曼、查尔斯·e·雷瑟森、罗纳德·L·李维斯特](http://www.flipkart.com/introduction-algorithms-3/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg)

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息