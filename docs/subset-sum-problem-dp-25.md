# 子集和问题| DP-25

> 原文:[https://www.geeksforgeeks.org/subset-sum-problem-dp-25/](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)

给定一组非负整数和一个值*和*，确定给定集合中是否有一个子集的和等于给定的*和*。

**示例:**

```
Input: set[] = {3, 34, 4, 12, 5, 2}, sum = 9
Output: True  
There is a subset (4, 5) with sum 9.

Input: set[] = {3, 34, 4, 12, 5, 2}, sum = 30
Output: False
There is no subset that add up to 30.
```

**<u>方法 1</u> :** 递归。
**方法:**对于递归方法，我们将考虑两种情况。

1.  考虑最后一个元素，现在**所需的总和=目标总和–最后一个元素的值**和**元素的数量=元素总数–1**
2.  保留“最后”元素，现在**所需总和=目标总和**和**元素数量=元素总数–1**

下面是 isSubsetSum()问题的递归公式。

```
isSubsetSum(set, n, sum) 
= isSubsetSum(set, n-1, sum) || 
  isSubsetSum(set, n-1, sum-set[n-1])
Base Cases:
isSubsetSum(set, n, sum) = false, if sum > 0 and n == 0
isSubsetSum(set, n, sum) = true, if sum == 0 
```

让我们看一下上述方法的模拟:

```
set[]={3, 4, 5, 2}
sum=9
(x, y)= 'x' is the left number of elements,
'y' is the required sum

              (4, 9)
             {True}
           /        \  
        (3, 6)       (3, 9)

        /    \        /   \ 
     (2, 2)  (2, 6)   (2, 5)  (2, 9)
     {True}  
     /   \ 
  (1, -3) (1, 2)  
{False}  {True} 
         /    \
       (0, 0)  (0, 2)
       {True} {False}      
```

![](img/841186538988faa51bf78706560435b6.png)

## C++

```
// A recursive solution for subset sum problem
#include <iostream>
using namespace std;

// Returns true if there is a subset
// of set[] with sum equal to given sum
bool isSubsetSum(int set[], int n, int sum)
{

    // Base Cases
    if (sum == 0)
        return true;
    if (n == 0)
        return false;

    // If last element is greater than sum,
    // then ignore it
    if (set[n - 1] > sum)
        return isSubsetSum(set, n - 1, sum);

    /* else, check if sum can be obtained by any
of the following:
      (a) including the last element
      (b) excluding the last element   */
    return isSubsetSum(set, n - 1, sum)
           || isSubsetSum(set, n - 1, sum - set[n - 1]);
}

// Driver code
int main()
{
    int set[] = { 3, 34, 4, 12, 5, 2 };
    int sum = 9;
    int n = sizeof(set) / sizeof(set[0]);
    if (isSubsetSum(set, n, sum) == true)
         cout <<"Found a subset with given sum";
    else
        cout <<"No subset with given sum";
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// A recursive solution for subset sum problem
#include <stdio.h>

// Returns true if there is a subset
// of set[] with sum equal to given sum
bool isSubsetSum(int set[], int n, int sum)
{
    // Base Cases
    if (sum == 0)
        return true;
    if (n == 0)
        return false;

    // If last element is greater than sum,
    // then ignore it
    if (set[n - 1] > sum)
        return isSubsetSum(set, n - 1, sum);

    /* else, check if sum can be obtained by any
of the following:
      (a) including the last element
      (b) excluding the last element   */
    return isSubsetSum(set, n - 1, sum)
           || isSubsetSum(set, n - 1, sum - set[n - 1]);
}

// Driver code
int main()
{
    int set[] = { 3, 34, 4, 12, 5, 2 };
    int sum = 9;
    int n = sizeof(set) / sizeof(set[0]);
    if (isSubsetSum(set, n, sum) == true)
        printf("Found a subset with given sum");
    else
        printf("No subset with given sum");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive solution for subset sum
// problem
class GFG {

    // Returns true if there is a subset
    // of set[] with sum equal to given sum
    static boolean isSubsetSum(int set[],
                               int n, int sum)
    {
        // Base Cases
        if (sum == 0)
            return true;
        if (n == 0)
            return false;

        // If last element is greater than
        // sum, then ignore it
        if (set[n - 1] > sum)
            return isSubsetSum(set, n - 1, sum);

        /* else, check if sum can be obtained
        by any of the following
            (a) including the last element
            (b) excluding the last element */
        return isSubsetSum(set, n - 1, sum)
            || isSubsetSum(set, n - 1, sum - set[n - 1]);
    }

    /* Driver code */
    public static void main(String args[])
    {
        int set[] = { 3, 34, 4, 12, 5, 2 };
        int sum = 9;
        int n = set.length;
        if (isSubsetSum(set, n, sum) == true)
            System.out.println("Found a subset"
                               + " with given sum");
        else
            System.out.println("No subset with"
                               + " given sum");
    }
}

/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# A recursive solution for subset sum
# problem

# Returns true if there is a subset
# of set[] with sun equal to given sum

def isSubsetSum(set, n, sum):

    # Base Cases
    if (sum == 0):
        return True
    if (n == 0):
        return False

    # If last element is greater than
    # sum, then ignore it
    if (set[n - 1] > sum):
        return isSubsetSum(set, n - 1, sum)

    # else, check if sum can be obtained
    # by any of the following
    # (a) including the last element
    # (b) excluding the last element
    return isSubsetSum(
        set, n-1, sum) or isSubsetSum(
        set, n-1, sum-set[n-1])

# Driver code
set = [3, 34, 4, 12, 5, 2]
sum = 9
n = len(set)
if (isSubsetSum(set, n, sum) == True):
    print("Found a subset with given sum")
else:
    print("No subset with given sum")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A recursive solution for subset sum problem
using System;

class GFG {
    // Returns true if there is a subset of set[] with sum
    // equal to given sum
    static bool isSubsetSum(int[] set, int n, int sum)
    {
        // Base Cases
        if (sum == 0)
            return true;
        if (n == 0)
            return false;

        // If last element is greater than sum,
        // then ignore it
        if (set[n - 1] > sum)
            return isSubsetSum(set, n - 1, sum);

        /* else, check if sum can be obtained
        by any of the following
        (a) including the last element
        (b) excluding the last element */
        return isSubsetSum(set, n - 1, sum)
          || isSubsetSum(set, n - 1, sum - set[n - 1]);
    }

    // Driver code
    public static void Main()
    {
        int[] set = { 3, 34, 4, 12, 5, 2 };
        int sum = 9;
        int n = set.Length;
        if (isSubsetSum(set, n, sum) == true)
            Console.WriteLine("Found a subset with given sum");
        else
            Console.WriteLine("No subset with given sum");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A recursive solution for subset sum problem

// Returns true if there is a subset of set
// with sun equal to given sum
function isSubsetSum($set, $n, $sum)
{
    // Base Cases
    if ($sum == 0)
        return true;
    if ($n == 0)
        return false;

    // If last element is greater
    // than sum, then ignore it
    if ($set[$n - 1] > $sum)
        return isSubsetSum($set, $n - 1, $sum);

    /* else, check if sum can be
       obtained by any of the following
        (a) including the last element
        (b) excluding the last element */
    return isSubsetSum($set, $n - 1, $sum) ||
        isSubsetSum($set, $n - 1,
                    $sum - $set[$n - 1]);
}

// Driver Code
$set = array(3, 34, 4, 12, 5, 2);
$sum = 9;
$n = 6;

if (isSubsetSum($set, $n, $sum) == true)
    echo"Found a subset with given sum";
else
    echo "No subset with given sum";

// This code is contributed by Anuj_67
?>
```

## java 描述语言

```
<script>
    // A recursive solution for subset sum problem

    // Returns true if there is a subset of set[] with sum
    // equal to given sum
    function isSubsetSum(set, n, sum)
    {
        // Base Cases
        if (sum == 0)
            return true;
        if (n == 0)
            return false;

        // If last element is greater than sum,
        // then ignore it
        if (set[n - 1] > sum)
            return isSubsetSum(set, n - 1, sum);

        /* else, check if sum can be obtained
        by any of the following
        (a) including the last element
        (b) excluding the last element */
        return isSubsetSum(set, n - 1, sum)
          || isSubsetSum(set, n - 1, sum - set[n - 1]);
    }

    let set = [ 3, 34, 4, 12, 5, 2 ];
    let sum = 9;
    let n = set.length;
    if (isSubsetSum(set, n, sum) == true)
      document.write("Found a subset with given sum");
    else
      document.write("No subset with given sum");

    // This code is contributed by mukesh07.
</script>
```

**Output**

```
Found a subset with given sum
```

**复杂度分析:**以上解决方案在最坏的情况下可能会尝试给定集合的所有子集。因此，上述解决方案的时间复杂度是指数的。问题其实是 [NP-Complete](http://en.wikipedia.org/wiki/NP-complete) ( *这个问题*没有已知的多项式时间解。

**<u>方法二</u> :** 用动态规划解决[伪多项式时间](http://en.wikipedia.org/wiki/Pseudo-polynomial_time)的问题。
所以我们将创建一个大小为(arr.size() + 1) * (target + 1)的 2D 数组，类型为**布尔型**。如果存在来自 A[0]的元素子集，状态 DP[i][j]将为**真**。i]与**的和值= 'j '。**解决问题的方法是:

```
if (A[i-1] > j)
DP[i][j] = DP[i-1][j]
else 
DP[i][j] = DP[i-1][j] OR DP[i-1][j-A[i-1]]
```

1.  这意味着，如果当前元素的值大于“当前总和值”，我们将复制以前案例的答案
2.  如果当前的和值大于“ith”元素，我们将看到是否有任何先前的状态已经经历了**和=“j”或者任何先前的状态经历了值“j–A[I]”**，这将解决我们的目的。

下面的模拟将阐明上述方法:

```
set[]={3, 4, 5, 2}
target=6

    0    1    2    3    4    5    6

0   T    F    F    F    F    F    F

3   T    F    F    T    F    F    F

4   T    F    F    T    T    F    F   

5   T    F    F    T    T    T    F

2   T    F    T    T    T    T    T
```

下面是上述方法的实现:

## C

```
// A Dynamic Programming solution
// for subset sum problem
#include <stdio.h>

// Returns true if there is a subset of set[]
// with sum equal to given sum
bool isSubsetSum(int set[], int n, int sum)
{
    // The value of subset[i][j] will be true if
    // there is a subset of set[0..j-1] with sum
    // equal to i
    bool subset[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for (int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            if (j < set[i - 1])
                subset[i][j] = subset[i - 1][j];
            if (j >= set[i - 1])
                subset[i][j] = subset[i - 1][j]
                               || subset[i - 1][j - set[i - 1]];
        }
    }

    /*   // uncomment this code to print table
     for (int i = 0; i <= n; i++)
     {
       for (int j = 0; j <= sum; j++)
          printf ("%4d", subset[i][j]);
       printf("\n");
     }*/

    return subset[n][sum];
}

// Driver code
int main()
{
    int set[] = { 3, 34, 4, 12, 5, 2 };
    int sum = 9;
    int n = sizeof(set) / sizeof(set[0]);
    if (isSubsetSum(set, n, sum) == true)
        printf("Found a subset with given sum");
    else
        printf("No subset with given sum");
    return 0;
}
// This code is contributed by Arjun Tyagi.
```

## C++

```
// A Dynamic Programming solution
// for subset sum problem
#include <iostream>
using namespace std;

// Returns true if there is a subset of set[]
// with sum equal to given sum
bool isSubsetSum(int set[], int n, int sum)
{
    // The value of subset[i][j] will be true if
    // there is a subset of set[0..j-1] with sum
    // equal to i
    bool subset[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for (int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            if (j < set[i - 1])
                subset[i][j] = subset[i - 1][j];
            if (j >= set[i - 1])
                subset[i][j] = subset[i - 1][j]
                               || subset[i - 1][j - set[i - 1]];
        }
    }

    /*   // uncomment this code to print table
     for (int i = 0; i <= n; i++)
     {
       for (int j = 0; j <= sum; j++)
          printf ("%4d", subset[i][j]);
       cout <<"\n";
     }*/

    return subset[n][sum];
}

// Driver code
int main()
{
    int set[] = { 3, 34, 4, 12, 5, 2 };
    int sum = 9;
    int n = sizeof(set) / sizeof(set[0]);
    if (isSubsetSum(set, n, sum) == true)
        cout <<"Found a subset with given sum";
    else
        cout <<"No subset with given sum";
    return 0;
}
// This code is contributed by shivanisinghss2110
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming solution for subset
// sum problem
class GFG {

    // Returns true if there is a subset of
    // set[] with sum equal to given sum
    static boolean isSubsetSum(int set[],
                               int n, int sum)
    {
        // The value of subset[i][j] will be
        // true if there is a subset of
        // set[0..j-1] with sum equal to i
        boolean subset[][] = new boolean[sum + 1][n + 1];

        // If sum is 0, then answer is true
        for (int i = 0; i <= n; i++)
            subset[0][i] = true;

        // If sum is not 0 and set is empty,
        // then answer is false
        for (int i = 1; i <= sum; i++)
            subset[i][0] = false;

        // Fill the subset table in bottom
        // up manner
        for (int i = 1; i <= sum; i++) {
            for (int j = 1; j <= n; j++) {
                subset[i][j] = subset[i][j - 1];
                if (i >= set[j - 1])
                    subset[i][j] = subset[i][j]
                                   || subset[i - set[j - 1]][j - 1];
            }
        }

        /* // uncomment this code to print table
        for (int i = 0; i <= sum; i++)
        {
        for (int j = 0; j <= n; j++)
            System.out.println (subset[i][j]);
        } */

        return subset[sum][n];
    }

    /* Driver code*/
    public static void main(String args[])
    {
        int set[] = { 3, 34, 4, 12, 5, 2 };
        int sum = 9;
        int n = set.length;
        if (isSubsetSum(set, n, sum) == true)
            System.out.println("Found a subset"
                               + " with given sum");
        else
            System.out.println("No subset with"
                               + " given sum");
    }
}

/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# A Dynamic Programming solution for subset
# sum problem Returns true if there is a subset of
# set[] with sun equal to given sum

# Returns true if there is a subset of set[]
# with sum equal to given sum
def isSubsetSum(set, n, sum):

    # The value of subset[i][j] will be
    # true if there is a
    # subset of set[0..j-1] with sum equal to i
    subset =([[False for i in range(sum + 1)]
            for i in range(n + 1)])

    # If sum is 0, then answer is true
    for i in range(n + 1):
        subset[i][0] = True

    # If sum is not 0 and set is empty,
    # then answer is false
    for i in range(1, sum + 1):
         subset[0][i]= False

    # Fill the subset table in bottom up manner
    for i in range(1, n + 1):
        for j in range(1, sum + 1):
            if j<set[i-1]:
                subset[i][j] = subset[i-1][j]
            if j>= set[i-1]:
                subset[i][j] = (subset[i-1][j] or
                                subset[i - 1][j-set[i-1]])

    # uncomment this code to print table
    # for i in range(n + 1):
    # for j in range(sum + 1):
    # print (subset[i][j], end =" ")
    # print()
    return subset[n][sum]

# Driver code
if __name__=='__main__':
    set = [3, 34, 4, 12, 5, 2]
    sum = 9
    n = len(set)
    if (isSubsetSum(set, n, sum) == True):
        print("Found a subset with given sum")
    else:
        print("No subset with given sum")

# This code is contributed by
# sahil shelangia.
```

## C#

```
// A Dynamic Programming solution for
// subset sum problem
using System;

class GFG {
    // Returns true if there is a subset
    // of set[] with sum equal to given sum
    static bool isSubsetSum(int[] set, int n, int sum)
    {
        // The value of subset[i][j] will be true if there
        // is a subset of set[0..j-1] with sum equal to i
        bool[, ] subset = new bool[sum + 1, n + 1];

        // If sum is 0, then answer is true
        for (int i = 0; i <= n; i++)
            subset[0, i] = true;

        // If sum is not 0 and set is empty,
        // then answer is false
        for (int i = 1; i <= sum; i++)
            subset[i, 0] = false;

        // Fill the subset table in bottom up manner
        for (int i = 1; i <= sum; i++) {
            for (int j = 1; j <= n; j++) {
                subset[i, j] = subset[i, j - 1];
                if (i >= set[j - 1])
                    subset[i, j] = subset[i, j]
                                   || subset[i - set[j - 1], j - 1];
            }
        }

        return subset[sum, n];
    }

    // Driver code
    public static void Main()
    {
        int[] set = { 3, 34, 4, 12, 5, 2 };
        int sum = 9;
        int n = set.Length;
        if (isSubsetSum(set, n, sum) == true)
            Console.WriteLine("Found a subset with given sum");
        else
            Console.WriteLine("No subset with given sum");
    }
}
// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming solution for
// subset sum problem

// Returns true if there is a subset of
// set[] with sum equal to given sum
function isSubsetSum( $set, $n, $sum)
{
    // The value of subset[i][j] will
    // be true if there is a subset of
    // set[0..j-1] with sum equal to i
    $subset = array(array());

    // If sum is 0, then answer is true
    for ( $i = 0; $i <= $n; $i++)
        $subset[$i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for ( $i = 1; $i <= $sum; $i++)
        $subset[0][$i] = false;

    // Fill the subset table in bottom
    // up manner
    for ($i = 1; $i <= $n; $i++)
    {
        for ($j = 1; $j <= $sum; $j++)
        {
            if($j < $set[$i-1])
                $subset[$i][$j] =
                      $subset[$i-1][$j];
            if ($j >= $set[$i-1])
                $subset[$i][$j] =
                       $subset[$i-1][$j] ||
                       $subset[$i - 1][$j -
                               $set[$i-1]];
        }
    }

    /* // uncomment this code to print table
    for (int i = 0; i <= n; i++)
    {
    for (int j = 0; j <= sum; j++)
        printf ("%4d", subset[i][j]);
    printf("n");
    }*/

    return $subset[$n][$sum];
}

// Driver code
$set = array(3, 34, 4, 12, 5, 2);
$sum = 9;
$n = count($set);

if (isSubsetSum($set, $n, $sum) == true)
    echo "Found a subset with given sum";
else
    echo "No subset with given sum";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // A Dynamic Programming solution for subset sum problem

    // Returns true if there is a subset of
    // set[] with sum equal to given sum
    function isSubsetSum(set, n, sum)
    {
        // The value of subset[i][j] will be
        // true if there is a subset of
        // set[0..j-1] with sum equal to i
        let subset = new Array(sum + 1);

        for(let i = 0; i < sum + 1; i++)
        {
            subset[i] = new Array(sum + 1);
            for(let j = 0; j < n + 1; j++)
            {
                subset[i][j] = 0;
            }
        }

        // If sum is 0, then answer is true
        for (let i = 0; i <= n; i++)
            subset[0][i] = true;

        // If sum is not 0 and set is empty,
        // then answer is false
        for (let i = 1; i <= sum; i++)
            subset[i][0] = false;

        // Fill the subset table in bottom
        // up manner
        for (let i = 1; i <= sum; i++) {
            for (let j = 1; j <= n; j++) {
                subset[i][j] = subset[i][j - 1];
                if (i >= set[j - 1])
                    subset[i][j] = subset[i][j]
                                   || subset[i - set[j - 1]][j - 1];
            }
        }

        /* // uncomment this code to print table
        for (int i = 0; i <= sum; i++)
        {
        for (int j = 0; j <= n; j++)
            System.out.println (subset[i][j]);
        } */

        return subset[sum][n];
    }

    let set = [ 3, 34, 4, 12, 5, 2 ];
    let sum = 9;
    let n = set.length;
    if (isSubsetSum(set, n, sum) == true)
      document.write("Found a subset" + " with given sum");
    else
      document.write("No subset with" + " given sum");

    // This code is contributed by decode2207.
</script>
```

**Output**

```
Found a subset with given sum
```

**求子集和的记忆技术:**

方法:

1.  在这种方法中，我们也遵循递归方法，但是在这种方法中，我们使用另一个二维矩阵，其中我们首先用-1 或任何负值初始化。
2.  在这种方法中，我们避免了一些重复的递归调用，这就是为什么我们使用二维矩阵。在这个矩阵中，我们存储了前一个调用值的值。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Taking the matrix as globally
int tab[2000][2000];

// Check if possible subset with
// given sum is possible or not
int subsetSum(int a[], int n, int sum)
{

    // If the sum is zero it means
    // we got our expected sum
    if (sum == 0)
        return 1;

    if (n <= 0)
        return 0;

    // If the value is not -1 it means it
    // already call the function
    // with the same value.
    // it will save our from the repetition.
    if (tab[n - 1][sum] != -1)
        return tab[n - 1][sum];

    // if the value of a[n-1] is
    // greater than the sum.
    // we call for the next value
    if (a[n - 1] > sum)
        return tab[n - 1][sum] = subsetSum(a, n - 1, sum);
    else
    {

        // Here we do two calls because we
        // don't know which value is
        // full-fill our criteria
        // that's why we doing two calls
        return tab[n - 1][sum] = subsetSum(a, n - 1, sum) ||
                       subsetSum(a, n - 1, sum - a[n - 1]);
    }
}

// Driver Code
int main()
{
    // Storing the value -1 to the matrix
    memset(tab, -1, sizeof(tab));
    int n = 5;
    int a[] = {1, 5, 3, 7, 4};
    int sum = 12;

    if (subsetSum(a, n, sum))
    {
        cout << "YES" << endl;
    }
    else
        cout << "NO" << endl;

    /* This Code is Contributed by Ankit Kumar*/
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Check if possible subset with
    // given sum is possible or not
    static int subsetSum(int a[], int n, int sum)
    {
        // Storing the value -1 to the matrix
        int tab[][] = new int[n + 1][sum + 1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                tab[i][j] = -1;
            }
        }

        // If the sum is zero it means
        // we got our expected sum
        if (sum == 0)
            return 1;

        if (n <= 0)
            return 0;

        // If the value is not -1 it means it
        // already call the function
        // with the same value.
        // it will save our from the repetition.
        if (tab[n - 1][sum] != -1)
            return tab[n - 1][sum];

        // if the value of a[n-1] is
        // greater than the sum.
        // we call for the next value
        if (a[n - 1] > sum)
            return tab[n - 1][sum]
                = subsetSum(a, n - 1, sum);
        else {

            // Here we do two calls because we
            // don't know which value is
            // full-fill our criteria
            // that's why we doing two calls
            if (subsetSum(a, n - 1, sum) != 0
                || subsetSum(a, n - 1, sum - a[n - 1])
                       != 0) {
                return tab[n - 1][sum] = 1;
            }
            else
                return tab[n - 1][sum] = 0;
        }
    }

      // Driver Code
    public static void main(String[] args)
    {

        int n = 5;
        int a[] = { 1, 5, 3, 7, 4 };
        int sum = 12;

        if (subsetSum(a, n, sum) != 0) {
            System.out.println("YES\n");
        }
        else
            System.out.println("NO\n");
    }
}

// This code is contributed by rajsanghavi9.
```

## 蟒蛇 3

```
# Python program for the above approach

# Taking the matrix as globally
tab = [[-1 for i in range(2000)] for j in range(2000)]

# Check if possible subset with
# given sum is possible or not
def subsetSum(a, n, sum):

    # If the sum is zero it means
    # we got our expected sum
    if (sum == 0):
        return 1

    if (n <= 0):
        return 0

    # If the value is not -1 it means it
    # already call the function
    # with the same value.
    # it will save our from the repetition.
    if (tab[n - 1][sum] != -1):
        return tab[n - 1][sum]

    # if the value of a[n-1] is
    # greater than the sum.
    # we call for the next value
    if (a[n - 1] > sum):
        tab[n - 1][sum] = subsetSum(a, n - 1, sum)
        return tab[n - 1][sum]
    else:

        # Here we do two calls because we
        # don't know which value is
        # full-fill our criteria
        # that's why we doing two calls
        tab[n - 1][sum] = subsetSum(a, n - 1, sum)
        return tab[n - 1][sum] or subsetSum(a, n - 1, sum - a[n - 1])

# Driver Code

n = 5
a = [1, 5, 3, 7, 4]
sum = 12

if (subsetSum(a, n, sum)):
    print("YES")
else:
    print("NO")

# This code is contributed by shivani.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Check if possible subset with
    // given sum is possible or not
    static int subsetSum(int []a, int n, int sum)
    {

        // Storing the value -1 to the matrix
        int [,]tab = new int[n + 1,sum + 1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                tab[i,j] = -1;
            }
        }

        // If the sum is zero it means
        // we got our expected sum
        if (sum == 0)
            return 1;

        if (n <= 0)
            return 0;

        // If the value is not -1 it means it
        // already call the function
        // with the same value.
        // it will save our from the repetition.
        if (tab[n - 1,sum] != -1)
            return tab[n - 1,sum];

        // if the value of a[n-1] is
        // greater than the sum.
        // we call for the next value
        if (a[n - 1] > sum)
            return tab[n - 1,sum]
                = subsetSum(a, n - 1, sum);
        else {

            // Here we do two calls because we
            // don't know which value is
            // full-fill our criteria
            // that's why we doing two calls
            if (subsetSum(a, n - 1, sum) != 0
                || subsetSum(a, n - 1, sum - a[n - 1])
                       != 0) {
                return tab[n - 1,sum] = 1;
            }
            else
                return tab[n - 1,sum] = 0;
        }
    }

      // Driver Code
    public static void Main(String[] args)
    {

        int n = 5;
        int []a = { 1, 5, 3, 7, 4 };
        int sum = 12;

        if (subsetSum(a, n, sum) != 0) {
            Console.Write("YES\n");
        }
        else
            Console.Write("NO\n");
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

        // JavaScript Program for the above approach

        // Check if possible subset with
        // given sum is possible or not
        function subsetSum(a, n, sum) {

            // If the sum is zero it means
            // we got our expected sum
            if (sum == 0)
                return 1;

            if (n <= 0)
                return 0;

            // If the value is not -1 it means it
            // already call the function
            // with the same value.
            // it will save our from the repetition.
            if (tab[n - 1][sum] != -1)
                return tab[n - 1][sum];

            // if the value of a[n-1] is
            // greater than the sum.
            // we call for the next value
            if (a[n - 1] > sum)
                return tab[n - 1][sum] = subsetSum(a, n - 1, sum);
            else {

                // Here we do two calls because we
                // don't know which value is
                // full-fill our criteria
                // that's why we doing two calls
                return tab[n - 1][sum] = subsetSum(a, n - 1, sum) ||
                    subsetSum(a, n - 1, sum - a[n - 1]);
            }
        }

        // Driver Code

        // Storing the value -1 to the matrix
        let tab = Array(2000).fill().map(() => Array(2000).fill(-1));

        let n = 5;
        let a = [1, 5, 3, 7, 4];
        let sum = 12;

        if (subsetSum(a, n, sum)) {
            document.write("YES" + "<br>");
        }
        else {
            document.write("NO" + "<br>");
        }

    // This code is contributed by Potta Lokesh

</script>
```

**Output**

```
YES
```

**复杂度分析:**

*   **时间复杂度:** O(和*n)，其中和为‘目标和’，n 为数组大小。
*   **辅助空间:** O(和*n)，因为二维数组的大小是和*n。

[O(和)空间中的子集和问题](https://www.geeksforgeeks.org/subset-sum-problem-osum-space/)
[完全数和问题(打印给定和的所有子集)](https://www.geeksforgeeks.org/perfect-sum-problem-print-subsets-given-sum/)
如发现有不正确的地方，或想分享更多关于以上讨论话题的信息，请写评论。