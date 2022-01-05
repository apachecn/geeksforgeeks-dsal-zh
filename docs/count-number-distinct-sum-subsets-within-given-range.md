# 计算给定范围内不同和子集的数量

> 原文:[https://www . geesforgeks . org/count-number-distinct-sum-subset-in-给定范围/](https://www.geeksforgeeks.org/count-number-distinct-sum-subsets-within-given-range/)

给定一组由 N 个数字组成的 S 和由两个数字 L(下限)和 R(上限)指定的范围。求位于给定范围内的 S 的某个子集的所有可能和的不同值的数目。
示例:

```
Input : S = { 1, 2, 2, 3, 5 }, L = 1 and R = 5
Output : 5
Explanation :  Every number between 
1 and 5 can be made out using some subset of S.
{1 as 1, 2 as 2, 3 as 3, 4 as 2 + 2 and 5 as 5} 

Input : S = { 2, 3, 5 }, L = 1 and R = 7
Output : 4
Explanation :  Only 4 numbers between 
1 and 7 can be made out, i.e. {2, 3, 5, 7}. 
3 numbers which are {1, 4, 6} can't be made out in any way.
```

**先决条件:** [位集](https://www.geeksforgeeks.org/c-bitset-and-its-application/) | [位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)
**方法 1(简单):**一种天真的方法是生成给定集的所有可能子集，按子集方式计算它们的和，并将它们推送到散列表中。迭代整个给定的范围，计算 hashmap 中存在的数字。
**方法 2(高效):**解决这个问题的有效方法是使用大小为 10 <sup>5</sup> 的位组。通过左移位集并与前一位集按位“或”来更新每个元素 X 的位集，以便新的可能和的位集变为 1。然后使用**前缀和**的概念，预计算前缀[1]在 1 和 I 之间所需的数字计数..i]如果同时有多个查询被询问，则回答 O(1)中的每个查询。对于查询 L 和 R，答案只是**前缀【R】–前缀【L–1】**

> **对于例如** S = { 2，3，5 }，L = 1 和 R = 7
> 为了简单起见，考虑大小为 32 的位集。最初 1 位于位组
> 的第 0 <sub>个</sub>位置，00000000000000000000000000001
> 对于输入 2，将位组左移 2，并与先前的位组
> 进行“或”运算

**下面是上述方法在 C++中的实现:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP Program to count the number
// distinct values of sum of some
// subset in a range
#include <bits/stdc++.h>

using namespace std;

// Constant size for bitset
#define SZ 100001

int countOfpossibleNumbers(int S[], int N,
                           int L, int R)
{
    // Creating a bitset of size SZ
    bitset <SZ> BS;

    // Set 0th position to 1
    BS[0] = 1;

    // Build the bitset
    for (int i = 0; i < N; i++) {

        // Left shift the bitset for each
        // element and taking bitwise OR
        // with previous bitset
        BS = BS | (BS << S[i]);
    }

    int prefix[SZ];

    // Initializing the prefix array to zero
    memset(prefix, 0, sizeof(prefix));

    // Build the prefix array
    for (int i = 1; i < SZ; i++) {
        prefix[i] = prefix[i - 1] + BS[i];
    }

    // Answer the given query
    int ans = prefix[R] - prefix[L - 1];

    return ans;
}

// Driver Code to test above functions
int main()
{
    int S[] = { 1, 2, 3, 5, 7 };
    int N = sizeof(S) / sizeof(S[0]);

    int L = 1, R = 18;

    cout << countOfpossibleNumbers(S, N, L, R);

    return 0;
}
```

**Output:** 

```
18
```

**时间复杂度:** O(S*Z)，其中 S*Z 是给定约束的最大和，即 10 <sup>5</sup>