# 平衡表达式，给定位置有左括号

> 原文:[https://www . geesforgeks . org/balanced-expressions-so-给定位置-有-开-括号/](https://www.geeksforgeeks.org/balanced-expressions-such-that-given-positions-have-opening-brackets/)

给定整数 n 和位置数组“位置[]”(1<= position[i] <= 2n), find the number of ways of proper bracket expressions that can be formed of length 2n such that given positions have opening bracket.
**)示例:**

```
Input : n = 3, position[] = [2}
Output : 3 
Explanation : 
The proper bracket sequences of length 6 and 
opening bracket at position 2 are:
[ [ ] ] [ ] 
[ [ [ ] ] ]
[ [ ] [ ] ]

Input : n = 2, position[] = {1, 3}
Output : 1
Explanation: The only possibility is:
[ ] [ ]
```

**进场:**这个问题可以通过 [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/) **解决。**。
设 **DP <sub>i，j</sub>** 为填充第一个 I 位置的有效方式数，使得类型为“[”的括号比类型为“]”的括号多 j 个。有效的方式意味着它是匹配括号表达式的前缀，并且强制“[”括号被强制的位置已经被满足。很容易看出 DP <sub>2N，0</sub> 就是最终答案。
DP 的基本情况是， **DP <sub>0，0</sub> =1。**我们需要在第一个位置填充一个“[”括号，只有一种方法可以做到。
如果位置**有一个可以用散列数组标记的左括号序列**，那么循环出现如下:

```
if(j != 0) dpi, j = dpi-1, j-1
else  dpi, j =  0; 
```

如果位置有**没有开括号顺序**，则**重复**发生如下:

```
if(j != 0) dpi, j = dpi - 1, j - 1 + dpi - 1, j + 1
 else  dpi, j = dpi - 1, j + 1
```

答案将是 **DP <sub>2n，0</sub>T3
下面给出的是上述方法的实现:** 

## C++

```
// CPP code to find number of ways of
// arranging bracket with proper expressions
#include <bits/stdc++.h>
using namespace std;

#define N 1000

// function to calculate the number
// of proper bracket sequence
long long arrangeBraces(int n, int pos[], int k)
{

    // hash array to mark the
    // positions of opening brackets
    bool h[N];

    // dp 2d array
    int dp[N][N];

    memset(h, 0, sizeof h);
    memset(dp, 0, sizeof dp);

    // mark positions in hash array
    for (int i = 0; i < k; i++)
        h[pos[i]] = 1;

    // first position marked as 1
    dp[0][0] = 1;

    // iterate and formulate the recurrences
    for (int i = 1; i <= 2 * n; i++) {
        for (int j = 0; j <= 2 * n; j++) {

            // if position has a opening bracket
            if (h[i]) {
                if (j != 0)
                    dp[i][j] = dp[i - 1][j - 1];
                else
                    dp[i][j] = 0;
            }
            else {
                if (j != 0)
                    dp[i][j] = dp[i - 1][j - 1] +
                               dp[i - 1][j + 1];
                else
                    dp[i][j] = dp[i - 1][j + 1];
            }
        }
    }

    // return answer
    return dp[2 * n][0];
}

// driver code
int main()
{
    int n = 3;

    // positions where opening braces
    // will be placed
    int pos[] = { 2 };
    int k = sizeof(pos)/sizeof(pos[0]);

    cout << arrangeBraces(n, pos, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find number of ways of
// arranging bracket with proper expressions

public class GFG {

    static final int N = 1000;

// function to calculate the number
// of proper bracket sequence
    static long arrangeBraces(int n, int pos[], int k) {

        // hash array to mark the
        // positions of opening brackets
        boolean h[] = new boolean[N];

        // dp 2d array
        int dp[][] = new int[N][N];

        // mark positions in hash array
        for (int i = 0; i < k; i++) {
            h[pos[i]] = true;
        }

        // first position marked as 1
        dp[0][0] = 1;

        // iterate and formulate the recurrences
        for (int i = 1; i <= 2 * n; i++) {
            for (int j = 0; j <= 2 * n; j++) {

                // if position has a opening bracket
                if (h[i]) {
                    if (j != 0) {
                        dp[i][j] = dp[i - 1][j - 1];
                    } else {
                        dp[i][j] = 0;
                    }
                } else if (j != 0) {
                    dp[i][j] = dp[i - 1][j - 1]
                            + dp[i - 1][j + 1];
                } else {
                    dp[i][j] = dp[i - 1][j + 1];
                }
            }
        }

        // return answer
        return dp[2 * n][0];
    }
// Driver code

    public static void main(String[] args) {
        int n = 3;

        // positions where opening braces
        // will be placed
        int pos[] = {2};
        int k = pos.length;
        System.out.print(arrangeBraces(n, pos, k));
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 code to find number of ways of
# arranging bracket with proper expressions
N = 1000

# function to calculate the number
# of proper bracket sequence
def arrangeBraces(n, pos, k):

    # hash array to mark the
    # positions of opening brackets
    h = [False for i in range(N)]

    # dp 2d array
    dp = [[0 for i in range(N)]
             for i in range(N)]

    # mark positions in hash array
    for i in range(k):
        h[pos[i]] = 1

    # first position marked as 1
    dp[0][0] = 1

    # iterate and formulate the recurrences
    for i in range(1, 2 * n + 1):
        for j in range(2 * n + 1):

            # if position has a opening bracket
            if (h[i]):
                if (j != 0):
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = 0
            else:
                if (j != 0):
                    dp[i][j] = (dp[i - 1][j - 1] +
                                dp[i - 1][j + 1])
                else:
                    dp[i][j] = dp[i - 1][j + 1]

    # return answer
    return dp[2 * n][0]

# Driver Code
n = 3

# positions where opening braces
# will be placed
pos = [ 2 ,];
k = len(pos)
print(arrangeBraces(n, pos, k))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# code to find number of ways of
// arranging bracket with proper expressions
using System;

class GFG
{
    static int N = 1000;

    // function to calculate the number
    // of proper bracket sequence
    public static long arrangeBraces(int n, int[] pos, int k)
    {

        // hash array to mark the
        // positions of opening brackets
        bool[] h = new bool[N];

        // dp 2d array
        int[,] dp = new int[N,N];

        for(int i = 0; i < N; i++)
            h[i] = false;

        for(int i = 0; i < N; i++)
            for(int j = 0; j < N; j++)
                dp[i,j] = 0;

        // mark positions in hash array
        for (int i = 0; i < k; i++)
            h[pos[i]] = true;

        // first position marked as 1
        dp[0,0] = 1;

        // iterate and formulate the recurrences
        for (int i = 1; i <= 2 * n; i++) {
            for (int j = 0; j <= 2 * n; j++) {

                // if position has a opening bracket
                if (h[i]) {
                    if (j != 0)
                        dp[i,j] = dp[i - 1,j - 1];
                    else
                        dp[i,j] = 0;
                }
                else {
                    if (j != 0)
                        dp[i,j] = dp[i - 1,j - 1] +
                                   dp[i - 1,j + 1];
                    else
                        dp[i,j] = dp[i - 1,j + 1];
                }
            }
        }

        // return answer
        return dp[2 * n,0];
    }

    // driver code
    static void Main()
    {
        int n = 3;

        // positions where opening braces
        // will be placed
        int[] pos = new int[]{ 2 };
        int k = pos.Length;

        Console.Write(arrangeBraces(n, pos, k));
    }
    //This code is contributed by DrRoot_
}
```

## java 描述语言

```
<script>
    // Javascript code to find number of ways of
    // arranging bracket with proper expressions

    let N = 1000;

    // function to calculate the number
    // of proper bracket sequence
    function arrangeBraces(n, pos, k) {

        // hash array to mark the
        // positions of opening brackets
        let h = new Array(N);
        h.fill(false);

        // dp 2d array
        let dp = new Array(N);
        for (let i = 0; i < N; i++)
        {
            dp[i] = new Array(N);
            for (let j = 0; j < N; j++)
            {
                dp[i][j] = 0;
            }
        }

        // mark positions in hash array
        for (let i = 0; i < k; i++) {
            h[pos[i]] = true;
        }

        // first position marked as 1
        dp[0][0] = 1;

        // iterate and formulate the recurrences
        for (let i = 1; i <= 2 * n; i++) {
            for (let j = 0; j <= 2 * n; j++) {

                // if position has a opening bracket
                if (h[i]) {
                    if (j != 0) {
                        dp[i][j] = dp[i - 1][j - 1];
                    } else {
                        dp[i][j] = 0;
                    }
                } else if (j != 0) {
                    dp[i][j] = dp[i - 1][j - 1]
                            + dp[i - 1][j + 1];
                } else {
                    dp[i][j] = dp[i - 1][j + 1];
                }
            }
        }

        // return answer
        return dp[2 * n][0];
    }

    let n = 3;

    // positions where opening braces
    // will be placed
    let pos = [2];
    let k = pos.length;
    document.write(arrangeBraces(n, pos, k));

</script>
```

**输出:**

```
3
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(n^2)