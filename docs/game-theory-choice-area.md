# 区域选择

> 原文:[https://www.geeksforgeeks.org/game-theory-choice-area/](https://www.geeksforgeeks.org/game-theory-choice-area/)

考虑一个游戏，其中你有两种类型的力量，A 和 B，有 3 种类型的区域 X，Y 和 z。每一秒你必须在这些区域之间切换，每个区域都有特定的属性，通过这些属性你的力量 A 和力量 B 增加或减少。我们需要不断选择区域，以使我们的生存时间最大化。当 A 或 B 中的任何一个力量小于 0 时，生存时间结束。
示例:

```
Initial value of Power A = 20        
Initial value of Power B = 8

Area X (3, 2) : If you step into Area X, 
                A increases by 3, 
                B increases by 2

Area Y (-5, -10) : If you step into Area Y, 
                   A decreases by 5, 
                   B decreases by 10

Area Z (-20, 5) : If you step into Area Z, 
                  A decreases by 20, 
                  B increases by 5

It is possible to choose any area in our first step.
We can survive at max 5 unit of time by following 
these choice of areas :
X -> Z -> X -> Y -> X

```

这个问题可以用递归来解决，在每个时间单位之后，我们可以去任何一个区域，但是我们会选择最终导致最大生存时间的那个区域。由于递归可以导致多次求解同一个子问题，我们将根据 A 和 B 的幂记住结果，如果我们达到相同的 A 和 B 的幂对，我们将不再求解它，而是取先前计算的结果。
下面给出的是上述方法的简单实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
//  C++ code to get maximum survival time
#include <bits/stdc++.h>
using namespace std;

//  structure to represent an area
struct area
{
    //  increment or decrement in A and B
    int a, b;
    area(int a, int b) : a(a), b(b)
    {}
};

//  Utility method to get maximum of 3 integers
int max(int a, int b, int c)
{
    return max(a, max(b, c));
}

//  Utility method to get maximum survival time
int maxSurvival(int A, int B, area X, area Y, area Z,
                int last, map<pair<int, int>, int>& memo)
{
    //  if any of A or B is less than 0, return 0
    if (A <= 0 || B <= 0)
        return 0;
    pair<int, int> cur = make_pair(A, B);

    //  if already calculated, return calculated value
    if (memo.find(cur) != memo.end())
        return memo[cur];

    int temp;

    //  step to areas on basis of last chose area
    switch(last)
    {
    case 1:
        temp = 1 + max(maxSurvival(A + Y.a, B + Y.b,
                                   X, Y, Z, 2, memo),
                       maxSurvival(A + Z.a, B + Z.b,
                                  X, Y, Z, 3, memo));
        break;
    case 2:
        temp = 1 + max(maxSurvival(A + X.a, B + X.b,
                                  X, Y, Z, 1, memo),
                       maxSurvival(A + Z.a, B + Z.b,
                                  X, Y, Z, 3, memo));
        break;
    case 3:
        temp = 1 + max(maxSurvival(A + X.a, B + X.b,
                                  X, Y, Z, 1, memo),
                       maxSurvival(A + Y.a, B + Y.b,
                                  X, Y, Z, 2, memo));
        break;
    }

    //  store the result into map
    memo[cur] = temp;

    return temp;
}

//  method returns maximum survival time
int getMaxSurvivalTime(int A, int B, area X, area Y, area Z)
{
    if (A <= 0 || B <= 0)
        return 0;
    map< pair<int, int>, int > memo;

    //  At first, we can step into any of the area
    return
        max(maxSurvival(A + X.a, B + X.b, X, Y, Z, 1, memo),
            maxSurvival(A + Y.a, B + Y.b, X, Y, Z, 2, memo),
            maxSurvival(A + Z.a, B + Z.b, X, Y, Z, 3, memo));
}

//  Driver code to test above method
int main()
{
    area X(3, 2);
    area Y(-5, -10);
    area Z(-20, 5);

    int A = 20;
    int B = 8;
    cout << getMaxSurvivalTime(A, B, X, Y, Z);

    return 0;
}
```

## 蟒蛇 3

```
# Python code to get maximum survival time

# Class to represent an area
class area:
    def __init__(self, a, b):
        self.a = a
        self.b = b

# Utility method to get maximum survival time
def maxSurvival(A, B, X, Y, Z, last, memo):
    # if any of A or B is less than 0, return 0
    if (A <= 0 or B <= 0):
        return 0
    cur = area(A, B)

    # if already calculated, return calculated value
    for ele in memo.keys():
        if (cur.a == ele.a and cur.b == ele.b):
            return memo[ele]

    # step to areas on basis of last chosen area
    if (last == 1):
        temp = 1 + max(maxSurvival(A + Y.a, B + Y.b,
                                   X, Y, Z, 2, memo),
                       maxSurvival(A + Z.a, B + Z.b,
                                   X, Y, Z, 3, memo))
    elif (last == 2):
        temp = 1 + max(maxSurvival(A + X.a, B + X.b,
                                   X, Y, Z, 1, memo),
               maxSurvival(A + Z.a, B + Z.b,
                   X, Y, Z, 3, memo))
    elif (last == 3):
        temp = 1 + max(maxSurvival(A + X.a, B + X.b,
                   X, Y, Z, 1, memo),
               maxSurvival(A + Y.a, B + Y.b,
                   X, Y, Z, 2, memo))

    # store the result into map
    memo[cur] = temp

    return temp

# method returns maximum survival time
def getMaxSurvivalTime(A, B, X, Y, Z):
    if (A <= 0 or B <= 0):
        return 0
    memo = dict()

    # At first, we can step into any of the area
    return max(maxSurvival(A + X.a, B + X.b, X, Y, Z, 1, memo),
           maxSurvival(A + Y.a, B + Y.b, X, Y, Z, 2, memo),
           maxSurvival(A + Z.a, B + Z.b, X, Y, Z, 3, memo))

# Driver code to test above method
X = area(3, 2)
Y = area(-5, -10)
Z = area(-20, 5)

A = 20
B = 8
print(getMaxSurvivalTime(A, B, X, Y, Z))

# This code is contributed by Soumen Ghosh.
```

Output:

```
5

```

本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。