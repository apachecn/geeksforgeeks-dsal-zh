# 用给定数字的位数

得到第 k 个最小数字

> 原文:[https://www . geesforgeks . org/get-the-kth-最小数字-使用给定数字的位数/](https://www.geeksforgeeks.org/get-the-kth-smallest-number-using-the-digits-of-the-given-number/)

给定一个非负数 **n** 和一个值 **k** 。用给定数字 **n** 的数字找到能够形成的最小数字 **kth** 。保证能形成 **kth** 最小数。请注意，该数字可能非常大，甚至可能不适合 long long int。

示例:

```
Input : n = 1234, k = 2
Output : 1243

Input : n = 36012679802, k = 4
Output : 10022366897

```

其思想是先对数字进行排序，找出最小的数字，然后从最小的数字开始寻找第 k 个置换。为了对数字进行排序，我们使用频率计数技术，因为数字的数量很少。

```
// C++ implementation to get the kth smallest
// number using the digits of the given number
#include <bits/stdc++.h>
using namespace std;

// function to get the smallest digit in 'num'
// which is greater than 0
char getSmallDgtGreaterThanZero(string num, int n)
{
    // 's_dgt' to store the smallest digit
    // greater than 0
        char s_dgt = '9';

    for (int i=0; i<n; i++)
        if (num[i] < s_dgt && num[i] != '0')
            s_dgt = num[i];

    // required smallest digit in 'num'
    return s_dgt;
}

// function to get the kth smallest number
string kthSmallestNumber(string num, int k)
{
    // FIND SMALLEST POSSIBLE NUMBER BY SORTING
    // DIGITS

    // count frequency of each digit
    int freq[10];
    string final_num = "";

    memset(freq, 0, sizeof(freq));
    int n = num.size();

    // counting frequency of each digit
    for (int i = 0; i < n; i++)
        freq[num[i] - '0']++;

    // get the smallest digit greater than 0
    char s_dgt = getSmallDgtGreaterThanZero(num, n);    

    // add 's_dgt' to 'final_num'
    final_num += s_dgt;

    // reduce frequency of 's_dgt' by 1 in 'freq'
    freq[s_dgt - '0']--;

    // add each digit according to its frequency
    // to 'final_num'
    for (int i=0; i<10; i++)
        for (int j=1; j<=freq[i]; j++)
            final_num += (char)(i+48);    

    // FIND K-TH PERMUTATION OF SMALLEST NUMBER
    for (int i=1; i<k; i++)
      next_permutation(final_num.begin(), final_num.end());

    // required kth smallest number
    return final_num;
}

// Driver program to test above
int main()
{
    string num = "36012679802";
    int k = 4;
    cout << kthSmallestNumber(num, k);
    return 0;
}
```

输出:

```
10022366897

```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。