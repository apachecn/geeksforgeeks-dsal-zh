# 频率长度乘积最高的子串

> 原文:[https://www . geesforgeks . org/substring-最高频率-长度-product/](https://www.geeksforgeeks.org/substring-highest-frequency-length-product/)

给定一个包含较低字母字符的字符串，我们需要找出这个字符串的这样一个子字符串，它的长度和频率的乘积在所有可能的子字符串选择中是最大的。
示例:

```
Input : String str = “abddab”
Output : 6
All unique substring with product of their 
frequency and length are,
Val["a"] = 2 * 1 = 2  
Val["ab"] = 2 * 2 = 4
Val["abd"] = 1 * 3 = 3
Val["abdd"] = 1 * 4 = 4
Val["abdda"] = 1 * 5 = 5
Val["abddab"] = 1 * 6 = 6
Val["b"] = 2 * 1 = 2
Val["bd"] = 1 * 2 = 2
Val["bdd"] = 1 * 3 = 3
Val["bdda"] = 1 * 4 = 4
Val["bddab"] = 1 * 5 = 5
Val["d"] = 2 * 1 = 2
Val["da"] = 1 * 2 = 2
Val["dab"] = 1 * 3 = 3
Val["dd"] = 1 * 2 = 2
Val["dda"] = 1 * 3 = 3
Val["ddab"] = 1 * 4 = 4

Input  : String str = “zzzzzz”
Output : 12
In above string maximum value 12 can 
be obtained with substring “zzzz”
```

一个**简单的解决方案**就是逐个考虑所有子串。对于每个子字符串，计算它在整个字符串中出现的次数。
一个**高效的解决方案**通过首先构造[最长公共前缀](https://www.geeksforgeeks.org/longest-common-prefix-set-1-word-by-word-matching/)数组来解决这个问题，现在假设 lcp[i]的值是 K，那么我们可以说第 I 个和第(i+1)个后缀共有 K 个长度前缀，即有一个长度为 K 的子串重复了两次。同样，假设 lcp 的三个连续值是(K，K-2，K+1)，那么我们可以说有一个长度为(K-2)的子串在字符串中重复了三次。
现在经过上面的观察，我们可以看到我们的结果将是这样一个 lcp 数组的范围，它的最小元素乘以范围内的元素个数是最大的，因为范围将对应于字符串的频率，范围的最小元素将对应于重复字符串的长度，现在这个改造后的问题可以类似于直方图问题中的[最大矩形来解决。
在下面的代码中 lcp 数组是由](//www.geeksforgeeks.org/largest-rectangle-under-histogram/”) [Kasai 的算法](//www.geeksforgeeks.org/kasais-algorithm-for-construction-of-lcp-array-from-suffix-array/”)构造的。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find substring with highest
// frequency length product
#include <bits/stdc++.h>
using namespace std;

// Structure to store information of a suffix
struct suffix
{
    int index;  // To store original index
    int rank[2]; // To store ranks and next rank pair
};

// A comparison function used by sort() to compare
// two suffixes. Compares two pairs, returns 1 if
// first pair is smaller
int cmp(struct suffix a, struct suffix b)
{
    return (a.rank[0] == b.rank[0])?
           (a.rank[1] < b.rank[1] ?1: 0):
           (a.rank[0] < b.rank[0] ?1: 0);
}

// This is the main function that takes a string
// 'txt' of size n as an argument, builds and
// return the suffix array for the given string
vector<int> buildSuffixArray(string txt, int n)
{
    // A structure to store suffixes and their indexes
    struct suffix suffixes[n];

    // Store suffixes and their indexes in an array
    // of structures. The structure is needed to sort
    // the suffixes alphabetically and maintain their
    // old indexes while sorting
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
    // This array is needed to get the index in suffixes[]
    // from original index.  This mapping is needed to get
    // next suffix.
    int ind[n];
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
            // If first rank and next ranks are same as
            // that of previous suffix in array, assign
            // the same new rank to this suffix
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

//    method to get LCP array
vector<int> getLCPArray(string str)
{
    vector<int>suffixArr = buildSuffixArray(str, str.length());
    return kasai(str, suffixArr);
}

// The main function to find the maximum rectangular
// area under given histogram with n bars
int getMaxArea(int hist[], int n)
{
    // Create an empty stack. The stack holds indexes
    // of hist[] array. The bars stored in stack are
    // always in increasing order of their heights.
    stack<int> s;

    int max_area = 0; // Initialize max area
    int tp;  // To store top of stack

    // To store area with top bar as the smallest bar
    int area_with_top;

    // Run through all bars of given histogram
    int i = 0;
    while (i < n)
    {
        // If this bar is higher than the bar on
        // top stack, push it to stack
        if (s.empty() || hist[s.top()] <= hist[i])
            s.push(i++);

        // If this bar is lower than top of stack,
        // then calculate area of rectangle with
        // stack top as the smallest (or minimum
        // height) bar. 'i' is 'right index' for
        // the top and element before top in stack
        // is 'left index'
        else
        {
            tp = s.top();  // store the top index
            s.pop();  // pop the top

            // Calculate the area with hist[tp]
            // stack as smallest bar
            area_with_top = hist[tp] * (s.empty() ?
                           (i + 1) : i - s.top());

            // update max area, if needed
            if (max_area < area_with_top)
                max_area = area_with_top;
        }
    }

    // Now pop the remaining bars from stack
    // and calculate area with every
    // popped bar as the smallest bar
    while (s.empty() == false)
    {
        tp = s.top();
        s.pop();
        area_with_top = hist[tp] * (s.empty() ?
                        (i + 1) : i - s.top());

        if (max_area < area_with_top)
            max_area = area_with_top;
    }

    return max_area;
}

// Returns maximum product of frequency and length
// of a substring.
int maxProductOfFreqLength(string str)
{
    //    get LCP array by Kasai's algorithm
    vector<int> lcp = getLCPArray(str);

    int hist[lcp.size()];

    //    copy lcp array into hist array
    for (int i = 0; i < lcp.size(); i++)
        hist[i] = lcp[i];

    //    get the maximum area under lcp histogram
    int substrMaxValue = getMaxArea(hist, lcp.size());

    // if string length itself is greater than
    // histogram area, then return that
    if (str.length() > substrMaxValue)
        return str.length();
    else
        return substrMaxValue;
}

// Driver code to test above methods
int main()
{
    string str = "abddab";
    cout << maxProductOfFreqLength(str) << endl;
    return 0;
}
```

输出:

```
6
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。