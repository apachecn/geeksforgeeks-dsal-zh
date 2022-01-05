# 使用位集的子集和查询

> 原文:[https://www . geesforgeks . org/subset-sum-query-using-bit set/](https://www.geeksforgeeks.org/subset-sum-queries-using-bitset/)

给定一个数组 **arr[]** 和多个查询，在每个查询中，我们必须检查数组中是否存在一个和给定数相等的子集。

示例:

```
Input : arr[]   = {1, 2, 3};
        query[] = {5, 3, 8}  
Output : Yes, Yes, No
There is a subset with sum 5, subset is {2, 3}
There is a subset with sum 3, subset is {1, 2}
There is no subset with sum 8.

Input : arr[] = {4, 1, 5};
        query[] = {7, 9}
Output : No, Yes
There is no subset with sum 7.
There is a subset with sum 9, subset is {4, 5}

```

想法是在 C++中使用[位集容器](https://www.geeksforgeeks.org/c-bitset-and-its-application)。利用比特集，我们可以在 O(n)中预先计算出数组中所有子集和的存在性，并在 O(1)中回答后续的查询。

我们基本上使用位数组**位[]** 来表示数组中元素的子集和。位[]的大小至少应为所有数组元素的总和加 1，以回答所有查询。如果 x 是给定数组的子集和，我们保留位[x]为 1，否则为假。请注意，索引假定从 0 开始。

```
For every element arr[i] of input array,
we do following

// bit[x] will be 1 if x is a subset
// sum of arr[], else 0
bit = bit | (bit << arr[i])
```

**这是怎么工作的？**

```
Let us consider arr[] = {3, 1, 5}, we need 
to whether a subset sum of x exists or not, 
where 0 ≤ x ≤ Σarri.

We create a bitset bit[10] and reset all the  
bits to 0, i.e., we make it 0000000000.

Set the 0th bit, because a subset sum of 0 
exists in every array.
Now, the bit array is 0000000001

Apply the above technique for all the elements
of the array :
Current bitset = 0000000001

After doing "bit = bit | (bit << 3)", 
bitset becomes    0000001001

After doing "bit | (bit << 1)", 
bitset becomes    0000011011

After doing "bit | (bit << 5)", 
bitset becomes    1101111011    

```

最后，我们将位数组设为 1101111011，因此，如果位[x]为 1，则 x 的子集和存在，否则不存在。我们可以清楚地观察到，除了 2 和 7 之外，从 0 到 9 的所有数字的子集和都存在于数组中。

下面是一个 C++实现:

```
// C++ program to answer subset sum queries using bitset
#include <bits/stdc++.h>
using namespace std;

// Maximum allowed query value
# define MAXSUM 10000

// function to check whether a subset sum equal to n
// exists in the array or not.
void processQueries(int query[], int nq, bitset<MAXSUM> bit)
{
    // One by one process subset sum queries
    for (int i=0; i<nq; i++)
    {
       int x = query[i];

       // If x is beyond size of bit[]
       if (x >= MAXSUM)
       {
           cout << "NA, ";
           continue;
       }

       // Else if x is a subset sum, then x'th bit
       // must be set
       bit[x]? cout << "Yes, " : cout << "No, ";
    }
}

// function to store all the subset sums in bit vector
void preprocess(bitset<MAXSUM> &bit, int arr[], int n)
{
    // set all the bits to 0
    bit.reset();

    // set the 0th bit because subset sum of 0 exists
    bit[0] = 1;

    // Process all array elements one by one
    for (int i = 0; i < n; ++i)

        // Do OR of following two
        // 1) All previous sums. We keep previous value
        //    of bit.
        // 2) arr[i] added to every previous sum. We
        //    move all previous indexes arr[i] ahead.
        bit |= (bit << arr[i]);
}

// Driver program
int main()
{
    int arr[] = {3, 1, 5};
    int query[] = {8, 7};

    int n  = sizeof(arr) / sizeof(arr[0]);
    int nq = sizeof(query) / sizeof(query[0]);

    // a vector of MAXSUM number of bits
    bitset<MAXSUM> bit;

    preprocess(bit, arr, n);
    processQueries(query, nq,  bit);

    return 0;
}
```

输出:

```
Yes, No, 

```

**时间复杂度** : O(n)为预计算，O(1)为后续查询，其中 n 为数组中的元素个数。

参考[http://stackoverflow . com/questions/12459563/c 位集大小是多少](http://stackoverflow.com/questions/12459563/what-is-the-size-of-bitset-in-c)了解该方法的空间要求。

本文由**阿维纳什库马尔锯**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。