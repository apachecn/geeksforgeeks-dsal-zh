# 从 2D 矩阵

> 原文：[https://www.geeksforgeeks.org/construct-a-doubly-linked-linked-list-from-2d-matrix/](https://www.geeksforgeeks.org/construct-a-doubly-linked-linked-list-from-2d-matrix/)

构造一个双向链接链表

给定 2D [矩阵](https://www.geeksforgeeks.org/matrix/)，任务是将其转换为[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，并使用四个指针分别指向下一个，上一个，上一个和下一个，该列表的每个节点应为 连接到其下一个，上一个，上和下节点。

**范例**：

```
Input: 2D matrix 
1 2 3
4 5 6
7 8 9
Output:

```

![](img/1880f18181f141db35c4a20b2a00e8ce.png)

**方法**：主要思想是为矩阵的每个元素构造一个新节点，然后递归地创建其上，下，上一个和下一个节点，并分别更改上一个和上一个指针的指针。

**以下是上述方法的实现**：

## C++

```cpp

// C++ programm to construct a Doubly
// linked linked list from 2D Matrix

#include <iostream>
using namespace std;

// define dimension of matrix
#define dim 3

// struct node of doubly linked
// list with four pointer
// next, prev, up, down
struct Node {
    int data;
    Node* next;
    Node* prev;
    Node* up;
    Node* down;
};

// function to create a new node
Node* createNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->next = NULL;
    temp->prev = NULL;
    temp->up = NULL;
    temp->down = NULL;
    return temp;
}

// function to construct the
// doubly linked list
Node* constructDoublyListUtil(
    int mtrx[][dim],
    int i, int j,
    Node* curr)
{

    if (i >= dim || j >= dim) {
        return NULL;
    }

    // Create Node with value contain
    // in matrix at index (i, j)
    Node* temp = createNode(mtrx[i][j]);

    // Assign address of curr into
    // the prev pointer of temp
    temp->prev = curr;

    // Assign address of curr into
    // the up pointer of temp
    temp->up = curr;

    // Recursive call for next pointer
    temp->next
        = constructDoublyListUtil(
            mtrx, i, j + 1, temp);

    // Recursive call for down pointer
    temp->down
        = constructDoublyListUtil(
            mtrx, i + 1, j, temp);

    // Return newly constructed node
    // whose all four node connected
    // at it's appropriate position
    return temp;
}

// Function to construct the doubly linked list
Node* constructDoublyList(int mtrx[][dim])
{
    // function call for construct
    // the doubly linked list
    return constructDoublyListUtil(
        mtrx, 0, 0, NULL);
}

// function for displaying
// doubly linked list data
void display(Node* head)
{
    // pointer to move right
    Node* rPtr;

    // pointer to move down
    Node* dPtr = head;

    // loop till node->down is not NULL
    while (dPtr) {

        rPtr = dPtr;

        // loop till node->right is not NULL
        while (rPtr) {
            cout << rPtr->data << " ";
            rPtr = rPtr->next;
        }

        cout << "\n";
        dPtr = dPtr->down;
    }
}

// driver code
int main()
{

    // initialise matrix
    int mtrx[dim][dim] = {
        { 1, 2, 3 },
        { 4, 5, 6 },
        { 7, 8, 9 }
    };

    Node* list = constructDoublyList(mtrx);

    display(list);

    return 0;
}

```

## Java

```java

// Java program to construct a Doubly
// linked linked list from 2D Matrix
import java.util.*;

class GFG{
    // define dimension of matrix
    static int dim= 3;

    // struct node of doubly linked
    // list with four pointer
    // next, prev, up, down
    static class Node {
        int data;
        Node next;
        Node prev;
        Node up;
        Node down;
    };

    // function to create a new node
    static Node createNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.next = null;
        temp.prev = null;
        temp.up = null;
        temp.down = null;
        return temp;
    }

    // function to construct the
    // doubly linked list
    static Node constructDoublyListUtil(int mtrx[][],int i, int j,Node curr)
    {

        if (i >= dim || j >= dim) {
            return null;
        }

        // Create Node with value contain
        // in matrix at index (i, j)
        Node temp = createNode(mtrx[i][j]);

        // Assign address of curr into
        // the prev pointer of temp
        temp.prev = curr;

        // Assign address of curr into
        // the up pointer of temp
        temp.up = curr;

        // Recursive call for next pointer
        temp.next
            = constructDoublyListUtil(mtrx, i, j + 1, temp);

        // Recursive call for down pointer
        temp.down= constructDoublyListUtil(mtrx, i + 1, j, temp);

        // Return newly constructed node
        // whose all four node connected
        // at it's appropriate position
        return temp;
    }

    // Function to construct the doubly linked list
    static Node constructDoublyList(int mtrx[][])
    {
        // function call for construct
        // the doubly linked list
        return constructDoublyListUtil(mtrx, 0, 0, null);
    }

    // function for displaying
    // doubly linked list data
    static void display(Node head)
    {
        // pointer to move right
        Node rPtr;

        // pointer to move down
        Node dPtr = head;

        // loop till node.down is not null
        while (dPtr != null) {

            rPtr = dPtr;

            // loop till node.right is not null
            while (rPtr!=null) {
                System.out.print(rPtr.data+" ");
                rPtr = rPtr.next;
            }

            System.out.print("\n");
            dPtr = dPtr.down;
        }
    }

    // driver code
    public static void main(String args[])
    {

        // initialise matrix
        int mtrx[][] = {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        };

        Node list = constructDoublyList(mtrx);

        display(list);

    }
}

// This code is contributed by AbhiThakur

```

## Python3

```py

# Python3 programm to construct 
# a Doubly linked linked list 
# from 2D Matrix

# define dimension of matrix
dim = 3

# struct node of doubly linked
# list with four pointer
# next, prev, up, down
class Node:

    def __init__(self, data):

        self.data = data
        self.prev = None
        self.up = None
        self.down = None
        self.next = None       

# function to create a 
# new node
def createNode(data):

    temp = Node(data);    
    return temp;

# function to construct the
# doubly linked list
def constructDoublyListUtil(mtrx, i, 
                            j, curr):

    if (i >= dim or
        j >= dim):
        return None;

    # Create Node with value 
    # contain in matrix at 
    # index (i, j)
    temp = createNode(mtrx[i][j]);

    # Assign address of curr into
    # the prev pointer of temp
    temp.prev = curr;

    # Assign address of curr into
    # the up pointer of temp
    temp.up = curr;

    # Recursive call for next 
    # pointer
    temp.next= constructDoublyListUtil(mtrx, i, 
                                       j + 1, 
                                       temp);

    # Recursive call for down pointer
    temp.down= constructDoublyListUtil(mtrx, 
                                       i + 1, 
                                       j, temp);

    # Return newly constructed node
    # whose all four node connected
    # at it's appropriate position
    return temp;

# Function to construct the
# doubly linked list
def constructDoublyList(mtrx):

    # function call for construct
    # the doubly linked list
    return constructDoublyListUtil(mtrx,
                                   0, 0, 
                                   None);

# function for displaying
# doubly linked list data
def display(head):

    # pointer to move right
    rPtr = None

    # pointer to move down
    dPtr = head;

    # loop till node->down 
    # is not NULL
    while (dPtr != None):

        rPtr = dPtr;

        # loop till node->right 
        # is not NULL
        while (rPtr != None):
            print(rPtr.data, 
                  end = ' ')
            rPtr = rPtr.next;

        print()
        dPtr = dPtr.down;

# Driver code
if __name__=="__main__":

    # initialise matrix
    mtrx =[[1, 2, 3], 
           [4, 5, 6], 
           [7, 8, 9]]

    list = constructDoublyList(mtrx); 
    display(list);

# This code is contributed by Rutvik_56

```

## C#

```cs

// C# program to construct a Doubly
// linked linked list from 2D Matrix
using System;

class GFG{
    // define dimension of matrix
    static int dim= 3;

    // struct node of doubly linked
    // list with four pointer
    // next, prev, up, down
    public class Node {
        public int data;
        public Node next, prev, up, down;
    };

    // function to create a new node
    static Node createNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.next = null;
        temp.prev = null;
        temp.up = null;
        temp.down = null;
        return temp;
    }

    // function to construct the
    // doubly linked list
    static Node constructDoublyListUtil(int[,] mtrx,int i, int j,Node curr)
    {

        if (i >= dim || j >= dim) {
            return null;
        }

        // Create Node with value contain
        // in matrix at index (i, j)
        Node temp = createNode(mtrx[i,j]);

        // Assign address of curr into
        // the prev pointer of temp
        temp.prev = curr;

        // Assign address of curr into
        // the up pointer of temp
        temp.up = curr;

        // Recursive call for next pointer
        temp.next
            = constructDoublyListUtil(mtrx, i, j + 1, temp);

        // Recursive call for down pointer
        temp.down= constructDoublyListUtil(mtrx, i + 1, j, temp);

        // Return newly constructed node
        // whose all four node connected
        // at it's appropriate position
        return temp;
    }

    // Function to construct the doubly linked list
    static Node constructDoublyList(int[,] mtrx)
    {
        // function call for construct
        // the doubly linked list
        return constructDoublyListUtil(mtrx, 0, 0, null);
    }

    // function for displaying
    // doubly linked list data
    static void display(Node head)
    {
        // pointer to move right
        Node rPtr;

        // pointer to move down
        Node dPtr = head;

        // loop till node.down is not null
        while (dPtr != null) {

            rPtr = dPtr;

            // loop till node.right is not null
            while (rPtr!=null) {
                Console.Write(rPtr.data+" ");
                rPtr = rPtr.next;
            }

            Console.Write("\n");
            dPtr = dPtr.down;
        }
    }

    // driver code
    public static void Main()
    {

        // initialise matrix
        int[,] mtrx = {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        };

        Node list = constructDoublyList(mtrx);

        display(list);

    }
}

// This code is contributed by AbhiThakur

```

**Output:** 

```
1 2 3 
4 5 6 
7 8 9

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。