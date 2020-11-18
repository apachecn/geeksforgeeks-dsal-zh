# 检查链接列表

中是否存在与给定产品的对

给定一个链表和一个乘积K。任务是检查链表中是否存在两个乘积等于给定数K的数字。如果存在两个数字，则打印它们。 如果有多个答案，请打印其中的任何一个。

**范例**：

```
Input : List  = 1 -> 2 -> 3 -> 4 -> 5 -> NULL 
        K = 2
Output : Pair is (1, 2)

Input : List = 10 -> 12 -> 31 -> 42 -> 53 -> NULL 
        K = 15
Output : No Pair Exists

```

**方法1（强力）**：运行两个嵌套循环以生成链表的所有可能对，并检查任何对的乘积是否与给定乘积K匹配。

下面是上述方法的实现：

## C ++

```

// CPP code to find the pair with given product 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer)  
    to the head of a list and an int,  
    push a new node on the front   
    of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Takes head pointer of the linked list and product*/
int check_pair_product(struct Node* head, int prod) 
{ 
    struct Node *p = head, *q; 
    while (p != NULL) { 

        q = p->next; 
        while (q != NULL) { 

            // check if both product is equal to 
            // given product 
            if ((p->data) * (q->data) == prod) { 
                cout << p->data << " " << q->data; 
                return true; 
            } 
            q = q->next; 
        } 

        p = p->next; 
    } 

    return 0; 
} 

/* Driver program to test above function */
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct linked list*/
    push(&head, 1); 
    push(&head, 4); 
    push(&head, 1); 
    push(&head, 12); 
    push(&head, 1); 
    push(&head, 18); 
    push(&head, 47); 
    push(&head, 16); 
    push(&head, 12); 
    push(&head, 14); 

    /* function to print the result*/
    bool res = check_pair_product(head, 26); 
    if (res == false) 
        cout << "NO PAIR EXIST"; 

    return 0; 
} 

```

## 爪哇

```

// A Java code to find the pair 
// with given product 
import java.util.*; 
class GFG  
{  

/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
} 
static Node head; 

/* Given a reference (pointer to pointer)  
    to the head of a list and an int,  
    push a new node on the front  
    of the list. */
static void push(Node head_ref,  
                 int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    head = head_ref; 
} 

/* Takes head pointer of the linked list 
and product*/
static boolean check_pair_product(Node head, 
                                   int prod) 
{ 
    Node p = head, q; 
    while (p != null) 
    { 
        q = p.next; 
        while (q != null)  
        { 

            // check if both product is equal to 
            // given product 
            if ((p.data) * (q.data) == prod)  
            { 
                System.out.print(p.data + " " +  
                                 q.data); 
                return true; 
            } 
            q = q.next; 
        } 
        p = p.next; 
    } 
    return false; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    /* Start with the empty list */
    head = null; 

    /* Use push() to conlinked list*/
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    push(head, 18); 
    push(head, 47); 
    push(head, 16); 
    push(head, 12); 
    push(head, 14); 

    /* function to print the result*/
    boolean res = check_pair_product(head, 26); 
    if (res == false) 
        System.out.println("NO PAIR EXIST"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```

# Python3 code to find the pair with  
# given product  

# Link list node 
class Node:  

    def __init__(self, data, next): 
        self.data = data 
        self.next = next

class LinkedList: 

    def __init__(self): 
        self.head = None

    # Push a new node on the front of the list.      
    def push(self, new_data): 
        new_node = Node(new_data, self.head) 
        self.head = new_node 

    # Takes head pointer of the linked  
    # list and product 
    def check_pair_product(self, prod):  

        p = self.head 
        while p != None:  

            q = p.next
            while q != None:  

                # Check if both product is equal  
                # to given product  
                if p.data * q.data == prod:  
                    print(p.data, q.data)  
                    return True

                q = q.next

            p = p.next

        return False

