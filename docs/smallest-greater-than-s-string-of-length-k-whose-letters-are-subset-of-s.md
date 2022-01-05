# 长度为 K 的最小(大于 S)字符串，其字母是 S 的子集

> 原文:[https://www . geesforgeks . org/最小长度大于 s 的字符串-k-其字母是-s 的子集/](https://www.geeksforgeeks.org/smallest-greater-than-s-string-of-length-k-whose-letters-are-subset-of-s/)

给定一个由小写英文字母和一个整数 K 组成的长度为 N 的字符串 S，求长度为 K 的字典最小的字符串 T，使得它的字母集是字母集 S 的子集，并且 T 在字典上大于 S。*注意:字母集是一个集合，而不是多集合。例如，abadaba 的字母集是{a，b，d}。*

示例:

> 输入:S =“abc”，K = 3
> 输出:T =“aca”
> **解释**:长度为 3 的字符串 T 的列表，使得 T 的字母集是 S 的字母子集如下:“aaa”、“aab”、“aac”、“aba”、“abb”、“ABC”、“ACA”、“acb”、…。其中，字典序大于“abc”的有:
> “ACA”、“acb”、…。在这些词汇中，最小的是“aca”。
> 
> 输入:S =“ABC”，K = 2
> 输出:T =“AC”

一个**简单的解决方案**是一个接一个地按递增顺序尝试所有长度为 k 的字符串。对于每个字符串，检查它是否大于 S，如果是，则返回它。

下面是一个**高效的方法**来解决这个问题。

我们来考虑两种情况:
**1。如果 N < K** :对于这种情况，我们可以简单地将最多 N 个字符的字符串 S 复制到字符串 T，对于剩余的(K–N)个字符，我们可以将字符串 S 中的最小字符(最少 ASCII 值)追加到字符串 T(K–N)次，因为我们必须找到字典上最小的字符串，它刚好大于字符串 S

**2。如果 N ≥ K** :对于这种情况，我们需要将最多 K 个字符的字符串 S 复制到字符串 T，然后对于字符串 T，通过反向迭代，我们必须用某个字符替换所有这些字符，直到字符串 T 成为字典上大于字符串 S 的最小字符串。为此，我们可以执行以下操作:

1.  将字符串 S 的字符存储在一个 STL 集合中(当然，按照排序顺序)
2.  将字符串复制到最多 K 个字符的字符串中。
3.  反方向迭代，找到一个字符(让它在“p”位置被找到)，对于该字符，集合中存在一些 ASCII 值更大的字符。
4.  用集合中的字符替换此字符。
5.  将第(p + 1) <sup>个</sup>索引后的所有字符替换为第 K 个<sup>个</sup>索引。

**图解:**Let S =“bcegkmyy”，N = 10，K = 9。Set = { b，c，e，g，I，k，m，y }。将字符串复制到最多 K 个字符。然后以相反的方向迭代，我们首先有“y”，但是在集合中没有比“y”更大的字符，所以继续前进。我们又有了“y”，继续前进现在我们有了“m ”,在这个场景中有一个更大的字符“y”。将“m”替换为“y”，然后在向前的“m”之后，将所有字符替换为最小字符，即“b”。因此，字符串 T 变成了 T =“bcegkybb”；

```
/* CPP Program to find the lexicographically
   smallest string T greater than S whose
   letters are subset of letters of S */
#include <bits/stdc++.h>

using namespace std;

// function to find the lexicographically
// smallest string greater than S
string findString(string S, int N, int K)
{
    // stores minimum character
    char minChar = 'z';

    // stores unique characters of
    // string in sorted order
    set<char> found;

    // Loop through to find the minimum character
    // and stores characters in the set
    for (int i = 0; i < N; i++) {
        found.insert(S[i]);
        if (S[i] < minChar)
            minChar = S[i];
    }

    string T;

    // Case 1: If N < K
    if (N < K) {

        // copy the string S upto N characters
        T = S;

        // append minChar to make the remaining 
        // characters
        for (int i = 0; i < (K - N); i++)
            T += minChar;
    }

    // Case 2 :  If N >= K
    else {
        T = "";

        // copy the string S upto K characters
        for (int i = 0; i < K; i++)
            T += S[i];

        int i;

        // an iterator to the set
        set<char>::iterator it;

        // iterating in reverse direction
        for (i = K - 1; i >= 0; i--) {

            // find the current character in the set
            it = found.find(T[i]);

            // increment the iterator
            it++;

            // check if some bigger character exists in set
            if (it != found.end())
                break;
        }

        // Replace current character with that found in set
        T[i] = *it;

        // Replace all characters after with minChar
        for (int j = i + 1; j < K; j++)
            T[j] = minChar;
    }

    return T;
}

// Driver Code to test the above function
int main()
{
    string S = "abc";
    int N = S.length();

    // Length of required string
    int K = 3;

    string T = findString(S, N, K);
    cout << "Lexicographically Smallest String "
            "greater than " << S
         << " is " << T << endl;
    return 0;
}
```

**Output:**

```
Lexicographically Smallest String greater than abc is aca

```

时间复杂度: **O(N + K)** ，其中 N 为给定字符串的长度，K 为所需字符串的长度。