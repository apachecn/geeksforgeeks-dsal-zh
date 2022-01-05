# kasai 从后缀数组

构造 LCP 数组的算法

> 原文:[https://www . geeksforgeeks . org/% C2 % ad % C2 % adkasais-算法构建 LCP-数组-从后缀-数组/](https://www.geeksforgeeks.org/%c2%ad%c2%adkasais-algorithm-for-construction-of-lcp-array-from-suffix-array/)

**背景后缀数组:**后缀数组是给定字符串的所有后缀的排序数组。
让给定的字符串为“香蕉”。

```
0 banana                          5 a
1 anana     Sort the Suffixes     3 ana
2 nana      ---------------->     1 anana  
3 ana        alphabetically       0 banana  
4 na                              4 na   
5 a                               2 nana
```

“香蕉”的后缀数组:
后缀[] = {5，3，1，0，4，2}
我们已经讨论了[后缀数组和它的 O(nLogn)构造](https://www.geeksforgeeks.org/suffix-array-set-2-a-nlognlogn-algorithm/)。
后缀数组一旦建立，我们就可以用它来有效地搜索文本中的模式。例如，我们可以使用二分搜索法找到一个模式(相同的完整代码在这里讨论)

**LCP 数组**
这里讨论的基于二分搜索法的解决方案花费 O(m*Logn)时间，其中 m 是要搜索的模式的长度，n 是文本的长度。借助 LCP 数组，我们可以在 O(m + Log n)时间内搜索到一个模式。例如，如果我们的任务是在“香蕉”中搜索“ana”，则 m = 3，n = 5。
***LCP 数组是一个大小为 n 的数组(类似后缀数组)。值 lcp[i]表示由后缀[i]和后缀[i+1]索引的后缀中最长公共前缀的长度。*** 后缀【n-1】没有定义，因为后面没有后缀。

```
txt[0..n-1] = "banana"
suffix[]  = {5, 3, 1, 0, 4, 2| 
lcp[]     = {1, 3, 0, 0, 2, 0}

Suffixes represented by suffix array in order are:
{"a", "ana", "anana", "banana", "na", "nana"}

lcp[0] = Longest Common Prefix of "a" and "ana"     = 1
lcp[1] = Longest Common Prefix of "ana" and "anana" = 3
lcp[2] = Longest Common Prefix of "anana" and "banana" = 0
lcp[3] = Longest Common Prefix of "banana" and "na" = 0
lcp[4] = Longest Common Prefix of "na" and "nana" = 2
lcp[5] = Longest Common Prefix of "nana" and None = 0
```

**如何构建 LCP 阵列？**
LCP 数组的构建有两种方式:
1)计算 LCP 数组作为后缀数组的副产品(曼博&迈尔斯算法)
2)使用已经构建的后缀数组来计算 LCP 值。(Kasai 算法)。
存在可以在 O(n)时间构造后缀数组的算法，因此我们总是可以在 O(n)时间构造 LCP 数组。但是在下面的实现中，讨论了一个 O(n Log n)算法。

