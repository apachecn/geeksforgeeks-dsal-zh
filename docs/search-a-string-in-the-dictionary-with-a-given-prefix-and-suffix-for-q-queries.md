# 在字典中搜索给定前缀和后缀的字符串进行 Q 查询

> 原文:[https://www . geesforgeks . org/search-a-string-in-in-dictionary-a-给定前缀和后缀的 q-query/](https://www.geeksforgeeks.org/search-a-string-in-the-dictionary-with-a-given-prefix-and-suffix-for-q-queries/)

给定一个由两个字符串形式的 **N** 字符串和 **Q** 查询组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，每个查询的任务是在给定数组中找到任意一个带有给定**前缀**和**后缀**的字符串。如果没有这样的字符串，则打印【T16 "-" 1 "。

**示例:**

> **输入:** arr[] = {“苹果”、“app”、“饼干”、“鼠标”、“橘子”、“蝙蝠”、“麦克风”、“我的”}，Query[]= { {a，e}、{ a，p}}
> **输出:**
> 苹果
> app
> **解释:**
> **查询 1:** 字符串“apple”是给定词典中唯一一个带有给定前缀“a”和后缀“e”的单词。
> **查询 2:** 字符串“app”是给定字典中唯一一个带有给定前缀“a”和后缀“p”的单词。
> 
> **输入:** arr[] = {“苹果”、“app”、“饼干”、“鼠标”、“橘子”、“蝙蝠”、“麦克风”、“我的”}，query[]= { { mi，ne}}
> **输出:**我的

**天真方法:**解决给定问题的最简单方法是[遍历给定的字符串数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**对于每个查询，如果存在任何具有给定前缀和后缀的字符串，则打印该字符串。否则，打印**-1”**。

***时间复杂度:** O(Q*N*M)，其中 M 为弦的最大* [*长度*](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/) *。*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用 [Trie 数据结构](https://www.geeksforgeeks.org/trie-insert-and-search/)进行优化来解决问题。trie 的实现可以修改为支持前缀和后缀搜索，方式如下:

*   假设字典中给定的单词是**苹果**。在这种情况下，单词**苹果**被插入 Trie。但是为了支持前缀和后缀同时搜索，可以在 Trie 中插入单词: **e{apple，le{apple，ple{apple，pple{apple，apple { apple }**。
*   请注意，这些单词的形式是**后缀{单词**，其中**后缀**是给定单词的所有可能后缀。
*   后缀和单词之间插入特殊字符 **{** 将它们分开。除了字母以外的任何特殊字符都可以用来代替 **{** ，但是 **{** 是首选的，因为它的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)是 123，比 **z** 的 ASCII 值多一个。

按照以下步骤解决问题:

*   使用变量 **i** 遍历数组**arr【】**中的所有字符串，并执行以下步骤:
    *   初始化一个字符串， **temp** 为 **'{' + arr[i]** 。
    *   [从头至尾遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、**arr【I】**中的所有字符，对于每个字符[将其附加到字符串](https://www.geeksforgeeks.org/stdstringinsert-in-c/) **temp** 的前面，然后[将该字符串插入到字符串](https://www.geeksforgeeks.org/trie-insert-and-search/)中。
*   创建 trie 后，[遍历所有查询](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)并执行以下步骤:
    *   存储当前查询的**前缀**和**后缀**字符串。
    *   初始化一个字符串， **t** 作为**后缀+ '{' +前缀**，[在 trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 中搜索。
    *   如果没有找到，则打印**-1”**。否则，打印匹配的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Trie Node
struct Trie {
    Trie* arr[27] = { NULL };

    // Stores the index of the word
    // in the dictionary
    int idx;
};

// Root node of the Trie
Trie* root = new Trie();

// Function to insert the words in
// the Trie
void insert(string word, int i)
{
    // Temporary pointer to the root
    // node of the Trie
    Trie* temp = root;

    // Traverse through all the
    // characters of current word
    for (char ch : word) {

        // Make a Trie Node, if not
        // already present
        if (temp->arr[ch - 'a'] == NULL) {
            Trie* t = new Trie();
            temp->arr[ch - 'a'] = t;
        }

        temp = temp->arr[ch - 'a'];
        temp->idx = i;
    }
}

// Function to search the words in Trie
int search(string word)
{
    Trie* temp = root;

    // Traverse through all the
    // characters of current word
    for (char ch : word) {

        // If no valid Trie Node exists
        // for the current character
        // then there is no match
        if (temp->arr[ch - 'a'] == NULL)
            return -1;
        temp = temp->arr[ch - 'a'];
    }

    // Return the resultant index
    return temp->idx;
}

// Function to search for a word in
// the dictionary with the given
// prefix and suffix for each query
void findMatchingString(
    string words[], int n,
    vector<vector<string> > Q)
{
    string temp, t;

    // Insertion in the Trie
    for (int i = 0; i < n; i++) {

        // Form all the words of the
        // form suffix{word and insert
        // them in the trie
        temp = "{" + words[i];

        for (int j = words[i].size() - 1;
             j >= 0; j--) {
            t = words[i][j] + temp;
            temp = t;

            // Insert into Trie
            insert(t, i);
        }
    }

    // Traverse all the queries
    for (int i = 0; i < Q.size(); i++) {

        string prefix = Q[i][0];
        string suffix = Q[i][1];
        string temp = suffix + "{" + prefix;

        // Stores the index of
        // the required word
        int res;

        // Store the index of the
        // word in the dictionary
        res = search(temp);

        // In case of match, print
        // the corresponding string
        if (res != -1) {
            cout << words[res] << '\n';
        }

        // Otherwise, No match found
        else
            cout << "-1\n";
    }
}

// Driver Code
int main()
{
    string arr[]
        = { "apple", "app", "biscuit",
            "mouse", "orange", "bat",
            "microphone", "mine" };
    int N = 8;
    vector<vector<string> > Q = { { "a", "e" }, { "mi", "ne" } };
    findMatchingString(arr, N, Q);

    return 0;
}
```

**Output:**

```
apple
mine

```

***时间复杂度:** O(N*M <sup>2</sup> + Q*M)，其中 M 是所有弦
**中最大的[长度辅助空间:](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)** O(N*M <sup>2</sup> )*