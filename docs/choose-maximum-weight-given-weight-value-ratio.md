# 选择给定重量和值比的最大重量

> 原文:[https://www . geesforgeks . org/choose-最大重量-给定重量-价值比/](https://www.geeksforgeeks.org/choose-maximum-weight-given-weight-value-ratio/)

给定 n 个项目的权重和值以及 K 个值。我们需要选择这些项目的子集，使得所选项目的权重和值之和的比率为 K，并且权重和值在所有可能的子集选择中最大。

```
Input : weight[] = [4, 8, 9]
        values[] = [2, 4, 6]
        K = 2
Output : 12
We can choose only first and second item only, 
because (4 + 8) / (2 + 4) = 2 which is equal to K
we can't include third item with weight 9 because 
then ratio condition won't be satisfied so result 
will be (4 + 8) = 12
```

我们可以用动态规划来解决这个问题。我们可以制作一个 2 状态 dp，其中 dp(i，j)将存储在给定条件下，当项目总数为 N 且所需比率为 k 时的最大可能权重总和。
现在在 dp 的两个状态中，我们将存储最后选择的项目以及权重总和与值总和之间的差值。我们将项目值乘以 K，这样 dp 的第二个状态将实际存储所选项目的(权重之和–K *(值之和))。现在我们可以看到，我们的答案将存储在 dp(N-1，0)中，因为最后一个项目是第(N-1)个，所以所有项目都在考虑之中，权重之和与 K*(值之和)之差为 0，这意味着权重之和与值之和的比值为 K。
定义上述 dp 状态后，我们可以简单地编写状态之间的转换，如下所示:

```
dp(last, diff) = max (dp(last - 1, diff),    
                 dp(last-1, diff + wt[last] - val[last]*K))

dp(last – 1, diff) represents the condition when current
                   item is not chosen and 
dp(last – 1, diff + wt[last] – val[last] * K)) represents 
the condition when current item is chosen so difference 
is updated with weight and value of current item.
```

在下面的代码中，自上而下的方法被用于解决这种动态编程，并且为了存储 dp 状态，使用了映射，因为差异也可以是负的，并且在这种情况下 2D 阵列会产生问题，需要特别小心。

## C++

```
// C++ program to choose item with maximum
// sum of weight under given constraint
#include <bits/stdc++.h>
using namespace std;

// memoized recursive method to return maximum
// weight with K as ratio of weight and values
int maxWeightRec(int wt[], int val[], int K,
                  map<pair<int, int>, int>& mp,
                            int last, int diff)
{
    //  base cases : if no item is remaining
    if (last == -1)
    {
        if (diff == 0)
            return 0;
        else
            return INT_MIN;
    }

    // first make pair with last chosen item and
    // difference between weight and values
    pair<int, int> tmp = make_pair(last, diff);
    if (mp.find(tmp) != mp.end())
        return mp[tmp];

    /*  choose maximum value from following two
        1) not selecting the current item and calling
           recursively
        2) selection current item, including the weight
           and updating the difference before calling
           recursively */
    mp[tmp] = max(maxWeightRec(wt, val, K, mp, last - 1, diff),
                   wt[last] + maxWeightRec(wt, val, K, mp,
                   last - 1, diff + wt[last] - val[last] * K));

    return mp[tmp];
}

// method returns maximum sum of weight with K
// as ration of sum of weight and their values
int maxWeight(int wt[], int val[], int K, int N)
{
    map<pair<int, int>, int> mp;
    return maxWeightRec(wt, val, K, mp, N - 1, 0);
}

//  Driver code to test above methods
int main()
{
    int wt[] = {4, 8, 9};
    int val[] = {2, 4, 6};
    int N = sizeof(wt) / sizeof(int);
    int K = 2;

    cout << maxWeight(wt, val, K, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to choose item with maximum
// sum of weight under given constraint

import java.awt.Point;
import java.util.HashMap;

class Test
{
    // memoized recursive method to return maximum
    // weight with K as ratio of weight and values
    static int maxWeightRec(int wt[], int val[], int K,
                      HashMap<Point, Integer> hm,
                                int last, int diff)
    {
        //  base cases : if no item is remaining
        if (last == -1)
        {
            if (diff == 0)
                return 0;
            else
                return Integer.MIN_VALUE;
        }

        // first make pair with last chosen item and
        // difference between weight and values
        Point tmp = new Point(last, diff);
        if (hm.containsKey(tmp))
            return hm.get(tmp);

        /*  choose maximum value from following two
            1) not selecting the current item and calling
               recursively
            2) selection current item, including the weight
               and updating the difference before calling
               recursively */
       hm.put(tmp,Math.max(maxWeightRec(wt, val, K, hm, last - 1, diff),
                       wt[last] + maxWeightRec(wt, val, K, hm,
                       last - 1, diff + wt[last] - val[last] * K)));

        return hm.get(tmp);
    }

    // method returns maximum sum of weight with K
    // as ration of sum of weight and their values
    static int maxWeight(int wt[], int val[], int K, int N)
    {
        HashMap<Point, Integer> hm = new HashMap<>();
        return maxWeightRec(wt, val, K, hm, N - 1, 0);
    }

    // Driver method
    public static void main(String args[])
    {
        int wt[] = {4, 8, 9};
        int val[] = {2, 4, 6};

        int K = 2;

        System.out.println(maxWeight(wt, val, K, wt.length));
    }
}
// This code is contributed by Gaurav Miglani
```

## 蟒蛇 3

```
# Python3 program to choose item with maximum
# sum of weight under given constraint
INT_MIN = -9999999999

def maxWeightRec(wt, val, K, mp, last, diff):

    # memoized recursive method to return maximum
    # weight with K as ratio of weight and values

    # base cases : if no item is remaining
    if last == -1:
        if diff == 0:
            return 0
        else:
            return INT_MIN

    # first make pair with last chosen item and
    # difference between weight and values
    tmp = (last, diff)
    if tmp in mp:
        return mp[tmp]

    # choose maximum value from following two
    # 1) not selecting the current item and
    #    calling recursively
    # 2) selection current item, including
    #    the weight and updating the difference
    #    before calling recursively

    mp[tmp] = max(maxWeightRec(wt, val, K, mp,
                               last - 1, diff), wt[last] +
                  maxWeightRec(wt, val, K, mp,
                               last - 1, diff +
                               wt[last] - val[last] * K))
    return mp[tmp]

def maxWeight(wt, val, K, N):

    # method returns maximum sum of weight with K
    # as ration of sum of weight and their values
    return maxWeightRec(wt, val, K, {}, N - 1, 0)

# Driver code
if __name__ == "__main__":
    wt = [4, 8, 9]
    val = [2, 4, 6]
    N = len(wt)
    K = 2
    print(maxWeight(wt, val, K, N))

# This code is contributed
# by vibhu4agarwal
```

**输出:**

```
12
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。