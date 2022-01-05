# N 元树的迭代后序遍历

> 原文:[https://www . geesforgeks . org/iterative-post-order-遍历 n 元树/](https://www.geeksforgeeks.org/iterative-postorder-traversal-of-n-ary-tree/)

给定一棵 N 元树，任务是迭代地找到给定树的后序遍历。
**例:**

```
Input:
     1
   / | \
  3  2  4
 / \
5   6
Output: [5, 6, 3, 2, 4, 1]

Input:
   1
  / \
 2   3
Output: [2, 3, 1]
```

**方法:**
我们已经讨论了[使用一个栈对二叉树进行迭代后序遍历](https://www.geeksforgeeks.org/iterative-postorder-traversal-using-stack/)。我们将把这种方法扩展到 n 元树。这个想法很简单，对于每个节点，我们必须在遍历该节点之前遍历该节点的所有子节点(从左到右)。
**伪码:**

*   从根开始。
*   重复以下所有步骤，直到任一根！=空或堆栈不为空。
    1.  如果根！= null，然后将 root 作为索引推入堆栈，并继续向左侧节点推进。
    2.  从堆栈中弹出元素并打印出来。
    3.  从堆栈中弹出所有元素，直到堆栈不为空&&弹出的节点是
        的最后一个子节点，它是父节点。
    4.  将根分配给堆栈顶部节点的下一个子节点。

以下是上述方法的实现:

## C++

```
// C++ Program to iterative Postorder
// Traversal of N-ary Tree
#include<bits/stdc++.h>
using namespace std;

// Node class
class Node
{
    public :
    int val;
    vector<Node*> children ;

    // Default constructor
    Node() {}

    Node(int _val)
    {
        val = _val;
    }

    Node(int _val, vector<Node*> _children)
    {
        val = _val;
        children = _children;
    }
};

// Helper class to push node and it's index
// into the st
class Pair
{
    public:
    Node* node;
    int childrenIndex;
    Pair(Node* _node, int _childrenIndex)
    {
        node = _node;
        childrenIndex = _childrenIndex;
    }
};

// We will keep the start index as 0,
// because first we always
// process the left most children
int currentRootIndex = 0;
stack<Pair*> st;
vector<int> postorderTraversal ;

// Function to perform iterative postorder traversal
vector<int> postorder(Node* root)
{
    while (root != NULL || st.size() > 0)
    {
        if (root != NULL)
        {

            // Push the root and it's index
            // into the st
            st.push(new Pair(root, currentRootIndex));
            currentRootIndex = 0;

            // If root don't have any children's that
            // means we are already at the left most
            // node, so we will mark root as NULL
            if (root->children.size() >= 1)
            {
                root = root->children[0];
            }
            else
            {
                root = NULL;
            }
            continue;
        }

        // We will pop the top of the st and
        // push_back it to our answer
        Pair* temp = st.top();
        st.pop();
        postorderTraversal.push_back(temp->node->val);

        // Repeatedly we will the pop all the
        // elements from the st till popped
        // element is last children of top of
        // the st
        while (st.size() > 0 && temp->childrenIndex ==
                st.top()->node->children.size() - 1)
        {
            temp = st.top();
            st.pop();

            postorderTraversal.push_back(temp->node->val);
        }

        // If st is not empty, then simply assign
        // the root to the next children of top
        // of st's node
        if (st.size() > 0)
        {
            root = st.top()->node->children[temp->childrenIndex + 1];
            currentRootIndex = temp->childrenIndex + 1;
        }
    }
    return postorderTraversal;
}

// Driver Code
int main()
{
    Node* root = new Node(1);

    root->children.push_back(new Node(3));
    root->children.push_back(new Node(2));
    root->children.push_back(new Node(4));

    root->children[0]->children.push_back(new Node(5));
    root->children[0]->children.push_back(new Node(6));
    vector<int> v = postorder(root);
    for(int i = 0; i < v.size(); i++)
        cout << v[i] << " ";
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
    // Node class
    static class Node {
        public int val;
        public List<Node> children = new ArrayList<Node>();

        // Default constructor
        public Node() {}

        public Node(int _val)
        {
            val = _val;
        }

        public Node(int _val, List<Node> _children)
        {
            val = _val;
            children = _children;
        }
    };

    // Helper class to push node and it's index
    // into the stack
    static class Pair {
        public Node node;
        public int childrenIndex;
        public Pair(Node _node, int _childrenIndex)
        {
            node = _node;
            childrenIndex = _childrenIndex;
        }
    }

    // We will keep the start index as 0,
    // because first we always
    // process the left most children
    int currentRootIndex = 0;
    Stack<Pair> stack = new Stack<Pair>();
    ArrayList<Integer> postorderTraversal =
                        new ArrayList<Integer>();

    // Function to perform iterative postorder traversal
    public ArrayList<Integer> postorder(Node root)
    {
        while (root != null || !stack.isEmpty()) {
            if (root != null) {

                // Push the root and it's index
                // into the stack
                stack.push(new Pair(root, currentRootIndex));
                currentRootIndex = 0;

                // If root don't have any children's that
                // means we are already at the left most
                // node, so we will mark root as null
                if (root.children.size() >= 1) {
                    root = root.children.get(0);
                }
                else {
                    root = null;
                }
                continue;
            }

            // We will pop the top of the stack and
            // add it to our answer
            Pair temp = stack.pop();
            postorderTraversal.add(temp.node.val);

            // Repeatedly we will the pop all the
            // elements from the stack till popped
            // element is last children of top of
            // the stack
            while (!stack.isEmpty() && temp.childrenIndex ==
                    stack.peek().node.children.size() - 1) {
                temp = stack.pop();

                postorderTraversal.add(temp.node.val);
            }

            // If stack is not empty, then simply assign
            // the root to the next children of top
            // of stack's node
            if (!stack.isEmpty()) {
                root = stack.peek().node.children.get(
                                        temp.childrenIndex + 1);
                currentRootIndex = temp.childrenIndex + 1;
            }
        }

        return postorderTraversal;
    }

    // Driver Code
    public static void main(String[] args)
    {
        GFG solution = new GFG();
        Node root = new Node(1);

        root.children.add(new Node(3));
        root.children.add(new Node(2));
        root.children.add(new Node(4));

        root.children.get(0).children.add(new Node(5));
        root.children.get(0).children.add(new Node(6));

        System.out.println(solution.postorder(root));
    }
}
```

## C#

```
// C# Program to iterative Postorder Traversal of N-ary Tree
using System;
using System.Collections.Generic;

class GFG
{
    // Node class
    public class Node
    {
        public int val;
        public List<Node> children = new List<Node>();

        // Default constructor
        public Node() {}

        public Node(int _val)
        {
            val = _val;
        }

        public Node(int _val, List<Node> _children)
        {
            val = _val;
            children = _children;
        }
    };

    // Helper class to.Push node and it's index
    // into the stack
    class Pair
    {
        public Node node;
        public int childrenIndex;
        public Pair(Node _node, int _childrenIndex)
        {
            node = _node;
            childrenIndex = _childrenIndex;
        }
    }

    // We will keep the start index as 0,
    // because first we always
    // process the left most children
    int currentRootIndex = 0;
    Stack<Pair> stack = new Stack<Pair>();
    List<int> postorderTraversal =
                        new List<int>();

    // Function to perform iterative postorder traversal
    public List<int> postorder(Node root)
    {
        while (root != null || stack.Count != 0)
        {
            if (root != null)
            {

                // Push the root and it's index
                // into the stack
                stack.Push(new Pair(root, currentRootIndex));
                currentRootIndex = 0;

                // If root don't have any children's that
                // means we are already at the left most
                // node, so we will mark root as null
                if (root.children.Count >= 1)
                {
                    root = root.children[0];
                }
                else
                {
                    root = null;
                }
                continue;
            }

            // We will.Pop the top of the stack and
            //.Add it to our answer
            Pair temp = stack.Pop();
            postorderTraversal.Add(temp.node.val);

            // Repeatedly we will the.Pop all the
            // elements from the stack till.Popped
            // element is last children of top of
            // the stack
            while (stack.Count != 0 && temp.childrenIndex ==
                    stack.Peek().node.children.Count - 1)
            {
                temp = stack.Pop();

                postorderTraversal.Add(temp.node.val);
            }

            // If stack is not empty, then simply assign
            // the root to the next children of top
            // of stack's node
            if (stack.Count != 0)
            {
                root = stack.Peek().node.children[temp.childrenIndex + 1];
                currentRootIndex = temp.childrenIndex + 1;
            }
        }

        return postorderTraversal;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        GFG solution = new GFG();
        Node root = new Node(1);

        root.children.Add(new Node(3));
        root.children.Add(new Node(2));
        root.children.Add(new Node(4));

        root.children[0].children.Add(new Node(5));
        root.children[0].children.Add(new Node(6));
        Console.Write("[");
        List<int> temp = solution.postorder(root);
        int size = temp.Count;
        int count = 0;
        foreach(int v in temp)
        {
            Console.Write(v);
            count++;
            if(count < size)
                Console.Write(", ");
        }
        Console.Write("]");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript Program to iterative
// Postorder Traversal of N-ary Tree
// Node class
class Node
{
    constructor(_val)
    {
        this.val = _val;
        this.children = [];
    }
};

// Helper class to.Push node and it's index
// into the stack
class Pair
{
    constructor(_node, _childrenIndex)
    {
        this.node = _node;
        this.childrenIndex = _childrenIndex;
    }
}

// We will keep the start index as 0,
// because first we always
// process the left most children
var currentRootIndex = 0;
var stack = [];
var postorderTraversal = [];

// Function to perform iterative postorder traversal
function postorder(root)
{
    while (root != null || stack.length != 0)
    {
        if (root != null)
        {

            // Push the root and it's index
            // into the stack
            stack.push(new Pair(root, currentRootIndex));
            currentRootIndex = 0;

            // If root don't have any children's that
            // means we are already at the left most
            // node, so we will mark root as null
            if (root.children.length >= 1)
            {
                root = root.children[0];
            }
            else
            {
                root = null;
            }
            continue;
        }

        // We will.Pop the top of the stack and
        //.push it to our answer
        var temp = stack.pop();
        postorderTraversal.push(temp.node.val);

        // Repeatedly we will the.Pop all the
        // elements from the stack till.Popped
        // element is last children of top of
        // the stack
        while (stack.length != 0 && temp.childrenIndex ==
                stack[stack.length-1].node.children.Count - 1)
        {
            temp = stack.pop();

            postorderTraversal.push(temp.node.val);
        }

        // If stack is not empty, then simply assign
        // the root to the next children of top
        // of stack's node
        if (stack.length != 0)
        {
            root = stack[stack.length-1].node.children[temp.childrenIndex + 1];
            currentRootIndex = temp.childrenIndex + 1;
        }
    }

    return postorderTraversal;
}

// Driver Code
var root = new Node(1);
root.children.push(new Node(3));
root.children.push(new Node(2));
root.children.push(new Node(4));
root.children[0].children.push(new Node(5));
root.children[0].children.push(new Node(6));
document.write("[");
var temp = postorder(root);
var size = temp.length;
var count = 0;
for(var v of temp)
{
    document.write(v);
    count++;
    if(count < size)
        document.write(", ");
}
document.write("]");

</script>
```

**Output:** 

```
[5, 6, 3, 2, 4, 1]
```