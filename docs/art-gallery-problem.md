# 美术馆问题

> 原文:[https://www.geeksforgeeks.org/art-gallery-problem/](https://www.geeksforgeeks.org/art-gallery-problem/)

**<u>问题描述</u> :**

**美术馆问题**在几何学中被表述为需要放置在一个 n 顶点简单多边形中的最小数量的守卫，这样内部的所有点都是可见的。简单多边形是一个连通的封闭区域，其边界由有限数量的线段定义。它是计算几何中一系列相关的**问题。如果连接两个点的线段位于多边形内，则可见性定义为两个点 **u** 和 **v** 相互可见。这里，我们讨论几个变体。下面讨论的变体中常用的术语:**

***   A simple (not necessarily convex) polygon **p** is used to describe the art gallery.*   A set of points **s** are used to describe the guards, in which each guard consists of **p.**T21】中的一个点来表示一个规则一个点 **A ∈ S** 可以守卫另一个点 **B ∈ P** 当且仅当 **A ∈ S** 、 **B ∈ P** 和线段 **AB****

**这个**美术馆问题**的很多变体被归类为 [NP 难问题](https://www.geeksforgeeks.org/difference-between-np-hard-and-np-complete-problem/)。在这里，我们将重点介绍那些承认多项式解的:**

***   Variant 1: Determine the upper limit of the minimum size of the set ***s*** .*   Variant 2: Determine a critical point **C** and another point *T22] D ∈ p *of in polygon **P** **if the guard is in the position of **C*********   Variant 3: Determine whether polygon **p** can be guarded by only one guard.*   Variant 4: If the guard can only be placed at the vertex **p** of the polygon and only need to guard the vertex, then determine the minimum size of the set **s** .****

***请注意，还有很多变体，至少已经为其编写了一本书。***

*****<u>解</u> :*****

****   The solution of variant 1 is the theoretical work of the museum theorem of **v aclav chvatal** . He pointed out that [N/3] guards are always enough and sometimes necessary to guard a simple polygon with n vertices.*   The solution of variant 2 includes testing whether the polygon **p** is concave (and therefore has a critical point). We can use the negative isconvex function of T2.*   If you haven't seen the solution of variant 3 before, it may be difficult. We can use the function of **cutting polygons** . We cut the polygon **p** counterclockwise with all the lines formed by the edges in **p** , and always keep the left side. If we still have a non-empty polygon at the end, we can put a guard in that non-empty polygon to protect the whole polygon **p** .*   The solution of variant 4 involves the calculation of the minimum vertex cover of the "visible graph" of polygon **p** . Generally speaking, this is another **NP-hard problem** .***