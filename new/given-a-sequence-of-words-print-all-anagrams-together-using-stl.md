# 给定一系列单词，请使用 STL

将所有字谜一起打印

给定一组单词，将所有字谜一起打印。
**例如，**

```
Input: array = {“cat”, “dog”, “tac”, “god”, “act”}
output: cat tac act, dog god
Explanation: cat tac and act are anagrams 
and dog and god are anagrams as 
they have the same set of characters.

Input: array = {“abc”, “def”, “ghi”}
output: abc, def, ghi
Explanation: There are no anagrams in the array.

```

这些帖子将在此处讨论其他方法：

*   [一起给单词顺序打印所有字谜](https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together/)
*   [给定单词顺序，将所有字母组合在一起打印集 2](https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together-set-2/)

**<u>方法：</u>** 这是使用 C ++标准模板库的 HashMap 解决方案，该库存储键值对。 在哈希图中，键将是字符的排序集合，值将是输出字符串。 当两个字谜的字符排序时，它们将相似。 现在

1.  将矢量元素存储在 HashMap 中，其中 key 为已排序的字符串。
2.  如果键相同，则将字符串添加到 HashMap（字符串向量）的值中。
3.  遍历 HashMap 并打印字谜字符串。

## CPP

```

// CPP program for finding all anagram
// pairs in the given array
#include <algorithm>
#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

// Utility function for
// printing anagram list
void printAnagram(
    unordered_map<string,
                  vector<string> >& store)
{
    unordered_map<string,
                  vector<string> >::iterator it;
    for (it = store.begin();
         it != store.end(); it++) {
        vector<string> temp_vec(it->second);
        int size = temp_vec.size();
        if (size > 1) {
            for (int i = 0; i < size; i++) {
                cout << temp_vec[i] << " ";
            }
            cout << "\n";
        }
    }
}

// Utility function for storing
// the vector of strings into HashMap
void storeInMap(vector<string>& vec)
{
    unordered_map<string,
                  vector<string> >
        store;
    for (int i = 0; i < vec.size(); i++) {

        string tempString(vec[i]);
        sort(tempString.begin(),
             tempString.end());

        // Check for sorted string
        // if it already exists
        if (store.find(
                tempString)
            == store.end()) {
            vector<string> temp_vec;
            temp_vec.push_back(vec[i]);
            store.insert(make_pair(
                tempString, temp_vec));
        }

        else {
            // Push new string to
            // already existing key
            vector<string> temp_vec(
                store[tempString]);
            temp_vec.push_back(vec[i]);
            store[tempString] = temp_vec;
        }
    }

    // print utility function for printing
    // all the anagrams
    printAnagram(store);
}

// Driver code
int main()
{
    // initialize vector of strings
    vector<string> arr;
    arr.push_back("geeksquiz");
    arr.push_back("geeksforgeeks");
    arr.push_back("abcd");
    arr.push_back("forgeeksgeeks");
    arr.push_back("zuiqkeegs");
    arr.push_back("cat");
    arr.push_back("act");
    arr.push_back("tca");

    // utility function for storing
    // strings into hashmap
    storeInMap(arr);
    return 0;
}

```

***注意：**使用 g ++中的-std = c ++ 11 标志编译以上程序*
**输出：**

```
cat act tca 
geeksforgeeks forgeeksgeeks 
geeksquiz zuiqkeegs 

```

**复杂度分析：**，

*   **时间复杂度：** O（n * m（log m）），其中 m 是单词的长度。
    需要对数组进行一次遍历。
*   **空间复杂度：** O（n）。
    字符串中有 n 个单词。 该映射需要 O（n）空间来存储字符串。

本文由 [**Mandeep Singh**](https://github.com/msdeep14) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。