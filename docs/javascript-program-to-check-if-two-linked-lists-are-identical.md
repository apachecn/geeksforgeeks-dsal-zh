# 检查两个链表是否相同的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序检查两个链表是否相同/](https://www.geeksforgeeks.org/javascript-program-to-check-if-two-linked-lists-are-identical/)

当两个链表具有相同的数据并且数据的排列也相同时，它们是相同的。例如，链表 a (1->2->3)和 b(1->2->3)是相同的。。编写一个函数来检查给定的两个链表是否相同。

**方法(递归):**
递归求解代码比迭代代码干净得多。然而，您可能不想将递归版本用于生产代码，因为它将使用与列表长度成比例的堆栈空间。

## java 描述语言

```
<script>
// A recursive javascript method to check if 
// two linked lists are identical or not
function areIdenticalRecur(a,  b)
{
    // If both lists are empty
    if (a == null && b == null)
        return true;

    // If both lists are not empty, then 
    // data of current nodes must match, 
    // and same should be recursively true 
    // for rest of the nodes.
    if (a != null && b != null)
        return (a.data == b.data) &&
               areIdenticalRecur(a.next, b.next);

    // If we reach here, then one of the lists
    // is empty and other is not
    return false;
}

/* Returns true if linked lists a and b 
   are identical, otherwise false */
function areIdentical( listb)
{
    return areIdenticalRecur(this.head, 
                             listb.head);
}
// This code contributed by aashish1995 
</script>
```

**时间复杂度:** O(n)对于迭代和递归版本。n 是 a 和 b 中较小列表的长度。

更多详情请参考[完全相同链表](https://www.geeksforgeeks.org/identical-linked-lists/)的完整文章！