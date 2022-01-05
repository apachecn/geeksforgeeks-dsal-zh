# 生成长度为 n 的林登单词

> 原文:[https://www . geesforgeks . org/generating-Lyndon-word-of-length-n/](https://www.geeksforgeeks.org/generating-lyndon-words-of-length-n/)

给定一个整数 *n* 和一个字符数组 *S* ，任务是生成长度为 *n* 的[林登单词](https://en.wikipedia.org/wiki/Lyndon_word)，其字符来自 *S* 。

> 林登单词是一个严格来说少于字典顺序中所有旋转的字符串。例如，字符串“012”是林登单词，因为它小于它的旋转“120”和“201”，但是“102”不是林登单词，因为它大于它的旋转“021”。
> **注:**“000”不认为是林登词，因为它等于旋转得到的字符串。

**示例:**

> **输入:** n = 2，S = {0，1，2}
> **输出:** 01
> 02
> 12
> 长度为 2 的其他可能字符串为“00”、“11”、“20”、“21”和“22”。所有这些都大于或等于它们的一个旋转。
> 
> **输入:** n = 1，S = {0，1，2 }
> T3】输出: 0
> 1
> 2

**方法:**存在一种生成林登单词的有效方法，该方法由让-皮埃尔·杜瓦尔给出，可用于生成所有林登单词，时间长度 n 与这些单词的数量成比例。(有关证明，请参考 Berstel 等人的论文“[杜瓦尔生成林登单词的算法的平均成本”](http://www-igm.univ-mlv.fr/~berstel/Articles/1994AverageCostDuval.pdf))
该算法按照字典顺序生成林登单词。如果 *w* 是林登单词，则通过以下步骤获得下一个单词:

1.  重复 *w* 以形成长度为 *n* 的弦 *v* ，使得*v【I】= w【I mod | w |】*。
2.  而 *v* 的最后一个字符是 *S* 排序中的最后一个字符，将其删除。
3.  将 *v* 的最后一个字符替换为 s 排序顺序中的后继字符。

> 例如，如果 n = 5，S = {a，b，c，d}，w =“add”，那么我们得到 v =“addad”。
> 由于‘d’是 S 的排序顺序中的最后一个字符，我们去掉它得到“adda”
> 然后用它的后继‘b’替换最后一个‘a’得到 Lyndon 单词“addb”。

下面是上述方法的实现:

## C++

```
// C++ implementation of 
// the above approach 
#include<bits/stdc++.h>
using namespace std;

int main()
{
    int n = 2;
    char S[] = {'0', '1', '2' };
    int k = 3;
    sort(S, S + 3);

    // To store the indices 
    // of the characters 
    vector<int> w;
    w.push_back(-1);

    // Loop till w is not empty     
    while(w.size() > 0)
    {

        // Incrementing the last character
        w[w.size()-1]++;
        int m = w.size();
        if(m == n)
        {
            string str;
            for(int i = 0; i < w.size(); i++)
            {
                str += S[w[i]];
            }
            cout << str << endl;
        }

        // Repeating w to get a 
        // n-length string
        while(w.size() < n)
        {
            w.push_back(w[w.size() - m]);
        }

        // Removing the last character 
        // as long it is equal to 
        // the largest character in S 
        while(w.size() > 0 && w[w.size() - 1] == k - 1)
        {
            w.pop_back();
        }
    }
    return 0;
}

// This code is contributed by AdeshSingh1
```

## 蟒蛇 3

```
# Python implementation of
# the above approach

n = 2
S = ['0', '1', '2']
k = len(S)
S.sort()

# To store the indices
# of the characters
w = [-1]

# Loop till w is not empty
while w:

    # Incrementing the last character
    w[-1] += 1
    m = len(w)
    if m == n:
        print(''.join(S[i] for i in w))

    # Repeating w to get a
    # n-length string
    while len(w) < n:
        w.append(w[-m])

    # Removing the last character
    # as long it is equal to
    # the largest character in S
    while w and w[-1] == k - 1:
        w.pop()
```

**Output:**

```
01
02
12

```