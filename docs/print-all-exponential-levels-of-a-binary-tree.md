# 打印二叉树的所有指数级

> 原文:[https://www . geesforgeks . org/print-全指数级二叉树/](https://www.geeksforgeeks.org/print-all-exponential-levels-of-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印给定二叉树中的所有指数级。

> 一个**指数级**是这样一个级，该级的所有节点等于 x <sup>y</sup> ，&，其中 x 是最小可能正常数& y 是可变正整数。

**示例:**

```
Input:
                  20
                /    \
               9      81
              / \    /  \
             3  10  70   243
                    /     \
                   81    909
Output:
 20
 9 81  
Explanation: 
There are 2 exponential levels:
20: 201 = 20.
9, 81: 32 = 9, 34 = 81.

Input: 
              8
           /     \
          4       81
         / \    /   \
        5  125  625   5
                    /   \
                   81   909
Output: 
8
5 125 625 5
```

**方法:**解决上述问题的主要思路是使用[级序树遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。

*   执行给定二叉树的[级顺序遍历，并将每一级存储在一个向量中。](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)
*   那么，在每一级中，如果每个节点都可以用 x <sup>y</sup> 的形式表示，则为 y ≥ 0。
*   如果该级节点的任何值不等于 x <sup>y</sup> ，则跳到下一级。
*   打印上述条件成立的所有级别。

**以下是上述方法的实施:**

## C++

```
// C++ program for printing all
// Exponential levels of binary Tree

#include <bits/stdc++.h>
using namespace std;

int N = 1e6;

// To store all prime numbers
vector<int> prime;

void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..N]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    bool check[N + 1];
    memset(check, true, sizeof(check));

    for (int p = 2; p * p <= N; p++) {

        // check if prime[p] is not changed,
        // then it is a prime
        if (check[p] == true) {
            prime.push_back(p);

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
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

// Function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function To check
// whether the given node
// equals to x^y for some y>0
bool is_key(int n, int x)
{
    double p;

    // Take logx(n) with base x
    p = log10(n) / log10(x);

    int no = (int)(pow(x, int(p)));

    if (n == no)
        return true;

    return false;
}

// Function to find x
int find_x(int n)
{
    if (n == 1)
        return 1;

    double num, den, p;

    // Take log10 of n
    num = log10(n);

    int x, no;

    for (int i = 2; i <= n; i++) {
        den = log10(i);

        // Log(n) with base i
        p = num / den;

        // Raising i to the power p
        no = (int)(pow(i, int(p)));

        if (abs(no - n) < 1e-6) {
            x = i;
            break;
        }
    }

    return x;
}

// Function to check whether Level
// is Exponential or not
bool isLevelExponential(vector<int>& L)
{

    // retrieve the value of x
    // for that level
    int x = find_x(L[0]);

    for (int i = 1; i < L.size(); i++) {

        // Checking that element is
        // equal x^y for some y
        if (!is_key(L[i], x))
            return false;
    }

    return true;
}

// Function to print an Exponential level
void printExponentialLevels(vector<int>& Lev)
{
    for (auto x : Lev) {
        cout << x << " ";
    }

    cout << endl;
}

// Utility function to get Exponential
// Level of a given Binary tree
void find_ExponentialLevels(struct Node* node,
                            struct Node* queue[],
                            int index, int size)
{

    vector<int> Lev;

    while (index < size) {
        int curr_size = size;

        while (index < curr_size) {
            struct Node* temp = queue[index];

            Lev.push_back(temp->key);

            // Push left child in a queue
            if (temp->left != NULL)
                queue[size++] = temp->left;

            // Push right child in a queue
            if (temp->right != NULL)
                queue[size++] = temp->right;

            // Increment index
            index++;
        }

        // check if level is exponential
        if (isLevelExponential(Lev)) {

            printExponentialLevels(Lev);
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

// Function to find Exponential levels
// In a given binary tree
void printExponentialLevels(struct Node* node)
{
    int t_size = findSize(node);

    // Create queue
    struct Node* queue[t_size];

    // Push root node in a queue
    queue[0] = node;

    find_ExponentialLevels(node, queue, 0, 1);
}

// Driver Code
int main()
{
    /*            20
                /    \
               9      81
              / \    /  \
             3   9  81   243
                    /     \
                   81      909 */

    // Create Binary Tree as shown
    Node* root = newNode(20);
    root->left = newNode(9);
    root->right = newNode(81);

    root->left->left = newNode(3);
    root->left->right = newNode(9);
    root->right->left = newNode(81);
    root->right->right = newNode(243);

    root->right->left->left = newNode(81);
    root->right->right->right = newNode(909);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print Exponential Levels
    printExponentialLevels(root);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for printing
# all Exponential levels of
# binary Tree
import math

# A Tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Utility function to create
# a new node
def newNode(key):

    temp = Node(key)
    return temp

N = 1000000

# Vector to store all the
# prime numbers
prime = []

# Function to store all the
# prime numbers in an array
def SieveOfEratosthenes():

    # Create a boolean array "prime[0..N]"
    # and initialize all the entries in it
    # as true. A value in prime[i]
    # will finally be false if
    # i is Not a prime, else true.
    check = [True for i in range(N + 1)]

    p = 2

    while(p * p <= N):

        # If prime[p] is not
        # changed, then it is
        # a prime
        if (check[p]):
            prime.append(p);

            # Update all multiples of p
            # greater than or equal to
            # the square of it
            # numbers which are multiples of p
            # and are less than p^2
            # are already marked.
            for i in range(p * p, N + 1, p):
                check[i] = False;

        p += 1         

# Function To check
# whether the given node
# equals to x^y for some y>0
def is_key(n, x):

    # Take logx(n) with base x
    p = (math.log10(n) /
         math.log10(x));

    no = int(math.pow(x, int(p)));

    if (n == no):
        return True;

    return False;

# Function to find x
def find_x(n):

    if (n == 1):
        return 1;

    den = 0
    p = 0

    # Take log10 of n
    num = math.log10(n);

    x = 0
    no = 0;

    for i in range(2, n + 1):   
        den = math.log10(i);

        # Log(n) with base i
        p = num / den;

        # Raising i to the power p
        no = int(math.pow(i, int(p)));

        if(abs(no - n) < 0.000001):
            x = i;
            break;

    return x;

# Function to check whether Level
# is Exponential or not
def isLevelExponential(L):

    # retrieve the value of x
    # for that level
    x = find_x(L[0]);

    for i in range(1, len(L)):

        # Checking that element is
        # equal x^y for some y
        if (not is_key(L[i], x)):
            return False;

    return True;

# Function to print an
# Exponential level
def printExponentialLevels(Lev):

    for x in Lev:
        print(x, end = ' ')

    print()

# Utility function to get Exponential
# Level of a given Binary tree
def find_ExponentialLevels(node, queue,
                           index, size):

    Lev = []

    while (index < size):       
        curr_size = size;
        while index < curr_size:           
            temp = queue[index]; 
            Lev.append(temp.key);

            # Push left child in a queue
            if (temp.left != None):
                queue[size] = temp.left;
                size += 1

            # Push right child in a queue
            if (temp.right != None):
                queue[size] = temp.right;
                size += 1

            # Increment index
            index += 1;       

        # check if level is exponential
        if (isLevelExponential(Lev)):
            printExponentialLevels(Lev);

        Lev.clear();   

# Function to find total no of nodes
# In a given binary tree
def findSize(node):

    # Base condition
    if (node == None):
        return 0;

    return (1 + findSize(node.left) +
                findSize(node.right));

 # Function to find Exponential levels
# In a given binary tree
def printExponentialLevel(node):

    t_size = findSize(node);

    # Create queue
    queue=[0 for i in range(t_size)]

    # Push root node in a queue
    queue[0] = node;

    find_ExponentialLevels(node, queue,
                           0, 1);

# Driver code   
if __name__ == "__main__":

    '''            20
                /    \
               9      81
              / \    /  \
             3   9  81   243
                    /     \
                   81      909 '''

    # Create Binary Tree as shown
    root = newNode(20);
    root.left = newNode(9);
    root.right = newNode(81);

    root.left.left = newNode(3);
    root.left.right = newNode(9);
    root.right.left = newNode(81);
    root.right.right = newNode(243);

    root.right.left.left = newNode(81);
    root.right.right.right = newNode(909);

    # To save all prime numbers
    SieveOfEratosthenes();

    # Print Exponential Levels
    printExponentialLevel(root);

# This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>

    // JavaScript program for printing all
    // Exponential levels of binary Tree

    let Lev = []

    // A Tree Node
    class Node {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    };

    // Function to create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return temp;
    }

    let N = 1e6;

    // To store all prime numbers
    let prime = [];

    function SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..N]" and initialize
        // all entries it as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.
        let check = new Array(N + 1);
        check.fill(true);

        for (let p = 2; p * p <= N; p++) {

            // check if prime[p] is not changed,
            // then it is a prime
            if (check[p] == true) {
                prime.push(p);

                // Update all multiples of p greater than or
                // equal to the square of it
                // numbers which are multiple of p and are
                // less than p^2 are already been marked.
                for (let i = p * p; i <= N; i += p)
                    check[i] = false;
            }
        }
    }

    // Function To check
    // whether the given node
    // equals to x^y for some y>0
    function is_key(n, x)
    {
        let p;

        // Take logx(n) with base x
        p = Math.log10(n) / Math.log10(x);

        let no = parseInt(Math.pow(x, parseInt(p, 10)), 10);

        if (n == no)
            return true;

        return false;
    }

    // Function to find x
    function find_x(n)
    {
        if (n == 1)
            return 1;

        let num, den, p;

        // Take log10 of n
        num = Math.log10(n);

        let x, no;

        for (let i = 2; i <= n; i++) {
            den = Math.log10(i);

            // Log(n) with base i
            p = num / den;

            // Raising i to the power p
            no = parseInt(Math.pow(i, parseInt(p, 10)), 10);

            if (Math.abs(no - n) < 1e-6) {
                x = i;
                break;
            }
        }

        return x;
    }

    // Function to check whether Level
    // is Exponential or not
    function isLevelExponential(L)
    {

        // retrieve the value of x
        // for that level
        let x = find_x(L[0]);

        for (let i = 1; i < L.length; i++) {

            // Checking that element is
            // equal x^y for some y
            if (!is_key(L[i], x))
                return false;
        }

        return true;
    }

    // Function to print an Exponential level
    function printExponentialLevels()
    {
        for (let x = 0; x < Lev.length; x++) {
            document.write(Lev[x] + " ");
        }

        document.write("</br>");
    }

    // Utility function to get Exponential
    // Level of a given Binary tree
    function find_ExponentialLevels(node, queue, index, size)
    {
        while (index < size) {
            let curr_size = size;

            while (index < curr_size) {
                let temp = queue[index];

                Lev.push(temp.key);

                // Push left child in a queue
                if (temp.left != null)
                    queue[size++] = temp.left;

                // Push right child in a queue
                if (temp.right != null)
                    queue[size++] = temp.right;

                // Increment index
                index++;
            }

            // check if level is exponential
            if (isLevelExponential(Lev)) {

                printExponentialLevels();
            }
            Lev = [];
        }
    }

    // Function to find total no of nodes
    // In a given binary tree
    function findSize(node)
    {
        // Base condition
        if (node == null)
            return 0;

        return 1
               + findSize(node.left)
               + findSize(node.right);
    }

    // Function to find Exponential levels
    // In a given binary tree
    function printexponentialLevels(node)
    {
        let t_size = findSize(node);

        // Create queue
        let queue = new Array(t_size);
        queue.fill(0);

        // Push root node in a queue
        queue[0] = node;

        find_ExponentialLevels(node, queue, 0, 1);
    }

    /*            20
                /    \
               9      81
              / \    /  \
             3   9  81   243
                    /     \
                   81      909 */

    // Create Binary Tree as shown
    let root = newNode(20);
    root.left = newNode(9);
    root.right = newNode(81);

    root.left.left = newNode(3);
    root.left.right = newNode(9);
    root.right.left = newNode(81);
    root.right.right = newNode(243);

    root.right.left.left = newNode(81);
    root.right.right.right = newNode(909);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print Exponential Levels
    printexponentialLevels(root);

</script>
```

**Output:** 

```
20 
9 81 
3 9 81 243
```