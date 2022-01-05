# 检查是否所有人都可以在两台机器上投票

> 原文:[https://www . geesforgeks . org/check-people-can-vote-two-machines/](https://www.geeksforgeeks.org/check-people-can-vote-two-machines/)

有 **n** 个人和两台一模一样的投票机。我们还获得一个 n 大小的数组 **a[]** ，这样 **a[i]** 存储第一个人去任何机器、标记他的投票并返回所需的时间。在某个时刻，每台机器上只能有一个人。给定值 x，定义机器运行的最大允许时间，检查是否所有人都可以投票。

**示例:**

```
Input  : n = 3, x = 4
         a[] = {2, 4, 2}
Output: YES
There are  n = 3 persons say and maximum
allowed time is x = 4 units. Let the persons
be P0, P1, and P2 and two machines be M0 and M1.
At t0: P0 goes to M0
At t0: P2 goes to M1
At t2: M0 is free, p3 goes to M0
At t4: both M0 and M1 are free and all 3 have
        given their vote.
```

**方法 1**
让**之和**为 n 个人所用的总时间。如果总和< =x，那么答案显然会是 YES。否则我们需要检查给定数组是否可以拆分成两部分，使得第一部分和第二部分之和都小于或等于 x，问题类似于[背包](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)问题。想象两个背包，每个背包的容量为 x。现在找到，在任何一台机器上可以投票的最大人数，即找到容量为 x 的背包的最大子集和。让这个和为 s1。如果(sum-s1) < = x，那么答案是肯定的，否则答案是否定的。

## C++

```
// C++ program to check if all people can
// vote using two machines within limited
// time
#include<bits/stdc++.h>
using namespace std;

// Returns true if n people can vote using
// two machines in x time.
bool canVote(int a[], int n, int x)
{
    // dp[i][j] stores maximum possible number
    // of people among arr[0..i-1] can vote
    // in j time.
    int dp[n+1][x+1];
    memset(dp, 0, sizeof(dp));

    // Find sum of all times
    int sum = 0;
    for (int i=0; i<=n; i++ )
        sum += a[i];

    // Fill dp[][] in bottom up manner (Similar
    // to knapsack).
    for (int i=1; i<=n; i++)
        for (int j=1; j<=x; j++)
            if (a[i] <= j)
                dp[i][j] = max(dp[i-1][j],
                        a[i] + dp[i-1][j-a[i]]);
            else
                dp[i][j] = dp[i-1][j];

    // If remaining people can go to other machine.
    return (sum - dp[n][x] <= x);
}

// Driver code
int main()
{
    int n = 3, x = 4;
    int a[] = {2, 4, 2};
    canVote(a, n, x)? cout << "YES\n" :
                      cout << "NO\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if all people can
// vote using two machines within limited
// time
public class Main
{
    // Returns true if n people can vote using
    // two machines in x time.
    static boolean canVote(int[] a, int n, int x)
    {
        // dp[i][j] stores maximum possible number
        // of people among arr[0..i-1] can vote
        // in j time.
        int[][] dp = new int[n + 1][x + 1];
        for(int i = 0; i < n + 1; i++)
        {
            for(int j = 0; j < x + 1; j++)
            {
                dp[i][j] = 0;
            }
        }

        // Find sum of all times
        int sum = 0;
        for (int i = 0; i < n; i++ )
            sum += a[i];

        // Fill dp[][] in bottom up manner (Similar
        // to knapsack).
        for (int i = 1; i < n; i++)
            for (int j = 1; j <= x; j++)
                if (a[i] <= j)
                    dp[i][j] = Math.max(dp[i - 1][j], a[i] + dp[i - 1][j - a[i]]);
                else
                    dp[i][j] = dp[i - 1][j];

        // If remaining people can go to other machine.
        return (sum - dp[n][x] >= x);
    }

    public static void main(String[] args) {
        int n = 3, x = 4;
        int[] a = {2, 4, 2};
        if(canVote(a, n, x))
        {
            System.out.println("YES");
        }
        else{
            System.out.println("NO");
        }
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program to check if all people can
# vote using two machines within limited
# time

# Function returns true if n people can vote
# using two machines in x time.
def canVote(a, n, x):

    # dp[i][j] stores maximum possible number
    # of people among arr[0..i-1] can vote
    # in j time.
    dp = [[0] * (x + 1) for _ in range(n + 1)]
    a = a[:]
    a.append(0)

    # Find sum of all times
    sm = 0
    for i in range(n + 1):
        sm += a[i]

    # Fill dp[][] in bottom up manner
    # (Similar to knapsack).
    for i in range(1, n + 1):
        for j in range(1, x + 1):
            if a[i] <= j:
                dp[i][j] = max(dp[i - 1][j], a[i] +
                               dp[i - 1][j - a[i]])
            else:
                dp[i][j] = dp[i - 1][j]

    # If remaining people can go to other machine.
    return (sm - dp[n][x]) <= x

# Driver Code
if __name__ == "__main__":
    n = 3
    x = 4
    a = [2, 4, 2]
    print("YES" if canVote(a, n, x) else "NO")

# This code is contributed
# by vibhu4agarwal
```

## C#

```
// C# program to check if all people can
// vote using two machines within limited
// time
using System;
class GFG {

    // Returns true if n people can vote using
    // two machines in x time.
    static bool canVote(int[] a, int n, int x)
    {
        // dp[i][j] stores maximum possible number
        // of people among arr[0..i-1] can vote
        // in j time.
        int[,] dp = new int[n + 1, x + 1];
        for(int i = 0; i < n + 1; i++)
        {
            for(int j = 0; j < x + 1; j++)
            {
                dp[i, j] = 0;
            }
        }

        // Find sum of all times
        int sum = 0;
        for (int i = 0; i < n; i++ )
            sum += a[i];

        // Fill dp[][] in bottom up manner (Similar
        // to knapsack).
        for (int i = 1; i < n; i++)
            for (int j = 1; j <= x; j++)
                if (a[i] <= j)
                    dp[i, j] = Math.Max(dp[i - 1, j],
                            a[i] + dp[i - 1, j - a[i]]);
                else
                    dp[i, j] = dp[i - 1, j];

        // If remaining people can go to other machine.
        return (sum - dp[n, x] >= x);
    }

  // Driver code
  static void Main()
  {
    int n = 3, x = 4;
    int[] a = {2, 4, 2};
    if(canVote(a, n, x))
    {
        Console.Write("YES");
    }
    else{
        Console.Write("NO");
    }
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript program to check if all people can
    // vote using two machines within limited
    // time

    // Returns true if n people can vote using
    // two machines in x time.
    function canVote(a, n, x)
    {
        // dp[i][j] stores maximum possible number
        // of people among arr[0..i-1] can vote
        // in j time.
        let dp = new Array(n+1);
        for(let i = 0; i < n + 1; i++)
        {
            dp[i] = new Array(x + 1);
            for(let j = 0; j < x+1; j++)
            {
                dp[i][j] = 0;
            }
        }

        // Find sum of all times
        let sum = 0;
        for (let i=0; i<n; i++ )
            sum += a[i];

        // Fill dp[][] in bottom up manner (Similar
        // to knapsack).
        for (let i = 1; i <= n; i++)
            for (let j = 1; j <= x; j++)
                if (a[i] <= j)
                    dp[i][j] = Math.max(dp[i-1][j],
                            a[i] + dp[i-1][j-a[i]]);
                else
                    dp[i][j] = dp[i-1][j];

        // If remaining people can go to other machine.
        return (sum - dp[n][x] <= x);
    }

    let n = 3, x = 4;
    let a = [2, 4, 2];
    if(canVote(a, n, x))
    {
        document.write("YES");
    }
    else{
        document.write("NO");
    }

// This code is contributed by decode2207.
</script>
```

**输出:**

```
YES
```

**时间复杂度:**O(x * n)
T3】辅助空间: O(x * n)

本文由 **Ekta Goel** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

**方法二**
上面的方法使用了 O(x * n)个额外空间，这里我们给出一个使用 O(n)个额外空间的方法。
思路是对数组进行排序，然后检查我们是否能得到任意两个可以是子数组的数组，该子数组可以在数组的开始和结束之间，这样它的和小于或等于 x，剩余元素的和也小于 x。
我们为此使用前缀和。我们设置 I 和 j，并检查 I 到 j–1 之间的排序数组是否给出总和< = x，其余元素也是总和< = x。

## C++

```
// C++ program to check if all people can
// vote using two machines within limited
// time
#include<bits/stdc++.h>
using namespace std;

// Returns true if n people can vote using
// two machines in x time.
bool canVote(vector<int> a, int n, int x)
{
    // calculate total sum i.e total
    // time taken by all people
    int total_sum = 0;
    for(auto x : a){
        total_sum += x;
    }

    // if total time is less than x then
    // all people can definitely vote
    // hence return true
    if(total_sum <= x)
        return true;

    // sort the vector
    sort(a.begin(), a.end());

    // declare a vector presum of same size
    // as that of a and initialize it with 0
    vector<int> presum(a.size(), 0);

    // prefixsum for first element
    // will be element itself
    presum[0] = a[0];
    // fill the array
    for(int i = 1; i < presum.size(); i++){
        presum[i] = presum[i - 1] + a[i];
    }

    // Set i and j and check if array
    // from i to j - 1 gives sum <= x
    for(int i = 0; i < presum.size(); i++){
        for(int j = i + 1; j < presum.size(); j++){
            int arr1_sum = (presum[i] +
                           (total_sum - presum[j]));
            if((arr1_sum <= x) &&
                        (total_sum - arr1_sum) <= x)
                return true;
        }   
    }

    return false;
}

// Driver code
int main()
{
    int n = 3, x = 4;
    vector<int>a = {2, 4, 2};
    canVote(a, n, x)? cout << "YES\n" :
                      cout << "NO\n";
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to check if all people can
# vote using two machines within limited
# time

# Returns true if n people can vote using
# two machines in x time.
def canVote(a, n, x):

    # calculate total sum i.e total
    # time taken by all people
    total_sum = 0
    for i in range(len(a)):
        total_sum += a[i]

    # if total time is less than x then
    # all people can definitely vote
    # hence return true
    if(total_sum <= x):
        return True

    # sort the list
    a.sort()

    # declare a list presum of same size
    # as that of a and initialize it with 0
    presum = [0 for i in range(len(a))]

    # prefixsum for first element
    # will be element itself
    presum[0] = a[0]

    # fill the array
    for i in range(1, len(presum)):
        presum[i] = presum[i - 1] + a[i]

    # Set i and j and check if array
    # from i to j - 1 gives sum <= x
    for i in range(0, len(presum)):
        for j in range(i + 1, len(presum)):
            arr1_sum = (presum[i] + (total_sum - presum[j]))
            if((arr1_sum <= x) and
               (total_sum - arr1_sum) <= x):
                return True

    return False

# Driver code
n = 3
x = 4
a = [2, 4, 2]
if(canVote(a, n, x)):
    print("YES")
else:
    print("NO")

# This code is contributed by ashutosh450
```

**时间复杂度:**O(n * n)
T3】辅助空间: O(n)
如发现有不正确的地方请写评论，或者想分享以上讨论话题的更多信息。