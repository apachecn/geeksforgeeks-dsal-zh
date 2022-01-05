# 使用 Trie 对字符串(或单词)数组进行排序

> 原文:[https://www . geesforgeks . org/sorting-array-strings-word-using-trie/](https://www.geeksforgeeks.org/sorting-array-strings-words-using-trie/)

给定一组字符串，按字母(字典)顺序打印它们。如果输入数组中有重复项，我们只需要打印一次。
示例:

```
Input : "abc", "xy", "bcd"
Output : abc bcd xy         

Input : "geeks", "for", "geeks", "a", "portal", 
        "to", "learn", "can", "be", "computer", 
        "science", "zoom", "yup", "fire", "in", "data"
Output : a be can computer data fire for geeks
         in learn portal science to yup zoom
```

[Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 是一种高效的数据结构，用于存储字符串等数据。要按字母顺序打印字符串，我们必须首先插入 trie，然后执行前序遍历以按字母顺序打印。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to sort an array of strings
// using Trie
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

struct Trie {

    // index is set when node is a leaf
    // node, otherwise -1;
    int index;

    Trie* child[MAX_CHAR];

    /*to make new trie*/
    Trie()
    {
        for (int i = 0; i < MAX_CHAR; i++)
            child[i] = NULL;
        index = -1;
    }
};

/* function to insert in trie */
void insert(Trie* root, string str, int index)
{
    Trie* node = root;

    for (int i = 0; i < str.size(); i++) {

        /* taking ascii value to find index of
          child node */
        char ind = str[i] - 'a';

        /* making new path if not already */
        if (!node->child[ind])
            node->child[ind] = new Trie();

        // go to next node
        node = node->child[ind];
    }

    // Mark leaf (end of word) and store
    // index of word in arr[]
    node->index = index;
}

/* function for preorder traversal */
bool preorder(Trie* node, string arr[])
{
    if (node == NULL)
        return false;

    for (int i = 0; i < MAX_CHAR; i++) {
        if (node->child[i] != NULL) {

            /* if leaf node then print key*/
            if (node->child[i]->index != -1)
                cout << arr[node->child[i]->index] << endl;

            preorder(node->child[i], arr);
        }
    }
}

void printSorted(string arr[], int n)
{
    Trie* root = new Trie();

    // insert all keys of dictionary into trie
    for (int i = 0; i < n; i++)
        insert(root, arr[i], i);

    // print keys in lexicographic order
    preorder(root, arr);
}

// Driver code
int main()
{
    string arr[] = { "abc", "xy", "bcd" };
    int n = sizeof(arr) / sizeof(arr[0]);
    printSorted(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array of strings using Trie

// Author : Rohit Jain
// GFG user_id : @rj03012002

import java.util.*;

class GFG {

    // Alphabet size
    static final int MAX_CHAR = 26;

    // trie node
    static class Trie {

        // index is set when node is a leaf
        // node, otherwise -1;
        int index;

        Trie child[] = new Trie[MAX_CHAR];

        /*to make new trie*/
        Trie()
        {

            for (int i = 0; i < MAX_CHAR; i++)
                child[i] = null;
            index = -1;
        }
    }

    /* function to insert in trie */
    static void insert(Trie root, String str, int index)
    {

        Trie node = root;

        for (int i = 0; i < str.length(); i++) {
            /* taking ascii value to find index of
          child node */
            int ind = str.charAt(i) - 'a';

            /* making new path if not already */
            if (node.child[ind] == null)
                node.child[ind] = new Trie();

            // go to next node
            node = node.child[ind];
        }

        // Mark leaf (end of word) and store
        // index of word in arr[]
        node.index = index;
    }

    /* function for preorder traversal */
    static boolean preorder(Trie node, String arr[])
    {

        if (node == null) {

            return false;
        }

        for (int i = 0; i < MAX_CHAR; i++) {

            if (node.child[i] != null) {

                /* if leaf node then print key*/
                if (node.child[i].index != -1) {

                    System.out.print(
                        arr[node.child[i].index] + " ");
                }

                preorder(node.child[i], arr);
            }
        }
        return false;
    }

    static void printSorted(String arr[], int n)
    {

        Trie root = new Trie();

        // insert all keys of dictionary into trie
        for (int i = 0; i < n; ++i) {

            insert(root, arr[i], i);
        }

        // print keys in lexicographic order
        preorder(root, arr);
    }

    public static void main(String[] args)
    {

        String arr[] = { "abc", "xy", "bcd" };

        int n = arr.length;

        printSorted(arr, n);
    }
}
```

输出:

```
abc bcd xy   
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。