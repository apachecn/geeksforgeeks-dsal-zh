# 链表

> 原文：[https://www.geeksforgeeks.org/run-length-decoding-in-linked-list/](https://www.geeksforgeeks.org/run-length-decoding-in-linked-list/)

中的游程长度解码

给定已编码的链表，该链表使用[游程长度编码](https://www.geeksforgeeks.org/run-length-encoding/)算法进行了编码。 任务是解码给定的链表并生成输入字符串。

**游程长度编码**：在游程长度编码中，通过将字符串中重复字符的子字符串替换为字符，再加上其计数，对输入字符串进行编码。 如果字符是单个字符且不重复，则不添加字符计数。 例如，如果输入字符串为“ wwwwaaadexxxxxx”，则该函数应返回“ w4a3dex6”

**示例**：

> **输入**：列表= a- > 5- > b- > r- > 3- >空
> **输出**：字符串=“ aaaaabrrr”
> **说明**：
> 在链表中，字符为**'a'**，其计数为`5`，因此该字符重复 **5 倍**。
> 下一个字符是**'b'**，而下一个字符不是数字，因此字符**'b'**仅重复一次。
> 下一个字符为**'r'**，计数为`3`，因此该字符被重复 **3 次**。
> 
> **输入**：列表= a- > b- > r- > 3- > a- > 3- >空
> **输出**：字符串=“ abrrraaa”

**方法**：

*   遍历链表。

*   将当前字符存储在变量 **c** 中。

*   检查下一个节点是否为数字并将该数字存储在**计数**中，否则将**计数**为`1`。

*   将字符 **c** 追加到列表**计数**次。

下面是上述方法的实现：

## C++

```cpp

// C++ program to decode a linked list 
#include <bits/stdc++.h> 
using namespace std; 

// Linked list node 
struct Node { 
    char data; 
    struct Node* next; 
}; 

// Utility function to create a new Node 
Node* newNode(char data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 

    return temp; 
} 

// Function to append nodes to a list 
void append(struct Node* head_ref, char new_data) 
{ 
    struct Node* new_node = new Node; 

    struct Node* last = head_ref; 

    new_node->data = new_data; 

    new_node->next = NULL; 

    if (head_ref == NULL) { 
        head_ref = new_node; 
        return; 
    } 

    while (last->next != NULL) 
        last = last->next; 

    last->next = new_node; 
    return; 
} 

// Function to print list 
void printList(Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 

        node = node->next; 
    } 
} 

// Function to decode the linked list 
string decodeList(Node* head) 
{ 
    Node* p = head; 
    string res = ""; 
    int count; 

    // While there are nodes left 
    while (p) { 

        // To store the count by which the current 
        // character needs to be repeated 
        count = 0; 

        // Get the current character 
        char c = p->data; 
        if (p->next) { 
            Node* temp = p->next; 

            // If current node is a digit 
            if (temp && temp->data >= '0'
                && temp->data <= '9') { 

                // Generate the integer from 
                // the consecutive digits 
                while (temp && temp->data >= '0'
                       && temp->data <= '9') { 
                    count = count * 10 + (temp->data - '0'); 
                    temp = temp->next; 
                } 
                p = temp; 
            } 
            else { 
                count = 1; 
                p = p->next; 
            } 
        } 
        else { 
            count = 1; 
            p = p->next; 
        } 

        // Repeat the character count times 
        for (int i = 0; i < count; i++) { 
            res += c; 
        } 
    } 

    return res; 
} 

// Driver code 
int main() 
{ 
    // Creating the linked list 
    Node* head = newNode('a'); 
    head->next = newNode('5'); 
    head->next->next = newNode('b'); 
    head->next->next->next = newNode('r'); 

    cout << decodeList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to decode a linked list 
class GFG { 

    // Linked list node 
    static class Node { 
        char data; 
        Node next; 
    }; 

    // Utility function to create a new Node 
    static Node newNode(char data) 
    { 
        Node temp = new Node(); 
        temp.data = data; 
        temp.next = null; 

        return temp; 
    } 

    // Function to append nodes to a list 
    static void append(Node head_ref, char new_data) 
    { 
        Node new_node = new Node(); 

        Node last = head_ref; 

        new_node.data = new_data; 

        new_node.next = null; 

        if (head_ref == null) { 
            head_ref = new_node; 
            return; 
        } 

        while (last.next != null) 
            last = last.next; 

        last.next = new_node; 
        return; 
    } 

    // Function to print list 
    static void printList(Node node) 
    { 
        while (node != null) { 
            System.out.print(node.data + " "); 

            node = node.next; 
        } 
    } 

    // Function to decode the linked list 
    static String decodeList(Node head) 
    { 
        // Pointer used to traverse through all 
        // the nodes in the list 
        Node p = head; 

        // String to store the decoded message 
        String res = ""; 

        int count; 

        // While there are nodes left 
        while (p != null) { 

            // To store the count by which the current 
            // character needs to be repeated 
            count = 0; 

            // Get the current character 
            char c = p.data; 
            if (p.next != null) { 
                Node temp = p.next; 

                // If current node is a digit 
                if (temp != null && temp.data >= '0'
                    && temp.data <= '9') { 

                    // Generate the integer from 
                    // the consecutive digits 
                    while (temp != null && temp.data >= '0'
                           && temp.data <= '9') { 
                        count = count * 10 + (temp.data - '0'); 
                        temp = temp.next; 
                    } 
                    p = temp; 
                } 
                else { 
                    count = 1; 
                    p = p.next; 
                } 
            } 
            else { 
                count = 1; 
                p = p.next; 
            } 

            // Repeat the character count times 
            for (int i = 0; i < count; i++) { 
                res += c; 
            } 
        } 

        return res; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        // Creating the linked list 
        Node head = newNode('a'); 
        head.next = newNode('5'); 
        head.next.next = newNode('b'); 
        head.next.next.next = newNode('r'); 

        System.out.println(decodeList(head)); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

## C#

```cs

// C# program to decode a linked list 
using System; 

public class GFG { 

    // Linked list node 
    public class Node { 
        public char data; 
        public Node next; 
    }; 

    // Utility function to create a new Node 
    static Node newNode(char data) 
    { 
        Node temp = new Node(); 
        temp.data = data; 
        temp.next = null; 

        return temp; 
    } 

    // Function to append nodes to a list 
    static void append(Node head_ref, char new_data) 
    { 
        Node new_node = new Node(); 

        Node last = head_ref; 

        new_node.data = new_data; 

        new_node.next = null; 

        if (head_ref == null) { 
            head_ref = new_node; 
            return; 
        } 

        while (last.next != null) 
            last = last.next; 

        last.next = new_node; 
        return; 
    } 

    // Function to print list 
    static void printList(Node node) 
    { 
        while (node != null) { 
            Console.Write(node.data + " "); 

            node = node.next; 
        } 
    } 

    // Function to decode the linked list 
    static String decodeList(Node head) 
    { 
        // Pointer used to traverse through all 
        // the nodes in the list 
        Node p = head; 

        // String to store the decoded message 
        String res = ""; 

        int count; 

        // While there are nodes left 
        while (p != null) { 

            // To store the count by which the current 
            // character needs to be repeated 
            count = 0; 

            // Get the current character 
            char c = p.data; 
            if (p.next != null) { 
                Node temp = p.next; 

                // If current node is a digit 
                if (temp != null && temp.data >= '0'
                    && temp.data <= '9') { 

                    // Generate the integer from 
                    // the consecutive digits 
                    while (temp != null && temp.data >= '0'
                           && temp.data <= '9') { 
                        count = count * 10 + (temp.data - '0'); 
                        temp = temp.next; 
                    } 
                    p = temp; 
                } 
                else { 
                    count = 1; 
                    p = p.next; 
                } 
            } 
            else { 
                count = 1; 
                p = p.next; 
            } 

            // Repeat the character count times 
            for (int i = 0; i < count; i++) { 
                res += c; 
            } 
        } 

        return res; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        // Creating the linked list 
        Node head = newNode('a'); 
        head.next = newNode('5'); 
        head.next.next = newNode('b'); 
        head.next.next.next = newNode('r'); 

        Console.WriteLine(decodeList(head)); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
aaaaabr

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。