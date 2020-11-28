# 两个链表的并集和交点

> 原文：[https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/](https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)

给定两个链表，创建包含给定列表中元素的并集和交集的并集和交集列表。 输出列表中元素的顺序无关紧要。

**示例**：

```
Input:
   List1: 10->15->4->20
   lsit2:  8->4->2->10
Output:
   Intersection List: 4->10
   Union List: 2->8->20->4->15->10

```

**方法 1（简单）**

以下是分别获取并集和交集列表的简单算法。

`intersect(list1, list2)`：

将结果列表初始化为`NULL`。 遍历`list1`并在`list2`中查找其每个元素，如果`list2`中存在该元素，则将其添加到结果中。

`union(list1, list2)`:

将结果列表初始化为`NULL`。 遍历`list1`并将其所有元素添加到结果中。

遍历列表 2。 如果结果中已经存在`list2`元素，则不要将其插入到结果中，否则插入。

此方法假定给定列表中没有重复项。

感谢 Shekhu 建议这种方法。 以下是此方法的 C 和 Java 实现。

## C/C++ 

```cpp

// C/C++ program to find union 
// and intersection of two unsorted 
// linked lists 
#include <stdbool.h> 
#include <stdio.h> 
#include <stdlib.h> 
/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* A utility function to insert a  
   node at the beginning ofa linked list*/
void push(struct Node** head_ref, int new_data); 

/* A utility function to check if  
   given data is present in a list */
bool isPresent(struct Node* head, int data); 

/* Function to get union of two  
   linked lists head1 and head2 */
struct Node* getUnion( 
    struct Node* head1, 
    struct Node* head2) 
{ 
    struct Node* result = NULL; 
    struct Node *t1 = head1, *t2 = head2; 

    // Insert all elements of 
    // list1 to the result list 
    while (t1 != NULL) { 
        push(&result, t1->data); 
        t1 = t1->next; 
    } 

    // Insert those elements of list2 
    // which are not present in result list 
    while (t2 != NULL) { 
        if (!isPresent(result, t2->data)) 
            push(&result, t2->data); 
        t2 = t2->next; 
    } 

    return result; 
} 

/* Function to get intersection of  
  two linked lists head1 and head2 */
struct Node* getIntersection(struct Node* head1, 
                             struct Node* head2) 
{ 
    struct Node* result = NULL; 
    struct Node* t1 = head1; 

    // Traverse list1 and search each element of it in 
    // list2\. If the element is present in list 2, then 
    // insert the element to result 
    while (t1 != NULL) { 
        if (isPresent(head2, t1->data)) 
            push(&result, t1->data); 
        t1 = t1->next; 
    } 

    return result; 
} 

/* A utility function to insert a  
   node at the beginning of a linked list*/
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node 
        = (struct Node*)malloc( 
            sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* A utility function to print a linked list*/
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* A utility function that returns true if data is  
   present in linked list else return false */
bool isPresent(struct Node* head, int data) 
{ 
    struct Node* t = head; 
    while (t != NULL) { 
        if (t->data == data) 
            return 1; 
        t = t->next; 
    } 
    return 0; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head1 = NULL; 
    struct Node* head2 = NULL; 
    struct Node* intersecn = NULL; 
    struct Node* unin = NULL; 

    /*create a linked lits 10->15->5->20 */
    push(&head1, 20); 
    push(&head1, 4); 
    push(&head1, 15); 
    push(&head1, 10); 

    /*create a linked lits 8->4->2->10 */
    push(&head2, 10); 
    push(&head2, 2); 
    push(&head2, 4); 
    push(&head2, 8); 

    intersecn = getIntersection(head1, head2); 
    unin = getUnion(head1, head2); 

    printf("\n First list is \n"); 
    printList(head1); 

    printf("\n Second list is \n"); 
    printList(head2); 

    printf("\n Intersection list is \n"); 
    printList(intersecn); 

    printf("\n Union list is \n"); 
    printList(unin); 

    return 0; 
} 

```

## Java

