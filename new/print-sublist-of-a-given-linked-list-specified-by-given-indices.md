# 打印由给定索引指定的给定链接列表的子列表

给定[链表](https://www.geeksforgeeks.org/data-structures/linked list/)和两个索引 **A** 和 **B** ，任务是打印一个从 **A** 开始并在**结尾的子列表。 B** 。

**示例：**

> **输入：**列表= 1-> 2-> 3-> 4-> 5-> 6-> 7-> 8-> 9-> 10-> NULL，A = 3，B = 9
> **输出：** 3 4 5 6 7 8 9
> 
> **输入：**列表= 1-> 3-> 4-> 10-> NULL，A = 2，B = 2
> **输出：** 3

**方法：**

请按照以下步骤解决问题：

1.  创建三个实例变量：

    1.  **当前：**给定链表的标题

    2.  **子流：**子列表的头

    3.  **子结尾：**子列表的尾部。

*   遍历链表并初始化 **index_count** 变量，该变量在每次迭代后增加。*   当 **index_count** 的值等于 A 时，将**子流**设置为当前指向的节点。*   如果 **index_count** 等于 B，则将**子端点**分配给当前引用的节点。 将 **subend.next** 指向 *NULL* ，表示子列表的末尾。*   从**子流**到**子端**打印列表内容。

下面的代码是上述方法的实现：

## Java

```java

// Java Program to find the 
// subList in a linked list 

import java.util.Scanner; 

// Class representing the 
// structure of a Linked List 
public class LinkedListSublist { 
    Node head; 
    class Node { 
        int data; 
        Node next = null; 
        Node(int new_data) 
        { 
            data = new_data; 
        } 
    } 

    // Function to push node 
    // at beginning of a 
    // Linked List 
    public void pushNode(int new_data) 
    { 
        Node new_node = new Node(new_data); 
        new_node.next = head; 
        head = new_node; 
    } 

    // Function to find sublist 
    public Node subList(Node head, 
                        int A, 
                        int B) 
    { 
        Node subcurrent = null; 
        Node subend = null; 
        Node current = head; 
        int i = 1; 

        // traverse between indices 
        while (current != null
               && i <= B) { 

            // If the starting index 
            // of the sublist is found 
            if (i == A) { 
                subcurrent = current; 
            } 

            // If the ending index of 
            // the sublist is found 
            if (i == B) { 
                subend = current; 
                subend.next = null; 
            } 

            // Move to next node 
            current = current.next; 
            i++; 
        } 

        // Return the head 
        // of the sublist 
        return subcurrent; 
    } 

    // Function to print 
    // the linked list 
    public void traversing() 
    { 
        Node current = head; 
        while (current != null) { 
            System.out.print(current.data 
                             + " -> "); 
            current = current.next; 
        } 
    } 

    // Driver Program 
    public static void main(String args[]) 
    { 

        LinkedListSublist list 
            = new LinkedListSublist(); 
        int N = 1; 
        int value = 10; 

        while (N < 11) { 
            list.pushNode(value--); 
            N++; 
        } 

        // Starting index 
        int A = 3; 

        // Ending index 
        int B = 9; 

        list.head 
            = list.subList( 
                list.head, A, B); 
        list.traversing(); 
    } 
} 

```

**Output:**

```
3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 ->

```

***时间复杂度：**`O(n)`*

***辅助空间：**`O(1)`*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。