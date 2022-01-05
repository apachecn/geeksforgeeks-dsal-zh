# 给定数组中具有最大长度的最长公共前缀的字符串对

> 原文:[https://www . geesforgeks . org/给定数组中具有最大长度的最长公共前缀的字符串对/](https://www.geeksforgeeks.org/pair-of-strings-having-longest-common-prefix-of-maximum-length-in-given-array/)

给定一个由[字符串](https://www.geeksforgeeks.org/string-data-structure/)**arr【】**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)，任务是从给定数组中找到其中最长公共前缀[长度最大的一对字符串。如果存在多个解决方案，则打印其中任何一个。](https://www.geeksforgeeks.org/longest-common-prefix-using-character-by-character-matching/)

**示例:**

> **输入:**arr[]= {“geeks forgeeks”、“geeks”、“geeks forcese”}
> **输出:** (geeksforgeeks、geeks forcese)
> **解释:**
> 所有可能的配对及其最长的公共前缀为:
> (“geeks forgeeks”、“geeks”)具有最长的公共前缀=“geeks”
> (“geeks forgeeks”、“geeks forcese”)具有最长的公共前缀=“geeks for”
> 
> **输入:**arr[]= {【abbcbgf】、【bcdee】、【bcde】、【abbcbde】}
> **输出:**(abbcbgf，abbcbde)

**天真方法:**解决这个问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的所有可能的对，并计算每对的[最长公共前缀的长度。最后，打印具有最长公共前缀的最大长度的对。](https://www.geeksforgeeks.org/longest-common-prefix-using-character-by-character-matching/)

***时间复杂度:** O(N <sup>2</sup> * M)，其中 M 表示最长字符串的长度*
***辅助空间:** O(1)*

**有效途径:**使用[特里](https://www.geeksforgeeks.org/trie-insert-and-search/)可以解决问题。想法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，找到 Trie 中存在的最长前缀的最大长度，[将当前元素插入 Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 。最后，打印具有最长公共前缀的最大长度的对。按照以下步骤解决问题:

*   创建一个 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 有根节点，比如**根**来存储给定数组的每个元素。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，找到 Trie 中存在的最长前缀的最大长度，并将当前元素插入 Trie。
*   最后，打印具有最长公共前缀的最大长度的对。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of Trie
struct TrieNode {
    // Stores characters of
    // each string
    TrieNode* child[256];

    TrieNode() { child[0] = child[1] = NULL; }
};

// Function to insert a string into Trie
void insertTrie(TrieNode* root, string str)
{

    // Stores length of the string
    int M = str.length();

    // Traverse the string str
    for (int i = 0; i < M; i++) {

        // If str[i] is not present
        // in current path of Trie
        if (!root->child[str[i]]) {

            // Create a new node
            // of Trie
            root->child[str[i]] = new TrieNode();
        }

        // Update root
        root = root->child[str[i]];
    }
}

// Function to find the maximum length of
// longest common prefix in Trie with str
int findStrLen(TrieNode* root, string str)
{

    // Stores length of str
    int M = str.length();

    // Stores length of longest
    // common prefix in Trie with str
    int len = 0;

    // Traverse the string str
    for (int i = 0; i < M; i++) {

        // If str[i] is present in
        // the current path of Trie
        if (root->child[str[i]]) {

            // Update len
            len++;

            // Update root
            root = root->child[str[i]];
        }
        else {
            return len;
        }
    }
    return len;
}

// Function to print the pair having maximum
// length of the longest common prefix
void findMaxLenPair(vector<string>& arr, int N)
{
    // Stores index of the string having
    // maximum length of longest common prefix
    int idx = -1;

    // Stores maximum length of longest
    // common prefix.
    int len = 0;

    // Create root node of Trie
    TrieNode* root = new TrieNode();

    // Insert arr[0] into Trie
    insertTrie(root, arr[0]);

    // Traverse the array.
    for (int i = 1; i < N; i++) {

        // Stores maximum length of longest
        // common prefix in Trie with arr[i]
        int temp = findStrLen(root, arr[i]);

        // If temp is greater than len
        if (temp > len) {

            // Update len
            len = temp;

            // Update idx
            idx = i;
        }

        insertTrie(root, arr[i]);
    }

    // Traverse array arr[]
    for (int i = 0; i < N; i++) {

        // Stores length of arr[i]
        int M = arr[i].length();

        // Check if maximum length of
        // longest common prefix > M
        if (i != idx && M >= len) {
            bool found = true;
            // Traverse string arr[i]
            // and arr[j]
            for (int j = 0; j < len; j++) {

                // If current character of both
                // string does not match.
                if (arr[i][j] != arr[idx][j]) {
                    found = false;
                    break;
                }
            }

            // Print pairs having maximum length
            // of the longest common prefix
            if (found) {
                cout << "(" << arr[i] << ", " << arr[idx]
                     << ")";
                return;
            }
        }
    }
}

// Driver Code
int main()
{
    vector<string> arr
        = { "geeksforgeeks", "geeks", "geeksforcse" };

    int N = arr.size();
    findMaxLenPair(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

// class of Trie
class TrieNode {
    TrieNode[] child = new TrieNode[256];
    TrieNode() {}
}

class GFG {

    // Function to insert a string into Trie
    private static void insertTrie(TrieNode root,
                                   String str)
    {

        // Stores length of the string
        int M = str.length();

        // Traverse the string str
        for (int i = 0; i < M; i++) {

            // If str[i] is not present
            // in current path of Trie
            if (root.child[str.charAt(i)] == null) {

                // Create a new node
                // of Trie
                root.child[str.charAt(i)] = new TrieNode();
            }

            // Update root
            root = root.child[str.charAt(i)];
        }
    }

    // Function to find the maximum length of
    // longest common prefix in Trie with str
    private static int findStrLen(TrieNode root, String str)
    {

        // Stores length of str
        int M = str.length();

        // Stores length of longest
        // common prefix in Trie with str
        int len = 0;

        // Traverse the string str
        for (int i = 0; i < M; i++) {

            // If str[i] is present in
            // the current path of Trie
            if (root.child[str.charAt(i)] != null) {

                // Update len
                len++;

                // Update root
                root = root.child[str.charAt(i)];
            }
            else {
                return len;
            }
        }
        return len;
    }

    // Function to print the pair having maximum
    // length of the longest common prefix
    private static void findMaxLenPair(List<String> arr,
                                       int N)
    {
        // Stores index of the string having
        // maximum length of longest common prefix
        int idx = -1;

        // Stores maximum length of longest
        // common prefix.
        int len = 0;

        // Create root node of Trie
        TrieNode root = new TrieNode();

        // Insert arr[0] into Trie
        insertTrie(root, arr.get(0));

        // Traverse the array.
        for (int i = 1; i < N; i++) {

            // Stores maximum length of longest
            // common prefix in Trie with arr[i]
            int temp = findStrLen(root, arr.get(i));

            // If temp is greater than len
            if (temp > len) {

                // Update len
                len = temp;

                // Update idx
                idx = i;
            }

            insertTrie(root, arr.get(i));
        }

        // Traverse array arr[]
        for (int i = 0; i < N; i++) {

            // Stores length of arr[i]
            int M = arr.get(i).length();

            // Check if maximum length of
            // longest common prefix > M
            if (i != idx && M >= len) {
                boolean found = true;
                // Traverse string arr[i]
                // and arr[j]
                for (int j = 0; j < len; j++) {

                    // If current character of both
                    // string does not match.
                    if (arr.get(i).charAt(j)
                        != arr.get(idx).charAt(j)) {
                        found = false;
                        break;
                    }
                }

                // Print pairs having maximum length
                // of the longest common prefix
                if (found) {
                    System.out.println("(" + arr.get(i)
                                       + ", " + arr.get(idx)
                                       + ")");
                    return;
                }
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        List<String> arr = Arrays.asList(new String[] {
            "geeksforgeeks", "geeks", "geeksforcse" });
        int N = arr.size();
        findMaxLenPair(arr, N);
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

// class of Trie
public class GFG
{

  public class TrieNode
  {
    public TrieNode[] child = new TrieNode[256];
    public TrieNode() {}
  };

  // Function to insert a string into Trie
  public static void insertTrie(TrieNode root,
                                String str)
  {

    // Stores length of the string
    int M = str.Length;

    // Traverse the string str
    for (int i = 0; i < M; i++) {

      // If str[i] is not present
      // in current path of Trie
      if (root.child[str[i]] == null) {

        // Create a new node
        // of Trie
        root.child[str[i]] = new TrieNode();
      }

      // Update root
      root = root.child[str[i]];
    }
  }

  // Function to find the maximum length of
  // longest common prefix in Trie with str
  public static int findStrLen(TrieNode root, String str)
  {

    // Stores length of str
    int M = str.Length;

    // Stores length of longest
    // common prefix in Trie with str
    int len = 0;

    // Traverse the string str
    for (int i = 0; i < M; i++) {

      // If str[i] is present in
      // the current path of Trie
      if (root.child[str[i]] != null) {

        // Update len
        len++;

        // Update root
        root = root.child[str[i]];
      }
      else {
        return len;
      }
    }
    return len;
  }

  // Function to print the pair having maximum
  // length of the longest common prefix
  public static void findMaxLenPair(List<string> arr,
                                    int N)
  {
    // Stores index of the string having
    // maximum length of longest common prefix
    int idx = -1;

    // Stores maximum length of longest
    // common prefix.
    int len = 0;

    // Create root node of Trie
    TrieNode root = new TrieNode();

    // Insert arr[0] into Trie
    insertTrie(root, arr[0]);

    // Traverse the array.
    for (int i = 1; i < N; i++) {

      // Stores maximum length of longest
      // common prefix in Trie with arr[i]
      int temp = findStrLen(root, arr[i]);

      // If temp is greater than len
      if (temp > len) {

        // Update len
        len = temp;

        // Update idx
        idx = i;
      }

      insertTrie(root, arr[i]);
    }

    // Traverse array arr[]
    for (int i = 0; i < N; i++) {

      // Stores length of arr[i]
      int M = arr[i].Length;

      // Check if maximum length of
      // longest common prefix > M
      if (i != idx && M >= len) {
        bool found = true;
        // Traverse string arr[i]
        // and arr[j]
        for (int j = 0; j < len; j++) {

          // If current character of both
          // string does not match.
          if (arr[i][j] != arr[idx][j]) {
            found = false;
            break;
          }
        }

        // Print pairs having maximum length
        // of the longest common prefix
        if (found) {
          Console.WriteLine("(" + arr[i]+ ", " + arr[idx]+ ")");
          return;
        }
      }
    }
  }

  // Driver Code
  public static void Main()
  {
    List<string> arr = new List<string>() {"geeksforgeeks", "geeks", "geeksforcse" };
    int N = arr.Count;
    findMaxLenPair(arr, N);
  }
}

// THIS CODE IS CONTRIBUTED BY SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Class of Trie
class TrieNode
{
    constructor()
    {
        this.child = Array(256);
    }
};

// Function to insert a string into Trie
function insertTrie(root, str)
{

    // Stores length of the string
    var M = str.length;

    // Traverse the string str
    for(var i = 0; i < M; i++)
    {

        // If str[i] is not present
        // in current path of Trie
        if (root.child[str[i]] == null)
        {

            // Create a new node
            // of Trie
            root.child[str[i]] = new TrieNode();
        }

        // Update root
        root = root.child[str[i]];
    }
}

// Function to find the maximum length of
// longest common prefix in Trie with str
function findStrLen(root, str)
{

    // Stores length of str
    var M = str.length;

    // Stores length of longest
    // common prefix in Trie with str
    var len = 0;

    // Traverse the string str
    for(var i = 0; i < M; i++)
    {

        // If str[i] is present in
        // the current path of Trie
        if (root.child[str[i]] != null)
        {

            // Update len
            len++;

            // Update root
            root = root.child[str[i]];
        }
        else
        {
            return len;
        }
    }
    return len;
}

// Function to print the pair having maximum
// length of the longest common prefix
function findMaxLenPair(arr, N)
{

    // Stores index of the string having
    // maximum length of longest common prefix
    var idx = -1;

    // Stores maximum length of longest
    // common prefix.
    var len = 0;

    // Create root node of Trie
    var root = new TrieNode();

    // Insert arr[0] into Trie
    insertTrie(root, arr[0]);

    // Traverse the array.
    for(var i = 1; i < N; i++)
    {

        // Stores maximum length of longest
        // common prefix in Trie with arr[i]
        var temp = findStrLen(root, arr[i]);

        // If temp is greater than len
        if (temp > len)
        {

            // Update len
            len = temp;

            // Update idx
            idx = i;
        }
        insertTrie(root, arr[i]);
    }

    // Traverse array arr[]
    for(var i = 0; i < N; i++)
    {

        // Stores length of arr[i]
        var M = arr[i].length;

        // Check if maximum length of
        // longest common prefix > M
        if (i != idx && M >= len)
        {
            var found = true;

            // Traverse string arr[i]
            // and arr[j]
            for(var j = 0; j < len; j++)
            {

                // If current character of both
                // string does not match.
                if (arr[i][j] != arr[idx][j])
                {
                    found = false;
                    break;
                }
            }

            // Print pairs having maximum length
            // of the longest common prefix
            if (found)
            {
                document.write("(" + arr[i] +
                               ", " + arr[idx] + ")");
                return;
            }
        }
    }
}

// Driver Code
var arr = [ "geeksforgeeks", "geeks",
            "geeksforcse" ];
var N = arr.length;

findMaxLenPair(arr, N);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
(geeksforgeeks, geeksforcse)
```

***时间复杂度:** O(N * M)，其中 M 表示最长字符串的长度*
***辅助空间:** 0(N * 256)*