```java

// Java program to find union and 
// intersection of two unsorted 
// linked lists 
class LinkedList { 
    Node head; // head of list 

    /* Linked list Node*/
    class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    /* Function to get Union of 2 Linked Lists */
    void getUnion(Node head1, Node head2) 
    { 
        Node t1 = head1, t2 = head2; 

        // insert all elements of list1 in the result 
        while (t1 != null) { 
            push(t1.data); 
            t1 = t1.next; 
        } 

        // insert those elements of list2 
        // that are not present 
        while (t2 != null) { 
            if (!isPresent(head, t2.data)) 
                push(t2.data); 
            t2 = t2.next; 
        } 
    } 

    void getIntersection(Node head1, Node head2) 
    { 
        Node result = null; 
        Node t1 = head1; 

        // Traverse list1 and search each 
        // element of it in list2\. 
        // If the element is present in 
        // list 2, then insert the 
        // element to result 
        while (t1 != null) { 
            if (isPresent(head2, t1.data)) 
                push(t1.data); 
            t1 = t1.next; 
        } 
    } 

    /* Utility function to print list */
    void printList() 
    { 
        Node temp = head; 
        while (temp != null) { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    /*  Inserts a node at start of linked list */
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* A utilty function that returns true  
       if data is present in linked list  
       else return false */
    boolean isPresent(Node head, int data) 
    { 
        Node t = head; 
        while (t != null) { 
            if (t.data == data) 
                return true; 
            t = t.next; 
        } 
        return false; 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist1 = new LinkedList(); 
        LinkedList llist2 = new LinkedList(); 
        LinkedList unin = new LinkedList(); 
        LinkedList intersecn = new LinkedList(); 

        /*create a linked lits 10->15->5->20 */
        llist1.push(20); 
        llist1.push(4); 
        llist1.push(15); 
        llist1.push(10); 

        /*create a linked lits 8->4->2->10 */
        llist2.push(10); 
        llist2.push(2); 
        llist2.push(4); 
        llist2.push(8); 

        intersecn.getIntersection(llist1.head, llist2.head); 
        unin.getUnion(llist1.head, llist2.head); 

        System.out.println("First List is"); 
        llist1.printList(); 

        System.out.println("Second List is"); 
        llist2.printList(); 

        System.out.println("Intersection List is"); 
        intersecn.printList(); 

        System.out.println("Union List is"); 
        unin.printList(); 
    } 
} /* This code is contributed by Rajat Mishra */

```

**输出**：

```
 First list is
10 15 4 20
 Second list is
8 4 2 10
 Intersection list is
4 10
 Union list is
2 8 20 4 15 10

```

**复杂度分析**：

*   **时间复杂度**：`O(m * n)`。

    这里的`m`和`n`分别是第一和第二列表中存在的元素数。

    **对于并集**：对于列表 2 中的每个元素，我们检查该元素是否已存在于使用列表 1 生成的结果列表中。

    **对于交集**：对于列表 1 中的每个元素，我们检查该元素是否也存在于列表 2 中。

*   **辅助空间**：`O(1)`。

    不使用任何数据结构来存储值。

**方法 2（使用合并排序）**

在此方法中，并集和交集算法非常相似。 首先，我们对给定的列表进行排序，然后遍历排序后的列表以获得并集和交集。

以下是获取并集和交集列表的步骤。

