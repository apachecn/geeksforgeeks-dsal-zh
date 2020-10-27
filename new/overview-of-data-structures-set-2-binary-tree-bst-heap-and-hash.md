# 数据结构概述| 第 2 组（二叉树，BST，堆和哈希）

我们已经讨论了[数组，链接列表，队列和堆栈的概述](https://www.geeksforgeeks.org/overview-of-data-structures-set-1-linear-data-structures/)。 在本文中，将讨论以下数据结构。

[**5.二进制树**](#code5) [
[**6.二进制搜索树**](#code6)
[**7.二进制堆[**](#code7) ，
[**9.散列**](#code9)

**二叉树**
与数组，链接列表，堆栈和队列（它们是线性数据结构）不同，树是分层数据结构。
二叉树是一种树数据结构，其中每个节点最多具有两个子节点，称为左子节点和右子节点。 它主要使用链接来实现。

**二叉树表示形式：**一棵树由指向树中最高节点的指针表示。 如果树为空，则 root 的值为 NULL。 二叉树节点包含以下部分。
1.数据
2.指向左孩子的指针
3.指向右孩子的指针

可以通过两种方式遍历二叉树：
深度优先遍历：有序（左-右-根），前序（根-左-右）和后序（左-右-根）
广度优先遍历： 级别顺序遍历

**二叉树属性：**

```
The maximum number of nodes at level ‘l’ = 2l-1.

Maximum number of nodes = 2h + 1 – 1.
Here h is height of a tree. Height is considered 
as the maximum number of edges on a path from root to leaf.

Minimum possible height =  ceil(Log2(n+1)) - 1  

In Binary tree, number of leaf nodes is always one 
more than nodes with two children.

Time Complexity of Tree Traversal: O(n)

```

**示例：**通常使用二叉树或二叉树的一个原因是为了形成层次结构。 它们在文件结构中很有用，其中每个文件都位于特定目录中，并且存在与文件和目录关联的特定层次结构。 使用树的另一个示例是存储分层对象，例如 JavaScript 文档对象模型，将 HTML 页面视为一棵树，其中标签嵌套作为父子关系。

**二进制搜索树**。
在二进制搜索树中是具有以下附加属性的二进制树：
1.节点的左子树仅包含键值小于节点键值的节点。
2.节点的右子树仅包含键大于节点键的节点。
3.左子树和右子树也必须都是二进制搜索树。

时间复杂度：

```
Search :  O(h)
Insertion : O(h)
Deletion : O(h)
Extra Space : O(n) for pointers

h: Height of BST
n: Number of nodes in BST

If Binary Search Tree is Height Balanced, 
then h = O(Log n) 

Self-Balancing BSTs such as AVL Tree, Red-Black
Tree and Splay Tree make sure that height of BST 
remains O(Log n)

```

BST 提供适度的访问/搜索（比“链表”更快，比阵列慢）。
BST 提供适度的插入/删除（比 Array 更快，比 Linked List 慢）。

**示例：**它的主要用途是在搜索应用程序中，在该应用程序中，数据不断进入/离开，并且需要按排序顺序打印数据。 例如，在电子商务网站的实施中，其中添加了新产品或产品缺货，并且所有产品均按排序顺序列出。

**二进制堆**，
二进制堆是具有以下属性的二进制树。
1）这是一棵完整的树（除了最后一个级别，所有级别都已完全填充，并且最后一个级别的所有键都尽可能保留）。 Binary Heap 的此属性使它们适合存储在数组中。
2）二进制堆是“最小堆”或“最大堆”。 在最小二进制堆中，在二进制堆中存在的所有密钥中，根密钥必须最小。 对于二叉树中的所有节点，相同的属性必须递归地为 true。 最大二进制堆类似于最小堆。 它主要使用数组来实现。

```
Get Minimum in Min Heap: O(1) [Or Get Max in Max Heap]
Extract Minimum Min Heap: O(Log n) [Or Extract Max in Max Heap]
Decrease Key in Min Heap: O(Log n)  [Or Decrease Key in Max Heap]
Insert: O(Log n) 
Delete: O(Log n)

```

**示例：**用于实现高效的优先级队列，而这些优先级队列又用于调度操作系统中的进程。 优先队列也用于 Dijikstra 和 Prim 的图算法中。
Heap 数据结构可用于有效地查找数组中的 k 个最小（或最大）元素，合并 k 个排序的数组，流的中位数等。
Heap 是一种特殊的数据结构，不能 用于搜索特定元素。

**HashingHash 函数：**将给定的大输入键转换为较小的实用整数值的函数。 映射的整数值用作哈希表中的索引。 良好的哈希函数应具有以下属性
1）有效地可计算。
2）应该均匀分配键（每个表在每个键上的位置可能性均等）

哈希表：一个数组，用于存储指向与给定电话号码对应的记录的指针。 如果没有现有电话号码的哈希函数值等于该条目的索引，则哈希表中的条目为 NIL。

冲突处理：由于哈希函数会为我们提供一个较小的数字，而该键是一个大整数或字符串，因此两个键可能会产生相同的值。 新插入的键映射到哈希表中已经占用的插槽的情况称为冲突，必须使用某种冲突处理技术来处理。 以下是处理冲突的方法：

链接：想法是使哈希表的每个单元指向具有相同哈希函数值的记录的链表。 链接很简单，但是需要在表外增加内存。
开放式寻址：在开放式寻址中，所有元素都存储在哈希表本身中。 每个表条目都包含一条记录或 NIL。 在搜索元素时，我们将逐个检查表插槽，直到找到所需的元素，或者很明显该元素不在表中。

```
Space : O(n)
Search    : O(1) [Average]    O(n) [Worst case]
Insertion : O(1) [Average]    O(n) [Worst Case]
Deletion  : O(1) [Average]    O(n) [Worst Case]

```

对于所有操作，散列似乎比 BST 更好。 但是在散列中，元素是无序的，而在 BST 中，元素是以有序的方式存储的。 同样，BST 易于实现，但是散列函数的生成有时可能非常复杂。 在 BST 中，我们还可以有效地找到价值的底线和底线。

**示例：**散列可用于从一组元素中删除重复项。 也可以用来查找所有项目的频率。 例如，在 Web 浏览器中，我们可以使用哈希检查访问的 URL。 在防火墙中，我们可以使用哈希检测垃圾邮件。 我们需要对 IP 地址进行哈希处理。 在 O（1）时间内需要 search（）insert（）和 delete（）的任何情况下都可以使用散列。

本文由 **Abhiraj Smit** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

