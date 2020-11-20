# 在保留旧节点的同时将起始 N 个节点拆分为新的循环链表

> 原文：[https://www.geeksforgeeks.org/splitting-starting-n-nodes-into-new-circular-linked-list-while-preserving-the-old-nodes/](https://www.geeksforgeeks.org/splitting-starting-n-nodes-into-new-circular-linked-list-while-preserving-the-old-nodes/)

给定一个具有 **N** 个节点和整数 **K** 的循环链表，其中 **0 < K < N** ，任务是拆分第一个 **将**个节点 K 放入一个新列表中，同时将其余的节点保留在原始循环链表中。

**示例**：

> **输入**：2-> 3-> 4-> 5-> 6-> 7-> 8，K = 3
> **输出 **：
> 原始列表：
> 2 3 4 5 6 7 8
> 新列表是：
> 2 3 4
> 5 6 7 8
> 
> **输入**：2-> 4-> 6-> 8- > 10-> 12，N = 4
> **输出**：[
> 原始列表：
> 2 4 6 8 10 12
> 新列表为：
> 2 4 6 8
> 10 12

**方法**：

*   遍历迭代器，直到所需的节点，即 **K <sup>第</sup>** 节点。

*   将 **K <sup>第</sup>** 节点之前的节点指向原始列表的开头。

*   将原始列表的最后一个节点指向 **K <sup>th</sup>** 节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include<bits/stdc++.h> 
using namespace std; 

class CircularLinkedList 
{ 
    public: 
    struct Node  
    { 
        int data; 
        Node* next; 
    }; 

    Node* last; 

    // Function to add a node to the empty list 
    Node* addToEmpty(int data) 
    { 
        // If not empty 
        if (last != NULL) 
            return last; 

        // Creating a node dynamically 
        Node *temp = new Node(); 

        // Assigning the data 
        temp->data = data; 
        last = temp; 

        // Creating the link 
        last->next = last; 

        return last; 
    } 

    // Function to add a node to the 
    // beginning of the list 
    Node* addBegin(int data) 
    { 

        // If list is empty 
        if (last == NULL) 
            return addToEmpty(data); 

        // Create node 
        Node *temp = new Node(); 

        // Assign data 
        temp->data = data; 
        temp->next = last->next; 
        last->next = temp; 

        return last; 
    } 

    // Function to traverse and print the list 
    void traverse() 
    { 
        Node* p; 

        // If list is empty 
        if (last == NULL) 
        { 
            cout<<("List is empty."); 
            return; 
        } 

        // Pointing to the first Node of the list 
        p = last->next; 

        // Traversing the list 
        do
        { 
            cout << p->data << " "; 
            p = p->next; 
        } while (p != last->next); 
        cout << endl; 
    } 

    // Function to find the length of the CircularLinkedList 
    int length() 
    { 
        // Stores the length 
        int x = 0; 

        // List is empty 
        if (last == NULL) 
            return x; 

        // Iterator Node to traverse the List 
        Node* itr = last->next; 
        while (itr->next != last->next)  
        { 
            x++; 
            itr = itr->next; 
        } 

        // Return the length of the list 
        return (x + 1); 
    } 

    // Function to split the first k nodes into 
    // a new CircularLinkedList and the remaining 
    // nodes stay in the original CircularLinkedList 
    Node* split(int k) 
    { 

        // Empty Node for reference 
        Node* pass = new Node(); 

        // Check if the list is empty 
        // If yes, then return NULL 
        if (last == NULL) 
            return last; 

        // NewLast will contain the last node of 
        // the new split list 
        // itr to iterate the node till 
        // the required node 
        Node* newLast, *itr = last; 
        for (int i = 0; i < k; i++)  
        { 
            itr = itr->next; 
        } 

        // Update NewLast to the required node and 
        // link the last to the start of rest of the list 
        newLast = itr; 
        pass->next = itr->next; 
        newLast->next = last->next; 
        last->next = pass->next; 

        // Return the last node of the required list 
        return newLast; 
    } 
}; 
    // Driver code 
int main() 
{ 
    CircularLinkedList* clist = new CircularLinkedList(); 
    clist->last = NULL; 

    clist->addToEmpty(12); 
    clist->addBegin(10); 
    clist->addBegin(8); 
    clist->addBegin(6); 
    clist->addBegin(4); 
    clist->addBegin(2); 
    cout<<("Original list:"); 
    clist->traverse(); 

    int k = 4; 

    // Create a new list for the starting k nodes 
    CircularLinkedList* clist2 = new CircularLinkedList(); 

    // Append the new last node into the new list 
    clist2->last = clist->split(k); 

    // Print the new lists 
    cout<<("The new lists are:"); 
    clist2->traverse(); 
    clist->traverse(); 
} 

// This code is contributed by Arnab Kundu 

```

## Java

```java

// Java implementation of the approach 
public class CircularLinkedList { 

    Node last; 

    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to add a node to the empty list 
    public Node addToEmpty(int data) 
    { 
        // If not empty 
        if (this.last != null) 
            return this.last; 

        // Creating a node dynamically 
        Node temp = new Node(); 

        // Assigning the data 
        temp.data = data; 
        this.last = temp; 

        // Creating the link 
        this.last.next = this.last; 

        return last; 
    } 

    // Function to add a node to the 
    // beginning of the list 
    public Node addBegin(int data) 
    { 

        // If list is empty 
        if (last == null) 
            return addToEmpty(data); 

        // Create node 
        Node temp = new Node(); 

        // Assign data 
        temp.data = data; 
        temp.next = this.last.next; 
        this.last.next = temp; 

        return this.last; 
    } 

    // Function to traverse and print the list 
    public void traverse() 
    { 
        Node p; 

        // If list is empty 
        if (this.last == null) { 
            System.out.println("List is empty."); 
            return; 
        } 

        // Pointing to the first Node of the list 
        p = this.last.next; 

        // Traversing the list 
        do { 
            System.out.print(p.data + " "); 
            p = p.next; 
        } while (p != this.last.next); 

        System.out.println(""); 
    } 

    // Function to find the length of the CircularLinkedList 
    public int length() 
    { 
        // Stores the length 
        int x = 0; 

        // List is empty 
        if (this.last == null) 
            return x; 

        // Iterator Node to traverse the List 
        Node itr = this.last.next; 
        while (itr.next != this.last.next) { 
            x++; 
            itr = itr.next; 
        } 

        // Return the length of the list 
        return (x + 1); 
    } 

    // Function to split the first k nodes into 
    // a new CircularLinkedList and the remaining 
    // nodes stay in the original CircularLinkedList 
    public Node split(int k) 
    { 

        // Empty Node for reference 
        Node pass = new Node(); 

        // Check if the list is empty 
        // If yes, then return null 
        if (this.last == null) 
            return this.last; 

        // NewLast will contain the last node of 
        // the new split list 
        // itr to iterate the node till 
        // the required node 
        Node newLast, itr = this.last; 
        for (int i = 0; i < k; i++) { 
            itr = itr.next; 
        } 

        // Update NewLast to the required node and 
        // link the last to the start of rest of the list 
        newLast = itr; 
        pass.next = itr.next; 
        newLast.next = this.last.next; 
        this.last.next = pass.next; 

        // Return the last node of the required list 
        return newLast; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        CircularLinkedList clist = new CircularLinkedList(); 
        clist.last = null; 

        clist.addToEmpty(12); 
        clist.addBegin(10); 
        clist.addBegin(8); 
        clist.addBegin(6); 
        clist.addBegin(4); 
        clist.addBegin(2); 
        System.out.println("Original list:"); 
        clist.traverse(); 

        int k = 4; 

        // Create a new list for the starting k nodes 
        CircularLinkedList clist2 = new CircularLinkedList(); 

        // Append the new last node into the new list 
        clist2.last = clist.split(k); 

        // Print the new lists 
        System.out.println("The new lists are:"); 
        clist2.traverse(); 
        clist.traverse(); 
    } 
} 

```

## C#

```cs

// C# implementation of the approach 
using System; 

public class CircularLinkedList 
{ 

    public Node last; 

    public class Node  
    { 
        public int data; 
        public Node next; 
    }; 

    // Function to add a node to the empty list 
    public Node addToEmpty(int data) 
    { 
        // If not empty 
        if (this.last != null) 
            return this.last; 

        // Creating a node dynamically 
        Node temp = new Node(); 

        // Assigning the data 
        temp.data = data; 
        this.last = temp; 

        // Creating the link 
        this.last.next = this.last; 

        return last; 
    } 

    // Function to add a node to the 
    // beginning of the list 
    public Node addBegin(int data) 
    { 

        // If list is empty 
        if (last == null) 
            return addToEmpty(data); 

        // Create node 
        Node temp = new Node(); 

        // Assign data 
        temp.data = data; 
        temp.next = this.last.next; 
        this.last.next = temp; 

        return this.last; 
    } 

    // Function to traverse and print the list 
    public void traverse() 
    { 
        Node p; 

        // If list is empty 
        if (this.last == null) 
        { 
            Console.WriteLine("List is empty."); 
            return; 
        } 

        // Pointing to the first Node of the list 
        p = this.last.next; 

        // Traversing the list 
        do 
        { 
            Console.Write(p.data + " "); 
            p = p.next; 
        } while (p != this.last.next); 

        Console.WriteLine(""); 
    } 

    // Function to find the length of the CircularLinkedList 
    public int length() 
    { 
        // Stores the length 
        int x = 0; 

        // List is empty 
        if (this.last == null) 
            return x; 

        // Iterator Node to traverse the List 
        Node itr = this.last.next; 
        while (itr.next != this.last.next)  
        { 
            x++; 
            itr = itr.next; 
        } 

        // Return the length of the list 
        return (x + 1); 
    } 

    // Function to split the first k nodes into 
    // a new CircularLinkedList and the remaining 
    // nodes stay in the original CircularLinkedList 
    public Node split(int k) 
    { 

        // Empty Node for reference 
        Node pass = new Node(); 

        // Check if the list is empty 
        // If yes, then return null 
        if (this.last == null) 
            return this.last; 

        // NewLast will contain the last node of 
        // the new split list 
        // itr to iterate the node till 
        // the required node 
        Node newLast, itr = this.last; 
        for (int i = 0; i < k; i++)  
        { 
            itr = itr.next; 
        } 

        // Update NewLast to the required node and 
        // link the last to the start of rest of the list 
        newLast = itr; 
        pass.next = itr.next; 
        newLast.next = this.last.next; 
        this.last.next = pass.next; 

        // Return the last node of the required list 
        return newLast; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        CircularLinkedList clist = new CircularLinkedList(); 
        clist.last = null; 

        clist.addToEmpty(12); 
        clist.addBegin(10); 
        clist.addBegin(8); 
        clist.addBegin(6); 
        clist.addBegin(4); 
        clist.addBegin(2); 
        Console.WriteLine("Original list:"); 
        clist.traverse(); 

        int k = 4; 

        // Create a new list for the starting k nodes 
        CircularLinkedList clist2 = new CircularLinkedList(); 

        // Append the new last node into the new list 
        clist2.last = clist.split(k); 

        // Print the new lists 
        Console.WriteLine("The new lists are:"); 
        clist2.traverse(); 
        clist.traverse(); 
    } 
} 

// This code is  contributed by Rajput-Ji 

```

**Output:**

```
Original list:
2 4 6 8 10 12 
The new lists are:
2 4 6 8 
10 12

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。