# 在包含父节点指针的 AVL 树中插入、搜索和删除

> 原文:[https://www . geesforgeks . org/AVL-trees-containing-a-parent-node-pointer/](https://www.geeksforgeeks.org/avl-trees-containing-a-parent-node-pointer/)

[AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)是自平衡的 [**二叉查找树(BST)**](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) 其中左右子树的高度差对于所有节点不能超过一。 **AVL 树**中的**插入和删除已经在[上一篇文章](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)中讨论过。在本文中，插入、搜索和删除操作在 AVL 树上进行讨论，这些树的[结构](https://www.geeksforgeeks.org/structures-c/)中也有一个父指针。**

AVL 树节点定义:

## c++

```
struct AVLwithparent {

    // Pointer to the left and the
    // right subtree
    struct AVLwithparent* left;
    struct AVLwithparent* right;

    // Stores the data in the node
    int key;

    // Stores the parent pointer
    struct AVLwithparent* par;

    // Stores the height of the
    // current tree
    int height;
}
```

**输出:**

```
Node: 30, Parent Node: NULL
Node: 20, Parent Node: 30
Node: 10, Parent Node: 20
Node: 25, Parent Node: 20
Node: 40, Parent Node: 30
Node: 50, Parent Node: 40

```