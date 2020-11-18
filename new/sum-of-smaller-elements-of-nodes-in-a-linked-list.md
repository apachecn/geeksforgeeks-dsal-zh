# 链表

中节点的较小元素的总和

给定一个链表，链表的每个节点都由一对整数变量**首先**和**第二**来保存数据，以及一个指向列表中下一个节点的指针。 任务是为每个节点找到 **min（第一，第二）**的总和。

**示例**：

> **输入**：（2，3）->（3，4）– >（1，10）->（20，15）->（7，5）- > NULL
> **输出**：26
> 2 + 3 +1 + 15 + 5 = 26
> 
> **输入**：（7，3）->（3，9）->（5，10）->（20，8）->（19，11）- > NULL
> **输出**：30
> 3 + 3 + 5 + 8 + 11 = 30

**方法**：遍历整个链表，对于每个节点，如果节点的第一个元素比该节点的第二个元素小，则将第一个元素添加到保存总和的变量中，否则添加 第二个要素。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Represents node of the linked list 
struct Node { 
    int first; 
    int second; 
    Node* next; 
}; 

// Insertion in linked list 
void insert(Node** head, int f, int s) 
{ 
    Node* ptr = *head; 
    Node* temp = new Node(); 
    temp->first = f; 
    temp->second = s; 
    temp->next = NULL; 

    if (*head == NULL) 
        *head = temp; 
    else { 
        while (ptr->next != NULL) 
            ptr = ptr->next; 

        ptr->next = temp; 
    } 
} 

// Function to return the required sum 
int calSum(Node* head) 
{ 
    int sum = 0; 
    while (head != NULL) { 

        // Check for smaller element 
        if (head->first > head->second) 
            sum += head->second; 
        else
            sum += head->first; 

        head = head->next; 
    } 
    return sum; 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 

    insert(&head, 2, 3); 
    insert(&head, 3, 4); 
    insert(&head, 1, 10); 
    insert(&head, 20, 15); 
    insert(&head, 7, 5); 

    cout << calSum(head) << endl; 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG { 
    // Represents node of the linked list 
    static class Node { 
        int first; 
        int second; 
        Node next; 
    } 

    // Insertion in linked list 
    static Node insert(Node head, int f, int s) 
    { 
        Node ptr = head; 
        Node temp = new Node(); 
        temp.first = f; 
        temp.second = s; 
        temp.next = null; 

        if (head == null) 
            head = temp; 
        else { 
            while (ptr.next != null) 
                ptr = ptr.next; 

            ptr.next = temp; 
        } 
        return head; 
    } 

    // Function to return the required sum 
    static int calSum(Node head) 
    { 
        int sum = 0; 
        while (head != null) { 

            // Check for smaller element 
            if (head.first > head.second) 
                sum += head.second; 
            else
                sum += head.first; 

            head = head.next; 
        } 
        return sum; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        Node head = null; 

        head = insert(head, 2, 3); 
        head = insert(head, 3, 4); 
        head = insert(head, 1, 10); 
        head = insert(head, 20, 15); 
        head = insert(head, 7, 5); 

        System.out.print(calSum(head)); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach 

# Represents node of the linked list 
class Node: 

    def __init__(self, f, s): 
        self.first = f 
        self.second = s 
        self.next = None

# Insertion in linked list 
def insert(head, f, s): 

    ptr = head 
    temp = Node(f, s) 

    if head == None: 
        head = temp 
    else: 
        while ptr.next != None: 
            ptr = ptr.next

        ptr.next = temp 

    return head 

# Function to return the required sum 
def calSum(head): 

    Sum = 0
    while head != None: 

        # Check for smaller element 
        if head.first > head.second: 
            Sum += head.second 
        else: 
            Sum += head.first 

        head = head.next

    return Sum

# Driver code 
if __name__ == "__main__": 

    head = None

    head = insert(head, 2, 3) 
    head = insert(head, 3, 4) 
    head = insert(head, 1, 10) 
    head = insert(head, 20, 15) 
    head = insert(head, 7, 5) 

    print(calSum(head)) 

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG { 

    // Represents node of the linked list 
    public class Node { 
        public int first; 
        public int second; 
        public Node next; 
    } 

    // Insertion in linked list 
    static Node insert(Node head, int f, int s) 
    { 
        Node ptr = head; 
        Node temp = new Node(); 
        temp.first = f; 
        temp.second = s; 
        temp.next = null; 

        if (head == null) 
            head = temp; 
        else { 
            while (ptr.next != null) 
                ptr = ptr.next; 

            ptr.next = temp; 
        } 
        return head; 
    } 

    // Function to return the required sum 
    static int calSum(Node head) 
    { 
        int sum = 0; 
        while (head != null) { 

            // Check for smaller element 
            if (head.first > head.second) 
                sum += head.second; 
            else
                sum += head.first; 

            head = head.next; 
        } 
        return sum; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        Node head = null; 

        head = insert(head, 2, 3); 
        head = insert(head, 3, 4); 
        head = insert(head, 1, 10); 
        head = insert(head, 20, 15); 
        head = insert(head, 7, 5); 

        Console.Write(calSum(head)); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
26

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。