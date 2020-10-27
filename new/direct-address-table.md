# 直接地址表

直接地址表是一种数据结构，具有使用数组将记录映射到其相应键的功能。 在直接地址表中，将记录的键值直接用作索引来放置记录。 它们有助于快速搜索，插入和删除操作。

我们可以使用以下示例来理解该概念。 我们创建一个大小等于最大值加一的数组（假定索引从 0 开始），然后将值用作索引。 例如，在下图中，键 21 直接用作索引。
![hmap](img/4e06d738a8e7231aa5777c93111a94c2.png)

**优势：**

1.  **在 O（1）时间中搜索：**直接地址表使用的数组是随机访问数据结构，因此，键值（也是数组的索引）可以很容易地用于在其中搜索记录 O（1）时间。
2.  **插入 O（1）时间：**我们可以轻松地在 O（1）时间将元素插入数组。 同样的事情也出现在直接地址表中。
3.  **的 O（1）时间删除：**元素的删除在数组中需要 O（1）时间。 同样，要删除直接地址表中的元素，我们需要 O（1）时间。

**局限性：**

1.  事先知道最大键值
2.  仅当最大值非常小时才实用。
3.  如果总记录和最大值之间存在显着差异，则会导致内存空间浪费。

[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以克服直接地址表的这些限制。

**如何处理碰撞？**
可以像哈希一样处理冲突。 我们可以使用[链接](https://www.geeksforgeeks.org/hashing-set-2-separate-chaining/)或[开放式寻址](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)来处理冲突。 与哈希的唯一区别在于，我们不使用哈希函数来查找索引。 我们宁愿直接使用值作为索引。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。