# 从 2D 矩阵

> 原文：[https://www.geeksforgeeks.org/construct-linked-list-2d-matrix/](https://www.geeksforgeeks.org/construct-linked-list-2d-matrix/)

构造一个链表

给定一个矩阵。 将其转换为链接列表矩阵，以便每个节点都连接到其下一个右节点和下一个节点。

**示例**：

```
Input : 2D matrix 
1 2 3
4 5 6
7 8 9

Output :
1 -> 2 -> 3 -> NULL
|    |    |
v    v    v
4 -> 5 -> 6 -> NULL
|    |    |
v    v    v
7 -> 8 -> 9 -> NULL
|    |    |
v    v    v
NULL NULL NULL

```

**问题来源**：[事实访谈经验 | 系列 9](https://www.geeksforgeeks.org/factset-interview-experience-set-9-campus-full-time/)

这个想法是为矩阵的每个元素构造一个新节点，并递归地创建其下和右节点。

## C++

```cpp

// CPP program to construct a linked list 
// from given 2D matrix 
#include <bits/stdc++.h> 
using namespace std; 

// struct node of linked list 
struct Node { 
    int data; 
    Node* right, *down; 
}; 

// returns head pointer of linked list 
// constructed from 2D matrix 
Node* construct(int arr[][3], int i, int j,  
                              int m, int n) 
{ 
    // return if i or j is out of bounds 
    if (i > n - 1 || j > m - 1) 
        return NULL; 

    // create a new node for current i and j 
    // and recursively allocate its down and 
    // right pointers 
    Node* temp = new Node(); 
    temp->data = arr[i][j]; 
    temp->right = construct(arr, i, j + 1, m, n); 
    temp->down  = construct(arr, i + 1, j, m, n); 
    return temp; 
} 

// utility function for displaying 
// linked list data 
void display(Node* head) 
{ 
    // pointer to move right 
    Node* Rp; 

    // pointer to move down 
    Node* Dp = head; 

    // loop till node->down is not NULL 
    while (Dp) { 
        Rp = Dp; 

        // loop till node->right is not NULL 
        while (Rp) { 
            cout << Rp->data << " "; 
            Rp = Rp->right; 
        } 
        cout << "\n"; 
        Dp = Dp->down; 
    } 
} 

// driver program 
int main() 
{ 
    // 2D matrix 
    int arr[][3] = { 
        { 1, 2, 3 }, 
        { 4, 5, 6 }, 
        { 7, 8, 9 } 
    }; 

    int m = 3, n = 3; 
    Node* head = construct(arr, 0, 0, m, n); 
    display(head); 
    return 0; 
} 

```

## Java

```java

// Java program to construct a linked list 
// from given 2D matrix 
public class Linked_list_2D_Matrix { 

    // node of linked list 
    static class Node { 
        int data; 
        Node right; 
        Node down; 
    }; 

    // returns head pointer of linked list 
    // constructed from 2D matrix 
    static Node construct(int arr[][], int i, int j,  
                                     int m, int n) { 

        // return if i or j is out of bounds 
        if (i > n - 1 || j > m - 1) 
            return null; 

        // create a new node for current i and j 
        // and recursively allocate its down and 
        // right pointers 
        Node temp = new Node(); 
        temp.data = arr[i][j]; 
        temp.right = construct(arr, i, j + 1, m, n); 
        temp.down = construct(arr, i + 1, j, m, n); 
        return temp; 
    } 

    // utility function for displaying 
    // linked list data 
    static void display(Node head) { 

        // pointer to move right 
        Node Rp; 

        // pointer to move down 
        Node Dp = head; 

        // loop till node->down is not NULL 
        while (Dp != null) { 
            Rp = Dp; 

            // loop till node->right is not NULL 
            while (Rp != null) { 
                System.out.print(Rp.data + " "); 
                Rp = Rp.right; 
            } 
            System.out.println(); 
            Dp = Dp.down; 
        } 
    } 

    // driver program 
    public static void main(String args[]) { 
        // 2D matrix 
        int arr[][] = { { 1, 2, 3 },  
                        { 4, 5, 6 },  
                       { 7, 8, 9 } }; 

        int m = 3, n = 3; 
        Node head = construct(arr, 0, 0, m, n); 
        display(head); 
    } 

} 
// This code is contributed by Sumit Ghosh 

```

## Python3

```py

    # Python3 program to construct a linked list 
# from given 2D matrix 
import math 

# struct node of linked list 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.right = None
        self.down = None

# returns head pointer of linked list 
# constructed from 2D matrix 
def construct(arr, i, j, m, n): 

    # return if i or j is out of bounds 
    if (i > n - 1 or j > m - 1): 
        return None

    # create a new node for current i and j 
    # and recursively allocate its down and 
    # right pointers 
    temp = Node(arr[i][j]) 
    temp.data = arr[i][j] 
    temp.right = construct(arr, i, j + 1, m, n) 
    temp.down = construct(arr, i + 1, j, m, n) 
    return temp 

# utility function for displaying 
# linked list data 
def display(head): 

    # pointer to move right 
    # Rp 

    # pointer to move down 
    Dp = head 

    # loop till node.down is not None 
    while (Dp): 
        Rp = Dp 

        # loop till node.right is not None 
        while (Rp): 
            print(Rp.data, end = " ") 
            Rp = Rp.right 

        print() 
        Dp = Dp.down 

# Driver Code 
if __name__=='__main__':  
    # 2D matrix 
    arr = [[ 1, 2, 3 ], 
           [ 4, 5, 6 ], 
           [ 7, 8, 9 ]] 

    m, n = 3, 3
    head = construct(arr, 0, 0, m, n) 
    display(head) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# program to construct a linked list 
// from given 2D matrix 
using System; 

public class Linked_list_2D_Matrix 
{ 

    // node of linked list 
    public class Node  
    { 
        public int data; 
        public Node right; 
        public Node down; 
    }; 

    // returns head pointer of linked list 
    // constructed from 2D matrix 
    static Node construct(int [,]arr, int i, int j,  
                                    int m, int n)  
    { 

        // return if i or j is out of bounds 
        if (i > n - 1 || j > m - 1) 
            return null; 

        // create a new node for current i and j 
        // and recursively allocate its down and 
        // right pointers 
        Node temp = new Node(); 
        temp.data = arr[i, j]; 
        temp.right = construct(arr, i, j + 1, m, n); 
        temp.down = construct(arr, i + 1, j, m, n); 
        return temp; 
    } 

    // utility function for displaying 
    // linked list data 
    static void display(Node head) 
    { 

        // pointer to move right 
        Node Rp; 

        // pointer to move down 
        Node Dp = head; 

        // loop till node->down is not NULL 
        while (Dp != null)  
        { 
            Rp = Dp; 

            // loop till node->right is not NULL 
            while (Rp != null)  
            { 
                Console.Write(Rp.data + " "); 
                Rp = Rp.right; 
            } 
            Console.WriteLine(); 
            Dp = Dp.down; 
        } 
    } 

    // Driver program 
    public static void Main()  
    { 
        // 2D matrix 
        int [,]arr = { { 1, 2, 3 },  
                        { 4, 5, 6 },  
                    { 7, 8, 9 } }; 

        int m = 3, n = 3; 
        Node head = construct(arr, 0, 0, m, n); 
        display(head); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
1 2 3 
4 5 6 
7 8 9

```

本文由 [**Mandeep Singh**](https://github.com/msdeep14) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

