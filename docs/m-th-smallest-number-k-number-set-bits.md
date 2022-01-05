# 具有 k 个设置位的第 M 个最小数。

> 原文:[https://www . geesforgeks . org/m-th-最小数字-k-数字-集合位/](https://www.geeksforgeeks.org/m-th-smallest-number-k-number-set-bits/)

给定两个非负整数 **m** 和 **k** 。问题是找到具有设定位数 **k** 的**第 m 个**最小数。
**约束:** 1 < = m，k.
**示例:**

```
Input : m = 4, k = 2
Output : 9
(9)10 = (1001)2, it is the 4th smallest
number having 2 set bits.

Input : m = 6, k = 4
Output : 39
```

**进场:**以下为步骤:

1.  找到具有 **k** 组位数的最小数。顺其自然 **num** ，其中**num**=(1<<k)–1。
2.  循环 **m-1** 次，每次将**数**替换为比“数”高的下一个数，其位数与“数”中的位数相同。参考[这篇](https://www.geeksforgeeks.org/next-higher-number-with-same-number-of-set-bits/)帖子，找到需要的下一个更高的号码。
3.  最后返回 **num** 。

## C++

```
// C++ implementation to find the mth smallest
// number having k number of set bits
#include <bits/stdc++.h>
using namespace std;

typedef unsigned int uint_t;

// function to find the next higher number
// with same number of set bits as in 'x'
uint_t nxtHighWithNumOfSetBits(uint_t x)
{
    uint_t rightOne;
    uint_t nextHigherOneBit;
    uint_t rightOnesPattern;

    uint_t next = 0;

    /* the approach is same as discussed in
       https://www.geeksforgeeks.org/next-higher-number-with-same-number-of-set-bits/ 
    */
    if (x) {
        rightOne = x & -(signed)x;

        nextHigherOneBit = x + rightOne;

        rightOnesPattern = x ^ nextHigherOneBit;

        rightOnesPattern = (rightOnesPattern) / rightOne;

        rightOnesPattern >>= 2;

        next = nextHigherOneBit | rightOnesPattern;
    }

    return next;
}

// function to find the mth smallest number
// having k number of set bits
int mthSmallestWithKSetBits(uint_t m, uint_t k)
{
    // smallest number having 'k'
    // number of set bits
    uint_t num = (1 << k) - 1;

    // finding the mth smallest number
    // having k set bits
    for (int i = 1; i < m; i++)
        num = nxtHighWithNumOfSetBits(num);

    // required number
    return num;
}

// Driver program to test above
int main()
{
    uint_t m = 6, k = 4;
    cout << mthSmallestWithKSetBits(m, k);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation to find the mth
# smallest number having k number of set bits

# function to find the next higher number
# with same number of set bits as in 'x'
def nxtHighWithNumOfSetBits(x):
    rightOne = 0
    nextHigherOneBit = 0
    rightOnesPattern = 0

    next = 0

    """ the approach is same as discussed in
    http:#www.geeksforgeeks.org/next-higher-number-with-same-number-of-set-bits/
    """
    if (x):
        rightOne = x & (-x)
        nextHigherOneBit = x + rightOne

        rightOnesPattern = x ^ nextHigherOneBit

        rightOnesPattern = (rightOnesPattern) // rightOne

        rightOnesPattern >>= 2

        next = nextHigherOneBit | rightOnesPattern

    return next

# function to find the mth smallest
# number having k number of set bits
def mthSmallestWithKSetBits(m, k):

    # smallest number having 'k'
    # number of set bits
    num = (1 << k) - 1

    # finding the mth smallest number
    # having k set bits
    for i in range(1, m):
        num = nxtHighWithNumOfSetBits(num)

    # required number
    return num

# Driver Code
if __name__ == '__main__':
    m = 6
    k = 4
    print(mthSmallestWithKSetBits(m, k))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

**输出:**

```
39
```

**时间复杂度:** O(m)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。