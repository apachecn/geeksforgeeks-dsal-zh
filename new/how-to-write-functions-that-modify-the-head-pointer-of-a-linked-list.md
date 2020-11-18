# 如何编写可修改链表头指针的 C 函数？

考虑链表的简单表示（没有任何虚拟节点）。 在此类链接列表上运行的功能可以分为两类：

**1）不修改头指针的功能**：此类功能的示例包括：打印链接列表，更新节点的数据成员（如将给定值添加到所有节点）或其他一些访问/更新操作 节点数据

通常很容易确定此类功能的原型。 我们总是可以将头指针作为参数传递并遍历/更新列表。 例如，以下函数将 x 添加到所有节点的数据成员。

```

void addXtoList(struct Node *node, int x) 
{ 
    while(node != NULL) 
    { 
        node->data = node->data + x; 
        node = node->next; 
    } 
}     

```

**2）修改头指针的功能**：示例包括，在开头插入一个节点（此功能中始终修改头指针），在结尾插入一个节点（仅当第一个指针被修改时，才修改头指针）。 插入节点），删除给定的节点（当删除的节点是第一个节点时，将修改头指针）。 在这些功能中，可能有不同的方法来更新头指针。 让我们使用以下简单问题讨论这些方式：

*“给出一个链表，编写一个函数 deleteFirst（）来删除给定链表的第一个节点。 例如，如果列表是 1- > 2- > 3- > 4，则应将其修改为 2- > 3- > 4”*

解决问题的算法是一个简单的 3 个步骤：（a）存储头指针（b）更改头指针以指向下一个节点（c）删除前一个头节点。

以下是在 deleteFirst（）中更新头指针的不同方法，以便可以在任何地方更新列表。

***2.1）**将头指针设为全局：*我们可以将头指针设为全局，以便可以在我们的函数中对其进行访问和更新。 以下是使用全局头指针的 C 代码。

```

// global head pointer  
struct Node *head = NULL; 

// function to delete first node: uses approach 2.1 
// See http://ideone.com/ClfQB for complete program and output 
void deleteFirst() 
{ 
    if(head != NULL) 
    { 
       // store the old value of head pointer     
       struct Node *temp = head; 

       // Change head pointer to point to next node  
       head = head->next;  

       // delete memory allocated for the previous head node 
       free(temp); 
    } 
} 

```

有关使用上述功能的完整运行程序，请参见此的[。](http://ideone.com/ClfQB)

不建议使用这种方法，因为它存在许多类似以下的问题：

a）head 可以全局访问，因此可以在项目中的任何位置进行修改，并可能导致无法预测的结果。

b）如果存在多个链接列表，则需要多个具有不同名称的全局头指针。

请参见[和](http://c2.com/cgi/wiki?GlobalVariablesAreBad)，以了解为什么我们应避免在项目中使用全局变量的所有原因。

***2.2）**返回头指针：*我们可以以这样的方式编写 deleteFirst（）：它返回修改后的头指针。 谁在使用此功能，都必须使用返回的值来更新头节点。

```

// function to delete first node: uses approach 2.2 
// See http://ideone.com/P5oLe for complete program and output 
struct Node *deleteFirst(struct Node *head) 
{ 
    if(head != NULL) 
    { 
       // store the old value of head pointer 
       struct Node *temp = head; 

       // Change head pointer to point to next node 
       head = head->next; 

       // delete memory allocated for the previous head node 
       free(temp); 
    } 

    return head; 
} 

```

有关完整的程序和输出，请参见此的[。

这种方法比以前的方法好得多。只有一个问题，如果用户错过了将返回值分配给 head 的事情，事情就会变得混乱。 C / C++编译器允许在不分配返回值的情况下调用函数。](http://ideone.com/P5oLe)

```

head = deleteFirst(head);  // proper use of deleteFirst() 
deleteFirst(head);  // improper use of deleteFirst(), allowed by compiler 

```

***2.3）**使用双指针：*此方法遵循简单的 C 规则：*如果要在另一个函数内修改一个函数的局部变量，请传递 指向该变量的指针*。 因此，我们可以将指针传递到头指针，以在 deleteFirst（）函数中修改头指针。

```

// function to delete first node: uses approach 2.3 
// See http://ideone.com/9GwTb for complete program and output 
void deleteFirst(struct Node **head_ref) 
{ 
    if(*head_ref != NULL) 
    { 
       // store the old value of pointer to head pointer 
       struct Node *temp = *head_ref; 

       // Change head pointer to point to next node 
       *head_ref = (*head_ref)->next; 

       // delete memory allocated for the previous head node 
       free(temp); 
    } 
} 

```

有关完整的程序和输出，请参见此的[。

这种方法似乎是这三种方法中最好的，因为出现问题的机会更少。](http://ideone.com/9GwTb)

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

