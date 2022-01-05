# 特里的自下而上遍历

> 原文:[https://www . geesforgeks . org/自下而上遍历 a-trie/](https://www.geeksforgeeks.org/bottom-up-traversal-of-a-trie/)

[Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 是一种高效的信息检索数据结构。使用 Trie，搜索复杂性可以达到最佳极限(密钥长度)。
给个三分。任务是以自下而上的方式打印字符
**自下而上遍历** :

> 首先打印最左侧子树的字符串(从下到上)，然后打印第二个左侧子树的字符串(从下到上)，然后打印第三个左侧子树，以此类推。

类似于[后序](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历一棵树
**例:**

```

Input :
                                          root
                                         /    \    
                                         a     t     
                                         |     |     
                                         n     h     
                                         | \   |   
                                         s  y  e     
                                         |     |  \ 
                                         w     i   r
                                         |     |   |
                                         e     r   e
                                         |        
                                         r        
Output : r, e, w, s, y, n, a, r, i, e, r, e, h, t  

Input : 
                                           root
                                          /     \    
                                         c       t     
                                         |       |     
                                         a       h     
                                         | \     |     
                                         l  t    e     
                                         |       |  \ 
                                         l       i   r
                                         | \     |   |
                                         e  i    r   e
                                         |  |
                                         r  n
                                            |
                                            g 

Output : r, e, g, n, i, l, l, t, a, c, r, i, e, r, e, h, t
```

**解释:**
在第一个例子中，根有两部分。第一部分包含字符串:“答案”和“任何”。
第二部分用字符串“他们的”和“那里”。

*   现在，我们首先得到包含字符串“答案”和“任何”的左子树，它们由字符“n”分隔。现在“n”分隔两部分字符“s”、“w”、“e”、“r”和“y”。因此，以相反的顺序打印“s”、“w”、“e”、“r”，然后打印“y”并向上打印“n”(分隔字符串)，然后向上打印“a”。现在第一个左子树以自下而上的方式打印' r '，' e '，' w '，' s '，' y '，' n '，' a '。
*   对根的另一个子树做同样的事情，这个子树包含由字符“e”分隔的字符串“他们”和“那里”。

**方法:**
这样做的想法是从 trie 的根节点开始遍历，每当我们找到一个 NON-NULL 子节点时，我们递归地向前移动，当我们得到“NULL”时，我们简单地返回并打印当前节点的值，并保持不变，直到我们找到一个叶子节点，它实际上标志着字符串的结束。
以下是上述办法的实施:

## C++

```
// CPP program to traverse in bottom up manner
#include <bits/stdc++.h>
using namespace std;
#define CHILDREN 26
#define MAX 100

// Trie node
struct trie {
    trie* child[CHILDREN];
    // endOfWord is true if the node represents
    // end of a word
    bool endOfWord;
};

// Function will return the new node(initialized to NULLs)
trie* createNode()
{
    trie* temp = new trie();
    temp->endOfWord = false;
    for (int i = 0; i < CHILDREN; i++) {
        // Initialise all child to the null, initially
        temp->child[i] = NULL;
    }

    // Return newly created node
    return temp;
}
// Function will insert the string in a trie recursively
void insertRecursively(trie* itr, string str, int i)
{
    if (i < str.length()) {
        int index = str[i] - 'a';
        if (itr->child[index] == NULL) {
            // Assigning a newly created node
            itr->child[index] = createNode();
        }
        // Recursive call for insertion
        // of a string in a trie
        insertRecursively(itr->child[index], str, i + 1);
    }
    else {
        // Make the endOfWord true which represents
        // the end of string
        itr->endOfWord = true;
    }
}
// Function call to insert a string
void insert(trie* itr, string str)
{
    // Function call with necessary arguments
    insertRecursively(itr, str, 0);
}
// Function to print traverse
// the tree in bottom to top manner
void printPattern(trie* itr)
{
    // Base condition
    if (itr == NULL)
        return;

    // Loop for printing t a value of character
    for (int i = 0; i < CHILDREN; i++) {

        // Recursive call for print pattern
        printPattern(itr->child[i]);
        if (itr->child[i] != NULL) {
            char ch = (i + 97);
            cout << ch << ", "; // Print character
        }
    }
}

// Driver code
int main()
{
    trie* root = createNode();

    // Function to insert a string
    insert(root, "their");
    insert(root, "there");
    insert(root, "answer");
    insert(root, "any");

    // Function call for printing a pattern
    printPattern(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to traverse in bottom up manner
public class Main
{
    static int CHILDREN = 26;

    // Trie node
    static class trie {

        public boolean endOfWord;
        public trie[] child;

        public trie()
        {
            endOfWord = false;

            // endOfWord is true if the node represents
            // end of a word
            child = new trie[CHILDREN];
        }
    }

    // Function will return the new node(initialized to NULLs)
    static trie createNode()
    {
        trie temp = new trie();
        temp.endOfWord = false;
        for (int i = 0; i < CHILDREN; i++)
        {

            // Initialise all child to the null, initially
            temp.child[i] = null;
        }

        // Return newly created node
        return temp;
    }

    // Function will insert the string in a trie recursively
    static void insertRecursively(trie itr, String str, int i)
    {
        if (i < str.length()) {
            int index = str.charAt(i) - 'a';
            if (itr.child[index] == null)
            {

                // Assigning a newly created node
                itr.child[index] = createNode();
            }

            // Recursive call for insertion
            // of a string in a trie
            insertRecursively(itr.child[index], str, i + 1);
        }
        else
        {

            // Make the endOfWord true which represents
            // the end of string
            itr.endOfWord = true;
        }
    }

    // Function call to insert a string
    static void insert(trie itr, String str)
    {

        // Function call with necessary arguments
        insertRecursively(itr, str, 0);
    }

    // Function to print traverse
    // the tree in bottom to top manner
    static void printPattern(trie itr)
    {

        // Base condition
        if (itr == null)
            return;

        // Loop for printing t a value of character
        for (int i = 0; i < CHILDREN; i++) {

            // Recursive call for print pattern
            printPattern(itr.child[i]);
            if (itr.child[i] != null) {
                char ch = (char)(i + 97);
                System.out.print(ch + ", "); // Print character
            }
        }
    }

    public static void main(String[] args) {
        trie root = createNode();

        // Function to insert a string
        insert(root, "their");
        insert(root, "there");
        insert(root, "answer");
        insert(root, "any");

        // Function call for printing a pattern
        printPattern(root);
    }
}

// This code is contributed by divyesh072019.
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

# Function will insert the string in a trie recursively
def insertRecursively(itr, str, i):

    if (i < len(str)):
        index = ord(str[i]) - ord('a')

        if (itr.child[index] == None):

            # Assigning a newly created node
            itr.child[index] = createNode()

        # Recursive call for insertion
        # of a string in a trie
        insertRecursively(itr.child[index], str, i + 1)

    else:
        # Make the endOfWord true which represents
        # the end of string
        itr.endOfWord = True

# Function call to insert a string
def insert(itr, str):

    # Function call with necessary arguments
    insertRecursively(itr, str, 0)

# Function to print traverse
# the tree in bottom to top manner
def printPattern(itr):

    # Base condition
    if(itr == None):
        return

    # Loop for printing t a value of character
    for i in range(CHILDREN):

        # Recursive call for print pattern
        printPattern(itr.child[i])
        if (itr.child[i] != None):
            ch = chr(i + 97)

            # Print character
            print(ch,end=', ')

# Driver code
if __name__=='__main__':

    root = createNode()

    # Function to insert a string
    insert(root, "their")
    insert(root, "there")
    insert(root, "answer")
    insert(root, "any")

    # Function call for printing a pattern
    printPattern(root)

    # This code is countributed by rutvik_56
```

## C#

```
// C# program to traverse in bottom up manner
using System;
class GFG {

    static int CHILDREN = 26;

    // Trie node
    class trie {

        public bool endOfWord;
        public trie[] child;

        public trie()
        {
            endOfWord = false;

            // endOfWord is true if the node represents
            // end of a word
            child = new trie[CHILDREN];
        }
    }

    // Function will return the new node(initialized to NULLs)
    static trie createNode()
    {
        trie temp = new trie();
        temp.endOfWord = false;
        for (int i = 0; i < CHILDREN; i++)
        {

            // Initialise all child to the null, initially
            temp.child[i] = null;
        }

        // Return newly created node
        return temp;
    }

    // Function will insert the string in a trie recursively
    static void insertRecursively(trie itr, string str, int i)
    {
        if (i < str.Length) {
            int index = str[i] - 'a';
            if (itr.child[index] == null)
            {

                // Assigning a newly created node
                itr.child[index] = createNode();
            }

            // Recursive call for insertion
            // of a string in a trie
            insertRecursively(itr.child[index], str, i + 1);
        }
        else
        {

            // Make the endOfWord true which represents
            // the end of string
            itr.endOfWord = true;
        }
    }

    // Function call to insert a string
    static void insert(trie itr, string str)
    {

        // Function call with necessary arguments
        insertRecursively(itr, str, 0);
    }

    // Function to print traverse
    // the tree in bottom to top manner
    static void printPattern(trie itr)
    {

        // Base condition
        if (itr == null)
            return;

        // Loop for printing t a value of character
        for (int i = 0; i < CHILDREN; i++) {

            // Recursive call for print pattern
            printPattern(itr.child[i]);
            if (itr.child[i] != null) {
                char ch = (char)(i + 97);
                Console.Write(ch + ", "); // Print character
            }
        }
    }

  static void Main() {
    trie root = createNode();

    // Function to insert a string
    insert(root, "their");
    insert(root, "there");
    insert(root, "answer");
    insert(root, "any");

    // Function call for printing a pattern
    printPattern(root);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // Javascript program to traverse in bottom up manner
    let CHILDREN = 26;

    // Trie node
    class trie
    {
        constructor()
        {

           // endOfWord is true if the node represents
           // end of a word
           this.child = new Array(CHILDREN);
           this.endOfWord = false;
        }
    }

    // Function will return the new node(initialized to NULLs)
    function createNode()
    {
        let temp = new trie();
        temp.endOfWord = false;
        for (let i = 0; i < CHILDREN; i++)
        {

            // Initialise all child to the null, initially
            temp.child[i] = null;
        }

        // Return newly created node
        return temp;
    }

    // Function will insert the string in a trie recursively
    function insertRecursively(itr, str, i)
    {
        if (i < str.length) {
            let index = str[i].charCodeAt() - 'a'.charCodeAt();
            if (itr.child[index] == null)
            {

                // Assigning a newly created node
                itr.child[index] = createNode();
            }

            // Recursive call for insertion
            // of a string in a trie
            insertRecursively(itr.child[index], str, i + 1);
        }
        else
        {

            // Make the endOfWord true which represents
            // the end of string
            itr.endOfWord = true;
        }
    }

    // Function call to insert a string
    function insert(itr, str)
    {

        // Function call with necessary arguments
        insertRecursively(itr, str, 0);
    }

    // Function to print traverse
    // the tree in bottom to top manner
    function printPattern(itr)
    {

        // Base condition
        if (itr == null)
            return;

        // Loop for printing t a value of character
        for (let i = 0; i < CHILDREN; i++) {

            // Recursive call for print pattern
            printPattern(itr.child[i]);
            if (itr.child[i] != null) {
                let ch = String.fromCharCode(i + 97);
                document.write(ch + ", "); // Print character
            }
        }
    }

    let root = createNode();

    // Function to insert a string
    insert(root, "their");
    insert(root, "there");
    insert(root, "answer");
    insert(root, "any");

    // Function call for printing a pattern
    printPattern(root);

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
 r, e, w, s, y, n, a, e, r, e, r, e, i, h, t,
```