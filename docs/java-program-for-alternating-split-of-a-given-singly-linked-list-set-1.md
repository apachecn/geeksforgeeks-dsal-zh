# 交替分割给定单链表的 Java 程序-集合 1

> 原文:[https://www . geeksforgeeks . org/Java-program-for-alternative-split-of-给定-single-link-list-set-1/](https://www.geeksforgeeks.org/java-program-for-alternating-split-of-a-given-singly-linked-list-set-1/)

编写一个函数 AlternatingSplit()，该函数取一个列表，并将其节点划分为两个较小的列表“a”和“b”。子列表应该由原始列表中的交替元素组成。因此，如果原始列表是 0->1->0->1->0->1，那么一个子列表应该是 0->0->0，另一个应该是 1->1->1。

**方法(使用虚拟节点):**
这是一种按照与源列表相同的顺序构建子列表的方法。代码在构建“a”和“b”列表时使用临时伪标题节点。每个子列表都有一个指向其当前最后一个节点的“尾部”指针，这样新节点就可以很容易地附加到每个列表的末尾。虚拟节点给尾部指针一些初始指向的东西。在这种情况下，虚拟节点是有效的，因为它们是临时的，并在堆栈中分配。或者，可以使用本地“引用指针”(总是指向列表中的最后一个指针，而不是最后一个节点)来避免虚拟节点。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
static void AlternatingSplit(Node source, 
                             Node aRef, 
                             Node bRef) 
{
    Node aDummy = new Node();

    // Points to the last node in 'a' 
    Node aTail = aDummy; 
    Node bDummy = new Node();

    // Points to the last node in 'b' 
    Node bTail = bDummy; 
    Node current = source;
    aDummy.next = null;
    bDummy.next = null;
    while (current != null) 
    {
       // Add at 'a' tail
        MoveNode((aTail.next), 
                  current); 

        // Advance the 'a' tail 
        aTail = aTail.next; 
        if (current != null) 
        {
            MoveNode((bTail.next), 
                      current);
            bTail = bTail.next;
        }
    }
    aRef = aDummy.next;
    bRef = bDummy.next;
}
// This code is contributed by rutvik_56
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。
来源:[http://cslibrary.stanford.edu/105/LinkedListProblems.pdf](http://cslibrary.stanford.edu/105/LinkedListProblems.pdf)
更多详情请参考完整文章[给定单链表的交替拆分|集合 1](https://www.geeksforgeeks.org/alternating-split-of-a-given-singly-linked-list/) ！