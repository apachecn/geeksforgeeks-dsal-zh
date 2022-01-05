# 打印二叉树的所有互素路径

> 原文:[https://www . geesforgeks . org/print-all-互素-二叉树路径/](https://www.geeksforgeeks.org/print-all-coprime-path-of-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印该树的所有[](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)****路径**。**

> **如果二叉树的一条路径的所有节点都是同素的，那么这条路径被称为**同素路径**。**

****示例:****

```
**Input:** 
                 1
                /  \ 
              12    11
             /     /   \ 
            3     4     13 
                   \    / 
                   15   3  
**Output:** 
 1 11 4 15
 1 11 13 3
**Explanation:** 
{1, 11, 4, 15} and {1, 11, 13, 3}
are coprimes because their GCD is 1.

**Input:**
                  5
                /  \ 
              21     77 
             /  \      \
            61   16     16 
                  \    / 
                   10  3    
                   /
                  23 
**Output:**
 5 21 61
 5 77 16 3
**Explanation:** 
{5, 21, 61} and {5, 77, 16, 3} 
are coprimes because their GCD is 1.
```

****方法:**想法是遍历树，检查该路径中的所有元素是否互素。因此，一个有效的解决方案是[使用厄拉多塞](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的[筛生成整数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的所有质因数。使用[散列](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，存储每个元素的计数，该计数是数组中任何数字的质因数。如果元素与其他元素不包含任何公共素因子，它总是与其他元素形成共素对。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for printing Co-prime
// paths of binary Tree

#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create
// a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

int N = 1000000;

// Vector to store all the
// prime numbers
vector<int> prime;

// Function to store all the
// prime numbers in an array
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..N]"
    // and initialize all the entries in it
    // as true. A value in prime[i]
    // will finally be false if
    // i is Not a prime, else true.
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

// Function to check whether Path
// is Co-prime or not
bool isPathCo_Prime(vector<int>& path)
{

    int max = 0;

    // Iterating through the array
    // to find the maximum element
    // in the array
    for (auto x : path) {
        if (max < x)
            max = x;
    }

    for (int i = 0;
         i * prime[i] <= max / 2;
         i++) {

        int ct = 0;

        // Incrementing the variable
        // if any of the value has
        // a factor
        for (auto x : path) {
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

// Function to print a Co-Prime path
void printCo_PrimePaths(vector<int>& path)
{
    for (auto x : path) {
        cout << x << " ";
    }

    cout << endl;
}

// Function to find co-prime paths of
// binary tree
void findCo_PrimePaths(struct Node* root,
                       vector<int>& path)
{
    // Base case
    if (root == NULL)
        return;

    // Store the value in path vector
    path.push_back(root->key);

    // Recursively call for left sub tree
    findCo_PrimePaths(root->left, path);

    // Recursively call for right sub tree
    findCo_PrimePaths(root->right, path);

    // Condition to check, if leaf node
    if (root->left == NULL
        && root->right == NULL) {

        // Condition to check,
        // if path co-prime or not
        if (isPathCo_Prime(path)) {

            // Print co-prime path
            printCo_PrimePaths(path);
        }
    }

    // Remove the last element
    // from the path vector
    path.pop_back();
}

// Function to find Co-Prime paths
// In a given binary tree
void printCo_PrimePaths(struct Node* node)
{
    // To save all prime numbers
    SieveOfEratosthenes();

    vector<int> path;
    // Function call
    findCo_PrimePaths(node, path);
}

// Driver Code
int main()
{
    /*         10 
            /   \ 
           48    3 
               /   \ 
              11    37 
              / \   / \ 
             7  29 42 19 
                      / 
                     7 
    */

    // Create Binary Tree as shown
    Node* root = newNode(10);
    root->left = newNode(48);
    root->right = newNode(3);

    root->right->left = newNode(11);
    root->right->right = newNode(37);

    root->right->left->left = newNode(7);
    root->right->left->right = newNode(29);
    root->right->right->left = newNode(42);
    root->right->right->right = newNode(19);
    root->right->right->right->left = newNode(7);

    // Print Co-Prime Paths
    printCo_PrimePaths(root);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for printing Co-prime
// paths of binary Tree
import java.util.*;

class GFG{

// A Tree node
static class Node {
    int key;
    Node left, right;
};

// Utility function to create
// a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

static int N = 1000000;

// Vector to store all the
// prime numbers
static Vector<Integer> prime = new Vector<Integer>();

// Function to store all the
// prime numbers in an array
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..N]"
    // and initialize all the entries in it
    // as true. A value in prime[i]
    // will finally be false if
    // i is Not a prime, else true.
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

// Function to check whether Path
// is Co-prime or not
static boolean isPathCo_Prime(Vector<Integer> path)
{

    int max = 0;

    // Iterating through the array
    // to find the maximum element
    // in the array
    for (int x : path) {
        if (max < x)
            max = x;
    }

    for (int i = 0;
         i * prime.get(i) <= max / 2;
         i++) {

        int ct = 0;

        // Incrementing the variable
        // if any of the value has
        // a factor
        for (int x : path) {
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

// Function to print a Co-Prime path
static void printCo_PrimePaths(Vector<Integer> path)
{
    for (int x : path) {
        System.out.print(x+ " ");
    }

    System.out.println();
}

// Function to find co-prime paths of
// binary tree
static void findCo_PrimePaths(Node root,
                       Vector<Integer> path)
{
    // Base case
    if (root == null)
        return;

    // Store the value in path vector
    path.add(root.key);

    // Recursively call for left sub tree
    findCo_PrimePaths(root.left, path);

    // Recursively call for right sub tree
    findCo_PrimePaths(root.right, path);

    // Condition to check, if leaf node
    if (root.left == null
        && root.right == null) {

        // Condition to check,
        // if path co-prime or not
        if (isPathCo_Prime(path)) {

            // Print co-prime path
            printCo_PrimePaths(path);
        }
    }

    // Remove the last element
    // from the path vector
    path.remove(path.size()-1);
}

// Function to find Co-Prime paths
// In a given binary tree
static void printCo_PrimePaths(Node node)
{
    // To save all prime numbers
    SieveOfEratosthenes();

    Vector<Integer> path = new Vector<Integer>();
    // Function call
    findCo_PrimePaths(node, path);
}

// Driver Code
public static void main(String[] args)
{
    /*         10 
            /   \ 
           48    3 
               /   \ 
              11    37 
              / \   / \ 
             7  29 42 19 
                      / 
                     7 
    */

    // Create Binary Tree as shown
    Node root = newNode(10);
    root.left = newNode(48);
    root.right = newNode(3);

    root.right.left = newNode(11);
    root.right.right = newNode(37);

    root.right.left.left = newNode(7);
    root.right.left.right = newNode(29);
    root.right.right.left = newNode(42);
    root.right.right.right = newNode(19);
    root.right.right.right.left = newNode(7);

    // Print Co-Prime Paths
    printCo_PrimePaths(root);

}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program for printing Co-prime
# paths of binary Tree

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

    while (p * p <= N):

        # If prime[p] is not changed,
        # then it is a prime
        if (check[p]):
            prime.append(p)

            # Update all multiples of p
            # greater than or equal to
            # the square of it numbers
            # which are multiples of p
            # and are less than p^2
            # are already marked.
            for i in range(p * p, N + 1, p):
                check[i] = False

        p += 1   

# Function to check whether Path
# is Co-prime or not
def isPathCo_Prime(path):

    max = 0

    # Iterating through the array
    # to find the maximum element
    # in the array
    for x in path:
        if (max < x):
            max = x

    i = 0

    while (i * prime[i] <= max // 2):
        ct = 0

        # Incrementing the variable
        # if any of the value has
        # a factor
        for x in path:
            if (x % prime[i] == 0):
                ct += 1

        # If not co-prime
        if (ct > 1):
            return False

        i += 1

    return True

# Function to print a Co-Prime path
def printCo_PrimePaths(path):

    for x in path:
        print(x, end = ' ')

    print()

# Function to find co-prime paths of
# binary tree
def findCo_PrimePaths(root, path):

    # Base case
    if (root == None):
        return path

    # Store the value in path vector
    path.append(root.key)

    # Recursively call for left sub tree
    path = findCo_PrimePaths(root.left, path)

    # Recursively call for right sub tree
    path = findCo_PrimePaths(root.right, path)

    # Condition to check, if leaf node
    if (root.left == None and root.right == None):

        # Condition to check,
        # if path co-prime or not
        if (isPathCo_Prime(path)):

            # Print co-prime path
            printCo_PrimePaths(path)

    # Remove the last element
    # from the path vector
    path.pop()

    return path

# Function to find Co-Prime paths
# In a given binary tree
def printCo_PrimePath(node):

    # To save all prime numbers
    SieveOfEratosthenes()

    path = []

    # Function call
    path = findCo_PrimePaths(node, path)

# Driver code   
if __name__=="__main__":

    '''       10 
            /   \ 
           48    3 
               /   \ 
              11    37 
              / \   / \ 
             7  29 42 19 
                      / 
                     7 
    '''

    # Create Binary Tree as shown
    root = newNode(10)

    root.left = newNode(48)
    root.right = newNode(3)

    root.right.left = newNode(11)
    root.right.right = newNode(37)

    root.right.left.left = newNode(7)
    root.right.left.right = newNode(29)
    root.right.right.left = newNode(42)
    root.right.right.right = newNode(19)
    root.right.right.right.left = newNode(7)

    # Print Co-Prime Paths
    printCo_PrimePath(root)

# This code is contributed by rutvik_56
```

## **C#**

```
// C# program for printing Co-prime
// paths of binary Tree
using System;
using System.Collections.Generic;

class GFG{

// A Tree node
class Node {
    public int key;
    public Node left, right;
};

// Utility function to create
// a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

static int N = 1000000;

// List to store all the
// prime numbers
static List<int> prime = new List<int>();

// Function to store all the
// prime numbers in an array
static void SieveOfEratosthenes()
{
    // Create a bool array "prime[0..N]"
    // and initialize all the entries in it
    // as true. A value in prime[i]
    // will finally be false if
    // i is Not a prime, else true.
    bool []check = new bool[N + 1];
    for(int i=0;i<=N;i++)
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

// Function to check whether Path
// is Co-prime or not
static bool isPathCo_Prime(List<int> path)
{

    int max = 0;

    // Iterating through the array
    // to find the maximum element
    // in the array
    foreach (int x in path) {
        if (max < x)
            max = x;
    }

    for (int i = 0;
         i * prime[i] <= max / 2;
         i++) {

        int ct = 0;

        // Incrementing the variable
        // if any of the value has
        // a factor
        foreach (int x in path) {
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

// Function to print a Co-Prime path
static void printCo_PrimePaths(List<int> path)
{
    foreach (int x in path) {
        Console.Write(x+ " ");
    }

    Console.WriteLine();
}

// Function to find co-prime paths of
// binary tree
static void findCo_PrimePaths(Node root,
                       List<int> path)
{
    // Base case
    if (root == null)
        return;

    // Store the value in path vector
    path.Add(root.key);

    // Recursively call for left sub tree
    findCo_PrimePaths(root.left, path);

    // Recursively call for right sub tree
    findCo_PrimePaths(root.right, path);

    // Condition to check, if leaf node
    if (root.left == null
        && root.right == null) {

        // Condition to check,
        // if path co-prime or not
        if (isPathCo_Prime(path)) {

            // Print co-prime path
            printCo_PrimePaths(path);
        }
    }

    // Remove the last element
    // from the path vector
    path.RemoveAt(path.Count-1);
}

// Function to find Co-Prime paths
// In a given binary tree
static void printCo_PrimePaths(Node node)
{
    // To save all prime numbers
    SieveOfEratosthenes();

    List<int> path = new List<int>();
    // Function call
    findCo_PrimePaths(node, path);
}

// Driver Code
public static void Main(String[] args)
{
    /*         10 
            /   \ 
           48    3 
               /   \ 
              11    37 
              / \   / \ 
             7  29 42 19 
                      / 
                     7 
    */

    // Create Binary Tree as shown
    Node root = newNode(10);
    root.left = newNode(48);
    root.right = newNode(3);

    root.right.left = newNode(11);
    root.right.right = newNode(37);

    root.right.left.left = newNode(7);
    root.right.left.right = newNode(29);
    root.right.right.left = newNode(42);
    root.right.right.right = newNode(19);
    root.right.right.right.left = newNode(7);

    // Print Co-Prime Paths
    printCo_PrimePaths(root);

}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

    // JavaScript program for printing
    // Co-prime paths of binary Tree

    // A Tree node
    class Node {
        constructor(key) {
         this.left = null;
         this.right = null;
         this.key = key;
      }
    }

    // Utility function to create
    // a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    let N = 1000000;

    // Vector to store all the
    // prime numbers
    let prime = [];

    // Function to store all the
    // prime numbers in an array
    function SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..N]"
        // and initialize all the entries in it
        // as true. A value in prime[i]
        // will finally be false if
        // i is Not a prime, else true.
        let check = new Array(N + 1);
        check.fill(true);

        for (let p = 2; p * p <= N; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (check[p] == true) {

                prime.push(p);

                // Update all multiples of p
                // greater than or equal to
                // the square of it
                // numbers which are multiples of p
                // and are less than p^2
                // are already marked.
                for (let i = p * p; i <= N; i += p)
                    check[i] = false;
            }
        }
    }

    // Function to check whether Path
    // is Co-prime or not
    function isPathCo_Prime(path)
    {

        let max = 0;

        // Iterating through the array
        // to find the maximum element
        // in the array
        for (let x = 0; x < path.length; x++) {
            if (max < path[x])
                max = path[x];
        }

        for (let i = 0; i * prime[i] <= parseInt(max / 2, 10); i++)
        {

            let ct = 0;

            // Incrementing the variable
            // if any of the value has
            // a factor
            for (let x = 0; x < path.length; x++) {
                if (path[x] % prime[i] == 0)
                    ct++;
            }

            // If not co-prime
            if (ct > 1) {
                return false;
            }
        }

        return true;
    }

    // Function to print a Co-Prime path
    function printCoPrimePaths(path)
    {
        for (let x = 0; x < path.length; x++) {
            document.write(path[x]+ " ");
        }

        document.write("</br>");
    }

    // Function to find co-prime paths of
    // binary tree
    function findCo_PrimePaths(root, path)
    {
        // Base case
        if (root == null)
            return;

        // Store the value in path vector
        path.push(root.key);

        // Recursively call for left sub tree
        findCo_PrimePaths(root.left, path);

        // Recursively call for right sub tree
        findCo_PrimePaths(root.right, path);

        // Condition to check, if leaf node
        if (root.left == null
            && root.right == null) {

            // Condition to check,
            // if path co-prime or not
            if (isPathCo_Prime(path)) {

                // Print co-prime path
                printCoPrimePaths(path);
            }
        }

        // Remove the last element
        // from the path vector
        path.pop();
    }

    // Function to find Co-Prime paths
    // In a given binary tree
    function printCo_PrimePaths(node)
    {
        // To save all prime numbers
        SieveOfEratosthenes();

        let path = [];
        // Function call
        findCo_PrimePaths(node, path);
    }

    /*         10
            /   \
           48    3
               /   \
              11    37
              / \   / \
             7  29 42 19
                      /
                     7
    */

    // Create Binary Tree as shown
    let root = newNode(10);
    root.left = newNode(48);
    root.right = newNode(3);

    root.right.left = newNode(11);
    root.right.right = newNode(37);

    root.right.left.left = newNode(7);
    root.right.left.right = newNode(29);
    root.right.right.left = newNode(42);
    root.right.right.right = newNode(19);
    root.right.right.right.left = newNode(7);

    // Print Co-Prime Paths
    printCo_PrimePaths(root);

</script>
```

****Output:** 

```
10 3 11 7 
10 3 11 29 
10 3 37 19 7
```**