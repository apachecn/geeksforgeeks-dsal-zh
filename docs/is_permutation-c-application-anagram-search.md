# 是 C++中的 _ 排列()及其在字谜搜索中的应用

> 原文:[https://www . geesforgeks . org/is _ arrange-c-application-anagram-search/](https://www.geeksforgeeks.org/is_permutation-c-application-anagram-search/)

is _ 置换()用于检查两个容器(如字符串和向量)是否相互置换。它接受三个参数，前两个参数是第一个对象的开始和结束位置，第三个参数是第二个对象的开始位置。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate working of
// is_permutation()
#include <bits/stdc++.h>
using namespace std;

// Driver program to test above
int main()
{
    vector<int> v1{1, 2, 3, 4};
    vector<int> v2{2, 3, 1, 4};

    // v1 and v2 are permutation of each other
    if (is_permutation(v1.begin(), v1.end(), v2.begin()))
        cout << "True\n";
    else
        cout << "False\n";

    // v1 and v3 are NOT permutation of each other
    vector<int> v3{5, 3, 1, 4};
    if (is_permutation(v1.begin(), v1.end(), v3.begin()))
        cout << "True\n";
    else
        cout << "False\n";

    return 0;
}
```

输出:

```
True
False
```

**应用:**
给定一个模式和一个文本，查找文本中模式及其字谜的所有出现。
示例:

```
Input : text ="forxxorfxdofr"  
        pat = "for"
Output :  3
There are three anagrams of "for"
int text.

Input : word = "aabaabaa" 
        text = "aaba"
Output : 4
```

我们已经讨论了一个解决方案。但是在这篇文章中，它是使用 is _ 置换()完成的。虽然复杂度高于[之前讨论的方法](https://www.geeksforgeeks.org/anagram-substring-search-search-permutations)，但目的是解释 is _ arrangement()的应用。
让待搜索图案的大小为 pat_len。这个想法是遍历给定的文本，对于 pat_len 大小的每个窗口，检查它是否是给定模式的排列。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count all permutation of
// given text
#include<bits/stdc++.h>
using namespace std;

// Function to count occurrences of anagrams of pat
int countAnagrams(string text, string pat)
{
    int t_len = text.length();
    int p_len = pat.length();

    // Start traversing the text
    int count = 0; // Initialize result
    for (int i=0; i<=t_len-p_len; i++)

        // Check if substring text[i..i+p_len]
        // is a permutation of pat[].
        // Three parameters are :
        // 1) Beginning position of current window in text
        // 2) End position of current window in text
        // 3) Pattern to be matched with current window
        if (is_permutation(text.begin()+i,
                           text.begin()+i+p_len,
                           pat.begin()))
            count++;

    return count;
}

// Driver code
int main()
{
    string str = "forxxorfxdofr";
    string pat = "for";
    cout << countAnagrams(str, pat) << endl;
    return 0;
}
```

输出:

```
3
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。