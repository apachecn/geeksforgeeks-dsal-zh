# 根据字符串中好词的出现频率对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-a-array-of-string-based-on-frequency-of-good-words-in-their/](https://www.geeksforgeeks.org/sort-an-array-of-strings-based-on-the-frequency-of-good-words-in-them/)

给定不同客户的一组**产品评论** ( **R** )和一串包含由 **_** 分隔的好词的 **S** ，任务是按照好值递减的**顺序对评论进行排序。
**优度值**由该评论中出现的好词数量来定义。**

**示例:**

> **输入:**S =“geeks _ for _ geeks _ is _ great”、
> R = {“geeks _ are _ geeks”、“geeks _ dont _ lose”、“geeks _ for _ geeks _ is _ love”}
> T4】输出:T6】geeks for geeks is love
> geeks 是 geeks
> geeks 不亏
> 
> **输入:**S =“cool _ wifi _ ice”、
> R = {“water _ is _ cool”、“cold _ ice _ 饮品”、“cool _ wifi _ speed”}
> T4】输出:T6】cool wifi speed
> water is cool
> 冷冰饮品

**天真方法:**将所有好词插入一个[无序 _ 集合](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)中，然后遍历评论数组中每个句子的每个词，并通过检查这个词是否出现在那个好词集合中来记录好词的数量。然后我们使用一个稳定的排序算法，根据 R 中出现的每个评论的好词数对数组 R 进行排序，很明显这个方法的时间复杂度**大于 O(N * NlogN)** 。

**有效方法:**对所有好词进行[特里亚](https://www.geeksforgeeks.org/trie-insert-and-search/)，并使用特里亚在复习中检查每个词的好度。

1.  把所有的好词插入一个句子。
2.  对于每次复习，通过检查给定的单词是否存在于 trie 中来计算其中好单词的数量。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define F first
#define S second
#define MAX 26

// Comparator function for sorting
bool cmp(const pair<int, int>& a, const pair<int, int>& b)
{

    // Compare the number of good words
    if (a.F == b.F)
        return a.S < b.S;
    return a.F > b.F;
}

// Structure of s Trie node
struct node {
    bool exist;
    node* arr[MAX];
    node(bool bul = false)
    {
        exist = bul;
        for (int i = 0; i < MAX; i++)
            arr[i] = NULL;
    }
};

// Function to add a string to the trie
void add(string s, node* trie)
{
    // Add a node to the trie
    int n = s.size();
    for (int i = 0; i < n; i++) {

        // If trie doesn't already contain
        // the current node then create one
        if (trie->arr[s[i] - 'a'] == NULL)
            trie->arr[s[i] - 'a'] = new node();

        trie = trie->arr[s[i] - 'a'];
    }
    trie->exist = true;
    return;
}

// Function that returns true if
// the trie contains the string s
bool search(string s, node* trie)
{
    // Search for a node in the trie
    for (int i = 0; i < s.size(); i++) {
        if (trie->arr[s[i] - 'a'] == NULL)
            return false;

        trie = trie->arr[s[i] - 'a'];
    }
    return trie->exist;
}

// Function to replace every '_' with a
// white space in the given string
void convert(string& str)
{
    // Convert '_' to spaces
    for (int i = 0; i < str.size(); i++)
        if (str[i] == '_')
            str[i] = ' ';
    return;
}

// Function to sort the array based on good words
void sortArr(string good, vector<string>& review)
{

    // Extract all the good words which
    // are '_' separated
    convert(good);
    node* trie = new node();
    string word;
    stringstream ss;
    ss << good;

    // Building the entire trie by stringstreaming
    // the 'good words' string
    while (ss >> word)
        add(word, trie);
    int k, n = review.size();

    // To store the number of good words
    // and the string index pairs
    vector<pair<int, int> > rating(n);
    for (int i = 0; i < n; i++) {
        convert(review[i]);
        ss.clear();
        ss << review[i];
        k = 0;
        while (ss >> word) {

            // If this word is present in the trie
            // then increment its count
            if (search(word, trie))
                k++;
        }

        // Store the number of good words in the
        // current string paired with its
        // index in the original array
        rating[i].F = k;
        rating[i].S = i;
    }

    // Using comparator function to
    // sort the array as required
    sort(rating.begin(), rating.end(), cmp);

    // Print the sorted array
    for (int i = 0; i < n; i++)
        cout << review[rating[i].S] << "\n";
}

// Driver code
int main()
{

    // String containing good words
    string S = "geeks_for_geeks_is_great";

    // Vector of strings to be sorted
    vector<string> R = { "geeks_are_geeks", "geeks_dont_lose",
                         "geeks_for_geeks_is_love" };

    // Sort the array based on the given conditions
    sortArr(S, R);
}
```

**Output:**

```
geeks for geeks is love
geeks are geeks
geeks dont lose

```