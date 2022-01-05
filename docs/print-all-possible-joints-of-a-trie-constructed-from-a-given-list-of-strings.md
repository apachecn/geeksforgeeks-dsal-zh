# 打印由给定字符串列表构建的 Trie 的所有可能关节

> 原文:[https://www . geeksforgeeks . org/print-从给定字符串列表中构造所有可能的节点/](https://www.geeksforgeeks.org/print-all-possible-joints-of-a-trie-constructed-from-a-given-list-of-strings/)

给定一组字符串 **str** ，任务是打印由给定的一组字符串构成的 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 的所有关节。

> trie 的关节是 Trie 中有多个子节点的节点。

**例:**

```
Input:
str = {"cat", "there", "caller",
       "their", "calling"}
Output: l, a, e
Explanation:
        root
       /     \    
      c       t     
      |       |     
      a       h     
    / |       |     
   t  l       e
      |       | \
      l       i   r
      | \     |   |
      e  i    r   e
      |  |
      r  n
      |
      g 

Input:
str = {"Candy", "cat",
       "Caller", "calling"}
Output: l, a
Explanation:
       root
        |    
        c   
        |   
        a        
     /  | \        
    l   n  t       
    |   |       
    l   d       
   | \  |      
   e  i y      
   |  |
   r  n
      |
      g
```

**方法:**
按照下面给出的步骤解决问题:

*   遍历 Trie，取一个 **currChild** 变量为零。
*   当前节点有子节点时，将 **currChild** 增加 1，从当前节点返回时，检查 **currChild** 是否大于 1。如果是，打印这个字符或关节。否则，跳到下一个字符。

以下是上述方法的实现:

## C++

```
// C++ program to print all the
// joints of a Trie constructed
// from a given set of strings

#include <bits/stdc++.h>
using namespace std;
#define CHILDREN 26
#define MAX 100

// Trie node
struct trie {
    trie* child[CHILDREN];
    bool endOfWord;
};

// Function will return the
// new node(initialized to NULLs)
trie* createNode()
{
    trie* temp = new trie();
    temp->endOfWord = false;
    for (int i = 0; i < CHILDREN; i++) {
        temp->child[i] = NULL;
    }
    return temp;
}

// Function will insert the
// string in a trie recursively
void insertRecursively(trie* itr,
                       string str, int i)
{
    if (i < str.length()) {
        int index = str[i] - 'a';
        if (itr->child[index] == NULL) {
            // Create a new node
            itr->child[index] = createNode();
        }

        // Recursive call for insertion
        // of string
        insertRecursively(itr->child[index],
                          str, i + 1);
    }

    else {
        // Make the endOfWord true
        // which represents
        // the end of string
        itr->endOfWord = true;
    }
}

// Function call to insert a string
void insert(trie* itr, string str)
{
    // Function call with
    // necessary arguments
    insertRecursively(itr, str, 0);
}

// Function to check whether the
// node is leaf or not
bool isLeafNode(trie* root)
{
    return root->endOfWord != false;
}

// Function to display the Joints of trie
void display(trie* root, trie* itr,
             char str[], int level)
{
    // Count current child
    int currChild = 0;

    for (int i = 0; i < CHILDREN; i++)

    {
        // Check for NON NULL child is found
        // add parent key to str and
        // call the display function
        // recursively for child node
        if (itr->child[i]) {
            str[level] = i + 'a';
            display(root, itr->child[i],
                    str, level + 1);
            currChild++;
        }
    }

    // Print character if it has more
    // than 1 child
    if (currChild > 1 && itr != root) {
        cout << str[level - 1] << endl;
    }
}

// Function call for displaying Joint
void displayJoint(trie* root)
{
    int level = 0;
    char str[MAX];
    display(root, root, str, level);
}

// Driver code
int main()
{
    trie* root = createNode();
    vector<string> s = { "geek", "geeky",
                         "geeks", "gel" };

    for (string str : s) {
        insert(root, str);
    }

    displayJoint(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all the
// joints of a Trie constructed
// from a given set of Strings
import java.util.*;

class GFG{
static final int CHILDREN = 26;
static final int MAX = 100;

// Trie node
static class trie
{
    trie []child = new trie[CHILDREN];
    boolean endOfWord;
};

// Function will return the
// new node(initialized to nulls)
static trie createNode()
{
    trie temp = new trie();
    temp.endOfWord = false;
    for (int i = 0; i < CHILDREN; i++)
    {
        temp.child[i] = null;
    }
    return temp;
}

// Function will insert the
// String in a trie recursively
static void insertRecursively(trie itr,
                            String str, int i)
{
    if (i < str.length())
    {
        int index = str.charAt(i) - 'a';
        if (itr.child[index] == null)
        {
            // Create a new node
            itr.child[index] = createNode();
        }

        // Recursive call for insertion
        // of String
        insertRecursively(itr.child[index],
                          str, i + 1);
    }

    else
    {
        // Make the endOfWord true
        // which represents
        // the end of String
        itr.endOfWord = true;
    }
}

// Function call to insert a String
static void insert(trie itr, String str)
{
    // Function call with
    // necessary arguments
    insertRecursively(itr, str, 0);
}

// Function to check whether the
// node is leaf or not
static boolean isLeafNode(trie root)
{
    return root.endOfWord != false;
}

// Function to display the Joints of trie
static void display(trie root, trie itr,
                    char str[], int level)
{
    // Count current child
    int currChild = 0;

    for (int i = 0; i < CHILDREN; i++)
    {
        // Check for NON null child is found
        // add parent key to str and
        // call the display function
        // recursively for child node
        if (itr.child[i] != null)
        {
            str[level] = (char) (i + 'a');
            display(root, itr.child[i],
                    str, level + 1);
            currChild++;
        }
    }

    // Print character if it has more
    // than 1 child
    if (currChild > 1 && itr != root)
    {
        System.out.print(str[level - 1] + "\n");
    }
}

// Function call for displaying Joint
static void displayJoint(trie root)
{
    int level = 0;
    char []str = new char[MAX];
    display(root, root, str, level);
}

// Driver code
public static void main(String[] args)
{
    trie root = createNode();
    String []s = { "geek", "geeky",
                   "geeks", "gel" };

    for (String str : s)
    {
        insert(root, str);
    }

    displayJoint(root);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to traverse in bottom up manner
CHILDREN = 26
MAX = 100

# Trie node
class trie:

    def __init__(self):
        self.child = [None for i in range(CHILDREN)]

        # endOfWord is true if the node represents
        # end of a word
        self.endOfWord = False

# Function will return the new node(initialized to NULLs)
def createNode():

    temp = trie()
    return temp

# Function will inert the string in a trie recursively
def insertRecursively(itr, str, i):

    if(i < len(str)):

        index = ord(str[i]) - ord('a')

        if(itr.child[index] == None ):

            #Create a new node
            itr.child[index] = createNode();

        # Recursive call for insertion of string
        insertRecursively(itr.child[index], str, i + 1);

    else:

        # Make the endOfWord true which represents
        # the end of string
        itr.endOfWord = True;

# Function call to insert a string
def insert(itr, str):

    # Function call with necessary arguments
    insertRecursively(itr, str, 0);

# Function to check whether the node is leaf or not
def isLeafNode(root):

    return root.endOfWord != False;

# Function to display the Joints of trie
def display(root, itr, str, level):

    # Count current child
    currChild = 0;

    for i in range(CHILDREN):

        # Check for NON NULL child is found
        # add parent key to str and
        # call the display function
        # recursively for child node
        if (itr.child[i]):
            str[level] = chr(i + ord('a'));
            display(root, itr.child[i],str, level + 1);
            currChild += 1

    # Print character if it has more
    # than 1 child
    if (currChild > 1 and itr != root):
        print(str[level - 1])

# Function call for displaying Joint
def displayJoint(root):

    level = 0;
    str = ['' for i in range(MAX)];
    display(root, root, str, level);

# Driver code
if __name__=='__main__':

    root = createNode()
    s = ["geek", "geeky", "geeks", "gel"]

    for str in s:   
        insert(root, str);

    displayJoint(root)

    # This code is contributed by rutvik_56
```

## C#

```
// C# program to print all the
// joints of a Trie constructed
// from a given set of Strings
using System;

class GFG{

static readonly int CHILDREN = 26;
static readonly int MAX = 100;

// Trie node
class trie
{
    public trie []child = new trie[CHILDREN];
    public bool endOfWord;
};

// Function will return the
// new node(initialized to nulls)
static trie createNode()
{
    trie temp = new trie();
    temp.endOfWord = false;

    for(int i = 0; i < CHILDREN; i++)
    {
       temp.child[i] = null;
    }
    return temp;
}

// Function will insert the
// String in a trie recursively
static void insertRecursively(trie itr,
                              String str, int i)
{
    if (i < str.Length)
    {
        int index = str[i] - 'a';
        if (itr.child[index] == null)
        {

            // Create a new node
            itr.child[index] = createNode();
        }

        // Recursive call for insertion
        // of String
        insertRecursively(itr.child[index],
                          str, i + 1);
    }

    else
    {

        // Make the endOfWord true
        // which represents
        // the end of String
        itr.endOfWord = true;
    }
}

// Function call to insert a String
static void insert(trie itr, String str)
{

    // Function call with
    // necessary arguments
    insertRecursively(itr, str, 0);
}

// Function to check whether the
// node is leaf or not
static bool isLeafNode(trie root)
{
    return root.endOfWord != false;
}

// Function to display the Joints of trie
static void display(trie root, trie itr,
                    char []str, int level)
{

    // Count current child
    int currChild = 0;

    for(int i = 0; i < CHILDREN; i++)
    {

       // Check for NON null child is found
       // add parent key to str and
       // call the display function
       // recursively for child node
       if (itr.child[i] != null)
       {
           str[level] = (char)(i + 'a');
           display(root, itr.child[i],
                   str, level + 1);
           currChild++;
       }
    }

    // Print character if it has more
    // than 1 child
    if (currChild > 1 && itr != root)
    {
        Console.Write(str[level - 1] + "\n");
    }
}

// Function call for displaying Joint
static void displayJoint(trie root)
{
    int level = 0;
    char []str = new char[MAX];
    display(root, root, str, level);
}

// Driver code
public static void Main(String[] args)
{
    trie root = createNode();
    String []s = { "geek", "geeky",
                   "geeks", "gel" };

    foreach(String str in s)
    {
        insert(root, str);
    }

    displayJoint(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to print all the
    // joints of a Trie constructed
    // from a given set of Strings

    let CHILDREN = 26;
    let MAX = 100;

    // Trie node
    class trie
    {
        constructor() {
        }
    }

    // Function will return the
    // new node(initialized to nulls)
    function createNode(endOfWord)
    {
        let temp = new trie();
        temp.child = new trie(CHILDREN);
        temp.endOfWord = endOfWord;
        for (let i = 0; i < CHILDREN; i++)
        {
            temp.child[i] = null;
        }
        return temp;
    }

    // Function will insert the
    // String in a trie recursively
    function insertRecursively(itr, str, i)
    {
        if (i < str.length)
        {
            let index = str[i].charCodeAt() - 'a'.charCodeAt();
            if (itr.child[index] == null)
            {
                // Create a new node
                itr.child[index] = createNode(false);
            }

            // Recursive call for insertion
            // of String
            insertRecursively(itr.child[index], str, i + 1);
        }

        else
        {
            // Make the endOfWord true
            // which represents
            // the end of String
            itr.endOfWord = true;
        }
    }

    // Function call to insert a String
    function insert(itr, str)
    {
        // Function call with
        // necessary arguments
        insertRecursively(itr, str, 0);
    }

    // Function to check whether the
    // node is leaf or not
    function isLeafNode(root)
    {
        return root.endOfWord != false;
    }

    // Function to display the Joints of trie
    function display(root, itr, str, level)
    {
        // Count current child
        let currChild = 0;

        for (let i = 0; i < CHILDREN; i++)
        {
            // Check for NON null child is found
            // add parent key to str and
            // call the display function
            // recursively for child node
            if (itr.child[i] != null)
            {
                str[level] = String.fromCharCode(i + 'a'.charCodeAt());
                display(root, itr.child[i], str, level + 1);
                currChild++;
            }
        }

        // Print character if it has more
        // than 1 child
        if (currChild > 1 && itr != root)
        {
            document.write(str[level - 1] + "</br>");
        }
    }

    // Function call for displaying Joint
    function displayJoint(root)
    {
        let level = 0;
        let str = new Array(MAX);
        display(root, root, str, level);
    }

    let root = createNode(false);
    let s = [ "geek", "geeky", "geeks", "gel" ];

    for (let str = 0; str < s.length; str++)
    {
        insert(root, s[str]);
    }

    displayJoint(root);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
k
e
```