# 反向索引与正向索引之间的差异

> 原文：[https://www.geeksforgeeks.org/difference-inverted-index-forward-index/](https://www.geeksforgeeks.org/difference-inverted-index-forward-index/)

[**反向索引**](https://www.geeksforgeeks.org/inverted-index/)

1.  它是一种数据结构，用于存储从单词到文档或文档集的映射，即从单词到文档的指导。

2.  建立反向索引的步骤是：

    *   提取文档并收集所有单词。

    *   检查每个单词（如果存在），然后将文档引用添加到索引，否则在该单词的索引中创建新条目。

    *   对所有文档重复上述步骤，并对单词进行排序。

3.  索引很慢，因为它首先检查单词是否存在。

4.  搜索非常快。

5.  Example of Inverted index:

    ```
    Word                              Documents
    hello                             doc1      
    sky                               doc1, doc3
    coffee                            doc2
    hi                                doc2
    greetings                         doc3                               

    ```

    它不会在索引中存储重复的关键字。

6.  现实生活中反向索引的示例：

    *   书后的索引。

    *   反向查询。

**前向索引**：

1.  它是一种数据结构，用于存储从文档到单词的映射，即引导您从文档到单词。

2.  建立前进索引的步骤是：

    *   提取文档并收集所有关键字。

    *   在此文档的索引条目中附加所有关键字。

    *   对所有文档重复上述步骤。

3.  索引编制非常快，因为它向前移动时仅附加关键字。

4.  搜索非常困难，因为它必须查看索引的每个内容才能检索与单词相关的所有页面。

5.  Example of forward index:

    ```
    Document                          Keywords
    doc1                              hello, sky, morning      
    doc2                              tea, coffee, hi
    doc3                              greetings, sky

    ```

    它在索引中存储重复的关键字。 例如：单词`"sky"`被多次存储。

6.  现实生活中的前向索引示例：

    *   书中的目录。

    *   DNS 查询。

**正向索引和反向索引之间的相似性**：

*   两者都用于搜索文档或文档集中的文本。



* * *

* * *



