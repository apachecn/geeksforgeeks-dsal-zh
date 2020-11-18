# 使用下一个随机指针克隆链接列表 | 系列 2

> 原文：[https://www.geeksforgeeks.org/clone-linked-list-next-arbit-pointer-set-2/](https://www.geeksforgeeks.org/clone-linked-list-next-arbit-pointer-set-2/)

我们已经讨论了两种克隆链表的不同方法。 在的[中，讨论了一种更简单的克隆链表的方法。](https://www.geeksforgeeks.org/a-linked-list-with-next-and-arbit-pointer/)

这个想法是使用哈希。 下面是算法。

1.遍历原始链表，并根据数据进行复制。

2.使用原始链表节点和复制链表节点对键值对进行哈希映射。

3.再次遍历原始链表，并使用哈希图调整克隆链表节点的下一个随机引用。

下面是上述方法的实现。

## C++

```cpp

// C++ program to clone a linked list with 
// random pointers 
#include<bits/stdc++.h> 
using namespace std; 

// Linked List Node 
class Node 
{ 
    public: 
    int data;//Node data 

    // Next and random reference 
    Node *next, *random; 

    Node(int data) 
    { 
        this->data = data; 
        this->next = this->random = NULL; 
    } 
}; 

// linked list class 
class LinkedList 
{ 
    public: 
    Node *head;// Linked list head reference 

    LinkedList(Node *head) 
    { 
        this->head = head; 
    } 

    // push method to put data always at 
    // the head in the linked list. 
    void push(int data) 
    { 
        Node *node = new Node(data); 
        node->next = head; 
        head = node; 
    } 

    // Method to print the list. 
    void print() 
    { 
        Node *temp = head; 
        while (temp != NULL) 
        { 
            Node *random = temp->random; 
            int randomData = (random != NULL)? 
                         random->data: -1; 
            cout << "Data = " << temp->data  
                 << ", "; 
            cout << "Random Data = " <<  
                 randomData << endl; 
            temp = temp->next; 
        } 
        cout << endl; 
    } 

    // Actual clone method which returns 
    // head reference of cloned linked 
    // list. 
    LinkedList* clone() 
    { 
        // Initialize two references, 
        // one with original list's head. 
        Node *origCurr = head; 
        Node *cloneCurr = NULL; 

        // Hash map which contains node  
        // to node mapping of original  
        // and clone linked list. 
        unordered_map<Node*, Node*> mymap; 

        // Traverse the original list and 
        // make a copy of that in the  
        // clone linked list. 
        while (origCurr != NULL) 
        { 
            cloneCurr = new Node(origCurr->data); 
            mymap[origCurr] = cloneCurr; 
            origCurr = origCurr->next; 
        } 

        // Adjusting the original list  
        // reference again. 
        origCurr = head; 

        // Traversal of original list again 
        // to adjust the next and random  
        // references of clone list using  
        // hash map. 
        while (origCurr != NULL) 
        { 
            cloneCurr = mymap[origCurr]; 
            cloneCurr->next = mymap[origCurr->next]; 
            cloneCurr->random = mymap[origCurr->random]; 
            origCurr = origCurr->next; 
        } 

        // return the head reference of  
        // the clone list. 
        return new LinkedList(mymap[head]); 
    } 
}; 

// driver code 
int main() 
{ 
    // Pushing data in the linked list. 
    LinkedList *mylist = new LinkedList(new Node(5)); 
    mylist->push(4); 
    mylist->push(3); 
    mylist->push(2); 
    mylist->push(1); 

    // Setting up random references. 
    mylist->head->random = mylist->head->next->next; 

    mylist->head->next->random = 
        mylist->head->next->next->next; 

    mylist->head->next->next->random = 
        mylist->head->next->next->next->next; 

    mylist->head->next->next->next->random = 
        mylist->head->next->next->next->next->next; 

    mylist->head->next->next->next->next->random = 
        mylist->head->next; 

    // Making a clone of the original 
    // linked list. 
    LinkedList *clone = mylist->clone(); 

    // Print the original and cloned  
    // linked list. 
    cout << "Original linked list\n"; 
    mylist->print(); 
    cout << "\nCloned linked list\n"; 
    clone->print(); 
} 
// This code is contributed by Chhavi 

```

## Java

```java

// Java program to clone a linked list with random pointers 
import java.util.HashMap; 
import java.util.Map; 

// Linked List Node class 
class Node 
{ 
    int data;//Node data 
    Node next, random;//Next and random reference 

    //Node constructor 
    public Node(int data) 
    { 
        this.data = data; 
        this.next = this.random = null; 
    } 
} 

// linked list class 
class LinkedList 
{ 
    Node head;//Linked list head reference 

    // Linked list constructor 
    public LinkedList(Node head) 
    { 
        this.head = head; 
    } 

    // push method to put data always at the head 
    // in the linked list. 
    public void push(int data) 
    { 
        Node node = new Node(data); 
        node.next = this.head; 
        this.head = node; 
    } 

    // Method to print the list. 
    void print() 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
            Node random = temp.random; 
            int randomData = (random != null)? random.data: -1; 
            System.out.println("Data = " + temp.data + 
                               ", Random data = "+ randomData); 
            temp = temp.next; 
        } 
    } 

    // Actual clone method which returns head 
    // reference of cloned linked list. 
    public LinkedList clone() 
    { 
        // Initialize two references, one with original 
        // list's head. 
        Node origCurr = this.head, cloneCurr = null; 

        // Hash map which contains node to node mapping of 
        // original and clone linked list. 
        Map<Node, Node> map = new HashMap<Node, Node>(); 

        // Traverse the original list and make a copy of that 
        // in the clone linked list. 
        while (origCurr != null) 
        { 
            cloneCurr = new Node(origCurr.data); 
            map.put(origCurr, cloneCurr); 
            origCurr = origCurr.next; 
        } 

        // Adjusting the original list reference again. 
        origCurr = this.head; 

        // Traversal of original list again to adjust the next 
        // and random references of clone list using hash map. 
        while (origCurr != null) 
        { 
            cloneCurr = map.get(origCurr); 
            cloneCurr.next = map.get(origCurr.next); 
            cloneCurr.random = map.get(origCurr.random); 
            origCurr = origCurr.next; 
        } 

        //return the head reference of the clone list. 
        return new LinkedList(map.get(this.head)); 
    } 
} 

// Driver Class 
class Main 
{ 
    // Main method. 
    public static void main(String[] args) 
    { 
        // Pushing data in the linked list. 
        LinkedList list = new LinkedList(new Node(5)); 
        list.push(4); 
        list.push(3); 
        list.push(2); 
        list.push(1); 

        // Setting up random references. 
        list.head.random = list.head.next.next; 
        list.head.next.random = 
            list.head.next.next.next; 
        list.head.next.next.random = 
            list.head.next.next.next.next; 
        list.head.next.next.next.random = 
            list.head.next.next.next.next.next; 
        list.head.next.next.next.next.random = 
            list.head.next; 

        // Making a clone of the original linked list. 
        LinkedList clone = list.clone(); 

        // Print the original and cloned linked list. 
        System.out.println("Original linked list"); 
        list.print(); 
        System.out.println("\nCloned linked list"); 
        clone.print(); 
    } 
}

```

## Python3

```py

# Python3 program to clone a linked list  
# with random pointers  
class Node:  
    def __init__(self, data): 

        # Node Data 
        self.data = data  

        # Node Next 
        self.next = None 

        # Node Random 
        self.random = None 

# Dictionary 
class MyDictionary(dict):  

    # __init__ function 
    def __init__(self): 

        super().__init__() 
        self = dict() 

        # Function to add key:value 
    def add(self, key, value): 

        # Adding Values to dictionary 
        self[key] = value  

# Linked list class  
class LinkedList: 

    # Linked list constructor 
    def __init__(self, node): 
        self.head = node 

    # Method to print the list. 
    def __repr__(self): 

        temp = self.head 
        while temp is not None: 
            random = temp.random 
            random_data = (random.data if 
                           random is not None else -1) 

            data = temp.data 
            print( 
                f"Data-{data}, Random data: {random_data}") 
            temp = temp.next

        return "\n"

    # push method to put data always at the head 
    # in the linked list. 
    def push(self, data): 

        node = Node(data) 
        node.next = self.head 
        self.head = node 

    # Actual clone method which returns head 
    # reference of cloned linked list. 
    def clone(self): 

        # Initialize two references, one  
        # with original list's head. 
        original = self.head 
        clone = None

        # Initialize two references, one  
        # with original list's head. 
        mp = MyDictionary() 

        # Traverse the original list and  
        # make a copy of that 
        # in the clone linked list 
        while original is not None: 
            clone = Node(original.data) 
            mp.add(original, clone) 
            original = original.next

        # Adjusting the original  
        # list reference again. 
        original = self.head 

        # Traversal of original list again 
        # to adjust the next and random  
        # references of clone list using hash map. 
        while original is not None: 
            clone = mp.get(original) 
            clone.next = mp.get(original.next) 
            clone.random = mp.get(original.random) 
            original = original.next

        # Return the head reference of the clone list. 
        return LinkedList(self.head) 

# Driver code 

# Pushing data in the linked list. 
l = LinkedList(Node(5)) 
l.push(4) 
l.push(3) 
l.push(2) 
l.push(1) 

# Setting up random references. 
l.head.random = l.head.next.next
l.head.next.random = l.head.next.next.next
l.head.next.next.random = l.head.next.next.next.next
l.head.next.next.next.random = (l.head.next.next.next. 
                                  next.next) 
l.head.next.next.next.next.random = l.head.next

# Making a clone of the  
# original linked list. 
clone = l.clone() 

# Print the original and cloned 
# linked list.s 
print("Original linked list") 
print(l) 
print("Cloned linked list") 
print(clone) 

# This code is contributed by ashwinathappan 

```

## C#

```cs

// C# program to clone a linked list with random pointers 
using System; 
using System.Collections; 
using System.Collections.Generic; 

class GFG 
{ 

// Linked List Node class 
public class Node 
{ 
    public int data;// Node data 
    public Node next, random;// Next and random reference 

    // Node constructor 
    public Node(int data) 
    { 
        this.data = data; 
        this.next = this.random = null; 
    } 
} 

// linked list class 
public class LinkedList 
{ 
    public Node head;// Linked list head reference 

    // Linked list constructor 
    public LinkedList(Node head) 
    { 
        this.head = head; 
    } 

    // push method to Add data always at the head 
    // in the linked list. 
    public void push(int data) 
    { 
        Node node = new Node(data); 
        node.next = this.head; 
        this.head = node; 
    } 

    // Method to print the list. 
    public void print() 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
            Node random = temp.random; 
            int randomData = (random != null)? random.data: -1; 
            Console.WriteLine("Data = " + temp.data + 
                            ", Random data = "+ randomData); 
            temp = temp.next; 
        } 
    } 

    // Actual clone method which returns head 
    // reference of cloned linked list. 
    public LinkedList clone() 
    { 
        // Initialize two references, one with original 
        // list's head. 
        Node origCurr = this.head, cloneCurr = null; 

        // Hash map which contains node to node mapping of 
        // original and clone linked list. 
        Dictionary<Node, Node> map = new Dictionary<Node, Node>(); 

        // Traverse the original list and make a copy of that 
        // in the clone linked list. 
        while (origCurr != null) 
        { 
            cloneCurr = new Node(origCurr.data); 
            map.Add(origCurr, cloneCurr); 
            origCurr = origCurr.next; 
        } 

        // Adjusting the original list reference again. 
        origCurr = this.head; 

        // Traversal of original list again to adjust the next 
        // and random references of clone list using hash map. 
        while (origCurr != null) 
        { 
            cloneCurr = map[origCurr]; 
            if(origCurr.next != null) 
                cloneCurr.next = map[origCurr.next]; 
            if(origCurr.random != null) 
                cloneCurr.random = map[origCurr.random]; 
            origCurr = origCurr.next; 
        } 

        // return the head reference of the clone list. 
        return new LinkedList(map[this.head]); 
    } 
} 

// Driver code 
public static void Main(String []args) 
{ 
    // Pushing data in the linked list. 
    LinkedList list = new LinkedList(new Node(5)); 
    list.push(4); 
    list.push(3); 
    list.push(2); 
    list.push(1); 

    // Setting up random references. 
    list.head.random = list.head.next.next; 
    list.head.next.random = 
        list.head.next.next.next; 
    list.head.next.next.random = 
        list.head.next.next.next.next; 
    list.head.next.next.next.random = 
        list.head.next.next.next.next.next; 
    list.head.next.next.next.next.random = 
        list.head.next; 

    // Making a clone of the original linked list. 
    LinkedList clone = list.clone(); 

    // Print the original and cloned linked list. 
    Console.WriteLine("Original linked list"); 
    list.print(); 
    Console.WriteLine("\nCloned linked list"); 
    clone.print(); 
} 
} 

// This code is contributed by Arnab Kundu 

```

**Output:**

```
Original linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2

Cloned linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2
```

时间复杂度：`O(n)`

辅助空间：`O(n)`

本文由 **Kumar Gautam** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论