1.  使用合并排序对第一个链表进行排序。 此步骤需要`O(mLogm)`时间。 有关此步骤的详细信息，请参见此帖子的[。](https://www.geeksforgeeks.org/archives/7740)

2.  使用合并排序对第二个链表进行排序。 此步骤需要`O(nLogn)`时间。 有关此步骤的详细信息，请参见此帖子的[。](https://www.geeksforgeeks.org/archives/7740)

3.  线性扫描两个排序列表以获取并集和交集。 此步骤需要`O(M + N)`时间。 可以使用与此处中讨论的排序数组算法相同的算法来实现此步骤。

此方法的时间复杂度为`O(mLogm + nLogn)`，优于方法 1 的时间复杂度。

**方法 3（使用哈希）**

`union(list1, list2)`：

将结果列表初始化为`NULL`并创建一个空哈希表。 遍历这两个元素都一个一个地列出，对于每个要访问的元素，在哈希表中查找该元素。 如果不存在该元素，则将该元素插入结果列表。 如果存在该元素，则将其忽略。

`intersect(list1, list2)`：

将结果列表初始化为`NULL`并创建一个空的哈希表。 遍历列表 1。 对于`list1`中要访问的每个元素，请将其插入哈希表。 遍历`list2`，对于`list2`中要访问的每个元素，在哈希表中查找该元素。 如果存在该元素，则将该元素插入结果列表。 如果该元素不存在，则将其忽略。

以上两种方法均假定没有重复项。

```

// Java code for Union and Intersection of two 
// Linked Lists 
import java.util.HashMap; 
import java.util.HashSet; 

class LinkedList { 
    Node head; // head of list 

    /* Linked list Node*/
    class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    /* Utility function to print list */
    void printList() 
    { 
        Node temp = head; 
        while (temp != null) { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    /* Inserts a node at start of linked list */
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
        Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    public void append(int new_data) 
    { 
        if (this.head == null) { 
            Node n = new Node(new_data); 
            this.head = n; 
            return; 
        } 
        Node n1 = this.head; 
        Node n2 = new Node(new_data); 
        while (n1.next != null) { 
            n1 = n1.next; 
        } 

        n1.next = n2; 
        n2.next = null; 
    } 

    /* A utilty function that returns true if data is 
    present in linked list else return false */
    boolean isPresent(Node head, int data) 
    { 
        Node t = head; 
        while (t != null) { 
            if (t.data == data) 
                return true; 
            t = t.next; 
        } 
        return false; 
    } 

    LinkedList getIntersection(Node head1, Node head2) 
    { 
        HashSet<Integer> hset = new HashSet<>(); 
        Node n1 = head1; 
        Node n2 = head2; 
        LinkedList result = new LinkedList(); 

        // loop stores all the elements of list1 in hset 
        while (n1 != null) { 
            if (hset.contains(n1.data)) { 
                hset.add(n1.data); 
            } 
            else { 
                hset.add(n1.data); 
            } 
            n1 = n1.next; 
        } 

        // For every element of list2 present in hset 
        // loop inserts the element into the result 
        while (n2 != null) { 
            if (hset.contains(n2.data)) { 
                result.push(n2.data); 
            } 
            n2 = n2.next; 
        } 
        return result; 
    } 

    LinkedList getUnion(Node head1, Node head2) 
    { 
        // HashMap that will store the 
        // elements of the lists with their counts 
        HashMap<Integer, Integer> hmap = new HashMap<>(); 
        Node n1 = head1; 
        Node n2 = head2; 
        LinkedList result = new LinkedList(); 

        // loop inserts the elements and the count of 
        // that element of list1 into the hmap 
        while (n1 != null) { 
            if (hmap.containsKey(n1.data)) { 
                int val = hmap.get(n1.data); 
                hmap.put(n1.data, val + 1); 
            } 
            else { 
                hmap.put(n1.data, 1); 
            } 
            n1 = n1.next; 
        } 

        // loop further adds the elements of list2 with 
        // their counts into the hmap 
        while (n2 != null) { 
            if (hmap.containsKey(n2.data)) { 
                int val = hmap.get(n2.data); 
                hmap.put(n2.data, val + 1); 
            } 
            else { 
                hmap.put(n2.data, 1); 
            } 
            n2 = n2.next; 
        } 

        // Eventually add all the elements 
        // into the result that are present in the hmap 
        for (int a : hmap.keySet()) { 
            result.append(a); 
        } 
        return result; 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist1 = new LinkedList(); 
        LinkedList llist2 = new LinkedList(); 
        LinkedList union = new LinkedList(); 
        LinkedList intersection = new LinkedList(); 

        /*create a linked list 10->15->4->20 */
        llist1.push(20); 
        llist1.push(4); 
        llist1.push(15); 
        llist1.push(10); 

        /*create a linked list 8->4->2->10 */
        llist2.push(10); 
        llist2.push(2); 
        llist2.push(4); 
        llist2.push(8); 

        intersection 
            = intersection.getIntersection(llist1.head, 
                                           llist2.head); 
        union = union.getUnion(llist1.head, llist2.head); 

        System.out.println("First List is"); 
        llist1.printList(); 

        System.out.println("Second List is"); 
        llist2.printList(); 

        System.out.println("Intersection List is"); 
        intersection.printList(); 

        System.out.println("Union List is"); 
        union.printList(); 
    } 
} 
// This code is contributed by Kamal Rawal 

```

**输出**：

```
First List is
10 15 4 20 
Second List is
8 4 2 10 
Intersection List is
10 4 
Union List is
2 4 20 8 10 15 

```

**复杂度分析**：

*   **时间复杂度**：`O(M + N)`。

    这里的`m`和`n`分别是第一和第二列表中存在的元素数。

    **对于并集**：遍历两个列表，将元素存储在哈希映射中并更新相应的计数。

    **对于交集**：首先遍历`list1`，将其元素存储在哈希映射中，然后对于`list2`中的每个元素，检查其是否已存在于映射中。 这需要`O(1)`时间。

*   **辅助空间**：`O(M + N)`。

    使用哈希映射数据结构存储值。

如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

