# 使用后缀树进行模式搜索

> 原文:[https://www . geesforgeks . org/pattern-search-use-后缀-tree/](https://www.geeksforgeeks.org/pattern-searching-using-suffix-tree/)

给定文本 txt[0..n-1]和模式 pat[0..m-1]，编写一个函数搜索(char pat[]，char txt[])，打印出所有出现在 txt[]中的 pat[]。你可以假设 n > m。

**预处理模式还是预处理文本？**
我们在之前的帖子里讨论过以下算法:

[KMP 算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)
[拉宾卡普算法](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)
[基于有限自动机的算法](https://www.geeksforgeeks.org/finite-automata-algorithm-for-pattern-searching/)
[博耶摩尔算法](https://www.geeksforgeeks.org/pattern-searching-set-7-boyer-moore-algorithm-bad-character-heuristic/)

所有上述算法都对模式进行预处理，以加快模式搜索速度。我们可以通过预处理模式得到的最佳时间复杂度是 O(n)，其中 n 是文本的长度。在这篇文章中，我们将讨论一种预处理文本的方法。后缀树是由文本构建的。在对文本进行预处理(构建文本后缀树)后，我们可以在 O(m)时间内搜索任何模式，其中 m 是模式的长度。
假设你已经存储了威廉·莎士比亚的完整作品并对其进行了预处理。你可以在整个作品中搜索任意字符串，搜索时间与模式的长度成正比。这确实是一个很大的改进，因为模式的长度通常比文本小得多。
如果文本频繁变化，文本的预处理可能会变得昂贵。但对于固定文本或不太频繁更改的文本来说，这是很好的。

**给定文本的后缀树是给定文本所有后缀的压缩树**。我们已经讨论了[标准特里](https://www.geeksforgeeks.org/trie-insert-and-search/)。让我们用以下一系列单词来理解**压缩的特里**。

```
{bear, bell, bid, bull, buy, sell, stock, stop}
```

以下是上述输入单词集的标准 trie。
![](img/90275ba5451b917cebf3ad36e742a3b1.png "standardtrie")

下面是压缩的 trie。压缩 trie 是通过连接单个节点的链从标准 Trie 获得的。压缩 trie 的节点可以通过在节点上存储索引范围来存储。
![](img/82ca45060bc484dbf1dcebb2c4a911a8.png "Compressed Trie")

**如何为给定的文本建立后缀树？**
如上所述，后缀树是所有后缀的压缩特里，所以下面是从给定文本构建后缀树的非常抽象的步骤。
1)生成给定文本的所有后缀。
2)将所有后缀视为单个单词，并构建一个压缩的 trie。

让我们考虑一个示例文本“香蕉\0”，其中“\0”是字符串终止字符。以下是“香蕉\0”的所有后缀

```
banana\0
anana\0
nana\0
ana\0
na\0
a\0
\0
```

如果我们把上面所有的后缀都看作是单独的单词，并建立一个 trie，我们会得到如下结果。
![](img/a06f9da5749449d790f3698d534d999c.png "suffixtrie")

如果我们加入单个节点的链，我们会得到下面的压缩 trie，它是给定文本“香蕉\ 0”
![](img/4b6388ce3c0907eda180743cb0036087.png "suffix tree")的后缀树

请注意，以上步骤只是手动创建后缀树。我们将在另一篇文章中讨论实际的算法和实现。

**如何在构建的后缀树中搜索模式？**
我们已经在上面讨论了如何构建后缀树，它是模式搜索中的预处理步骤。以下是在构建的后缀树中搜索模式的抽象步骤。
**1)** 从模式的第一个字符和后缀树的根开始，对每个字符执行以下操作。
….. **a)** 对于模式的当前字符，如果后缀树的当前节点有一条边，则跟随该边。
….. **b)** 如果没有边缘，打印“文字中不存在图案”并返回。
**2)** 如果模式的所有字符都已处理，即给定模式的字符从根有一个路径，则打印“模式找到”。

让我们将示例模式视为“nan”来查看搜索过程。下图显示了搜索“nan”或“nana”所遵循的路径。

![](img/c61555ab218c0ae79dd304c477014f71.png "suffixTreeSearch")

**这是如何工作的？**
文本中存在的每个模式(或者我们可以说文本的每个子串)都必须是所有可能后缀之一的前缀。这个说法看似复杂，其实是一个简单的说法，我们只需要举个例子来检验它的有效性。

**后缀树的应用**
后缀树可以用于各种各样的问题。以下是后缀树提供最佳时间复杂度解决方案的一些著名问题。
1) [模式搜索](https://www.geeksforgeeks.org/suffix-tree-application-2-searching-all-patterns/)
2) [寻找最长的重复子串](http://en.wikipedia.org/wiki/Longest_repeated_substring_problem)
3) [寻找最长的公共子串](http://en.wikipedia.org/wiki/Longest_common_substring_problem)
4) [寻找字符串中最长的回文](http://en.wikipedia.org/wiki/Longest_palindromic_substring)

还有很多其他的应用。详见[本](http://en.wikipedia.org/wiki/Suffix_tree#Functionality)。

Ukkonen 的后缀树构造将在以下文章中讨论:
[Ukkonen 的后缀树构造–第 1 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-1/ "Ukkonen’s Suffix Tree Construction – Part 1")
[Ukkonen 的后缀树构造–第 2 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-2/ "Ukkonen’s Suffix Tree Construction – Part 2")
[Ukkonen 的后缀树构造–第 3 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-3/ "Ukkonen’s Suffix Tree Construction – Part 3")
[Ukkonen 的后缀树构造–第 4 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-4/ "Ukkonen’s Suffix Tree Construction – Part 4")
T13】Ukkonen 的后缀树构造–第 5 部分
[Ukkonen 的后缀树构造](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-6/ "Ukkonen’s Suffix Tree Construction – Part 6")

**参考文献:**
[http://fbim . FH-regensburg . de/~ saj 39122/sal/skript/progr/pr 45102/trys . pdf](http://fbim.fh-regensburg.de/~saj39122/sal/skript/progr/pr45102/Tries.pdf)
[http://www.cs.ucf.edu/~shzhang/Combio12/lec3.pdf](http://www.cs.ucf.edu/~shzhang/Combio12/lec3.pdf)
[http://www.allisons.org/ll/AlgDS/Tree/Suffix/](http://www.allisons.org/ll/AlgDS/Tree/Suffix/)