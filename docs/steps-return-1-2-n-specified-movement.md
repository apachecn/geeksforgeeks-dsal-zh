# 返回{1，2，..n}指定运动

> 原文:[https://www . geesforgeks . org/steps-return-1-2-n-specified-movement/](https://www.geeksforgeeks.org/steps-return-1-2-n-specified-movement/)

给定一个包含前 n 个自然数的置换的数组 moves[]，该数组的每个元素代表一个移动，即每个元素显示一个索引，该元素在每个步骤后的位置。现在按照这些步骤，我们需要告诉数组有多少步[1..n]返回[1..N]。步骤定义如下，一个步骤后，每个元素将被移动到移动数组索引定义的位置。
**例:**

```
Input  : moves[] = [4, 5, 1, 3, 2]
Output : 6
Explanation:
We need to consider an array of first 5 
natural numbers, i.e., arr[] = {1, 2, 3, 4, 5} as
size of moves[] is 5.
Now we one by one move elements of arr[] using 
given moves.
      moves[] = [4, 5, 1, 3, 2]
    arr[] = [1, 2, 3, 4, 5] 
In step 1, we move 1 to position 4, 2 to position
5, 3 to position 1, 4 to position 3 and 5 to 
position 2.
After step 1: arr[] = [3, 5, 4, 1, 2]
In step 2, we move 3 to position 4, 5 to position
5, 4 to position 1, 1 to position 3 and 2 to 
position 2
After step 2: arr[] = [4, 2, 1, 3, 5]
After step 3: arr[] = [1, 5, 3, 4, 2]
After step 4: arr[] = [3, 2, 4, 1, 5]
After step 5: arr[] = [4, 5, 1, 3, 2]
After step 6: arr[] = [1, 2, 3, 4, 5]
So we can reach to initial array in 6 steps, 
this is the minimum steps for reverting to 
the initial configuration of array.

Input  : moves[] = {3, 2, 1}
Output : 2
```

我们可以通过观察形成的序列中的模式来解决这个问题。一组特定的元素移动数组，形成一个循环。如上所述，移动数组示例[4，1，3]和[5，2]是两个这样的集合。这两个循环是独立的。

```
[4, 1, 3] causes [1, 3, 4] -> [3, 4, 1] -> [4, 1, 3] 
-> [1, 3, 4] -> [3, 4, 1] -> [4, 1, 3] -> [1, 3, 4]

[5, 2] causes [2, 5] -> [5, 2] -> [2, 5] -> [5, 2]
 -> [2, 5] -> [5, 2] -> [2, 5]
```

从上面的变化可以看出，长度为 3 的周期，需要 3 步才能达到相同的状态，长度为 2 的周期，需要 2 步才能达到相同的状态。一般来说，如果一个周期的长度为 N，那么经过 N 步之后，我们可以达到相同的状态。
现在，如果给定的移动数组只有一个周期，那么我们可以在移动次数等于数组中所有元素总数的情况下到达起始状态，但是如果它有 1 个以上的周期，那么它们都独立地移动它们的元素，并且它们都将在 x 个移动次数之后到达起始状态，其中 x 应该可以被所有周期长度整除，因为除以所有周期长度的最小 x 是它们的 LCM，我们仍然需要找到所有周期长度的 LCM。
循环长度可以通过逐个访问元素来找到，从我们将移动的任何元素开始，直到我们到达起始元素，我们将计算该过程中元素的数量，这将是相应的循环长度。

```
Below is example of cycles found for some moves arrays,
[2, 3, 1, 5, 4]     ->  [2, 3, 1] and [5, 4]
[1, 2, 3, 4, 5] ->  [1] [2] [3] [4] [5]
[2, 3, 4, 1, 5] ->  [2, 3, 4, 1] and [5]
```

唯一剩下的就是计算这些长度的 LCM，这可以很容易地用 GCD 计算出来。

## C++

```
// C++ program to get minimum steps to return to
// initial array with specified movement
#include <bits/stdc++.h>
using namespace std;

// Utility method to get lcm of a and b
int lcm(int a, int b)
{
    return (a * b) / __gcd(a, b);
}

// Method returns minimum number of steps to
// return to initial array
int getMinStepsToSort(int moves[], int N)
{
    // initially all cells are unvisited
    bool visit[N];
    memset(visit, false, sizeof(visit));

    // looping over all elements to get
    // various cycle
    int steps = 1;
    for (int i = 0; i < N; i++) {
        // if already visited, that means it
        // was a part of some cycle
        if (visit[i])
            continue;

        int cycleLen = 0;

        // Looping among cycle elements,  -1 is
        // for converting value to 0-index based
        for (int j = i; !visit[j]; j = moves[j] - 1) {
            cycleLen++;
            visit[j] = true;
        }

        // Take the lcm of current result and
        // new cycle length
        steps = lcm(steps, cycleLen);
    }
    return steps;
}

// Driver code to test above methods
int main()
{
    int moves[] = { 4, 5, 1, 3, 2 };
    int N = sizeof(moves) / sizeof(int);

    cout << getMinStepsToSort(moves, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get minimum steps to
// return to initial array with specified
// movement
import java.util.Arrays;

class GFG {

    // Recursive function to return gcd
    // of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);

        return __gcd(a, b - a);
    }

    // Utility method to get lcm of a and b
    static int lcm(int a, int b)
    {
        return (a * b) / __gcd(a, b);
    }

    // Method returns minimum number of steps
    // to return to initial array
    static int getMinStepsToSort(int moves[],
                                 int N)
    {

        // initially all cells are unvisited
        boolean visit[] = new boolean[N];
        Arrays.fill(visit, false);

        // looping over all elements to get
        // various cycle
        int steps = 1;
        for (int i = 0; i < N; i++) {

            // if already visited, that
            // means it was a part of some
            // cycle
            if (visit[i])
                continue;

            int cycleLen = 0;

            // Looping among cycle elements,
            // -1 is for converting value to
            // 0-index based
            for (int j = i; !visit[j];
                 j = moves[j] - 1) {

                cycleLen++;
                visit[j] = true;
            }

            // Take the lcm of current result
            // and new cycle length
            steps = lcm(steps, cycleLen);
        }

        return steps;
    }

    // Driver code
    public static void main(String arg[])
    {
        int moves[] = { 4, 5, 1, 3, 2 };
        int N = moves.length;

        System.out.print(getMinStepsToSort(
            moves, N));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to get
# minimum steps to return to
# initial array with
# specified movement

# Recursive function to
# return gcd of a and b
def  __gcd(a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return __gcd(a-b, b)
    return __gcd(a, b-a)

# Utility method to
# get lcm of a and b
def lcm(a, b):

    return (a * b) // __gcd(a, b)

# Method returns minimum
# number of steps to
# return to initial array
def getMinStepsToSort(moves, N):

    # initially all cells are unvisited
    visit =[False for i in range(N + 1)]

    # looping over all
    # elements to get
    # various cycle
    steps = 1
    for i in range(N):

        # if already visited,
        # that means it
        # was a part of some cycle
        if(visit[i]):
            continue

        cycleLen = 0

        # Looping among cycle
        # elements,  -1 is
        # for converting value
        # to 0-index based
        j = i
        while(not visit[j]):

            cycleLen+= 1
            visit[j] = True
            j = moves[j] - 1

        # Take the lcm of
        # current result and
        # new cycle length
        steps = lcm(steps, cycleLen)

    return steps

# Driver code

moves = [4, 5, 1, 3, 2]
N = len(moves)

print(getMinStepsToSort(moves, N))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to get minimum steps to return
// to initial array with specified movement
using System;

class GFG {

    // Recursive function to return gcd
    // of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);

        return __gcd(a, b - a);
    }

    // Utility method to get lcm of a and b
    static int lcm(int a, int b)
    {
        return (a * b) / __gcd(a, b);
    }

    // Method returns minimum number of steps
    // to return to initial array
    static int getMinStepsToSort(int[] moves,
                                       int N)
    {
        // initially all cells are unvisited
        bool[] visit = new bool[N];

        // looping over all elements to get
        // various cycle
        int steps = 1;
        for (int i = 0; i < N; i++) {

            // if already visited, that
            // means it was a part of some cycle
            if (visit[i])
                continue;

            int cycleLen = 0;

            // Looping among cycle elements,
            // -1 is for converting value to
            // 0-index based
            for (int j = i; !visit[j];
                j = moves[j] - 1) {

                cycleLen++;
                visit[j] = true;
            }

            // Take the lcm of current result
            // and new cycle length
            steps = lcm(steps, cycleLen);
        }

        return steps;
    }

    // Driver code
    public static void Main()
    {
        int[] moves = { 4, 5, 1, 3, 2 };
        int N = moves.Length;

        Console.WriteLine(getMinStepsToSort(moves, N));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
    // Javascript program to get minimum steps to return
    // to initial array with specified movement

    // Recursive function to return gcd
    // of a and b
    function __gcd(a, b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);

        return __gcd(a, b - a);
    }

    // Utility method to get lcm of a and b
    function lcm(a, b)
    {
        return parseInt((a * b) / __gcd(a, b), 10);
    }

    // Method returns minimum number of steps
    // to return to initial array
    function getMinStepsToSort(moves, N)
    {
        // initially all cells are unvisited
        let visit = new Array(N);
        visit.fill(false);

        // looping over all elements to get
        // various cycle
        let steps = 1;
        for (let i = 0; i < N; i++) {

            // if already visited, that
            // means it was a part of some cycle
            if (visit[i])
                continue;

            let cycleLen = 0;

            // Looping among cycle elements,
            // -1 is for converting value to
            // 0-index based
            for (let j = i; !visit[j]; j = moves[j] - 1) {

                cycleLen++;
                visit[j] = true;
            }

            // Take the lcm of current result
            // and new cycle length
            steps = lcm(steps, cycleLen);
        }

        return steps;
    }

    let moves = [ 4, 5, 1, 3, 2 ];
    let N = moves.length;

    document.write(getMinStepsToSort(moves, N));

</script>
```

输出:

```
6
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。