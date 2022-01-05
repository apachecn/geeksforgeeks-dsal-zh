# 如何使用三元搜索树实现文本自动完成功能

> 原文:[https://www . geesforgeks . org/如何实现-文本-自动-完成-特征-使用-三元-搜索-树/](https://www.geeksforgeeks.org/how-to-implement-text-auto-complete-feature-using-ternary-search-tree/)

给定一组字符串 **S** 和一个字符串**模式**，任务是使用[三元搜索树](https://www.geeksforgeeks.org/ternary-search-tree/)自动完成字符串**模式**到以**模式**为前缀的 **S** 的字符串。如果没有匹配给定前缀的字符串，打印**“无”**。
**举例:**

> **输入:**S = {“wall street”“geeks forgeeks”“wall mart”“Walmart”“wald mort”“word”】、
> patt = "wall"
> **输出:**T6】wall street
> wall mart
> T9】解释:
> 只有两个字符串{“wall street”“wall mart”}从 S 匹配给定的图案“wall”。
> **输入:**S = {“word”“wall street”“wall”“wall mart”“Walmart”“Waldo”“won”}，patt =“geeks”
> **输出:** None
> **解释:**
> 由于集合中没有与模式匹配的 word，因此将打印空列表。

**Trie 方法:**请参考[本文](https://www.geeksforgeeks.org/auto-complete-feature-using-trie/)了解使用 [Trie 数据结构](https://www.geeksforgeeks.org/trie-insert-and-search/)的实现。
[**三元搜索树**](https://www.geeksforgeeks.org/ternary-search-tree/) **逼近**按照以下步骤解决问题:

*   根据以下条件将 **S** 中字符串的所有字符插入三元搜索树:
    1.  如果要插入的字符小于当前节点值，则遍历左侧子树。
    2.  如果要插入的字符大于当前节点值，则遍历右子树。
    3.  如果要插入的字符与当前节点值的字符相同，如果它不是单词的结尾，则遍历相等的子树。如果是，将该节点标记为单词的结尾。
*   遵循类似的方法提取建议。
*   按照上面提到的类似遍历技术，遍历树以搜索给定的前缀**模式**。
*   如果找不到给定的前缀，则打印“无”。
*   如果找到给定的前缀，从前缀结束的节点开始遍历树。遍历左边的子树，从每个节点生成建议，然后是右边相等的子树。
*   每次遇到设置了 **endofWord** 变量的节点，都表示已经获得了建议。将该建议插入**词语**。
*   生成所有可能的建议后返回**字**。

以下是上述方法的实现:

## C++

```
// C++ Program to generate
// autocompleted texts from
// a given prefix using a
// Ternary Search Tree
#include <bits/stdc++.h>
using namespace std;

// Define the Node of the
// tree
struct Node {

    // Store the character
    // of a string
    char data;
    // Store the end of
    // word
    int end;
    // Left Subtree
    struct Node* left;

    // Equal Subtree
    struct Node* eq;

    // Right Subtree
    struct Node* right;
};

// Function to create a Node
Node* createNode(char newData)
{
    struct Node* newNode = new Node();
    newNode->data = newData;
    newNode->end = 0;
    newNode->left = NULL;
    newNode->eq = NULL;
    newNode->right = NULL;
    return newNode;
}

// Function to insert a word
// in the tree
void insert(Node** root,
            string word,
            int pos = 0)
{

    // Base case
    if (!(*root))
        *root = createNode(word[pos]);

    // If the current character is
    // less than root's data, then
    // it is inserted in the
    // left subtree

    if ((*root)->data > word[pos])
        insert(&((*root)->left), word,
               pos);

    // If current character is
    // more than root's data, then
    // it is inserted in the right
    // subtree

    else if ((*root)->data < word[pos])
        insert(&((*root)->right), word,
               pos);

    // If current character is same
    // as that of the root's data

    else {
        // If it is the end of word

        if (pos + 1 == word.size())
            // Mark it as the
            // end of word
            (*root)->end = 1;

        // If it is not the end of
        // the string, then the
        // current character is
        // inserted in the equal subtree

        else
            insert(&((*root)->eq), word, pos + 1);
    }
}

// Function to traverse the ternary search tree
void traverse(Node* root,
              vector<string>& ret,
              char* buff,
              int depth = 0)
{
    // Base case
    if (!root)
        return;
    // The left subtree is
    // traversed first
    traverse(root->left, ret,
             buff, depth);

    // Store the current character
    buff[depth] = root->data;

    // If the end of the string
    // is detected, store it in
    // the final ans
    if (root->end) {
        buff[depth + 1] = '\0';
        ret.push_back(string(buff));
    }

    // Traverse the equal subtree
    traverse(root->eq, ret,
             buff, depth + 1);

    // Traverse the right subtree
    traverse(root->right, ret,
             buff, depth);
}

// Utility function to find
// all the words
vector<string> util(Node* root,
                    string pattern)
{
    // Stores the words
    // to suggest
    char buffer[1001];

    vector<string> ret;

    traverse(root, ret, buffer);

    if (root->end == 1)
        ret.push_back(pattern);
    return ret;
}

// Function to autocomplete
// based on the given prefix
// and return the suggestions
vector<string> autocomplete(Node* root,
                            string pattern)
{
    vector<string> words;
    int pos = 0;

    // If pattern is empty
    // return an empty list
    if (pattern.empty())
        return words;

    // Iterating over the characters
    // of the pattern and find it's
    // corresponding node in the tree

    while (root && pos < pattern.length()) {

        // If current character is smaller
        if (root->data > pattern[pos])
            // Search the left subtree
            root = root->left;

        // current character is greater
        else if (root->data < pattern[pos])
            // Search right subtree
            root = root->right;

        // If current character is equal
        else if (root->data == pattern[pos]) {

            // Search equal subtree
              // since character is found, move to the next character in the pattern
            root = root->eq;
            pos++;
        }

        // If not found
        else
            return words;

    }

    // Search for all the words
    // from the current node
    words = util(root, pattern);

    return words;
}

// Function to print
// suggested words

void print(vector<string> sugg,
           string pat)
{
    for (int i = 0; i < sugg.size();
         i++)
        cout << pat << sugg[i].c_str()
             << "\n";
}

// Driver Code
int main()
{
    vector<string> S
        = { "wallstreet", "geeksforgeeks",
            "wallmart", "walmart",
            "waldormort", "word" };

    Node* tree = NULL;

    // Insert the words in the
    // Ternary Search Tree
    for (string str : S)
        insert(&tree, str);

    string pat = "wall";

    vector<string> sugg
        = autocomplete(tree, pat);

    if (sugg.size() == 0)
        cout << "None";

    else
        print(sugg, pat);

    return 0;
}
```

**Output**

```
wallmart
wallstreet
```

***时间复杂度:** O(L* log N)其中 **L** 是最长单词的长度。*
*空间与要存储的字符串长度成正比。*
**辅助空间:** O(N)