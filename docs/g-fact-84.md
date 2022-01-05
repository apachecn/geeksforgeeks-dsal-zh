# 插值搜索 vs 二分搜索法

> 原文:[https://www.geeksforgeeks.org/g-fact-84/](https://www.geeksforgeeks.org/g-fact-84/)

[插值搜索](http://en.wikipedia.org/wiki/Interpolation_search)对于排序的和**均匀分布的**数组比二分搜索法效果更好。

不管搜索关键字是什么，二分搜索法都会去中间元素进行检查。另一方面，插值搜索可以根据搜索关键字去不同的位置。如果搜索关键字的值接近最后一个元素，插值搜索可能会开始向末端搜索。

平均而言，插值搜索会进行 log(log(n))比较(如果元素均匀分布)，其中 n 是要搜索的元素数量。在最坏的情况下(例如，键的数值呈指数增长)，它可以进行多达 O(n)次比较。

[插值搜索文章](https://www.geeksforgeeks.org/interpolation-search/)

**来源:**T2[http://en.wikipedia.org/wiki/Interpolation_search](http://en.wikipedia.org/wiki/Interpolation_search)