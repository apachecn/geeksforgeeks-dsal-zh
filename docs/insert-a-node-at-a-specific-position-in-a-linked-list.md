# 在链表中的特定位置插入节点

> 原文：[https://www.geeksforgeeks.org/insert-a-node-at-a-specific-position-in-a-linked-list/](https://www.geeksforgeeks.org/insert-a-node-at-a-specific-position-in-a-linked-list/)

给定一个单链表，一个位置和一个元素，任务是编写一个程序以将该元素插入到链表中的给定位置。

**示例**：

```
Input: 3->5->8->10, data = 2, position = 2
Output: 3->2->5->8->10

Input: 3->5->8->10, data = 11, position = 5
Output: 3->5->8->10->11

```

**方法**：要在指定位置插入给定数据，请遵循以下算法：

*   遍历链表直到*位置 1* 的节点。

*   遍历所有*位置 1* 的节点后，将内存和给定数据分配给新节点。

*   将新节点的下一个指针指向当前节点的下一个指针。

*   将当前节点的下一个指针指向新节点。

下面是上述算法的实现。

## C++

```cpp

// C++ program for insertion in a single linked 
// list at a specified position 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list Node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Size of linked list 
int size = 0; 

// function to create and return a Node 
Node* getNode(int data) 
{ 
    // allocating space 
    Node* newNode = new Node(); 

    // inserting the required data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// function to insert a Node at required position 
void insertPos(Node** current, int pos, int data) 
{ 
    // This condition to check whether the 
    // position given is valid or not. 
    if (pos < 1 || pos > size + 1) 
        cout << "Invalid position!" << endl; 
    else { 

        // Keep looping until the pos is zero 
        while (pos--) { 

            if (pos == 0) { 

                // adding Node at required position 
                Node* temp = getNode(data); 

                // Making the new Node to point to  
                // the old Node at the same position 
                temp->next = *current; 

                // Changing the pointer of the Node previous  
                // to the old Node to point to the new Node 
                *current = temp; 
            } 
            else
              // Assign double pointer variable to point to the  
              // pointer pointing to the address of next Node  
              current = &(*current)->next; 
        } 
        size++; 
    } 
} 

// This function prints contents  
// of the linked list  
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        cout << " " << head->data; 
        head = head->next; 
    } 
    cout << endl; 
} 

// Driver Code 
int main() 
{ 
    // Creating the list 3->5->8->10 
    Node* head = NULL; 
    head = getNode(3); 
    head->next = getNode(5); 
    head->next->next = getNode(8); 
    head->next->next->next = getNode(10); 

    size = 4; 

    cout << "Linked list before insertion: "; 
    printList(head); 

    int data = 12, pos = 3; 
    insertPos(&head, pos, data); 
    cout << "Linked list after insertion of 12 at position 3: "; 
    printList(head); 

    // front of the linked list 
    data = 1, pos = 1; 
    insertPos(&head, pos, data); 
    cout << "Linked list after insertion of 1 at position 1: "; 
    printList(head); 

    // insetion at end of the linked list 
    data = 15, pos = 7; 
    insertPos(&head, pos, data); 
    cout << "Linked list after insertion of 15 at position 7: "; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program for insertion in a single linked  
// list at a specified position  

class GFG { 
    // A linked list Node 
    static class Node { 
        public int data; 
        public Node nextNode; 

        // inserting the required data 
        public Node(int data) { 
            this.data = data; 

        } 
    } 

    // function to create and return a Node 
    static Node GetNode(int data) { 
        return new Node(data); 
    } 

    // function to insert a Node at required position 
    static Node InsertPos(Node headNode, int position, int data) { 
        Node head = headNode; 
        if (position < 1) 
            System.out.print("Invalid position"); 

        // if position is 1 then new node is 
        // set infornt of head node 
        // head node is changing. 
        if (position == 1) { 
            Node newNode = new Node(data); 
            newNode.nextNode = headNode; 
            head = newNode; 
        } else { 
            while (position-- != 0) { 
                if (position == 1) { 
                    // adding Node at required position 
                    Node newNode = GetNode(data); 

                    // Making the new Node to point to 
                    // the old Node at the same position 
                    newNode.nextNode = headNode.nextNode; 

                    // Replacing current with new Node 
                    // to the old Node to point to the new Node 
                    headNode.nextNode = newNode; 
                    break; 
                } 
                headNode = headNode.nextNode; 
            } 
            if (position != 1) 
                System.out.print("Position out of range"); 
        } 
        return head; 
    } 

    static void PrintList(Node node) { 
        while (node != null) { 
            System.out.print(node.data); 
            node = node.nextNode; 
            if (node != null) 
                System.out.print(","); 
        } 
        System.out.println(); 
    } 

    // Driver code 
    public static void main(String[] args) { 
        Node head = GetNode(3); 
        head.nextNode = GetNode(5); 
        head.nextNode.nextNode = GetNode(8); 
        head.nextNode.nextNode.nextNode = GetNode(10); 

        System.out.print("Linked list before insertion: "); 
        PrintList(head); 

        int data = 12, pos = 3; 
        head = InsertPos(head, pos, data); 
        System.out.print("Linked list after" + " insertion of 12 at position 3: "); 
        PrintList(head); 

        // front of the linked list 
        data = 1; 
        pos = 1; 
        head = InsertPos(head, pos, data); 
        System.out.print("Linked list after" + "insertion of 1 at position 1: "); 
        PrintList(head); 

        // insetion at end of the linked list 
        data = 15; 
        pos = 7; 
        head = InsertPos(head, pos, data); 
        System.out.print("Linked list after" + " insertion of 15 at position 7: "); 
        PrintList(head); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# program for insertion in a single linked  
// list at a specified position  
using System; 

namespace InsertIntoLinkedList 
{ 
    class Program 
    { 
        // A linked list Node 
        private class Node 
        { 
            public int data; 
            public Node nextNode; 

            // inserting the required data  
            public Node(int data) => this.data = data; 
        } 

        // function to create and return a Node  
        static Node GetNode(int data) => new Node(data); 

        // function to insert a Node at required position  
        static Node InsertPos(Node headNode,  
                            int position, int data) 
        { 
            var head = headNode; 
            if (position < 1) 
                Console.WriteLine("Invalid position"); 

            //if position is 1 then new node is  
            // set infornt of head node 
            //head node is changing. 
            if (position == 1) 
            { 
                var newNode = new Node(data); 
                newNode.nextNode = headNode; 
                head = newNode; 
            } 
            else
            { 
                while (position-- != 0) 
                { 
                    if (position == 1) 
                    { 
                        // adding Node at required position 
                        Node newNode = GetNode(data); 

                        // Making the new Node to point to  
                        // the old Node at the same position  
                        newNode.nextNode = headNode.nextNode; 

                        // Replacing current with new Node  
                        // to the old Node to point to the new Node  
                        headNode.nextNode = newNode; 
                        break; 
                    } 
                    headNode = headNode.nextNode; 
                } 
                if (position != 1) 
                    Console.WriteLine("Position out of range"); 
            } 
            return head; 
        } 

        static void PrintList(Node node) 
        { 
            while (node != null) 
            { 
                Console.Write(node.data); 
                node = node.nextNode; 
                if(node != null) 
                    Console.Write(","); 
            } 
            Console.WriteLine(); 
        } 

        // Driver code 
        static void Main(string[] args) 
        { 
            var head = GetNode(3); 
            head.nextNode = GetNode(5); 
            head.nextNode.nextNode = GetNode(8); 
            head.nextNode.nextNode.nextNode = GetNode(10); 

            Console.WriteLine("Linked list before insertion: "); 
            PrintList(head); 

            int data = 12, pos = 3; 
            head = InsertPos(head, pos, data); 
            Console.WriteLine("Linked list after" + 
                            " insertion of 12 at position 3: "); 
            PrintList(head); 

            // front of the linked list  
            data = 1; pos = 1; 
            head = InsertPos(head, pos, data); 
            Console.WriteLine("Linked list after" +  
                            "insertion of 1 at position 1: "); 
            PrintList(head); 

            // insetion at end of the linked list  
            data = 15; pos = 7; 
            head = InsertPos(head, pos, data); 
            Console.WriteLine("Linked list after" +  
                            " insertion of 15 at position 7: "); 
            PrintList(head); 
        } 
    } 
} 

// This code is contributed by dhirucoool 

```

**时间复杂度**：`O(N)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。