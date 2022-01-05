# 打印给定数组中的所有唯一字符串

> 原文:[https://www . geesforgeks . org/print-all-unique-strings-present-in-a-给定数组/](https://www.geeksforgeeks.org/print-all-unique-strings-present-in-a-given-array/)

给定一个字符串数组 **arr[]** ，任务是打印给定数组中存在的所有唯一字符串。

**示例:**

> **输入:** arr[] = {“极客”“极客”“ab”“极客”“代码”“卡雷加”}
> **输出:**极客 ab 代码卡雷加
> **解释:**
> 字符串“极客”的出现频率为 1。
> 弦“极客”的频率为 2。
> 字符串“ab”的频率为 1。
> 字符串“代码”的频率为 1。
> 字符串“karega”的频率为 1。
> 因此，需要的输出是“极客 ab 代码 karega”
> 
> **输入:**arr[]= {“abcd”、“ABCD”、“co”；【code】}
> **输出:**ABCD co code

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)对于遇到的每个字符串，检查该字符串是否出现在剩余的数组中。打印那些在数组中只出现一次的字符串。
***时间复杂度:** O(N <sup>2</sup> * M)，其中 M 为弦的最大长度*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[特里](https://www.geeksforgeeks.org/trie-insert-and-search/)进行优化。其思想是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于数组中的每一个**I<sup>th</sup>T9】字符串，检查**arr【I】**是否存在于 **Trie** 中。如果发现为真，则将 **arr[i]** 标记为重复数组元素。否则，将 **arr[i]** 标记为唯一数组元素，[将 **arr[i]** 插入到 trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 中。按照以下步骤解决问题:**

*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如 **isUniq[]** ，来[检查一个数组元素是否唯一](https://www.geeksforgeeks.org/find-the-element-that-appears-once/)。
*   创建一个具有根节点的 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) ，比如**根**，来存储给定数组中每个字符串的字符。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个 **i <sup>第</sup>个**元素，检查**arr【I】**是否存在于 **Trie** 中。如果发现为真，则将 **isUniq[i]** 更新为假。
*   否则，将 **isUniq[i]** 更新为真，并将 **arr[i]** 插入 **Trie。**
*   最后，[使用变量 **i** 遍历**ISU niq【】**数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个 **i <sup>th</sup>** 元素，检查**ISU niq【I】**是否为真。如果发现为真，则打印 **arr[i]** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of
// a Trie node
struct TrieNode {

    // Stores index
    // of string
    int idx;

    // Check if a character is
    // present in the string or not
    TrieNode* child[26];

    // Initialize a TrieNode
    TrieNode()
    {
        // Idx = -1: String is not
        // present in TrieNode
        idx = -1;

        // Initialize all child nodes
        // of a TrieNode to NULL
        for (int i = 0; i < 26; i++) {

            // Update child[i]
            child[i] = NULL;
        }
    }
};

// Function to insert a string into Trie
void Insert(TrieNode* root,
            string str, int i)
{
    // Stores length of the string
    int N = str.length();

    // Traverse the string str
    for (int i = 0; i < N; i++) {

        // If str[i] not present in
        // a Trie at current index
        if (!root->child[str[i] - 'a']) {

            // Create a new node of Trie.
            root->child[str[i] - 'a']
                = new TrieNode();
        }

        // Update root
        root = root->child[str[i] - 'a'];
    }

    // Store index of str
    // in the TrieNode
    root->idx = i;
}

// Function to check if string str present
// in the Trie or not
int SearchString(TrieNode* root, string str)
{
    // Stores length of
    // the string
    int N = str.length();

    // Traverse the string
    for (int i = 0; i < N; i++) {

        // If a character not present
        // in Trie at current index
        if (!root->child[str[i] - 'a']) {

            // Return str as
            // unique string
            return -1;
        }

        // Update root
        root
            = root->child[str[i] - 'a'];
    }

    // Return index of str
    return root->idx;
}

// Utility function to find the unique
// string in array of strings
void UtilUniqStr(vector<string>& arr, int N)
{
    // Stores root node of the Trie
    TrieNode* root = new TrieNode();

    // isUniq[i]: Check if i-th string
    // is unique or not
    bool isUniq[N];

    // Initialize isUniq[] to false
    memset(isUniq, false, sizeof(isUniq));

    // Insert arr[0] into the Trie
    Insert(root, arr[0], 0);

    // Mark arr[0] as unique string
    isUniq[0] = true;

    // Traverse the given array
    for (int i = 1; i < N; i++) {

        // Stores previous 1st index
        // of arr[i] in the array
        int idx = SearchString(root,
                               arr[i]);

        // If arr[i] not present
        // in the Trie
        if (idx == -1) {

            // Mark i-th string
            // as unique string
            isUniq[i] = true;

            // Insert arr[i] into Trie
            Insert(root, arr[i], i);
        }

        // If arr[i] already present
        // in the Trie
        else {

            // Mark i-th string as
            // duplicate string in Trie
            isUniq[idx] = false;
        }
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If i-th string is unique,
        // then print the string
        if (isUniq[i]) {

            cout << arr[i] << " ";
        }
    }
}

// Driver Code
int main()
{

    vector<string> arr = { "geeks", "for",
                           "geek", "ab", "geek",
                           "for", "code", "karega" };

    int N = arr.size();

    UtilUniqStr(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;

class GFG
{

// Structure of
// a Trie node
static class TrieNode {

    // Stores index
    // of String
    int idx;

    // Check if a character is
    // present in the String or not
    TrieNode []child = new TrieNode[26];

    // Initialize a TrieNode
    TrieNode()
    {

        // Idx = -1: String is not
        // present in TrieNode
        idx = -1;

        // Initialize all child nodes
        // of a TrieNode to null
        for (int i = 0; i < 26; i++) {

            // Update child[i]
            child[i] = null;
        }
    }
};

// Function to insert a String into Trie
static void Insert(TrieNode root,
            String str, int i)
{

    // Stores length of the String
    int N = str.length();

    // Traverse the String str
    for (int j = 0; j < N; j++) {

        // If str[i] not present in
        // a Trie at current index
        if (root.child[str.charAt(j) - 'a']==null) {

            // Create a new node of Trie.
            root.child[str.charAt(j) - 'a']
                = new TrieNode();
        }

        // Update root
        root = root.child[str.charAt(j) - 'a'];
    }

    // Store index of str
    // in the TrieNode
    root.idx = i;
}

// Function to check if String str present
// in the Trie or not
static int SearchString(TrieNode root, String str)
{
    // Stores length of
    // the String
    int N = str.length();

    // Traverse the String
    for (int i = 0; i < N; i++) {

        // If a character not present
        // in Trie at current index
        if (root.child[str.charAt(i) - 'a'] == null) {

            // Return str as
            // unique String
            return -1;
        }

        // Update root
        root
            = root.child[str.charAt(i) - 'a'];
    }

    // Return index of str
    return root.idx;
}

// Utility function to find the unique
// String in array of Strings
static void UtilUniqStr(String[] arr, int N)
{
    // Stores root node of the Trie
    TrieNode root = new TrieNode();

    // isUniq[i]: Check if i-th String
    // is unique or not
    boolean []isUniq = new boolean[N];

    // Insert arr[0] into the Trie
    Insert(root, arr[0], 0);

    // Mark arr[0] as unique String
    isUniq[0] = true;

    // Traverse the given array
    for (int i = 1; i < N; i++) {

        // Stores previous 1st index
        // of arr[i] in the array
        int idx = SearchString(root,
                               arr[i]);

        // If arr[i] not present
        // in the Trie
        if (idx == -1) {

            // Mark i-th String
            // as unique String
            isUniq[i] = true;

            // Insert arr[i] into Trie
            Insert(root, arr[i], i);
        }

        // If arr[i] already present
        // in the Trie
        else {

            // Mark i-th String as
            // duplicate String in Trie
            isUniq[idx] = false;
        }
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If i-th String is unique,
        // then print the String
        if (isUniq[i]) {

            System.out.print(arr[i]+ " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

   String[] arr = { "geeks", "for",
                           "geek", "ab", "geek",
                           "for", "code", "karega" };

    int N = arr.length;

    UtilUniqStr(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
root = None

# Structure of
# a Trie node
class TrieNode:

    # Stores index
    # of string
    def __init__(self):
        self.idx = -1
        self.child = [None]*26

# Function to insert a string into Trie
def Insert(str, i):
    global root

    # Stores length of the string
    N = len(str)

    root1 = root

    # Traverse the string str
    for i in range(N):

        # If str[i] not present in
        # a Trie at current index
        if (not root1.child[ord(str[i]) - ord('a')]):

            # Create a new node of Trie.
            root1.child[ord(str[i]) - ord('a')] = TrieNode()

        # Update root
        root1 = root1.child[ord(str[i]) - ord('a')]

    # Store index of str
    # in the TrieNode
    root1.idx = i

    return root1

# Function to check if string str present
# in the Trie or not
def SearchString(str):
    global root

    root1 = root

    # Stores length of
    # the
    N = len(str)

    # Traverse the
    for i in range(N):

        # If a character not present
        # in Trie at current index
        if (not root1.child[ord(str[i]) - ord('a')]):

            # Return str as
            # unique
            return -1

        # Update root
        root1 = root1.child[ord(str[i]) - ord('a')]

    # Return index of str
    return root1.idx

# Utility function to find the unique
# string in array of strings
def UtilUniqStr(arr, N):
    global root

    # Stores root node of the Trie
    root = TrieNode()

    d = {}

    for i in arr:
        d[i] = d.get(i, 0) + 1

    # isUniq[i]: Check if i-th string
    # is unique or not
    isUniq = [False] * N

    # Initialize isUniq[] to false
    # memset(isUniq, false, sizeof(isUniq));

    # Insert arr[0] into the Trie
    Insert(arr[0], 0)

    # Mark arr[0] as unique string
    isUniq[0] = True
    # print(root.child[6].child)

    # Traverse the given array
    for i in range(1, N):

        # Stores previous 1st index
        # of arr[i] in the array
        idx = SearchString(arr[i])

        # If arr[i] not present
        # in the Trie
        if (idx == -1 and d[arr[i]] == 1):

            # Mark i-th string
            # as unique string
            isUniq[i] = True

            # Insert arr[i] into Trie
            Insert(arr[i], i)

        # If arr[i] already present
        # in the Trie
        else:

            # Mark i-th string as
            # duplicate string in Trie
            isUniq[idx] = False

    # Traverse the array
    for i in range(N):

        # If i-th string is unique,
        # then print the string
        if (isUniq[i]):

            print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':
    arr = ["geeks", "for","geek", "ab", "geek","for", "code", "karega"]

    N = len(arr)

    UtilUniqStr(arr, N)

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Structure of
// a Trie node
class TrieNode {

    // Stores index
    // of String
    public int idx;

    // Check if a character is
    // present in the String or not
    public TrieNode []child = new TrieNode[26];

    // Initialize a TrieNode
    public TrieNode()
    {

        // Idx = -1: String is not
        // present in TrieNode
        idx = -1;

        // Initialize all child nodes
        // of a TrieNode to null
        for (int i = 0; i < 26; i++) {

            // Update child[i]
            child[i] = null;
        }
    }
};

// Function to insert a String into Trie
static void Insert(TrieNode root,
            String str, int i)
{

    // Stores length of the String
    int N = str.Length;

    // Traverse the String str
    for (int j = 0; j < N; j++) {

        // If str[i] not present in
        // a Trie at current index
        if (root.child[str[j] - 'a'] == null) {

            // Create a new node of Trie.
            root.child[str[j] - 'a']
                = new TrieNode();
        }

        // Update root
        root = root.child[str[j] - 'a'];
    }

    // Store index of str
    // in the TrieNode
    root.idx = i;
}

// Function to check if String str present
// in the Trie or not
static int SearchString(TrieNode root, String str)
{
    // Stores length of
    // the String
    int N = str.Length;

    // Traverse the String
    for (int i = 0; i < N; i++) {

        // If a character not present
        // in Trie at current index
        if (root.child[str[i] - 'a'] == null) {

            // Return str as
            // unique String
            return -1;
        }

        // Update root
        root
            = root.child[str[i] - 'a'];
    }

    // Return index of str
    return root.idx;
}

// Utility function to find the unique
// String in array of Strings
static void UtilUniqStr(String[] arr, int N)
{
    // Stores root node of the Trie
    TrieNode root = new TrieNode();

    // isUniq[i]: Check if i-th String
    // is unique or not
    bool []isUniq = new bool[N];

    // Insert arr[0] into the Trie
    Insert(root, arr[0], 0);

    // Mark arr[0] as unique String
    isUniq[0] = true;

    // Traverse the given array
    for (int i = 1; i < N; i++) {

        // Stores previous 1st index
        // of arr[i] in the array
        int idx = SearchString(root,
                               arr[i]);

        // If arr[i] not present
        // in the Trie
        if (idx == -1) {

            // Mark i-th String
            // as unique String
            isUniq[i] = true;

            // Insert arr[i] into Trie
            Insert(root, arr[i], i);
        }

        // If arr[i] already present
        // in the Trie
        else {

            // Mark i-th String as
            // duplicate String in Trie
            isUniq[idx] = false;
        }
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If i-th String is unique,
        // then print the String
        if (isUniq[i]) {

            Console.Write(arr[i] + " ");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{

   String[] arr = { "geeks", "for",
                           "geek", "ab", "geek",
                           "for", "code", "karega" };

    int N = arr.Length;

    UtilUniqStr(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Structure of
// a Trie node
class TrieNode
{
    constructor()
    {
        this.idx = -1;

        this.child = new Array(26);

        for (let i = 0; i < 26; i++) {

            // Update child[i]
            this.child[i] = null;
        }

    }
}

// Function to insert a String into Trie
function Insert(root,str,i)
{
    // Stores length of the String
    let N = str.length;

    // Traverse the String str
    for (let j = 0; j < N; j++) {

        // If str[i] not present in
        // a Trie at current index
        if (root.child[str[j].charCodeAt(0) -
        'a'.charCodeAt(0)]==null) {

            // Create a new node of Trie.
            root.child[str[j].charCodeAt(0) -
            'a'.charCodeAt(0)]
                = new TrieNode();
        }

        // Update root
        root = root.child[str[j].charCodeAt(0) -
        'a'.charCodeAt(0)];
    }

    // Store index of str
    // in the TrieNode
    root.idx = i;
}

// Function to check if String str present
// in the Trie or not
function SearchString(root,str)
{
    // Stores length of
    // the String
    let N = str.length;

    // Traverse the String
    for (let i = 0; i < N; i++) {

        // If a character not present
        // in Trie at current index
        if (root.child[str[i].charCodeAt(0) -
        'a'.charCodeAt(0)] == null) {

            // Return str as
            // unique String
            return -1;
        }

        // Update root
        root
            = root.child[str[i].charCodeAt(0) -
            'a'.charCodeAt(0)];
    }

    // Return index of str
    return root.idx;
}

// Utility function to find the unique
// String in array of Strings
function UtilUniqStr(arr,N)
{
    // Stores root node of the Trie
    let root = new TrieNode();

    // isUniq[i]: Check if i-th String
    // is unique or not
    let isUniq = new Array(N);

    // Insert arr[0] into the Trie
    Insert(root, arr[0], 0);

    // Mark arr[0] as unique String
    isUniq[0] = true;

    // Traverse the given array
    for (let i = 1; i < N; i++) {

        // Stores previous 1st index
        // of arr[i] in the array
        let idx = SearchString(root,
                               arr[i]);

        // If arr[i] not present
        // in the Trie
        if (idx == -1) {

            // Mark i-th String
            // as unique String
            isUniq[i] = true;

            // Insert arr[i] into Trie
            Insert(root, arr[i], i);
        }

        // If arr[i] already present
        // in the Trie
        else {

            // Mark i-th String as
            // duplicate String in Trie
            isUniq[idx] = false;
        }
    }

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // If i-th String is unique,
        // then print the String
        if (isUniq[i]) {

            document.write(arr[i]+ " ");
        }
    }
}

// Driver Code
let arr=["geeks", "for",
         "geek", "ab", "geek",
         "for", "code", "karega" ];
let N = arr.length;

UtilUniqStr(arr, N);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
geeks ab code karega
```

***时间复杂度:** O(N * M)，其中 **M** 为弦的最大长度*
***辅助空间:** O(N * 26)*