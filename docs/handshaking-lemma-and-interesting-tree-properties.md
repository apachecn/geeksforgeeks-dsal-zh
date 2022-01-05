# 握手引理和有趣树属性

> 原文:[https://www . geeksforgeeks . org/handsking-lemma-和-interest-tree-properties/](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)

**什么是握手引理？**
[握手引理](http://en.wikipedia.org/wiki/Handshaking_lemma)是关于一个无向图的。在每个有限无向图中，偶数个顶点总是有奇数个度数。握手引理是度和公式的结果(有时也称为握手引理)
![\sum_{u \epsilon v} deg(v) = 2\left | E \right |    ](img/b0dd977917b9defc6d6303c96d9be423.png "Rendered by QuickLaTeX.com")

**握手引理在树形数据结构中有什么用？**
下面是一些有趣的事实，可以用握手引理来证明。

***1)在每个节点都有 0 或 k 个子节点的 k 元树中，以下属性始终为真。**T3】*

```
  L = (k - 1)*I + 1
Where L = Number of leaf nodes
      I = Number of internal nodes  
```

**证明:**
证明可以分为两种情况。

***情况 1*** (根为叶):树中只有一个节点。对于 L = 1，I = 0 的单个节点，上述公式成立。

***情况 2*** (根是内部节点):对于有 1 个以上节点的树，根永远是内部节点。对于这种情况，可以用握手引理证明上述公式。树是无向无环图。

树中边的总数是节点数减 1，即| E | = L+I–1。

给定树类型中除根之外的所有内部节点都具有 k + 1 度。根的度数是 k。所有的叶子都是 1 度。将握手引理应用于这样的树，我们得到以下关系。

```
  Sum of all degrees  = 2 * (Sum of Edges)

  Sum of degrees of leaves + 
  Sum of degrees for Internal Node except root + 
  Root's degree = 2 * (No. of nodes - 1)

  Putting values of above terms,   
  L + (I-1)*(k+1) + k = 2 * (L + I - 1) 
  L + k*I - k + I -1 + k = 2*L  + 2I - 2
  L + K*I + I - 1 = 2*L + 2*I - 2
  K*I + 1 - I = L
  (K-1)*I + 1 = L   
```

所以上面的性质是用握手引理证明的，让我们讨论一个更有趣的性质。

**交替证明:**(不使用握手定理)
由于有 I 个内部节点，每个节点都有 K 个子节点，因此树中的子节点总数= K * I

有 I-1 个内部节点是某个其他节点的子节点(根已被排除，因此比内部节点总数少一个)

也就是说，在这些 K*I 子节点中，I-1 是内部节点，因此其余的(K * I –( I-1))是叶子。

因此 L = (K-1)*I + 1。

***2)在二叉树中，*** ***的叶节点数总是比有两个子节点的节点多一个。***

```
   L = T + 1
Where L = Number of leaf nodes
      T = Number of internal nodes with two children 
```

**证明:**
让若干个有 2 个孩子的节点都是 t .证明可以分为三种情况。

***情况 1:*** 只有一个节点，关系成立
为 T = 0，L = 1。

***例 2:*** Root 有两个孩子，即 Root 的度数为 2。

```
   Sum of degrees of nodes with two children except root + 
   Sum of degrees of nodes with one child + 
   Sum of degrees of leaves + Root's degree = 2 * (No. of Nodes - 1)   

   Putting values of above terms,
   (T-1)*3 + S*2 + L + 2 = (S + T + L - 1)*2

   Cancelling 2S from both sides.
     (T-1)*3 + L + 2 = (T + L - 1)*2
     T - 1 = L - 2
     T = L - 1 
```

***例 3:*** 根有一子，即根的度数为 1。

```
   Sum of degrees of nodes with two children + 
   Sum of degrees of nodes with one child except root + 
   Sum of degrees of leaves + Root's degree = 2 * (No. of Nodes - 1)   

   Putting values of above terms,
   T*3 + (S-1)*2 + L + 1 = (S + T + L - 1)*2

   Cancelling 2S from both sides.
     3*T + L -1 = 2*T + 2*L - 2
     T - 1 = L - 2
     T = L - 1 
```

因此，在所有三种情况下，我们得到 T = L-1。

我们用握手引理讨论了树的两个重要性质的证明。很多关于这些属性的 GATE 问题被问到，以下是一些链接。

[GATE-CS-2015(第 3 集)|问题 35](http://geeksquiz.com/gate-gate-cs-2015-set-3-question-35/)
[GATE-CS-2015(第 2 集)|问题 20](http://geeksquiz.com/gate-gate-cs-2015-set-2-question-20/)
[GATE-CS-2005 |问题 36](http://geeksquiz.com/gate-gate-cs-2005-question-36/)
[GATE-CS-2002 |问题 34](http://geeksquiz.com/gate-gate-cs-2010-question-12/)
[GATE-CS-2007 |问题 43](http://geeksquiz.com/gate-gate-cs-2007-question-43/)

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息