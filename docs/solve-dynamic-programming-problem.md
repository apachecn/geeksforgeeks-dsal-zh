# 如何解决一个动态规划问题？

> 原文:[https://www . geesforgeks . org/solve-dynamic-programming-problem/](https://www.geeksforgeeks.org/solve-dynamic-programming-problem/)

动态编程是一种在多项式时间内解决某些特定类型问题的技术。动态规划解决方案比指数蛮力方法更快，并且很容易证明其正确性。在我们学习如何动态思考问题之前，我们需要学习:

1.  [重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)
2.  [最佳子结构属性](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/)

```
Steps to solve a DP
1) Identify if it is a DP problem
2) Decide a state expression with 
   least parameters
3) Formulate state relationship    
4) Do tabulation (or add memoization)
```

**<u>第一步:如何将一个问题归类为动态规划问题？</u>T3】**

*   通常，所有需要最大化或最小化某些量的问题，或者说在某些条件下计数排列的计数问题，或者某些概率问题，都可以通过使用动态规划来解决。
*   所有动态规划问题都满足重叠子问题的性质，大多数经典动态问题也满足最优子结构的性质。一旦我们在给定的问题中观察到这些属性，请确保它可以使用 DP 来解决。

**<u>第二步:决定状态</u>**
DP 问题都是关于状态及其过渡的。这是最基本的步骤，必须非常小心地完成，因为状态转换取决于您对状态定义的选择。那么，让我们看看术语“状态”是什么意思。

**状态**状态可以定义为能够唯一识别给定问题中某个位置或站位的一组参数。这组参数应该尽可能小，以减少状态空间。

例如:在我们著名的[背包问题](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)中，我们通过两个参数**指标**和**权重**来定义我们的状态，即 DP【指标】【权重】。这里 DP[指数][重量]告诉我们，它可以通过从 0 到指数范围内的项目获得最大利润，这些项目的容量为重量。因此，这里参数**索引**和**权重**一起可以唯一地识别背包问题的子问题。

因此，我们的第一步将是在确定问题是 DP 问题后，确定问题的状态。
众所周知，DP 就是用计算结果来表达最终结果。
所以，我们的下一步将是找到之前状态之间的关系，以达到当前状态。

**<u>第三步:制定各州之间的关系</u>**
这部分是解决 DP 问题最难的部分，需要大量的直觉、观察和实践。让我们通过考虑一个样例问题来理解它

```
Given 3 numbers {1, 3, 5}, we need to tell
the total number of ways we can form a number 'N' 
using the sum of the given three numbers.
(allowing repetitions and different arrangements).

Total number of ways to form 6 is: 8
1+1+1+1+1+1
1+1+1+3
1+1+3+1
1+3+1+1
3+1+1+1
3+3
1+5
5+1
```

让我们动态地思考这个问题。所以，首先，我们为给定的问题决定一个状态。我们将采用参数 n 来决定状态，因为它可以唯一地识别任何子问题。所以，我们的状态 dp 看起来像状态(n)。这里，state(n)表示通过使用{1，3，5}作为元素形成 n 的排列的总数。
现在，我们需要计算状态(n)。

**怎么做？**
所以直觉在这里发挥作用。因为我们只能用 1、3 或 5 组成一个给定的数。假设我们知道 n = 1，2，3，4，5，6 的结果；作为术语，让我们说我们知道
状态(n = 1)、状态(n = 2)、状态(n = 3) ……状态(n = 6)
的结果现在，我们希望知道状态(n = 7)的结果。看，我们只能加 1，3 和 5。现在我们可以通过以下 3 种方法得到 7 的总和:

**1)在状态(n = 6)**
的所有可能组合上加 1:Eg:【(1+1+1+1+1+1)+1】
【(1+1+1+3)+1】
【(1+1+3+1)+1】
【(1+3+1+1)+1】+1】
【(3+1+1+1)+1】+1】
[(3+3)+1]
【(1+1)】

**2)向所有可能的状态组合加 3(n = 4)；**
Eg:【(1+1+1+1)+3】
【(1+3)+3】
【(3+1)+3】

**3)在所有可能的状态组合(n = 2)** 上加 5
Eg:[(1+1)+5]

现在，仔细想一想，确信以上三种情况涵盖了所有可能的方式，形成 7 的总和；
因此，我们可以说结果为
状态(7) =状态(6) +状态(4) +状态(2)
或
状态(7) =状态(7-1) +状态(7-3) +状态(7-5)
一般来说，
T6】状态(n) =状态(n-1) +状态(n-3) +状态(n-5)
所以，我们的代码看起来会像:

## C++

```
// Returns the number of arrangements to
// form 'n'
int solve(int n)
{
   // base case
   if (n < 0)
      return 0;
   if (n == 0) 
      return 1; 

   return solve(n-1) + solve(n-3) + solve(n-5);
}   
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Returns the number of arrangements to
// form 'n'
static int solve(int n)
{
   // base case
   if (n < 0)
      return 0;
   if (n == 0) 
      return 1; 

   return solve(n-1) + solve(n-3) + solve(n-5);
}   

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Returns the number of arrangements to
# form 'n'
def solve(n):

  # Base case
  if n < 0:
    return 0
  if n == 0:
    return 1

  return (solve(n - 1) +
          solve(n - 3) +
          solve(n - 5))

# This code is contributed by GauriShankarBadola
```

