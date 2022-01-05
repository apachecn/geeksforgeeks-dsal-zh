# 实现没有 C++ STL 容器的集合

> 原文:[https://www . geesforgeks . org/implementing-set-不带-c-stl-containers/](https://www.geeksforgeeks.org/implementing-sets-without-c-stl-containers/)

一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)是不同元素的集合。元素一旦添加就不能修改。有各种与集合相关联的操作，例如并集、交集、幂集、笛卡儿积、集差、补集和等式。

**设定方法:**

*   添加(数据)–向集合中添加“数据”
*   联合集–返回集合与集合的联合
*   相交集–返回具有集合的相交集
*   补集(U)–返回具有通用集“U”的集的补集
*   运算符-(s)–返回集合和集合的差
*   运算符= =(s)–返回集合是否等于集合
*   显示产品–将集合和集合的笛卡尔乘积打印到控制台
*   显示电源集()–将电源集打印到控制台
*   toArray()–将集合作为其元素的数组返回
*   包含–返回集合是否包含元素
*   显示设置()–将设置打印到控制台
*   getSize()–返回集合的大小

下面是使用[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)的一组实现:

## C++

```
// C++ implementation of the approach
#include <algorithm>
#include <iostream>
#include <math.h>
#include <stack>
#include <string>
using namespace std;

// Structure to implement a node of a BST
template <typename T>
struct Node {

    // The data content of the node
    T data;

    // Link to the left child
    Node* left;

    // Link to the right child
    Node* right;

public:
    // Function to print the inorder
    // traversal of the BST
    void inorder(Node* r)
    {
        if (r == NULL) {
            return;
        }
        inorder(r->left);
        cout << r->data << " ";
        inorder(r->right);
    }

    /*
        Function to check if BST contains a node
        with the given data

        @param r pointer to the root node
        @param d the data to search
        @return 1 if the node is present else 0
    */
    int containsNode(Node* r, T d)
    {
        if (r == NULL) {
            return 0;
        }
        int x = r->data == d ? 1 : 0;
        return x | containsNode(r->left, d) | containsNode(r->right, d);
    }

    /*
        Function to insert a node with
        given data into the BST

        @param r pointer to the root node
        @param d the data to insert
        @return pointer to the root of the resultant BST
    */
    Node* insert(Node* r, T d)
    {

        // Add the node when NULL node is encountered
        if (r == NULL) {
            Node<T>* tmp = new Node<T>;
            tmp->data = d;
            tmp->left = tmp->right = NULL;
            return tmp;
        }

        // Traverse the left subtree if data
        // is less than the current node
        if (d < r->data) {
            r->left = insert(r->left, d);
            return r;
        }

        // Traverse the right subtree if data
        // is greater than the current node
        else if (d > r->data) {
            r->right = insert(r->right, d);
            return r;
        }
        else
            return r;
    }
};

// Class to implement a Set using BST
template <typename T>
class Set {

    // Pointer to the root of the
    // BST storing the set data
    Node<T>* root;

    // The number of elements in the set
    int size;

public:
    // Default constructor
    Set()
    {
        root = NULL;
        size = 0;
    }

    // Copy constructor
    Set(const Set& s)
    {
        root = s.root;
        size = s.size;
    }

    /*
        Function to Add an element to the set

        @param data the element to add to the set
    */
    void add(const T data)
    {
        if (!root->containsNode(root, data)) {
            root = root->insert(root, data);
            size++;
        }
    }

    /*
        Function to compute the union of two sets

        @param s set to find union with
        @return the union set
    */
    Set unionSet(Set& s)
    {
        Set<T> res;

        // Second set is returned
        // if first set is empty
        if (root == NULL)
            return res;

        // First set is returned
        // if second set is empty
        if (s.root == NULL)
            return *this;

        // The elements of the first set
        // are added to the resultant set
        stack<Node<T>*> nodeStack;
        nodeStack.push(root);

        // Preorder traversal of the BST
        while (!nodeStack.empty()) {
            Node<T>* node;
            node = nodeStack.top();
            nodeStack.pop();

            // The data is added to the resultant set
            res.add(node->data);

            if (node->right)
                nodeStack.push(node->right);
            if (node->left)
                nodeStack.push(node->left);
        }

        // The elements of the second set
        // are added to the resultant set
        stack<Node<T>*> nodeStack1;
        nodeStack1.push(s.root);

        while (!nodeStack1.empty()) {
            Node<T>* node;
            node = nodeStack1.top();
            nodeStack1.pop();

            res.add(node->data);

            if (node->right)
                nodeStack1.push(node->right);
            if (node->left)
                nodeStack1.push(node->left);
        }

        return res;
    }

    /**
        Computes the intersection of two sets

        @param s the set to find intersection with
        @return the intersection set
    */
    Set intersectionSet(Set& s)
    {
        Set<T> res;
        stack<Node<T>*> nodeStack;
        nodeStack.push(root);

        while (!nodeStack.empty()) {
            Node<T>* node;
            node = nodeStack.top();
            nodeStack.pop();
            if (s.contains(node->data)) {
                res.add(node->data);
            }
            if (node->right)
                nodeStack.push(node->right);
            if (node->left)
                nodeStack.push(node->left);
        }
        return res;
    }

    /*
        Function to compute the complement of the set

        @param U the universal set
        @return the complement set
    */
    Set complementSet(Set& U)
    {
        return (U - *this);
    }

    /*
        Function to compute the difference of two sets

        @param s the set to be subtracted
        @return the difference set
    */
    Set operator-(Set& s)
    {
        Set<T> res;
        stack<Node<T>*> nodeStack;
        nodeStack.push(this->root);

        while (!nodeStack.empty()) {
            Node<T>* node;
            node = nodeStack.top();
            nodeStack.pop();
            if (!s.contains(node->data)) {
                res.add(node->data);
            }
            if (node->right)
                nodeStack.push(node->right);
            if (node->left)
                nodeStack.push(node->left);
        }
        return res;
    }

    /*
        Function that checks equality of two sets

        @param s set to check equality with
        @return boolean value denoting result of check
    */
    bool operator==(Set& s)
    {
        if (s.getSize() != size) {
            return false;
        }
        stack<Node<T>*> nodeStack;
        nodeStack.push(this->root);

        while (!nodeStack.empty()) {
            Node<T>* node;
            node = nodeStack.top();
            nodeStack.pop();
            if (!s.contains(node->data)) {
                return false;
            }
            if (node->right)
                nodeStack.push(node->right);
            if (node->left)
                nodeStack.push(node->left);
        }
        return true;
    }

    /*
        Function to print the cartesian product of two sets

        @param s the set to find product with
    */
    void displayProduct(Set& s)
    {
        int i, j, n2 = s.getSize();
        T* A = toArray();
        T* B = s.toArray();

        i = 0;

        cout << "{ ";
        for (i = 0; i < size; i++) {
            for (j = 0; j < n2; j++) {
                cout << "{ " << A[i] << " " << B[j] << " } ";
            }
        }
        cout << "}" << endl;
    }

    // Function to print power set of the set
    void displayPowerSet()
    {
        int n = pow(2, size);
        T* A = toArray();
        int i;
        while (n-- > 0) {
            cout << "{ ";
            for (int i = 0; i < size; i++) {
                if ((n & (1 << i)) == 0) {
                    cout << A[i] << " ";
                }
            }
            cout << "}" << endl;
        }
    }

    /*
        Function to convert the set into an array

        @return array of set elements
    */
    T* toArray()
    {
        T* A = new T[size];
        int i = 0;
        stack<Node<T>*> nodeStack;
        nodeStack.push(this->root);

        while (!nodeStack.empty()) {
            Node<T>* node;
            node = nodeStack.top();
            nodeStack.pop();

            A[i++] = node->data;

            if (node->right)
                nodeStack.push(node->right);
            if (node->left)
                nodeStack.push(node->left);
        }
        return A;
    }

    /*
        Function to check whether the set contains an element

        @param data the element to search
        @return relut of check
    */
    bool contains(T data)
    {
        return root->containsNode(root, data) ? true : false;
    }

    // Function to print the contents of the set
    void displaySet()
    {
        cout << "{ ";
        root->inorder(root);
        cout << "}" << endl;
    }

    /*
        Function to return the current size of the Set

        @return size of set
    */
    int getSize()
    {
        return size;
    }
};

// Driver code
int main()
{

    // Create Set A
    Set<int> A;

    // Add elements to Set A
    A.add(1);
    A.add(2);
    A.add(3);
    A.add(2);

    // Display the contents of Set A
    cout << "A = ";
    A.displaySet();
    cout << "P(A) = " << endl;
    A.displayPowerSet();

    // Check if Set A contains some elements
    cout << "A " << (A.contains(3) ? "contains"
                                   : "does not contain")
         << " 3" << endl;
    cout << "A " << (A.contains(4) ? "contains"
                                   : "does not contain")
         << " 4" << endl;
    cout << endl;

    // Create Set B
    Set<int> B;

    // Insert elements to Set B
    B.add(1);
    B.add(2);
    B.add(4);

    // Display the contents of Set B
    cout << "B = ";
    B.displaySet();
    cout << "P(B) = " << endl;
    B.displayPowerSet();
    cout << endl;

    // Create Set C
    Set<int> C;
    C.add(1);
    C.add(2);
    C.add(4);

    // Display the contents of Set C
    cout << "C = ";
    C.displaySet();
    cout << endl;

    // Set F contains the difference
    // of the Sets A and B
    Set<int> F = A - B;
    cout << "A - B = ";
    F.displaySet();
    cout << endl;

    // Set D contains the union
    // of the Sets A and B
    Set<int> D = A.unionSet(B);
    cout << "A union B = ";
    D.displaySet();
    cout << endl;

    // Set E contains the intersection
    // of the Sets A and B
    Set<int> E = A.intersectionSet(B);
    cout << "A intersection B = ";
    E.displaySet();
    cout << endl;

    // Display the product
    cout << "A x B = ";
    A.displayProduct(B);
    cout << endl;

    // Equality tests
    cout << "Equality of Sets:" << endl;

    cout << "A "
         << ((A == B) ? "" : "!") << "= B"
         << endl;
    cout << "B "
         << ((B == C) ? "" : "!") << "= C"
         << endl;
    cout << "A "
         << ((A == C) ? "" : "!") << "= C"
         << endl;
    cout << endl;

    Set<int> U;
    U.add(1);
    U.add(2);
    U.add(3);
    U.add(4);
    U.add(5);
    U.add(6);
    U.add(7);

    // Complements of the respective Sets
    Set<int> A1 = A.complementSet(U);
    Set<int> B1 = B.complementSet(U);
    Set<int> C1 = C.complementSet(U);

    cout << "A' = ";
    A1.displaySet();
    cout << "B' = ";
    B1.displaySet();
    cout << "C' = ";
    C1.displaySet();

    return 0;
}
```

**Output:** 

```
A = { 1 2 3 }
P(A) = 
{ }
{ 1 }
{ 2 }
{ 1 2 }
{ 3 }
{ 1 3 }
{ 2 3 }
{ 1 2 3 }
A contains 3
A does not contain 4

B = { 1 2 4 }
P(B) = 
{ }
{ 1 }
{ 2 }
{ 1 2 }
{ 4 }
{ 1 4 }
{ 2 4 }
{ 1 2 4 }

C = { 1 2 4 }

A - B = { 3 }

A union B = { 1 2 3 4 }

A intersection B = { 1 2 }

A x B = { { 1 1 } { 1 2 } { 1 4 } { 2 1 } { 2 2 } { 2 4 } { 3 1 } { 3 2 } { 3 4 } }

Equality of Sets:
A != B
B = C
A != C

A' = { 4 5 6 7 }
B' = { 3 5 6 7 }
C' = { 3 5 6 7 }
```

[AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)或[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-2-insert/)可以代替简单的 BST，使插入和搜索 O(log(n))的最坏情况复杂度。
使用 STL 集合，参考本文【C++标准模板库(STL) 中的[集合。](https://www.geeksforgeeks.org/set-in-cpp-stl/)