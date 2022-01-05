# 后缀数组|集合 1(简介)

> 原文:[https://www . geesforgeks . org/后缀-数组-集合-1-简介/](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)

我们强烈建议阅读以下关于后缀树的文章，作为这篇文章的先决条件。
[模式搜索|集合 8(后缀树介绍)](https://www.geeksforgeeks.org/pattern-searching-set-8-suffix-tree-introduction/)
***后缀数组是给定字符串所有后缀的排序数组*** 。定义类似于[后缀树，它是给定文本](https://www.geeksforgeeks.org/pattern-searching-set-8-suffix-tree-introduction/)的所有后缀的压缩三元组。任何基于后缀树的算法都可以用使用附加信息增强的后缀数组的算法来代替，并以相同的时间复杂度解决相同的问题(来源 [Wiki](http://en.wikipedia.org/wiki/Suffix_array) )。
通过对后缀树进行 DFS 遍历，可以从后缀树构造后缀数组。事实上，后缀数组和后缀树都可以在线性时间内相互构造。
后缀数组相对于后缀树的优势包括改进的空间需求、更简单的线性时间构造算法(例如，与 Ukkonen 的算法相比)和改进的缓存局部性(来源: [Wiki](http://en.wikipedia.org/wiki/Suffix_array#Correspondence_to_suffix_trees) )
***示例:***

```
Let the given string be "banana".

0 banana                          5 a
1 anana     Sort the Suffixes     3 ana
2 nana      ---------------->     1 anana  
3 ana        alphabetically       0 banana  
4 na                              4 na   
5 a                               2 nana

So the suffix array for "banana" is {5, 3, 1, 0, 4, 2}
```

***构建后缀数组的幼稚方法***
构建后缀数组的简单方法是将所有后缀组成一个数组，然后对数组进行排序。下面是简单方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Naive algorithm for building suffix array of a given text
#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;

// Structure to store information of a suffix
struct suffix
{
    int index;
    char *suff;
};

// A comparison function used by sort() to compare two suffixes
int cmp(struct suffix a, struct suffix b)
{
    return strcmp(a.suff, b.suff) < 0? 1 : 0;
}

// This is the main function that takes a string 'txt' of size n as an
// argument, builds and return the suffix array for the given string
int *buildSuffixArray(char *txt, int n)
{
    // A structure to store suffixes and their indexes
    struct suffix suffixes[n];

    // Store suffixes and their indexes in an array of structures.
    // The structure is needed to sort the suffixes alphabetically
    // and maintain their old indexes while sorting
    for (int i = 0; i < n; i++)
    {
        suffixes[i].index = i;
        suffixes[i].suff = (txt+i);
    }

    // Sort the suffixes using the comparison function
    // defined above.
    sort(suffixes, suffixes+n, cmp);

    // Store indexes of all sorted suffixes in the suffix array
    int *suffixArr = new int[n];
    for (int i = 0; i < n; i++)
        suffixArr[i] = suffixes[i].index;

    // Return the suffix array
    return  suffixArr;
}

// A utility function to print an array of given size
void printArr(int arr[], int n)
{
    for(int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver program to test above functions
int main()
{
    char txt[] = "banana";
    int n = strlen(txt);
    int *suffixArr = buildSuffixArray(txt,  n);
    cout << "Following is suffix array for " << txt << endl;
    printArr(suffixArr, n);
    return 0;
}
```

输出:

```
Following is suffix array for banana
5 3 1 0 4 2
```

如果我们考虑一个用于排序的 O(nLogn)算法，上述建立后缀数组方法的时间复杂度为 O(n <sup>2</sup> Logn)。排序步骤本身需要 0(n)<sup>2</sup>Logn)时间，因为每次比较都是两个字符串的比较，并且比较需要 0(n)时间。
建立后缀数组有很多高效的算法。我们很快将把它们作为单独的帖子进行报道。
***使用构建的后缀数组***
搜索模式为了在文本中搜索模式，我们对文本进行预处理，并构建文本的后缀数组。因为我们有所有后缀的排序数组，[二分搜索法](http://geeksquiz.com/binary-search/)可以用来搜索。下面是搜索功能。请注意，该函数并不报告模式的所有出现，它只报告其中的一个。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// This code only contains search() and main. To make it a complete running
// above code or see https://ide.geeksforgeeks.org/oY7OkD

// A suffix array based search function to search a given pattern
// 'pat' in given text 'txt' using suffix array suffArr[]
void search(char *pat, char *txt, int *suffArr, int n)
{
    int m = strlen(pat);  // get length of pattern, needed for strncmp()

    // Do simple binary search for the pat in txt using the
    // built suffix array
    int l = 0, r = n-1;  // Initialize left and right indexes
    while (l <= r)
    {
        // See if 'pat' is prefix of middle suffix in suffix array
        int mid = l + (r - l)/2;
        int res = strncmp(pat, txt+suffArr[mid], m);

        // If match found at the middle, print it and return
        if (res == 0)
        {
            cout << "Pattern found at index " << suffArr[mid];
            return;
        }

        // Move to left half if pattern is alphabetically less than
        // the mid suffix
        if (res < 0) r = mid - 1;

        // Otherwise move to right half
        else l = mid + 1;
    }

    // We reach here if return statement in loop is not executed
    cout << "Pattern not found";
}

// Driver program to test above function
int main()
{
    char txt[] = "banana";  // text
    char pat[] = "nan";   // pattern to be searched in text

    // Build suffix array
    int n = strlen(txt);
    int *suffArr = buildSuffixArray(txt, n);

    // search pat in txt using the built suffix array
    search(pat, txt, suffArr, n);

    return 0;
}
```

输出:

```
Pattern found at index 2
```

**时间复杂度:**O(mlogn)
T3】辅助空间: O(m+n)

一旦后缀数组建立，就有更有效的算法来搜索模式。事实上，有一个基于 O(m)后缀数组的算法来搜索模式。我们将很快讨论搜索的有效算法。
***后缀数组的应用***
后缀数组是一种极其有用的数据结构，它可以用于各种各样的问题。以下是后缀数组可以使用的一些著名问题。
1)模式搜索
2) [查找最长重复子串](http://en.wikipedia.org/wiki/Longest_repeated_substring_problem)
3) [查找最长公共子串](http://en.wikipedia.org/wiki/Longest_common_substring_problem)
4) [查找字符串中最长回文](http://en.wikipedia.org/wiki/Longest_palindromic_substring)

更多可以使用后缀数组的问题参见[本](http://www.stanford.edu/class/cs97si/suffix-array.pdf)。
此帖为简单介绍。后缀数组中有很多内容需要介绍。我们在这里讨论了[后缀数组构造的 O(nLogn)算法](https://www.geeksforgeeks.org/suffix-array-set-2-a-nlognlogn-algorithm/) [。我们将很快讨论更有效的后缀数组算法。
**参考文献:**](https://www.geeksforgeeks.org/suffix-array-set-2-a-nlognlogn-algorithm/) [http://www.stanford.edu/class/cs97si/suffix-array.pdf](http://www.stanford.edu/class/cs97si/suffix-array.pdf)
[http://en.wikipedia.org/wiki/Suffix_array](http://en.wikipedia.org/wiki/Suffix_array)
如有不正确的地方请写评论，或者想分享以上讨论话题的更多信息