## C#

```
// Returns the number of arrangements to
// form 'n'
static int solve(int n)
{
   // base case
   if (n < 0)
      return 0;
   if (n == 0) 
      return 1; 

   return solve(n-1) + solve(n-3) + solve(n-5);
}   

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Returns the number of arrangements to
// form 'n'

function solve(n)
{
   // base case
   if (n < 0)
      return 0;
   if (n == 0) 
      return 1; 

   return solve(n-1) + solve(n-3) + solve(n-5);
}   

// This Code is Contributed by Harshit Srivastava

</script>
```

上面的代码看起来是指数级的，因为它一次又一次地计算相同的状态。所以，我们只需要增加记忆。

**<u>第四步:为状态</u>**
添加记忆或列表这是动态规划解决方案中最简单的部分。我们只需要存储状态答案，以便下次需要该状态时，我们可以直接从内存中使用它

在上面的代码中添加记忆

## C++

```
// initialize to -1
int dp[MAXN];

// this function returns the number of
// arrangements to form 'n'
int solve(int n)
{
  // base case
  if (n < 0) 
      return 0;
  if (n == 0)
      return 1;

  // checking if already calculated
  if (dp[n]!=-1)
      return dp[n];

  // storing the result and returning
  return dp[n] = solve(n-1) + solve(n-3) + solve(n-5);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// initialize to -1
public static int[] dp = new int[MAXN];

// this function returns the number of
// arrangements to form 'n'
static int solve(int n)
{
  // base case
  if (n < 0) 
      return 0;
  if (n == 0)
      return 1;

  // checking if already calculated
  if (dp[n]!=-1)
      return dp[n];

  // storing the result and returning
  return dp[n] = solve(n-1) + solve(n-3) + solve(n-5);
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# This function returns the number of
# arrangements to form 'n'

# lookup dictionary/hashmap is initialized
def solve(n, lookup = {}):

    # Base cases
    # negative number can't be
    # produced, return 0
    if n < 0:
        return 0

    # 0 can be produced by not
    # taking any number whereas
    # 1 can be produced by just taking 1
    if n == 0:
        return 1

    # Checking if number of way for
    # producing n is already calculated
    # or not if calculated, return that,
    # otherwise calulcate and then return
    if n not in lookup:
        lookup[n] = (solve(n - 1) +
                     solve(n - 3) +
                     solve(n - 5))

    return lookup[n]

# This code is contributed by GauriShankarBadola
```

## C#

```
// initialize to -1
public static int[] dp = new int[MAXN];

// this function returns the number of
// arrangements to form 'n'
static int solve(int n)
{
  // base case
  if (n < 0) 
      return 0;
  if (n == 0)
      return 1;

  // checking if already calculated
  if (dp[n]!=-1)
      return dp[n];

  // storing the result and returning
  return dp[n] = solve(n-1) + solve(n-3) + solve(n-5);
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// initialize to -1
let dp = new Array(MAXN);

// this function returns the number of
// arrangements to form 'n'
function solve(n)
{

    // base case
  if (n < 0)
      return 0;
  if (n == 0)
      return 1;

  // checking if already calculated
  if (dp[n]!=-1)
      return dp[n];

  // storing the result and returning
  return dp[n] = solve(n-1) + solve(n-3) + solve(n-5);
}

// This code is contributed by avanitrachhadiya2155
</script>
```

另一种方法是添加制表，使解迭代。详情请参考[列表和记忆](https://www.geeksforgeeks.org/tabulation-vs-memoizatation/)。
动态规划伴随着大量的实践。必须尝试解决各种经典的差压问题，这些问题可以在[这里](https://www.geeksforgeeks.org/fundamentals-of-algorithms/#DynamicProgramming)找到。

您可以先检查以下问题，然后尝试使用上述步骤解决它们:-

*   [http://www.spoj.com/problems/COINS/](http://www.spoj.com/problems/COINS/)
*   [http://www.spoj.com/problems/ACODE/](http://www.spoj.com/problems/ACODE/)
*   [https://www . geesforgeks . org/dynamic-programming-set-6-min-cost-path/](https://www.geeksforgeeks.org/dynamic-programming-set-6-min-cost-path/)
*   [https://www . geesforgeks . org/dynamic-programming-subset-sum-problem/](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)
*   [https://www . geesforgeks . org/dynamic-programming-set-7-coin-change/](https://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)
*   [https://www . geesforgeks . org/dynamic-programming-set-5-edit-distance/](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)

本文由 [**尼提什·库马尔**](https://www.linkedin.com/in/nk17kumar/) 供稿。如果你喜欢极客博客并想投稿，你也可以用 write.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。