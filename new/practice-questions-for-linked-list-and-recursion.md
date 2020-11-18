# 链接列表和递归

的练习题

假定“链表”节点的结构如下。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `struct` `Node``{` `int` `data;` `struct` `Node *next;``};` |

*chevron_right**filter_none*

解释以下C函数的功能。

**1.以下功能对给定的链表有什么作用？**

## C ++

```

void fun1(struct Node* head) 
{ 
if(head == NULL) 
    return; 

fun1(head->next); 
cout << head->data << " "; 
} 

// This code is contributed by shubhamsingh10 

```

## C

```

void fun1(struct Node* head) 
{ 
  if(head == NULL) 
    return; 

  fun1(head->next); 
  printf("%d  ", head->data); 
} 

```

## 爪哇

```

static void fun1(Node head) 
{ 
    if (head == null) 
    { 
        return; 
    } 

    fun1(head.next); 
    System.out.print(head.data + " "); 
} 

// This code is contributed by shubhamsingh10 

```

## 蟒蛇

```

def fun1(head): 
    if(head == None): 
        return
    fun1(head.next)  
    print(head.data, end = " ") 

# This code is contributed by shubhamsingh10 

```

## C＃

```

static void fun1(Node head) 
{ 
    if (head == null) 
    { 
        return; 
    } 

    fun1(head.next); 
    Console.Write(head.data + " "); 
} 

// This code is contributed by shubhamsingh10 

```

fun1() prints the given Linked List in reverse manner. For Linked List 1->2->3->4->5, fun1() prints 5->4->3->2->1.

**2.以下功能对给定的链表有什么作用？**

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `void` `fun2(` `struct` `Node* head)``{` `if` `(head == NULL)` `return` `;` `cout << head->data <<` `" "` `; ` `if` `(head->next != NULL )` `fun2(head->next->next);` `cout << head->data <<` `" "` `;``}`的`// This code is contributed by shubhamsingh10` |

*chevron_right**filter_none*