# 根据给定的顺序对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/基于给定顺序对字符串数组进行排序/](https://www.geeksforgeeks.org/sort-an-array-of-strings-based-on-the-given-order/)

给定一个字符串数组**单词[]** 和字母的**顺序**，我们的任务是根据给定的顺序对数组进行排序。假设字典和单词只包含小写字母。

**示例:**

> **输入:**单词= {“hello”、“geeksforgeeks”}，顺序=“hlabcdefgijknmopqrstuvwxyz”
> **输出:**“hello”、“geeksforgeeks”
> **解释:**
> 根据给定的顺序‘h’出现在‘g’之前，因此单词被认为是排序的。
> 
> **输入:**字数= {“word”、“world”、“row”}，顺序=“worldabcegfghijkmnpqstuxyz”
> **输出:**“world”、“word”、“row”
> **解释:**
> 按照给定的顺序‘l’出现在‘d’之前因此‘world’这个词会先保留。

**方法:**为了解决上面提到的问题，我们需要**按照给定的顺序保持每个角色**的优先级。为此，请使用 [**地图数据结构**](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 。

*   按照给定的顺序迭代，并将字符的优先级设置为其索引值。
*   使用自定义比较器函数对数组进行排序。
*   在比较器函数中，遍历两个单词之间最小大小的单词，并尝试找到第一个不同的字符，优先级值较低的单词将是较小的单词。
*   如果单词有相同的前缀，那么较小的单词就是较小的单词。

**以下是上述方法的实施:**

## C++

```
// C++ program to sort an array
// of strings based on the given order

#include <bits/stdc++.h>
using namespace std;

// For storing priority of each character
unordered_map<char, int> mp;

// Custom comparator function for sort
bool comp(string& a, string& b)
{

    // Loop through the minimum size
    // between two words
    for (int i = 0;
         i < min(a.size(), b.size());
         i++) {

        // Check if the characters
        // at position i are different,
        // then the word containing lower
        // valued character is smaller
        if (mp[a[i]] != mp[b[i]])
            return mp[a[i]] < mp[b[i]];
    }

    /* When loop breaks without returning, it
       means the prefix of both words were same
       till the execution of the loop.
       Now, the word with the smaller size will
       occur before in sorted order
        */
    return (a.size() < b.size());
}

// Function to print the
// new sorted array of strings
void printSorted(vector<string> words,
                 string order)
{

    // Mapping each character
    // to its occurrence position
    for (int i = 0; i < order.size(); i++)
        mp[order[i]] = i;

    // Sorting with custom sort function
    sort(words.begin(), words.end(), comp);

    // Printing the sorted order of words
    for (auto x : words)
        cout << x << " ";
}

// Driver code
int main()
{

    vector<string> words
        = { "word", "world", "row" };
    string order
        = { "worldabcefghijkmnpqstuvxyz" };

    printSorted(words, order);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to sort an array
# of strings based on the given order
from functools import cmp_to_key

# For storing priority of each character
mp = {}

# Custom comparator function for sort
def comp(a, b):

    # Loop through the minimum size
    # between two words
    for i in range( min(len(a), len(b))):

        # Check if the characters
        # at position i are different,
        # then the word containing lower
        # valued character is smaller
        if (mp[a[i]] != mp[b[i]]):
            if mp[a[i]] < mp[b[i]]:
                return -1
            else:
                return 1

    '''When loop breaks without returning, it
    means the prefix of both words were same
    till the execution of the loop.
    Now, the word with the smaller size will
    occur before in sorted order'''
    if (len(a) < len(b)):
        return -1
    else:
        return 1

# Function to print the
# new sorted array of strings
def printSorted(words, order):

    # Mapping each character
    # to its occurrence position
    for i in range(len(order)):
        mp[order[i]] = i

    # Sorting with custom sort function
    words = sorted(words, key = cmp_to_key(comp))

    # Printing the sorted order of words
    for x in words:
        print(x, end = " ")

# Driver code
words = [ "word", "world", "row" ]
order = "worldabcefghijkmnpqstuvxyz"

printSorted(words, order)

# This code is contributed by Shivani
```

**Output:** 

```
world word row
```