# Driver Code 
if __name__ == "__main__": 

    # Start with the empty list 
    linkedlist = LinkedList() 

    # Use push() to construct linked list 
    linkedlist.push(1)  
    linkedlist.push(4)  
    linkedlist.push(1)  
    linkedlist.push(12)  
    linkedlist.push(1)  
    linkedlist.push(18)  
    linkedlist.push(47)  
    linkedlist.push(16)  
    linkedlist.push(12)  
    linkedlist.push(14)  

    # function to print the result 
    res = linkedlist.check_pair_product(26)  
    if res == False:  
        print("NO PAIR EXIST")  

# This code is contributed by Rituraj Jain 

```

## C＃

```

// A C# code to find the pair 
// with given product 
using System; 

class GFG  
{  

/* Link list node */
public class Node  
{ 
    public int data; 
    public Node next; 
} 
static Node head; 

/* Given a reference (pointer to pointer)  
    to the head of a list and an int,  
    push a new node on the front  
    of the list. */
static void push(Node head_ref,  
                 int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    head = head_ref; 
} 

/* Takes head pointer of the linked list 
and product*/
static Boolean check_pair_product(Node head, 
                                  int prod) 
{ 
    Node p = head, q; 
    while (p != null) 
    { 
        q = p.next; 
        while (q != null)  
        { 

            // check if both product is equal to 
            // given product 
            if ((p.data) * (q.data) == prod)  
            { 
                Console.Write(p.data + " " +  
                              q.data); 
                return true; 
            } 
            q = q.next; 
        } 
        p = p.next; 
    } 
    return false; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    /* Start with the empty list */
    head = null; 

    /* Use push() to conlinked list*/
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    push(head, 18); 
    push(head, 47); 
    push(head, 16); 
    push(head, 12); 
    push(head, 14); 

    /* function to print the result*/
    Boolean res = check_pair_product(head, 26); 
    if (res == false) 
        Console.WriteLine("NO PAIR EXIST"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
NO PAIR EXIST

```

**时间复杂度：** O（N <sup>2</sup> ），其中N是链​​表的长度。

**方法2（使用哈希）**：

1.  取一个哈希表，并将所有元素标记为零。
2.  在链表中将哈希表中的所有元素迭代标记为1。
3.  现在，开始遍历链表，并检查给定产品是否可被链表的当前元素整除，如果是，则检查哈希表中是否存在链表的（K / current_element）。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP code to find the pair with given product``#include <bits/stdc++.h>``#define MAX 100000``using` `namespace` `std;` [`/* Link list node */``struct` `Node {` `int` `data;` `struct` `Node* next;``};``/* Given a reference (pointer to pointer) ` `to the head of a list and an int, ` `push a new node on the front  ` `of the list. */``void` `push(` `struct` `Node** head_ref,` `int` `new_data)``{` `struct` `Node* new_node =` `new` `Node;` `new_node->data = new_data;` `new_node->next = (*head_ref);` `(*head_ref) = new_node;``}``// Function to check if pair with the given product``// exists in the list``// Takes head pointer of the linked list and product``bool` `check_pair_product(` `struct` `Node* head,` `int` `prod)``{` `unordered_set<` `int` `> s;` `struct` `Node* p = head;` `while` `(p != NULL) {` `int` `curr = p->data;` `// Check if pair exits` `if` `((prod % curr == 0) && (s.find(prod / curr) != s.end())) {` `cout << curr <<` `" "` `<< prod / curr;` `return` `true` `;` `}` `s.insert(p->data);` `p = p->next;` `}` `return` `false` `;``}``/* Driver program to test above function*/``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` [ `/* Use push() to construct linked list */` `push(&head, 1);` `push(&head, 2);`​​  `push(&head, 1);` `push(&head, 12);` `push(&head, 1);` `push(&head, 18);` `push(&head, 47);` `push(&head, 16);` `push(&head, 12);` `push(&head, 14);` `/* function to print the result*/` `bool` `res = check_pair_product(head, 24);` `if` `(res ==` `false` `)` `cout <<` `"NO PAIR EXIST"` `;` `return` `0;``}` |

*chevron_right**filter_none*