# 哈希的应用

> 原文：[https://www.geeksforgeeks.org/applications-of-hashing/](https://www.geeksforgeeks.org/applications-of-hashing/)

在本文中，我们将讨论[哈希](https://www.geeksforgeeks.org/hashing-set-1-introduction/)的应用。

哈希平均提供恒定时间的搜索，插入和删除操作。 这就是为什么散列是最常用的数据结构之一的原因，示例问题包括[不同的元素](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)，计数项目的频率，查找重复项等。

哈希还有许多其他应用，包括现代密码学哈希函数。 下面列出了其中一些应用：

*   信息摘要

*   密码验证

*   数据结构（编程语言）

*   编译器操作

*   拉宾·卡普算法

*   将文件名和路径链接在一起

**消息摘要**：

这是加密哈希函数的应用。 密码散列函数是产生输出的函数，从该输出到达输入几乎是不可能的。 哈希函数的此属性称为**不可逆**。

让我们举一个**示例**：

假设您必须将文件存储在任何可用的云服务上。 您必须确保所存储的文件未被任何第三方篡改。 您可以通过使用加密哈希算法计算该文件的“哈希”来实现。 常见的密码哈希算法之一是 **SHA 256**。 这样计算出的散列的最大大小为 32 个字节。 因此，计算大量文件的哈希将不会有问题。 您可以将这些哈希保存在本地计算机上。

现在，当您下载文件时，您将再次计算哈希值。 然后将其与先前计算的哈希值匹配。 因此，您知道您的文件是否被篡改。 如果有人篡改该文件，则该文件的哈希值肯定会发生变化。 在不更改哈希值的情况下篡改文件几乎是不可能的。

**密码验证**

密码哈希函数在密码验证中非常常用。 让我们用**示例**来了解这一点：

当您使用任何需要用户登录的在线网站时，请输入电子邮件和密码以验证您尝试使用的帐户属于您。 输入密码后，将计算出密码的哈希值，然后将其发送到服务器以验证密码。 存储在服务器上的密码实际上是原始密码的计算得出的哈希值。 这样做是为了确保当密码从客户端发送到服务器时，不会出现嗅探。

**数据结构（编程语言）**：

各种编程语言都有基于哈希表的数据结构。 基本思想是创建一个键值对，其中键应该是唯一值，而不同键的值可以相同。 在 C++ 中的`unordered_set`和`unordered_map`，Java 中的`HashSet`和`HashMap`，Python 中的`dict`等中可以看到此实现。

**编译器操作**：

编程语言的关键字与其他标识符的处理方式不同。 为了区分编程语言的关键字（如果是，用于返回等）和其他标识符并成功地编译程序，编译器将所有这些关键字存储在使用哈希表实现的集合中。

**Rabin-Karp 算法**：

哈希最著名的应用之一是 Rabin-Karp 算法。 这基本上是一个字符串搜索算法，它使用哈希来查找字符串中的任何一组模式。 该算法的实际应用是检测抄袭。 要了解有关 Rabin-Karp 算法的更多信息，请浏览[系列 3（Rabin-Karp 算法）](https://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/)。

**将文件名和路径链接在一起**：

在本地系统上浏览文件时，我们观察到文件的两个非常关键的组成部分，即`file_name`和`file_path`。 为了存储`file_name`和`file_path`之间的对应关系，系统使用通过哈希表实现的`map(file_name, file_path)`。

**相关文章**：

 [哈希 vs BST](https://www.geeksforgeeks.org/advantages-of-bst-over-hash-table/) [哈希 vs Trie](https://www.geeksforgeeks.org/advantages-trie-data-structure/)



* * *

* * *



