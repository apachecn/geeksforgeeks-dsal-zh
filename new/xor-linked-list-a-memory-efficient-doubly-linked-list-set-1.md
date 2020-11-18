# XOR链表–内存有效的双链表| 设置1

普通的双向链接列表需要两个地址字段的空间来存储上一个和下一个节点的地址。 可以仅对每个节点使用一个空间作为地址字段来创建内存高效版本的双链表。 这种高效的内存双链表称为XOR链表或内存高效，因为该表使用按位XOR操作来节省一个地址的空间。 在XOR链接列表中，每个节点不存储实际的内存地址，而是存储上一个和下一个节点的地址的XOR。

[![](img/37893f21aca278041b130165ec847a26.png "doublyll")](https://media.geeksforgeeks.org/wp-content/uploads/XorLinkedList.jpg)

考虑上面的双链表。 以下是双链表的普通和XOR（或内存有效）表示形式。

**普通表示形式：**
节点A：
prev = NULL，next = add（B）//前一个为NULL，下一个为B的地址

节点B：
prev = add（A），next = add（C）//前一个是A的地址，下一个是C的地址

节点C：
prev = add（B），next = add（D）//上一个是B的地址，下一个是D的地址

节点D：
prev = add（C），next = NULL //前一个是C的地址，下一个是NULL

**XOR列表表示形式：**
让我们以XOR表示形式npx（下一个和上一个的XOR）调用地址变量

节点A：
npx = 0 XOR add（B）//零与B的地址按位XOR

节点B：
npx = add（A）XOR add（C）// A地址和C地址的按位XOR

节点C：
npx = add（B）XOR add（D）// B地址和D地址的按位XOR

节点D：
npx = add（C）XOR 0 // C和0的地址的按位XOR

**遍历XOR链接列表：**
我们可以在正反两个方向上遍历XOR列表。 在遍历列表时，我们需要记住先前访问的节点的地址，以便计算下一个节点的地址。 例如，当我们在节点C时，我们必须具有地址B。add（B）和C的 *npx* 的XOR给我们add（D）。 原因很简单：npx（C）是“ add（B）XOR add（D）”。 如果我们用add（B）对npx（C）进行异或，则得到的结果为“ add（B）XOR add（D）XOR add（B）”，即“ add（D）XOR 0”，即“ add” （D）”。 因此，我们有了下一个节点的地址。 同样，我们可以向后遍历列表。

在下面的文章中，我们将在XOR链接列表中介绍更多内容。

[XOR链表–内存有效的双链表| 设置2](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)

**参考：**
[http://en.wikipedia.org/wiki/XOR_linked_list](http://en.wikipedia.org/wiki/XOR_linked_list)
[http://www.linuxjournal.com/article/6828？ 页面= 0,0](http://www.linuxjournal.com/article/6828?page=0,0)

