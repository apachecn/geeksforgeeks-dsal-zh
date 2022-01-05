# 徒步采访体验|第五集

> 原文:[https://www . geesforgeks . org/hike-面试-体验-设置-5/](https://www.geeksforgeeks.org/hike-interview-experience-set-5/)

第一轮
1。实现过期缓存系统:缓存中的每一页都有 id 和过期时间(几秒钟的 TTL)。页面过期后，它表现为可用空间，可用于新页面/替换。对一切都进行了长时间的讨论。

第二回合
很无聊的回合
1。[二叉树中给定距离的节点](https://practice.geeksforgeeks.org/problems/nodes-at-given-distance-in-binary-tree/1)
2。[检查 N 元树中的镜像](https://practice.geeksforgeeks.org/problems/check-mirror-in-n-ary-tree/0)
3。[最大和邻接子阵](https://practice.geeksforgeeks.org/problems/kadanes-algorithm/0)
圆三
很无聊的圆
1。[逐行层次顺序遍历](https://practice.geeksforgeeks.org/problems/level-order-traversal-line-by-line/1)
2。[树的之字形遍历](https://practice.geeksforgeeks.org/problems/zigzag-tree-traversal/1)
3。[旋转阵列搜索](https://practice.geeksforgeeks.org/problems/search-in-a-rotated-array/0)
4。[值等于指数值](https://practice.geeksforgeeks.org/problems/value-equal-to-index-value/0)
终于有新东西了..
5。给定一个排序数组，比如 A : (-4，-2，0，1，4，6，8，10)。有一个函数 f(x) = a*x^2 + b*x + c，把这个函数应用在 a 上，其中 x 是数组 a 中的任意一个元素，a，b，c 属于一组实数。将对 f(A)进行排序，如果没有，则在 O(n)中进行排序。
如果你还记得数学中二次方程的概念，那就很容易了。我不记得了，所以他帮助了我。
逻辑是任何二次方程在图上用抛物线表示，图在 dy/dx = 0 处有最小值，即 2*a*x + b = 0。这个点图的两边根据 a 的值不断增加/减少到无穷大。计算 x = -b/(2*a)的值。在排序数组中找到它，或者在 log n 中找到它的上限，从这一点开始到两端，执行合并排序。

第四轮
1。[实行](https://practice.geeksforgeeks.org/problems/lru-cache/1)LRU 缓存
2。实施以下措施。
请求有三种类型:
I)[www.someurl.com/conn_id=?&<wbr>超时=](http://www.someurl.com/conn_id=?&timeout=) ？-:对于此 conn_id，您将等待超时秒，在此之后返回响应，同时您可以获得三种类型中任意一种的更多请求
ii)[www.someurl.com/stat/](http://www.someurl.com/stat/)-:返回所有等待超时的 id 及其剩余的超时间隔
ii)[www.someurl.com/kill/conn_id=](http://www.someurl.com/kill/conn_id=)？-:结束此 conn_id 的等待超时，并返回此 conn_id 的响应

我用 heap 给出了一个解决方案。当一个请求在等待提莫的时候，他问如何处理，同时新的请求来了。在这种情况下如何做到服务器端的可扩展性。

3.他询问了我目前的工作和技术。我说 Java，后端是 Spring MVC，前端是 html、css、javascript，突然他问 Java 和 javascript 有什么区别。当时想不出来。Javascript 也是一种面向对象的语言，可以像 node js 一样在服务器端使用。还是有很多不同。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论

## 相关实践问题

[Two Mirror Trees](https://practice.geeksforgeeks.org/problems/two-mirror-trees/1)[Level order traversal Line by Line](https://practice.geeksforgeeks.org/problems/level-order-traversal-line-by-line/1)[Nodes at given distance in binary tree](https://practice.geeksforgeeks.org/problems/nodes-at-given-distance-in-binary-tree/1)[LRU Cache](https://practice.geeksforgeeks.org/problems/lru-cache/1)[Search in a Rotated Array](https://practice.geeksforgeeks.org/problems/search-in-a-rotated-array/0)[Level order traversal in spiral form](https://practice.geeksforgeeks.org/problems/level-order-traversal-in-spiral-form/1)[Kadane’s Algorithm](https://practice.geeksforgeeks.org/problems/kadanes-algorithm/0)[All Practice Problems for Hike](https://practice.geeksforgeeks.org/company/Hike/) !