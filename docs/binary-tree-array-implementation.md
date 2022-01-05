# 二叉树(数组实现)

> 原文:[https://www . geesforgeks . org/二叉树-数组-实现/](https://www.geeksforgeeks.org/binary-tree-array-implementation/)

给定一个表示树的数组，数组索引是树节点中的值，数组值给出该特定索引(或节点)的父节点。根节点索引的值总是-1，因为根没有父节点。从这个给定的表示构造给定二叉树的标准链接表示。[一定要参考，以便理解如何从给定的父数组表示](https://www.geeksforgeeks.org/construct-a-binary-tree-from-parent-array-representation/)构建二叉树。

**表示方式:**

树可以用下面列出的两种方式表示:

1.  动态节点表示[(链接表示)。](https://www.geeksforgeeks.org/binary-tree-set-1-introduction/)
2.  数组表示(顺序表示)。

现在，我们将讨论树的顺序表示。为了使用数组表示树，节点的编号可以从 0 –( n-1)或 1–n 开始，请考虑下图:

插图:

```
       A(0)    
     /   \
    B(1)  C(2)  
  /   \      \
 D(3)  E(4)   F(6) 
OR,
      A(1)    
     /   \
    B(2)  C(3)  
  /   \      \
 D(4)  E(5)   F(7)  
```

**程序:**

> **注:**父亲、left_son、right_son 为数组的索引值。

**情况 1:** (0—n-1)

```
if (say)father=p; 
then left_son=(2*p)+1; 
and right_son=(2*p)+2;
```

**病例 2:** 1—n

```
if (say)father=p; 
then left_son=(2*p); 
and right_son=(2*p)+1; 
```

**实施:**

**例**T2】

## C++

```
// C++ implementation of tree using array
// numbering starting from 0 to n-1.
#include<bits/stdc++.h>
using namespace std;
char tree[10];
int root(char key) {
  if (tree[0] != '\0')
    cout << "Tree already had root";
  else
    tree[0] = key;
  return 0;
}

int set_left(char key, int parent) {
  if (tree[parent] == '\0')
    cout << "\nCan't set child at"
    << (parent * 2) + 1
    << " , no parent found";
  else
    tree[(parent * 2) + 1] = key;
  return 0;
}

int set_right(char key, int parent) {
  if (tree[parent] == '\0')
    cout << "\nCan't set child at"
    << (parent * 2) + 2
    << " , no parent found";
  else
    tree[(parent * 2) + 2] = key;
  return 0;
}

int print_tree() {
  cout << "\n";
  for (int i = 0; i < 10; i++) {
    if (tree[i] != '\0')
      cout << tree[i];
    else
      cout << "-";
  }
  return 0;
}

// Driver Code
int main() {
  root('A');
  //insert_left('B',0);
  set_right('C', 0);
  set_left('D', 1);
  set_right('E', 1);
  set_right('F', 2);
  print_tree();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of tree using array
// numbering starting from 0 to n-1.

// Importing required classes
import java.io.*;
import java.lang.*;
import java.util.*;

// Class 1
// Helper class (Node class)
class Tree {

    // Main driver method
    public static void main(String[] args)
    {

        // Creating object of class 2 inside main() method
        Array_imp obj = new Array_imp();

        // Setting root node
        obj.Root("A");

        // obj.set_Left("B", 0);
        obj.set_Right("C", 0);
        obj.set_Left("D", 1);
        obj.set_Right("E", 1);
        obj.set_Left("F", 2);
        obj.print_Tree();
    }
}

// Class 2
// Helper class
class Array_imp {

    // Member variables of this class
    static int root = 0;
    static String[] str = new String[10];

    // Method 1
    // Creating root node
    public void Root(String key) { str[0] = key; }

    // Method 2
    // Creating left son of root
    public void set_Left(String key, int root)
    {
        int t = (root * 2) + 1;

        if (str[root] == null) {
            System.out.printf(
                "Can't set child at %d, no parent found\n",
                t);
        }
        else {
            str[t] = key;
        }
    }

    // Method 3
    // Creating right son of root
    public void set_Right(String key, int root)
    {
        int t = (root * 2) + 2;

        if (str[root] == null) {
            System.out.printf(
                "Can't set child at %d, no parent found\n",
                t);
        }
        else {
            str[t] = key;
        }
    }

    // Method 4
    // To print our tree
    public void print_Tree()
    {

        // Iterating using for loop
        for (int i = 0; i < 10; i++) {
            if (str[i] != null)
                System.out.print(str[i]);
            else
                System.out.print("-");
        }
    }
}
```

## C#

```
// C# implementation of tree using array
// numbering starting from 0 to n-1.
using System;

public class Tree {
    public static void Main(String[] args)
    {
        Array_imp obj = new Array_imp();
        obj.Root("A");
        // obj.set_Left("B", 0);
        obj.set_Right("C", 0);
        obj.set_Left("D", 1);
        obj.set_Right("E", 1);
        obj.set_Left("F", 2);
        obj.print_Tree();
    }
}

class Array_imp {
    static int root = 0;
    static String[] str = new String[10];

    /*create root*/
    public void Root(String key)
    {
        str[0] = key;
    }

    /*create left son of root*/
    public void set_Left(String key, int root)
    {
        int t = (root * 2) + 1;

        if (str[root] == null) {
            Console.Write("Can't set child at {0}, no parent found\n", t);
        }
        else {
            str[t] = key;
        }
    }

    /*create right son of root*/
    public void set_Right(String key, int root)
    {
        int t = (root * 2) + 2;

        if (str[root] == null) {
            Console.Write("Can't set child at {0}, no parent found\n", t);
        }
        else {
            str[t] = key;
        }
    }

    public void print_Tree()
    {
        for (int i = 0; i < 10; i++) {
            if (str[i] != null)
                Console.Write(str[i]);
            else
                Console.Write("-");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of tree using array
# numbering starting from 0 to n-1.
tree = [None] * 10

def root(key):
    if tree[0] != None:
        print("Tree already had root")
    else:
        tree[0] = key

def set_left(key, parent):
    if tree[parent] == None:
        print("Can't set child at", (parent * 2) + 1, ", no parent found")
    else:
        tree[(parent * 2) + 1] = key

def set_right(key, parent):
    if tree[parent] == None:
        print("Can't set child at", (parent * 2) + 2, ", no parent found")
    else:
        tree[(parent * 2) + 2] = key

def print_tree():
    for i in range(10):
        if tree[i] != None:
            print(tree[i], end="")
        else:
            print("-", end="")
    print()

# Driver Code
root('A')
set_right('C', 0)
set_left('D', 1)
set_right('E', 1)
set_right('F', 2)
print_tree()

# This code is contributed by Gaurav Kumar Tailor
```

**Output**

```
Can't set child at3 , no parent found
Can't set child at4 , no parent found
A-C---F---
```