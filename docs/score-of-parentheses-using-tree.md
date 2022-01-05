# 使用树的括号得分

> 原文:[https://www . geesforgeks . org/score-of-of-括号-use-tree/](https://www.geeksforgeeks.org/score-of-parentheses-using-tree/)

给定一个包含多对平衡括号的字符串 **str** ，任务是根据给定的规则计算给定字符串的分数:

1.  “()”的得分为 1。
2.  “x y”的得分为 x + y，其中 x 和 y 是独立的平衡括号对。
3.  “(x)”有两次得分为 x(即得分为 2 *得分为 x。

**示例:**

> **输入:**str = "()"
> **输出:** 2
> **解释:**
> 这里的输入是“xy”的形式，使得总分= x 的分数+y 的分数
> ，因此，分数= 1 + 1 = 2
> 
> **输入:**str =(())”
> **输出:** 2
> **解释:**
> 这里的输入是“(x)”的形式，使得总分= 2 * x 的分数
> ，因此，分数= 2 * 1 = 2
> 
> **输入:**str =(()()))”
> **输出:** 6
> **解释:**
> 这里的输入是“(xyz)”的形式，使得总分= 2 *(x 的分数+
> 的分数+y 的分数+z 的分数)，因此是 2*(1 + 1 + 1) = 6

**方法:**想法是使用[树数据结构](https://www.geeksforgeeks.org/binary-tree-2/)和[递归](https://www.geeksforgeeks.org/recursion/)一起解决这个问题。

*   我们的树结构的根节点将代表我们输入括号的最外面一对。
*   对于包含在最外面括号内的每对平衡括号，我们将向根节点添加一个子节点。
*   向根节点声明子节点的过程将是递归的，因此它将在我们的树结构中为层次结构中的每对平衡括号创建一个节点。
*   每一对平衡的圆括号都将被视为最外层(递归地)，并生成一个节点，从而允许我们计算分数。
*   当计算分数时，我们的树的每个叶节点将被认为具有 1 的分数，为了获得其各自根节点的分数，我们需要将每个子节点的分数相加，并将该总和加倍。
*   下图显示了生成的树的递归结构，我们从底部开始计算每个级别的分数，直到到达最外面的结束括号。

下面是上述方法的实现:

## C++

```
// C++ program to find the score of
// parentheses using Tree

#include <iostream>
#include <vector>

using namespace std;

// Customized tree class or struct,
// contains all required methods.
class TreeNode {
    TreeNode* parent = NULL;
    vector<TreeNode*> children;

public:
    // Function to add a child into
    // the list of children
    void addChild(TreeNode* node)
    {
        children.push_back(node);
    }

    // Function to change the parent
    // pointer to the node passed
    void setParent(TreeNode* node)
    {
        parent = node;
    }

    // Function to return the parent
    // of the current node
    TreeNode* getParent()
    {
        return parent;
    }

    // Function to compute the score recursively.
    int computeScore()
    {

        // Base case
        if (children.size() == 0)
            return 1;

        int res = 0;

        // Adds scores of all children
        for (TreeNode* curr : children)
            res += curr->computeScore();

        if (parent == NULL)
            return res;
        else
            return 2 * res;
    }
};

// Function to create the tree structure
TreeNode* computeTree(string s)
{

    TreeNode* current = new TreeNode();
    TreeNode* root = current;

    // Creating a node for every "()"
    for (int i = 0; i < s.size(); i++) {

        // If we find "(" we add a node as
        // a child
        if (s[i] == '(') {
            TreeNode* child = new TreeNode();
            child->setParent(current);
            current->addChild(child);
            current = child;
        }

        // On finding ")" which confirms that
        // a pair is closed, we go back
        // to the parent
        else {

            current = current->getParent();
        }
    }
    return root;
}

// Driver code
int main()
{
    string s = "(()(()))";

    // Generating the tree
    TreeNode* root = computeTree(s);

    // Computing the score
    cout << root->computeScore();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the score of
// parentheses using Tree
import java.util.*;
public class Main
{
    // Customized tree class or struct,
    // contains all required methods.
    static class TreeNode {

        public TreeNode parent = null;
        public Vector<TreeNode> children = new Vector<TreeNode>();

        // Function to add a child into
        // the list of children
        public void addChild(TreeNode node)
        {
            children.add(node);
        }

        // Function to change the parent
        // pointer to the node passed
        public void setParent(TreeNode node)
        {
            parent = node;
        }

        // Function to return the parent
        // of the current node
        public TreeNode getParent()
        {
            return parent;
        }

        // Function to compute the score
        // recursively.
        public int computeScore()
        {

            // Base case
            if (children.size() == 0)
                return 1;

            int res = 0;

            // Adds scores of all children
            for(TreeNode curr : children)
                res += curr.computeScore();

            if (parent == null)
                return res;
            else
                return 2 * res;
        }
    }

    // Function to create the tree structure
    static TreeNode computeTree(String s)
    {
        TreeNode current = new TreeNode();
        TreeNode root = current;

        // Creating a node for every "()"
        for(int i = 0; i < s.length(); i++)
        {

            // If we find "(" we add a node as
            // a child
            if (s.charAt(i) == '(')
            {
                TreeNode child = new TreeNode();
                child.setParent(current);
                current.addChild(child);
                current = child;
            }

            // On finding ")" which confirms that
            // a pair is closed, we go back
            // to the parent
            else
            {
                current = current.getParent();
            }
        }
        return root;
    }

    public static void main(String[] args) {
        String s = "(()(()))";

        // Generating the tree
        TreeNode root = computeTree(s);

        // Computing the score
        System.out.print(root.computeScore());
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 program to find the score of
# parentheses using Tree

# Customized tree class or struct,
# contains all required methods.
class TreeNode:

    def __init__(self):
        self.parent = None
        self.children = []

    # Function to add a child into
    # the list of children
    def addChild(self, node):

        self.children.append(node);

    # Function to change the parent
    # pointer to the node passed
    def setParent(self, node):

        self.parent = node;

    # Function to return the parent
    # of the current node
    def getParent(self):

        return self.parent;

    # Function to compute the score recursively.
    def computeScore(self):

        # Base case
        if (len(self.children) == 0):
            return 1;

        res = 0;

        # Adds scores of all children
        for curr in self.children:

            res += curr.computeScore();

        if (self.parent == None):
            return res;
        else:
            return 2 * res;

# Function to create the tree structure
def computeTree(s):

    current = TreeNode();
    root = current;

    # Creating a node for every "()"
    for i in range(len(s)):

        # If we find "(" we add a node as
        # a child
        if (s[i] == '('):

            child = TreeNode();
            child.setParent(current);
            current.addChild(child);
            current = child;

        # On finding ")" which confirms that
        # a pair is closed, we go back
        # to the parent
        else:

            current = current.getParent();

    return root;

# Driver code
if __name__=='__main__':

    s = "(()(()))";

    # Generating the tree
    root = computeTree(s);

    # Computing the score
    print(root.computeScore())

    # This code is contributed by rutvik_56
```

## C#

```
// C# program to find the score of
// parentheses using Tree
using System;
using System.Collections;

class GFG{

// Customized tree class or struct,
// contains all required methods.
class TreeNode
{
    public TreeNode parent = null;
    public ArrayList children = new ArrayList();

    // Function to add a child into
    // the list of children
    public void addChild(TreeNode node)
    {
        children.Add(node);
    }

    // Function to change the parent
    // pointer to the node passed
    public void setParent(TreeNode node)
    {
        parent = node;
    }

    // Function to return the parent
    // of the current node
    public TreeNode getParent()
    {
        return parent;
    }

    // Function to compute the score
    // recursively.
    public int computeScore()
    {

        // Base case
        if (children.Count == 0)
            return 1;

        int res = 0;

        // Adds scores of all children
        foreach(TreeNode curr in children)
            res += curr.computeScore();

        if (parent == null)
            return res;
        else
            return 2 * res;
    }
};

// Function to create the tree structure
static TreeNode computeTree(string s)
{
    TreeNode current = new TreeNode();
    TreeNode root = current;

    // Creating a node for every "()"
    for(int i = 0; i < s.Length; i++)
    {

        // If we find "(" we add a node as
        // a child
        if (s[i] == '(')
        {
            TreeNode child = new TreeNode();
            child.setParent(current);
            current.addChild(child);
            current = child;
        }

        // On finding ")" which confirms that
        // a pair is closed, we go back
        // to the parent
        else
        {
            current = current.getParent();
        }
    }
    return root;
}

// Driver code
public static void Main()
{
    string s = "(()(()))";

    // Generating the tree
    TreeNode root = computeTree(s);

    // Computing the score
    Console.Write(root.computeScore());
}
}

// This code is contributed by pratham76
```

**Output:** 

```
6
```

**时间复杂度:** *O(N)* ，其中 N 为输入字符串的长度。
**空间复杂度:** *O(N)* ，其中 N 为输入字符串的长度。