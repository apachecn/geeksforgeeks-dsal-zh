# 使用 Trie

以反向字典顺序打印字符串

> 原文:[https://www . geesforgeks . org/print-strings-in-reverse-dictionary-order-using-trie/](https://www.geeksforgeeks.org/print-strings-in-reverse-dictionary-order-using-trie/)

Trie 是一种高效的**信息检索数据结构**。使用 Trie，搜索复杂性可以达到最佳极限。
给**一串弦**。任务是使用 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 以相反的字典顺序打印所有字符串。如果输入数组中有重复项，我们只需要打印一次。

**示例:**

```
Input: str = {"cat", "there", "caller", "their", "calling"}
Output: there
        their
        cat
        calling
        caller

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

Input: str = {"Candy", "cat", "Caller", "calling"}
Output: cat
        candy
        calling
        caller
                                        root
                                         |    
                                         c            
                                         |            
                                         a            
                                      /   | \        
                                     l    n  t       
                                     |    |       
                                     l    d       
                                     | \  |      
                                     e  i y      
                                     |  |
                                     r  n
                                        |
                                        g
```

**进场:**

为了解决上面提到的问题，首先，使用所有字符串构造一个 Trie，然后从上到下打印一串最右边的子树，然后从上到下打印一串第二个右子树，然后打印第三个右子树，以此类推。它类似于从右到左的树的[前序](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历。

下面是上述方法的实现:

## C++

```
// C++ program to print array of string
// in reverse dictionary order using trie

#include <bits/stdc++.h>
using namespace std;

#define CHILDREN 26
#define MAX 100

// Trie node
struct trie {
    trie* child[CHILDREN];

    // endOfWord is true
    // if the node represents
    // end of a word
    bool endOfWord;
};

// Function will return
// the new node initialized NULL
trie* createNode()
{
    trie* temp = new trie();

    temp->endOfWord = false;

    for (int i = 0; i < CHILDREN; i++) {

        // Initialize null to the all child
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

        // Recursive call for insertion of string
        insertRecursively(itr->child[index], str, i + 1);
    }
    else {

        // Make the endOfWord
        // true which represents
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

// Function to check whether the node is leaf or not
bool isLeafNode(trie* root)
{
    return root->endOfWord != false;
}

// Function to display the content of trie
void displayContent(trie* root, char str[], int level)
{

    // If node is leaf node, it indicates end
    // of string, so a null character is added
    // and string is displayed
    if (isLeafNode(root)) {
        // Assign a null character in temporary string
        str[level] = '\0';
        cout << str << endl;
    }

    for (int i = CHILDREN - 1; i >= 0; i--) {

        // check if NON NULL child is found
        // add parent key to str and
        // call the display function recursively
        // for child node
        if (root->child[i]) {
            str[level] = i + 'a';
            displayContent(root->child[i], str, level + 1);
        }
    }
}

// Function call for displaying content
void display(trie* itr)
{
    int level = 0;

    char str[MAX];

    displayContent(itr, str, level);
}

// Driver code
int main()
{
    trie* root = createNode();
    insert(root, "their");
    insert(root, "there");
    insert(root, "answer");
    insert(root, "any");

    /* After inserting strings, trie will look like
                                        root
                                        / \
                                        a     t    
                                        |     |    
                                        n     h    
                                        | \ |
                                        s y e    
                                        |     | \
                                        w     i r
                                        |     | |
                                        e     r e
                                        |    
                                        r
    */

    display(root);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to print array of string
# in reverse dictionary order using trie

CHILDREN = 26
MAX = 100

# Trie node
class trie:

    def __init__(self):      
        self.child = [0 for i in range(CHILDREN)]

        # endOfWord is true
        # if the node represents
        # end of a word
        self.endOfWord = False;

# Function will return
# the new node initialized NONE
def createNode():

    temp = trie();

    temp.endOfWord = False;

    for i in range(CHILDREN):

        # Initialize null to the all child
        temp.child[i] = None;

    return temp;

# Function will insert the
# string in a trie recursively
def insertRecursively(itr, str, i):

    if (i < len(str)):

        index = ord(str[i]) - ord('a');

        if (itr.child[index] == None):

            # Create a new node
            itr.child[index] = createNode();

        # Recursive call for insertion of string
        insertRecursively(itr.child[index], str, i + 1);

    else:

        # Make the endOfWord
        # true which represents
        # the end of string
        itr.endOfWord = True;

# Function call to insert a string
def insert(itr, str):

    # Function call with necessary arguments
    insertRecursively(itr, str, 0);

# Function to check whether the node is leaf or not
def isLeafNode(root):

    return root.endOfWord != False;

# Function to display the content of trie
def displayContent(root, str, level):

    # If node is leaf node, it indicates end
    # of string, so a null character is added
    # and string is displayed
    if (isLeafNode(root)):

        # Assign a null character in temporary string
        print("".join(str[:level]))

    for i in range(CHILDREN-1, -1, -1):

        # check if NON NONE child is found
        # add parent key to str and
        # call the display function recursively
        # for child node
        if (root.child[i]):
            str[level] = chr(i + ord('a'));
            displayContent(root.child[i], str, level + 1);

# Function call for displaying content
def display(itr):

    level = 0;

    str = ['' for i in range(MAX)];

    displayContent(itr, str, level);

# Driver code
if __name__=='__main__':

    root = createNode();

    insert(root, "their");
    insert(root, "there");
    insert(root, "answer");
    insert(root, "any");

    ''' After inserting strings, trie will look like
                                        root
                                        / \
                                        a     t    
                                        |     |    
                                        n     h    
                                        | \ |
                                        s y e    
                                        |     | \
                                        w     i r
                                        |     | |
                                        e     r e
                                        |    
                                        r
    '''

    display(root);

# This code is contributed by rutvik_56
```

**Output:** 

```
there
their
any
answer
```