**kasai 的算法**
本文讨论的是 kasai 的算法。该算法在 O(n)时间内由后缀数组和输入文本构造 LCP 数组。这个想法是基于以下事实:
让从 txt[I]开始的后缀的 lcp 为 k，如果 k 大于 0，那么从 txt[i+1]开始的后缀的 lcp 至少为-k-1。原因是，字符的相对顺序保持不变。如果我们从两个后缀中删除第一个字符，我们知道至少有 k 个字符匹配。例如，对于子字符串“ana”，lcp 为 3，因此对于字符串“na”，lcp 至少为-2。参考[本](http://www.mi.fu-berlin.de/wiki/pub/ABI/RnaSeqP4/suffix-array.pdf)进行证明。

下面是 Kasai 算法的 C++实现。

## C++

```
// C++ program for building LCP array for given text
#include <bits/stdc++.h>
using namespace std;

// Structure to store information of a suffix
struct suffix
{
    int index;  // To store original index
    int rank[2]; // To store ranks and next rank pair
};

// A comparison function used by sort() to compare two suffixes
// Compares two pairs, returns 1 if first pair is smaller
int cmp(struct suffix a, struct suffix b)
{
    return (a.rank[0] == b.rank[0])? (a.rank[1] < b.rank[1] ?1: 0):
           (a.rank[0] < b.rank[0] ?1: 0);
}

// This is the main function that takes a string 'txt' of size n as an
// argument, builds and return the suffix array for the given string
vector<int> buildSuffixArray(string txt, int n)
{
    // A structure to store suffixes and their indexes
    struct suffix suffixes[n];

    // Store suffixes and their indexes in an array of structures.
    // The structure is needed to sort the suffixes alphabetically
    // and maintain their old indexes while sorting
    for (int i = 0; i < n; i++)
    {
        suffixes[i].index = i;
        suffixes[i].rank[0] = txt[i] - 'a';
        suffixes[i].rank[1] = ((i+1) < n)? (txt[i + 1] - 'a'): -1;
    }

    // Sort the suffixes using the comparison function
    // defined above.
    sort(suffixes, suffixes+n, cmp);

    // At his point, all suffixes are sorted according to first
    // 2 characters.  Let us sort suffixes according to first 4
    // characters, then first 8 and so on
    int ind[n];  // This array is needed to get the index in suffixes[]
    // from original index.  This mapping is needed to get
    // next suffix.
    for (int k = 4; k < 2*n; k = k*2)
    {
        // Assigning rank and index values to first suffix
        int rank = 0;
        int prev_rank = suffixes[0].rank[0];
        suffixes[0].rank[0] = rank;
        ind[suffixes[0].index] = 0;

        // Assigning rank to suffixes
        for (int i = 1; i < n; i++)
        {
            // If first rank and next ranks are same as that of previous
            // suffix in array, assign the same new rank to this suffix
            if (suffixes[i].rank[0] == prev_rank &&
                    suffixes[i].rank[1] == suffixes[i-1].rank[1])
            {
                prev_rank = suffixes[i].rank[0];
                suffixes[i].rank[0] = rank;
            }
            else // Otherwise increment rank and assign
            {
                prev_rank = suffixes[i].rank[0];
                suffixes[i].rank[0] = ++rank;
            }
            ind[suffixes[i].index] = i;
        }

        // Assign next rank to every suffix
        for (int i = 0; i < n; i++)
        {
            int nextindex = suffixes[i].index + k/2;
            suffixes[i].rank[1] = (nextindex < n)?
                                  suffixes[ind[nextindex]].rank[0]: -1;
        }

        // Sort the suffixes according to first k characters
        sort(suffixes, suffixes+n, cmp);
    }

    // Store indexes of all sorted suffixes in the suffix array
    vector<int>suffixArr;
    for (int i = 0; i < n; i++)
        suffixArr.push_back(suffixes[i].index);

    // Return the suffix array
    return  suffixArr;
}

/* To construct and return LCP */
vector<int> kasai(string txt, vector<int> suffixArr)
{
    int n = suffixArr.size();

    // To store LCP array
    vector<int> lcp(n, 0);

    // An auxiliary array to store inverse of suffix array
    // elements. For example if suffixArr[0] is 5, the
    // invSuff[5] would store 0.  This is used to get next
    // suffix string from suffix array.
    vector<int> invSuff(n, 0);

    // Fill values in invSuff[]
    for (int i=0; i < n; i++)
        invSuff[suffixArr[i]] = i;

    // Initialize length of previous LCP
    int k = 0;

    // Process all suffixes one by one starting from
    // first suffix in txt[]
    for (int i=0; i<n; i++)
    {
        /* If the current suffix is at n-1, then we don’t
           have next substring to consider. So lcp is not
           defined for this substring, we put zero. */
        if (invSuff[i] == n-1)
        {
            k = 0;
            continue;
        }

        /* j contains index of the next substring to
           be considered  to compare with the present
           substring, i.e., next string in suffix array */
        int j = suffixArr[invSuff[i]+1];

        // Directly start matching from k'th index as
        // at-least k-1 characters will match
        while (i+k<n && j+k<n && txt[i+k]==txt[j+k])
            k++;

        lcp[invSuff[i]] = k; // lcp for the present suffix.

        // Deleting the starting character from the string.
        if (k>0)
            k--;
    }

    // return the constructed lcp array
    return lcp;
}

// Utility function to print an array
void printArr(vector<int>arr, int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver program
int main()
{
    string str = "banana";

    vector<int>suffixArr = buildSuffixArray(str, str.length());
    int n = suffixArr.size();

    cout << "Suffix Array : \n";
    printArr(suffixArr, n);

    vector<int>lcp = kasai(str, suffixArr);

    cout << "\nLCP Array : \n";
    printArr(lcp, n);
    return 0;
}
```

**输出:**

```
Suffix Array : 
5 3 1 0 4 2 

LCP Array : 
1 3 0 0 2 0
```

插图:

```
txt[]     = "banana",  suffix[]  = {5, 3, 1, 0, 4, 2| 

Suffix array represents
{"a", "ana", "anana", "banana", "na", "nana"}

Inverse Suffix Array would be 
invSuff[] = {3, 2, 5, 1, 4, 0}
```

LCP 值按以下顺序评估
我们首先计算文本中第一个后缀为“**香蕉**的 LCP。我们需要后缀数组中的下一个后缀来计算 LCP(记住 lcp[i]定义为后缀[i]和后缀[i+1]的最长公共前缀)。**要在 suffixArr 中找到下一个后缀，我们使用 sufixar[]**。下一个后缀是“na”。由于“香蕉”和“na”之间没有共同的前缀，“香蕉”的 LCP 值为 0，在后缀数组中位于索引 3，因此我们将 **lcp[3]** 填充为 0。
接下来我们计算第二个后缀“ **anana** ”的 LCP。后缀数组中“anana”的下一个后缀是“banana”。由于没有公共前缀，所以“anana”的 LCP 值为 0，位于后缀数组的索引 2 处，因此我们将 **lcp[2]** 填充为 0。
接下来我们计算第三个后缀“**娜娜**”的 LCP。由于没有下一个后缀，所以没有定义“nana”的 LCP 值。我们将 **lcp[5]** 填充为 0。
文本中的下一个后缀是“ana”。后缀数组中“ **ana** ”的下一个后缀是“anana”。因为有一个长度为 3 的公共前缀，所以“ana”的 LCP 值为 3。我们将 **lcp[1]** 填充为 3。
现在我们 lcp 为文本中的下一个后缀“ **na** ”。这就是 Kasai 的算法使用 LCP 值必须至少为 2 的技巧的地方，因为以前的 LCP 值是 3。由于“na”后没有字符，LCP 的最终值为 2。我们将 **lcp[4]** 填充为 2。
文本中的下一个后缀是“ **a** ”。LCP 值必须至少为 1，因为以前的值为 2。由于“a”后没有字符，LCP 的最终值为 1。我们将 **lcp[0]** 填充为 1。
我们很快将讨论借助 LCP 数组实现搜索，以及 LCP 数组如何帮助将时间复杂度降低到 O(m + Log n)。

**参考文献:**
[【http://web.stanford.edu/class/cs97si/suffix-array.pdf】](http://web.stanford.edu/class/cs97si/suffix-array.pdf)
[http://www . mi . fu-Berlin . de/wiki/pub/ABI/rnaseqp 4/后缀-array . pdf](http://www.mi.fu-berlin.de/wiki/pub/ABI/RnaSeqP4/suffix-array.pdf)
[http://codeforces.com/blog/entry/12796](http://codeforces.com/blog/entry/12796)

本文由**普拉哈尔·阿格沃尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息