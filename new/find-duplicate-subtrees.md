# 查找所有重复的子树

给定一棵二叉树，找到所有重复的子树。 对于每个重复的子树，我们只需要返回其中任何一个的根节点。 如果两棵树具有相同的结构和相同的节点值，则它们是重复的。

**示例：**

```
Input :
       1
      / \
     2   3
    /   / \
   4   2   4
      /
     4

Output : 
   2           
  /    and    4
 4
Explanation: Above Trees are two duplicate subtrees. 
Therefore, you need to return above trees root in the 
form of a list.

```

这个想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。 我们在哈希中存储子树的[有序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。 由于简单的有序遍历无法唯一地识别树，因此我们使用“（”和“）”之类的符号来表示 NULL 节点。
我们将 C ++ 中的[无序映射作为辅助函数的参数传递，该函数以递归方式计算有序字符串并增加其在 map 中的计数。 如果任何字符串被重复，那么它将暗示以该节点为根的子树的重复，因此将该节点推入最终结果并返回这些节点的向量。](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)

## C ++

```

// C++ program to find averages of all levels 
// in a binary tree. 
#include <bits/stdc++.h> 
using namespace std; 

/* A binary tree node has data, pointer to 
left child and a pointer to right child */
struct Node { 
    int data; 
    struct Node* left, *right; 
}; 

string inorder(Node* node, unordered_map<string, int>& m) 
{ 
    if (!node) 
        return ""; 

    string str = "("; 
    str += inorder(node->left, m); 
    str += to_string(node->data); 
    str += inorder(node->right, m); 
    str += ")"; 

    // Subtree already present (Note that we use 
    // unordered_map instead of unordered_set 
    // because we want to print multiple duplicates 
    // only once, consider example of 4 in above 
    // subtree, it should be printed only once. 
    if (m[str] == 1) 
        cout << node->data << " "; 

    m[str]++; 

    return str; 
} 

// Wrapper over inorder() 
void printAllDups(Node* root) 
{ 
    unordered_map<string, int> m; 
    inorder(root, m); 
} 

/* Helper function that allocates a 
new node with the given data and 
NULL left and right pointers. */
Node* newNode(int data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->left = temp->right = NULL; 
    return temp; 
} 

// Driver code 
int main() 
{ 
    Node* root = NULL; 
    root = newNode(1); 
    root->left = newNode(2); 
    root->right = newNode(3); 
    root->left->left = newNode(4); 
    root->right->left = newNode(2); 
    root->right->left->left = newNode(4); 
    root->right->right = newNode(4); 
    printAllDups(root); 
    return 0; 
} 

```

## 爪哇

```

// A java program to find all duplicate subtrees  
// in a binary tree. 
import java.util.HashMap; 
public class Duplicate_subtress { 

    /* A binary tree node has data, pointer to 
    left child and a pointer to right child */
    static HashMap<String, Integer> m; 
    static class Node { 
        int data; 
        Node left; 
        Node right; 
        Node(int data){ 
            this.data = data; 
            left = null; 
            right = null; 
        } 
    } 
    static String inorder(Node node) 
    { 
        if (node == null) 
            return ""; 

        String str = "("; 
        str += inorder(node.left); 
        str += Integer.toString(node.data); 
        str += inorder(node.right); 
        str += ")"; 

        // Subtree already present (Note that we use 
        // HashMap instead of HashSet 
        // because we want to print multiple duplicates 
        // only once, consider example of 4 in above 
        // subtree, it should be printed only once.        
        if (m.get(str) != null && m.get(str)==1 ) 
            System.out.print( node.data + " "); 

        if (m.containsKey(str)) 
            m.put(str, m.get(str) + 1); 
        else
            m.put(str, 1); 

        return str; 
    } 

    // Wrapper over inorder() 
    static void printAllDups(Node root) 
    { 
        m = new HashMap<>(); 
        inorder(root); 
    }  
    // Driver code 
    public static void main(String args[]) 
    { 
        Node root = null; 
        root = new Node(1); 
        root.left = new Node(2); 
        root.right = new Node(3); 
        root.left.left = new Node(4); 
        root.right.left = new Node(2); 
        root.right.left.left = new Node(4); 
        root.right.right = new Node(4); 
        printAllDups(root); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python3

```

# Python3 program to find averages of  
# all levels in a binary tree.  

# Helper function that allocates a  
# new node with the given data and  
# None left and right pointers.  
class newNode: 
    def __init__(self, data): 
        self.data = data  
        self.left = self.right = None

def inorder(node, m): 
    if (not node):  
        return ""  

    Str = "("
    Str += inorder(node.left, m)  
    Str += str(node.data)  
    Str += inorder(node.right, m)  
    Str += ")"

    # Subtree already present (Note that  
    # we use unordered_map instead of  
    # unordered_set because we want to print 
    # multiple duplicates only once, consider  
    # example of 4 in above subtree, it  
    # should be printed only once.  
    if (Str in m and m[Str] == 1):  
        print(node.data, end = " ")  
    if Str in m: 
        m[Str] += 1
    else: 
        m[Str] = 1

    return Str

# Wrapper over inorder()  
def printAllDups(root): 
    m = {}  
    inorder(root, m) 

# Driver code  
if __name__ == '__main__': 
    root = None
    root = newNode(1)  
    root.left = newNode(2)  
    root.right = newNode(3)  
    root.left.left = newNode(4)  
    root.right.left = newNode(2)  
    root.right.left.left = newNode(4)  
    root.right.right = newNode(4)  
    printAllDups(root)  

# This code is contributed by PranchalK 

```

## C＃

```

// A C# program to find all duplicate subtrees  
// in a binary tree. 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

    /* A binary tree node has data, pointer to 
    left child and a pointer to right child */
    static Dictionary<String,  
                      int> m = new Dictionary<String,  
                                              int>(); 
    public class Node  
    { 
        public int data; 
        public Node left; 
        public Node right; 
        public Node(int data) 
        { 
            this.data = data; 
            left = null; 
            right = null; 
        } 
    } 

    static String inorder(Node node) 
    { 
        if (node == null) 
            return ""; 

        String str = "("; 
        str += inorder(node.left); 
        str += (node.data).ToString(); 
        str += inorder(node.right); 
        str += ")"; 

        // Subtree already present (Note that we use 
        // HashMap instead of HashSet 
        // because we want to print multiple duplicates 
        // only once, consider example of 4 in above 
        // subtree, it should be printed only once.      
        if (m.ContainsKey(str) && m[str] == 1 ) 
            Console.Write(node.data + " "); 

        if (m.ContainsKey(str)) 
            m[str] = m[str] + 1; 
        else
            m.Add(str, 1); 

        return str; 
    } 

    // Wrapper over inorder() 
    static void printAllDups(Node root) 
    { 
        m = new Dictionary<String, int>(); 
        inorder(root); 
    }  

    // Driver code 
    public static void Main(String []args) 
    { 
        Node root = null; 
        root = new Node(1); 
        root.left = new Node(2); 
        root.right = new Node(3); 
        root.left.left = new Node(4); 
        root.right.left = new Node(2); 
        root.right.left.left = new Node(4); 
        root.right.right = new Node(4); 
        printAllDups(root); 
    } 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
4 2

```

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。