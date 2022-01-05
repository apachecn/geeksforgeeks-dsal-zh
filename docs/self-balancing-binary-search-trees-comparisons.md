# 自平衡-二进制-搜索-树(比较)

> 原文:[https://www . geesforgeks . org/自平衡-二进制-搜索-树-比较/](https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/)

**自平衡二分搜索法树**是 ***高度平衡*** 二分搜索法树，在对树进行插入和删除操作时，自动保持高度尽可能小。高度通常保持在对数 n 的数量级，因此所有操作平均花费 O(对数 n)个时间。

**例:**
红黑树

![Red Black Tree](img/c7f0376aba91d7d4c88da1179f9d1da8.png)

AVL 树:

![](img/91e12578c30fe537b93f04e4aa19d1c7.png)

**语言实现:** [在 C++ STL 中设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)和[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。Java 中的 [TreeSet](https://www.geeksforgeeks.org/treeset-in-java-with-examples/) 和 [TreeMap](https://www.geeksforgeeks.org/treemap-in-java/) 。大多数库实现使用红黑树。Python 标准库不支持自平衡 BST。在 Python 中，我们可以使用[平分](https://www.geeksforgeeks.org/bisect-algorithm-functions-in-python/)模块来保存一组排序后的数据。我们也可以使用像 [rbtree](https://pypi.org/project/rbtree/) (红黑树的实现)和[pyavl](https://pypi.org/project/pyavl/)(AVL 树的实现)这样的 PyPi 模块。

**自平衡树如何保持高度？**
树木做的一个典型操作就是轮换。以下是可以执行的两个基本操作，以在不违反 BST 属性的情况下重新平衡 BST(键(左)<键(根)<键(右))。
1)左旋转
2)右旋转

```
T1, T2 and T3 are subtrees of the tree 
rooted with y (on the left side) or x (on 
the right side)           
     y                               x
    / \     Right Rotation          /  \
   x   T3   - - - - - - - >        T1   y 
  / \       < - - - - - - -            / \
 T1  T2     Left Rotation            T2  T3
Keys in both of the above trees follow the 
following order 
 keys(T1) < key(x) < keys(T2) < key(y) < keys(T3)
So BST property is not violated anywhere.
```

我们已经讨论过 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)、[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)和[八字树](https://www.geeksforgeeks.org/splay-tree-set-2-insert-delete/)。在本文中，我们将比较这些树的效率:

<figure class="table">

| 公制的 | RB 树 | 树 | 张开树 |
| --- | --- | --- | --- |
| **插入**
**最坏情况** | **O(1)** | **O(logn)** | **摊余 O(logn)** |
| **树的最大高度**
 | **2*log(n)** | **1.44*log(n)** | **O(n)** |
| **搜索**
**最坏情况** | **O(logn)**T2**中等** | **O(logn)**T2**更快** | **摊销 O(logn)**T2**较慢** |
| **高效实施需要** | **每个节点有一个颜色位的三个指针** | **每个**
**节点有两个带平衡因子的指针** | **只有两个指针跟**
**没有多余信息** |
| **删除在**
**最坏的情况下** | **O(logn)** | **O(logn)** | **摊余 O(logn)** |
| **常用** | **作为通用数据结构** | **需要频繁查找时** | **当同一元素被**
**一次又一次地取回** |
| **真实世界应用** | **数据库事务** | **多集、多地图、地图、集合等。** | **缓存实现，垃圾收集算法** |

</figure>