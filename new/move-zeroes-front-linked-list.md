# 将所有零移动到链接列表的前面

给定一个链表。 任务是将全 0 移到链接列表的前面。 重新排列后，除 0 以外的所有其他元素的顺序应相同。

**示例**：

```
Input : 0 1 0 1 2 0 5 0 4 0
Output :0 0 0 0 0 1 1 2 5 4

Input :1 1 2 3 0 0 0 
Output :0 0 0 1 1 2 3 

```

**简单解决方案**是将所有链接列表元素存储在数组中。 然后将数组的所有元素移到开头。 最后，将数组元素复制回链接列表。

**有效解决方案**是从第二个节点遍历链表。 对于每个值为 0 的节点，我们将其与当前位置断开连接，然后将节点移到最前面。

## C++

```cpp

// CPP program to move all zeros 
// to the end of the linked list. 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
  int data; 
  struct Node *next; 
}; 

/* Given a reference (pointer to pointer) to 
the head of a list and an int, push a new 
node on the front of the list. */
void push(struct Node **head_ref, int new_data) { 
  struct Node *new_node = new Node; 
  new_node->data = new_data; 
  new_node->next = (*head_ref); 
  (*head_ref) = new_node; 
} 

/* moving zeroes to the beginning in linked list */
void moveZeroes(struct Node **head) { 
  if (*head == NULL) 
    return; 

  // Traverse the list from second node. 
  struct Node *temp = (*head)->next, *prev = *head; 
  while (temp != NULL) { 

    // If current node is 0, move to 
    // beginning of linked list 
    if (temp->data == 0) { 

      // Disconnect node from its 
      // current position 
      Node *curr = temp; 
      temp = temp->next; 
      prev->next = temp; 

      // Move to beginning 
      curr->next = (*head); 
      *head = curr; 
    } 

    // For non-zero values 
    else { 
      prev = temp; 
      temp = temp->next; 
    } 
  } 
} 

// function to displaying nodes 
void display(struct Node *head) { 
  while (head != NULL) { 
    cout << head->data << "->"; 
    head = head->next; 
  } 
  cout << "NULL"; 
} 

/* Driver program to test above function*/
int main() { 

  /* Start with the empty list */
  struct Node *head = NULL; 

  /* Use push() to construct below list 
  0->0->1->0->1->0->2->0->3->0 */
  push(&head, 0); 
  push(&head, 3); 
  push(&head, 0); 
  push(&head, 2); 
  push(&head, 0); 
  push(&head, 1); 
  push(&head, 0); 
  push(&head, 1); 
  push(&head, 0); 
  push(&head, 0); 

  // displaying list before rearrangement 
  cout << "Linked list before rearrangement\n"; 
  display(head); 

  /* Check the move_zeroes function */
  moveZeroes(&head); 

  // displaying list after rearrangement 
  cout << "\n Linked list after rearrangement \n"; 
  display(head); 

  return 0; 
} 

```

## Java

```java

// JAVA program to move all zeros 
// to the end of the linked list. 
class GFG 
{ 

    /* Link list node */
    static class Node  
    { 
        int data; 
        Node next; 
    }; 

    /* Given a reference (pointer to pointer) to 
    the head of a list and an int, push a new 
    node on the front of the list. */
    static Node push(Node head_ref, int new_data)  
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = head_ref; 
        head_ref = new_node; 
        return new_node; 
    } 

    /* moving zeroes to the beginning in linked list */
    static Node moveZeroes(Node head)  
    { 
        if (head == null) 
            return null; 

        // Traverse the list from second node. 
        Node temp = (head).next, prev = head; 
        while (temp != null) 
        { 

            // If current node is 0, move to 
            // beginning of linked list 
            if (temp.data == 0) 
            { 

                // Disconnect node from its 
                // current position 
                Node curr = temp; 
                temp = temp.next; 
                prev.next = temp; 

                // Move to beginning 
                curr.next = (head); 
                head = curr; 
            } 

            // For non-zero values 
            else 
            { 
                prev = temp; 
                temp = temp.next; 
            } 

        } 
        return head; 
    } 

    // function to displaying nodes 
    static void display(Node head) 
    { 
        while (head != null)  
        { 
            System.out.print(head.data+ "->"); 
            head = head.next; 
        } 
        System.out.print("null"); 
    } 

    /* Driver code*/
    public static void main(String[] args) 
    { 

        /* Start with the empty list */
        Node head = null; 

        /* Use push() to conbelow list 
        0.0.1.0.1.0.2.0.3.0 */
        head = push(head, 0); 
        head = push(head, 3); 
        head = push(head, 0); 
        head = push(head, 2); 
        head = push(head, 0); 
        head = push(head, 1); 
        head = push(head, 0); 
        head = push(head, 1); 
        head = push(head, 0); 
        head = push(head, 0); 

        // displaying list before rearrangement 
        System.out.print("Linked list before rearrangement\n"); 
        display(head); 

        /* Check the move_zeroes function */
        head = moveZeroes(head); 

        // displaying list after rearrangement 
        System.out.print("\n Linked list after rearrangement \n"); 
        display(head); 

    } 
} 

// This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# program to move all zeros 
// to the end of the linked list. 
using System; 

class GFG 
{ 

    /* Link list node */
    class Node  
    { 
        public int data; 
        public Node next; 
    }; 

    /* Given a reference (pointer to pointer) to 
    the head of a list and an int, push a new 
    node on the front of the list. */
    static Node push(Node head_ref, int new_data)  
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = head_ref; 
        head_ref = new_node; 
        return new_node; 
    } 

    /* moving zeroes to the beginning in linked list */
    static Node moveZeroes(Node head)  
    { 
        if (head == null) 
            return null; 

        // Traverse the list from second node. 
        Node temp = (head).next, prev = head; 
        while (temp != null) 
        { 

            // If current node is 0, move to 
            // beginning of linked list 
            if (temp.data == 0) 
            { 

                // Disconnect node from its 
                // current position 
                Node curr = temp; 
                temp = temp.next; 
                prev.next = temp; 

                // Move to beginning 
                curr.next = (head); 
                head = curr; 
            } 

            // For non-zero values 
            else
            { 
                prev = temp; 
                temp = temp.next; 
            } 
        } 
        return head; 
    } 

    // function to displaying nodes 
    static void display(Node head) 
    { 
        while (head != null)  
        { 
            Console.Write(head.data + "->"); 
            head = head.next; 
        } 
        Console.Write("null"); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 

        /* Start with the empty list */
        Node head = null; 

        /* Use push() to conbelow list 
        0->0->1->0->1->0->2->0->3->0 */
        head = push(head, 0); 
        head = push(head, 3); 
        head = push(head, 0); 
        head = push(head, 2); 
        head = push(head, 0); 
        head = push(head, 1); 
        head = push(head, 0); 
        head = push(head, 1); 
        head = push(head, 0); 
        head = push(head, 0); 

        // displaying list before rearrangement 
        Console.Write("Linked list before rearrangement\n"); 
        display(head); 

        /* Check the move_zeroes function */
        head = moveZeroes(head); 

        // displaying list after rearrangement 
        Console.Write("\n Linked list after rearrangement \n"); 
        display(head); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
Linked list before rearrangement
0->0->1->0->1->0->2->0->3->0->NULL

Linked list after rearrangement
0->0->0->0->0->0->1->1->2->3->NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。