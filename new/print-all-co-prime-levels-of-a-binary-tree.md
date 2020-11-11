# 打印二叉树的所有副本级

> 原文：[https://www.geeksforgeeks.org/print-all-co-prime-levels-of-a-binary-tree/](https://www.geeksforgeeks.org/print-all-co-prime-levels-of-a-binary-tree/)

给定[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印该树的所有**互质级别**。

> 如果此树的所有节点彼此都是[互质](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)，则将二叉树的任何级别都称为**互质级别**。

**示例**：

```
Input: 
                 1
                /  \ 
              15    5
             /     /   \ 
            11    4     15 
                   \    / 
                   2   3  
Output: 
 1
 11 4 15
 2 3
Explanation: 
First, Third and Fourth levels
are co-prime levels.

Input:
                  7
                /  \ 
              21     14 
             /  \      \
            77   16     3 
           / \     \    / 
          2   5    10  11    
                   /
                  23 
Output:
 7
 77 16 3
 23
Explanation: 
First, Third and Fifth levels
are co-prime levels.

```

**方法**：为了检查某个级别是否为同等级别，

*   首先，我们必须使用 Eratosthenes 筛子来[存储所有质数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。

*   然后，我们必须对二叉树进行[分层顺序遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)，并且必须将该级的所有元素保存到向量中。

*   此向量用于在执行层次顺序遍历时存储树的级别。

*   然后，对于每个级别，检查元素的 GCD 是否等于 1。 如果是，则此级别不是“同等优先”，否则打印该级别的所有元素。

下面是上述方法的实现：

## C++

```cpp

// C++ program for printing Co-prime 
// levels of binary Tree 

#include <bits/stdc++.h> 
using namespace std; 

int N = 1000000; 

// To store all prime numbers 
vector<int> prime; 

void SieveOfEratosthenes() 
{ 
    // Create a boolean array "prime[0..N]" 
    // and initialize all entries it as true. 
    // A value in prime[i] will finally 
    // be false if i is Not a prime, else true. 
    bool check[N + 1]; 
    memset(check, true, sizeof(check)); 

    for (int p = 2; p * p <= N; p++) { 

        // If prime[p] is not changed, 
        // then it is a prime 
        if (check[p] == true) { 

            prime.push_back(p); 

            // Update all multiples of p 
            // greater than or equal to 
            // the square of it 
            // numbers which are multiples of p 
            // and are less than p^2 
            // are already marked. 
            for (int i = p * p; i <= N; i += p) 
                check[i] = false; 
        } 
    } 
} 

// A Tree node 
struct Node { 
    int key; 
    struct Node *left, *right; 
}; 

// Utility function to create a new node 
Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->key = key; 
    temp->left = temp->right = NULL; 
    return (temp); 
} 

// Function to check whether Level 
// is Co-prime or not 
bool isLevelCo_Prime(vector<int>& L) 
{ 

    int max = 0; 
    for (auto x : L) { 
        if (max < x) 
            max = x; 
    } 

    for (int i = 0; 
         i * prime[i] <= max / 2; 
         i++) { 

        int ct = 0; 

        for (auto x : L) { 
            if (x % prime[i] == 0) 
                ct++; 
        } 

        // If not co-prime 
        if (ct > 1) { 
            return false; 
        } 
    } 

    return true; 
} 

// Function to print a Co-Prime level 
void printCo_PrimeLevels(vector<int>& Lev) 
{ 
    for (auto x : Lev) { 
        cout << x << " "; 
    } 

    cout << endl; 
} 

// Utility function to get Co-Prime 
// Level of a given Binary tree 
void findCo_PrimeLevels( 
    struct Node* node, 
    struct Node* queue[], 
    int index, int size) 
{ 

    vector<int> Lev; 
    // Run while loop 
    while (index < size) { 
        int curr_size = size; 

        // Run inner while loop 
        while (index < curr_size) { 
            struct Node* temp = queue[index]; 

            Lev.push_back(temp->key); 

            // Push left child in a queue 
            if (temp->left != NULL) 
                queue[size++] = temp->left; 

            // Push right child in a queue 
            if (temp->right != NULL) 
                queue[size++] = temp->right; 

            // Increament index 
            index++; 
        } 

        // If condition to check, level is 
        // prime or not 
        if (isLevelCo_Prime(Lev)) { 

            // Function call to print 
            // prime level 
            printCo_PrimeLevels(Lev); 
        } 
        Lev.clear(); 
    } 
} 

// Function to find total no of nodes 
// In a given binary tree 
int findSize(struct Node* node) 
{ 
    // Base condition 
    if (node == NULL) 
        return 0; 

    return 1 
           + findSize(node->left) 
           + findSize(node->right); 
} 

// Function to find Co-Prime levels 
// In a given binary tree 
void printCo_PrimeLevels(struct Node* node) 
{ 
    int t_size = findSize(node); 

    // Create queue 
    struct Node* queue[t_size]; 

    // Push root node in a queue 
    queue[0] = node; 

    // Function call 
    findCo_PrimeLevels(node, queue, 0, 1); 
} 

// Driver Code 
int main() 
{ 
    /*       10  
            /  \  
           48   12  
               /  \  
              18   35  
              / \  / \  
            21 29  43 16  
                      /  
                     7 
    */

    // Create Binary Tree as shown 
    Node* root = newNode(10); 
    root->left = newNode(48); 
    root->right = newNode(12); 

    root->right->left = newNode(18); 
    root->right->right = newNode(35); 

    root->right->left->left = newNode(21); 
    root->right->left->right = newNode(29); 
    root->right->right->left = newNode(43); 
    root->right->right->right = newNode(16); 
    root->right->right->right->left = newNode(7); 

    // To save all prime numbers 
    SieveOfEratosthenes(); 

    // Print Co-Prime Levels 
    printCo_PrimeLevels(root); 

    return 0; 
} 

```

## Java

```java

// Java program for printing Co-prime 
// levels of binary Tree 
import java.util.*; 

class GFG{ 

static int N = 1000000; 

// To store all prime numbers 
static Vector<Integer> prime = new Vector<Integer>(); 

static void SieveOfEratosthenes() 
{ 
    // Create a boolean array "prime[0..N]" 
    // and initialize all entries it as true. 
    // A value in prime[i] will finally 
    // be false if i is Not a prime, else true. 
    boolean []check = new boolean[N + 1]; 
    Arrays.fill(check, true); 

    for (int p = 2; p * p <= N; p++) { 

        // If prime[p] is not changed, 
        // then it is a prime 
        if (check[p] == true) { 

            prime.add(p); 

            // Update all multiples of p 
            // greater than or equal to 
            // the square of it 
            // numbers which are multiples of p 
            // and are less than p^2 
            // are already marked. 
            for (int i = p * p; i <= N; i += p) 
                check[i] = false; 
        } 
    } 
} 

// A Tree node 
static class Node { 
    int key; 
    Node left, right; 
}; 

// Utility function to create a new node 
static Node newNode(int key) 
{ 
    Node temp = new Node(); 
    temp.key = key; 
    temp.left = temp.right = null; 
    return (temp); 
} 

// Function to check whether Level 
// is Co-prime or not 
static boolean isLevelCo_Prime(Vector<Integer> L) 
{ 

    int max = 0; 
    for (int x : L) { 
        if (max < x) 
            max = x; 
    } 

    for (int i = 0; 
         i * prime.get(i) <= max / 2; 
         i++) { 

        int ct = 0; 

        for (int x : L) { 
            if (x % prime.get(i) == 0) 
                ct++; 
        } 

        // If not co-prime 
        if (ct > 1) { 
            return false; 
        } 
    } 

    return true; 
} 

// Function to print a Co-Prime level 
static void printCo_PrimeLevels(Vector<Integer> Lev) 
{ 
    for (int x : Lev) { 
        System.out.print(x+ " "); 
    } 

    System.out.println(); 
} 

// Utility function to get Co-Prime 
// Level of a given Binary tree 
static void findCo_PrimeLevels( 
    Node node, 
    Node queue[], 
    int index, int size) 
{ 

    Vector<Integer> Lev = new Vector<Integer>(); 
    // Run while loop 
    while (index < size) { 
        int curr_size = size; 

        // Run inner while loop 
        while (index < curr_size) { 
            Node temp = queue[index]; 

            Lev.add(temp.key); 

            // Push left child in a queue 
            if (temp.left != null) 
                queue[size++] = temp.left; 

            // Push right child in a queue 
            if (temp.right != null) 
                queue[size++] = temp.right; 

            // Increament index 
            index++; 
        } 

        // If condition to check, level is 
        // prime or not 
        if (isLevelCo_Prime(Lev)) { 

            // Function call to print 
            // prime level 
            printCo_PrimeLevels(Lev); 
        } 
        Lev.clear(); 
    } 
} 

// Function to find total no of nodes 
// In a given binary tree 
static int findSize(Node node) 
{ 
    // Base condition 
    if (node == null) 
        return 0; 

    return 1
           + findSize(node.left) 
           + findSize(node.right); 
} 

// Function to find Co-Prime levels 
// In a given binary tree 
static void printCo_PrimeLevels(Node node) 
{ 
    int t_size = findSize(node); 

    // Create queue 
    Node []queue = new Node[t_size]; 

    // Push root node in a queue 
    queue[0] = node; 

    // Function call 
    findCo_PrimeLevels(node, queue, 0, 1); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    /*       10  
            /  \  
           48   12  
               /  \  
              18   35  
              / \  / \  
            21 29  43 16  
                      /  
                     7 
    */

    // Create Binary Tree as shown 
    Node root = newNode(10); 
    root.left = newNode(48); 
    root.right = newNode(12); 

    root.right.left = newNode(18); 
    root.right.right = newNode(35); 

    root.right.left.left = newNode(21); 
    root.right.left.right = newNode(29); 
    root.right.right.left = newNode(43); 
    root.right.right.right = newNode(16); 
    root.right.right.right.left = newNode(7); 

    // To save all prime numbers 
    SieveOfEratosthenes(); 

    // Print Co-Prime Levels 
    printCo_PrimeLevels(root); 

} 
} 

// This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# program for printing Co-prime 
// levels of binary Tree 
using System; 
using System.Collections.Generic; 

class GFG{ 

static int N = 1000000; 

// To store all prime numbers 
static List<int> prime = new List<int>(); 

static void SieveOfEratosthenes() 
{ 
    // Create a bool array "prime[0..N]" 
    // and initialize all entries it as true. 
    // A value in prime[i] will finally 
    // be false if i is Not a prime, else true. 
    bool []check = new bool[N + 1]; 
    for(int i = 0; i <= N; i++) 
        check[i] = true; 

    for (int p = 2; p * p <= N; p++) { 

        // If prime[p] is not changed, 
        // then it is a prime 
        if (check[p] == true) { 

            prime.Add(p); 

            // Update all multiples of p 
            // greater than or equal to 
            // the square of it 
            // numbers which are multiples of p 
            // and are less than p^2 
            // are already marked. 
            for (int i = p * p; i <= N; i += p) 
                check[i] = false; 
        } 
    } 
} 

// A Tree node 
class Node { 
    public int key; 
    public Node left, right; 
}; 

// Utility function to create a new node 
static Node newNode(int key) 
{ 
    Node temp = new Node(); 
    temp.key = key; 
    temp.left = temp.right = null; 
    return (temp); 
} 

// Function to check whether Level 
// is Co-prime or not 
static bool isLevelCo_Prime(List<int> L) 
{ 

    int max = 0; 
    foreach (int x in L) { 
        if (max < x) 
            max = x; 
    } 

    for (int i = 0; 
         i * prime[i] <= max / 2; 
         i++) { 

        int ct = 0; 

        foreach (int x in L) { 
            if (x % prime[i] == 0) 
                ct++; 
        } 

        // If not co-prime 
        if (ct > 1) { 
            return false; 
        } 
    } 

    return true; 
} 

// Function to print a Co-Prime level 
static void printCo_PrimeLevels(List<int> Lev) 
{ 
    foreach (int x in Lev) { 
        Console.Write(x+ " "); 
    } 

    Console.WriteLine(); 
} 

// Utility function to get Co-Prime 
// Level of a given Binary tree 
static void findCo_PrimeLevels( 
    Node node, 
    Node []queue, 
    int index, int size) 
{ 

    List<int> Lev = new List<int>(); 
    // Run while loop 
    while (index < size) { 
        int curr_size = size; 

        // Run inner while loop 
        while (index < curr_size) { 
            Node temp = queue[index]; 

            Lev.Add(temp.key); 

            // Push left child in a queue 
            if (temp.left != null) 
                queue[size++] = temp.left; 

            // Push right child in a queue 
            if (temp.right != null) 
                queue[size++] = temp.right; 

            // Increament index 
            index++; 
        } 

        // If condition to check, level is 
        // prime or not 
        if (isLevelCo_Prime(Lev)) { 

            // Function call to print 
            // prime level 
            printCo_PrimeLevels(Lev); 
        } 
        Lev.Clear(); 
    } 
} 

// Function to find total no of nodes 
// In a given binary tree 
static int findSize(Node node) 
{ 
    // Base condition 
    if (node == null) 
        return 0; 

    return 1 
           + findSize(node.left) 
           + findSize(node.right); 
} 

// Function to find Co-Prime levels 
// In a given binary tree 
static void printCo_PrimeLevels(Node node) 
{ 
    int t_size = findSize(node); 

    // Create queue 
    Node []queue = new Node[t_size]; 

    // Push root node in a queue 
    queue[0] = node; 

    // Function call 
    findCo_PrimeLevels(node, queue, 0, 1); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    /*       10  
            /  \  
           48   12  
               /  \  
              18   35  
              / \  / \  
            21 29  43 16  
                      /  
                     7 
    */

    // Create Binary Tree as shown 
    Node root = newNode(10); 
    root.left = newNode(48); 
    root.right = newNode(12); 

    root.right.left = newNode(18); 
    root.right.right = newNode(35); 

    root.right.left.left = newNode(21); 
    root.right.left.right = newNode(29); 
    root.right.right.left = newNode(43); 
    root.right.right.right = newNode(16); 
    root.right.right.right.left = newNode(7); 

    // To save all prime numbers 
    SieveOfEratosthenes(); 

    // Print Co-Prime Levels 
    printCo_PrimeLevels(root); 

} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
10 
18 35 
21 29 43 16 
7

```



* * *

* * *



