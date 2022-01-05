# 将一个集合划分为两个子集，使得子集和的差最小

> 原文:[https://www . geesforgeks . org/partition-a-set-in-two-subset-sums-difference-is-minimum/](https://www.geeksforgeeks.org/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum/)

给定一组整数，任务是把它分成两组 S1 和 S2，使它们的和之间的绝对差最小。
如果有一个集合 S 有 n 个元素，那么如果我们假设 sub t1 有 m 个元素，sub T2 必须有 n-m 个元素，ABS(sum(sub t1)–sum(sub T2))的值应该最小。

**示例:**

```
Input:  arr[] = {1, 6, 11, 5} 
Output: 1
Explanation:
Subset1 = {1, 5, 6}, sum of Subset1 = 12 
Subset2 = {11}, sum of Subset2 = 11        
```

这个问题主要是[动态规划|集合 18(划分问题)的扩展。](https://www.geeksforgeeks.org/dynamic-programming-set-18-partition-problem/)
**【递归求解】**
递归方法是从数组的所有值生成所有可能的和，并检查哪个解是最优解。
要生成总和，我们要么在集合 1 中包含第 I 项，要么不包含，即在集合 2 中包含。

## C++

```
// A Recursive C++ program to solve minimum sum partition
// problem.
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum
int findMinRec(int arr[], int i, int sumCalculated,
               int sumTotal)
{
    // If we have reached last element.  Sum of one
    // subset is sumCalculated, sum of other subset is
    // sumTotal-sumCalculated.  Return absolute difference
    // of two sums.
    if (i == 0)
        return abs((sumTotal - sumCalculated)
                   - sumCalculated);

    // For every item arr[i], we have two choices
    // (1) We do not include it first set
    // (2) We include it in first set
    // We return minimum of two choices
    return min(
        findMinRec(arr, i - 1, sumCalculated + arr[i - 1],
                   sumTotal),
        findMinRec(arr, i - 1, sumCalculated, sumTotal));
}

// Returns minimum possible difference between sums
// of two subsets
int findMin(int arr[], int n)
{
    // Compute total sum of elements
    int sumTotal = 0;
    for (int i = 0; i < n; i++)
        sumTotal += arr[i];

    // Compute result using recursive function
    return findMinRec(arr, n, 0, sumTotal);
}

// Driver program to test above function
int main()
{
    int arr[] = { 3, 1, 4, 2, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "The minimum difference between two sets is "
         << findMin(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to partition a set into two subsets
// such that the difference of subset sums
// is minimum
import java.util.*;

class GFG {

    // Function to find the minimum sum
    public static int findMinRec(int arr[], int i,
                                 int sumCalculated,
                                 int sumTotal)
    {
        // If we have reached last element.
        // Sum of one subset is sumCalculated,
        // sum of other subset is sumTotal-
        // sumCalculated.  Return absolute
        // difference of two sums.
        if (i == 0)
            return Math.abs((sumTotal - sumCalculated)
                            - sumCalculated);

        // For every item arr[i], we have two choices
        // (1) We do not include it first set
        // (2) We include it in first set
        // We return minimum of two choices
        return Math.min(
            findMinRec(arr, i - 1,
                       sumCalculated + arr[i - 1],
                       sumTotal),
            findMinRec(arr, i - 1, sumCalculated,
                       sumTotal));
    }

    // Returns minimum possible difference between
    // sums of two subsets
    public static int findMin(int arr[], int n)
    {
        // Compute total sum of elements
        int sumTotal = 0;
        for (int i = 0; i < n; i++)
            sumTotal += arr[i];

        // Compute result using recursive function
        return findMinRec(arr, n, 0, sumTotal);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 3, 1, 4, 2, 2, 1 };
        int n = arr.length;
        System.out.print("The minimum difference"
                         + " between two sets is "
                         + findMin(arr, n));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
# A Recursive C program to
# solve minimum sum partition
# problem.

# Function to find the minimum sum

def findMinRec(arr, i, sumCalculated,
               sumTotal):

    # If we have reached last element.
    # Sum of one subset is sumCalculated,
    # sum of other subset is sumTotal-
    # sumCalculated.  Return absolute
    # difference of two sums.
    if (i == 0):
        return abs((sumTotal - sumCalculated) -
                   sumCalculated)

    # For every item arr[i], we have two choices
    # (1) We do not include it first set
    # (2) We include it in first set
    # We return minimum of two choices
    return min(findMinRec(arr, i - 1,
                          sumCalculated+arr[i - 1],
                          sumTotal),
               findMinRec(arr, i - 1,
                          sumCalculated, sumTotal))

# Returns minimum possible
# difference between sums
# of two subsets

def findMin(arr,  n):

    # Compute total sum
    # of elements
    sumTotal = 0
    for i in range(n):
        sumTotal += arr[i]

    # Compute result using
    # recursive function
    return findMinRec(arr, n,
                      0, sumTotal)

# Driver code
if __name__ == "__main__":

    arr = [3, 1, 4, 2, 2, 1]
    n = len(arr)
    print("The minimum difference " +
          "between two sets is ",
          findMin(arr, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# code to partition a set into two subsets
// such that the difference of subset sums
// is minimum
using System;

class GFG {

    // Function to find the minimum sum
    public static int findMinRec(int[] arr, int i,
                                 int sumCalculated,
                                 int sumTotal)
    {
        // If we have reached last element.
        // Sum of one subset is sumCalculated,
        // sum of other subset is sumTotal-
        // sumCalculated. Return absolute
        // difference of two sums.
        if (i == 0)
            return Math.Abs((sumTotal - sumCalculated)
                            - sumCalculated);

        // For every item arr[i], we have two choices
        // (1) We do not include it first set
        // (2) We include it in first set
        // We return minimum of two choices
        return Math.Min(
            findMinRec(arr, i - 1,
                       sumCalculated + arr[i - 1],
                       sumTotal),
            findMinRec(arr, i - 1, sumCalculated,
                       sumTotal));
    }

    // Returns minimum possible difference between
    // sums of two subsets
    public static int findMin(int[] arr, int n)
    {

        // Compute total sum of elements
        int sumTotal = 0;
        for (int i = 0; i < n; i++)
            sumTotal += arr[i];

        // Compute result using recursive function
        return findMinRec(arr, n, 0, sumTotal);
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 3, 1, 4, 2, 2, 1 };
        int n = arr.Length;
        Console.Write("The minimum difference"
                      + " between two sets is "
                      + findMin(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// JAVAscript code to partition a set into two subsets
// such that the difference of subset sums
// is minimum

    // Function to find the minimum sum
    function findMinRec(arr, i, sumCalculated, sumTotal)
    {

        // If we have reached last element.
        // Sum of one subset is sumCalculated,
        // sum of other subset is sumTotal-
        // sumCalculated.  Return absolute
        // difference of two sums.
        if (i == 0)
            return Math.abs((sumTotal-sumCalculated) -
                                   sumCalculated);

        // For every item arr[i], we have two choices
        // (1) We do not include it first set
        // (2) We include it in first set
        // We return minimum of two choices
        return Math.min(findMinRec(arr, i - 1, sumCalculated
                                   + arr[i-1], sumTotal),
                                 findMinRec(arr, i-1,
                                  sumCalculated, sumTotal));
    }

    // Returns minimum possible difference between
    // sums of two subsets
    function findMin(arr, n)
    {

         // Compute total sum of elements
        let sumTotal = 0;
        for (let i = 0; i < n; i++)
            sumTotal += arr[i];

        // Compute result using recursive function
        return findMinRec(arr, n, 0, sumTotal);
    }

     /* Driver program to test above function */
    let arr=[3, 1, 4, 2, 2, 1];
    let n = arr.length;
    document.write("The minimum difference"+
                        " between two sets is " +
                         findMin(arr, n));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
The minimum difference between two sets is 1
```

**时间复杂度:**

```
All the sums can be generated by either 
(1) including that element in set 1.
(2) without including that element in set 1.
So possible combinations are :-  
arr[0]      (1 or 2)  -> 2 values
arr[1]    (1 or 2)  -> 2 values
.
.
.
arr[n]     (2 or 2)  -> 2 values
So time complexity will be 2*2*..... *2 (For n times),
that is O(2^n).
```

**动态规划**
当元素之和不太大时，使用动态规划可以解决这个问题。我们可以创建一个 2D 数组 dp[n+1][sum+1]，其中 n 是给定集合中的元素数量，sum 是所有元素的总和。我们可以以自下而上的方式构建解决方案。

```
The task is to divide the set into two parts. 
We will consider the following factors for dividing it. 
Let 
  dp[n+1][sum+1] = {1 if some subset from 1st to i'th has a sum 
                      equal to j
                   0 otherwise}

    i ranges from {1..n}
    j ranges from {0..(sum of all elements)}  

So      
    dp[n+1][sum+1]  will be 1 if 
    1) The sum j is achieved including i'th item
    2) The sum j is achieved excluding i'th item.

Let sum of all the elements be S.  

To find Minimum sum difference, w have to find j such 
that Min{sum - j*2  : dp[n][j]  == 1 } 
    where j varies from 0 to sum/2

The idea is, sum of S1 is j and it should be closest
to sum/2, i.e., 2*j should be closest to sum.
```

下面是上面代码的实现。

## C++

```
// A Recursive C program to solve minimum sum partition
// problem.
#include <bits/stdc++.h>
using namespace std;

// Returns the minimum value of the difference of the two
// sets.
int findMin(int arr[], int n)
{
    // Calculate sum of all elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Create an array to store results of subproblems
    bool dp[n + 1][sum + 1];

    // Initialize first column as true. 0 sum is possible
    // with all elements.
    for (int i = 0; i <= n; i++)
        dp[i][0] = true;

    // Initialize top row, except dp[0][0], as false. With
    // 0 elements, no other sum except 0 is possible
    for (int i = 1; i <= sum; i++)
        dp[0][i] = false;

    // Fill the partition table in bottom up manner
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            // If i'th element is excluded
            dp[i][j] = dp[i - 1][j];

            // If i'th element is included
            if (arr[i - 1] <= j)
                dp[i][j] |= dp[i - 1][j - arr[i - 1]];
        }
    }

    // Initialize difference of two sums.
    int diff = INT_MAX;

    // Find the largest j such that dp[n][j]
    // is true where j loops from sum/2 t0 0
    for (int j = sum / 2; j >= 0; j--) {
        // Find the
        if (dp[n][j] == true) {
            diff = sum - 2 * j;
            break;
        }
    }
    return diff;
}

// Driver program to test above function
int main()
{
    int arr[] = { 3, 1, 4, 2, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "The minimum difference between 2 sets is "
         << findMin(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Recursive java program to solve
// minimum sum partition problem.
import java.io.*;

class GFG {
    // Returns the minimum value of
    // the difference of the two sets.
    static int findMin(int arr[], int n)
    {
        // Calculate sum of all elements
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Create an array to store
        // results of subproblems
        boolean dp[][] = new boolean[n + 1][sum + 1];

        // Initialize first column as true.
        // 0 sum is possible  with all elements.
        for (int i = 0; i <= n; i++)
            dp[i][0] = true;

        // Initialize top row, except dp[0][0],
        // as false. With 0 elements, no other
        // sum except 0 is possible
        for (int i = 1; i <= sum; i++)
            dp[0][i] = false;

        // Fill the partition table
        // in bottom up manner
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                // If i'th element is excluded
                dp[i][j] = dp[i - 1][j];

                // If i'th element is included
                if (arr[i - 1] <= j)
                    dp[i][j] |= dp[i - 1][j - arr[i - 1]];
            }
        }

        // Initialize difference of two sums.
        int diff = Integer.MAX_VALUE;

        // Find the largest j such that dp[n][j]
        // is true where j loops from sum/2 t0 0
        for (int j = sum / 2; j >= 0; j--) {
            // Find the
            if (dp[n][j] == true) {
                diff = sum - 2 * j;
                break;
            }
        }
        return diff;
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = { 3, 1, 4, 2, 2, 1 };
        int n = arr.length;
        System.out.println(
            "The minimum difference between 2 sets is "
            + findMin(arr, n));
    }
}
// This code is contributed by vt_m
```

## 蟒蛇 3

```
# A Recursive Python3 program to solve
# minimum sum partition problem.
import sys

# Returns the minimum value of the
# difference of the two sets.

def findMin(a, n):

    su = 0

    # Calculate sum of all elements
    su = sum(a)

    # Create an 2d list to store
    # results of subproblems
    dp = [[0 for i in range(su + 1)]
          for j in range(n + 1)]

    # Initialize first column as true.
    # 0 sum is possible
    # with all elements.
    for i in range(n + 1):
        dp[i][0] = True

    # Initialize top row, except dp[0][0],
    # as false. With 0 elements, no other
    # sum except 0 is possible
    for j in range(1, su + 1):
        dp[0][j] = False

    # Fill the partition table in
    # bottom up manner
    for i in range(1, n + 1):
        for j in range(1, su + 1):

            # If i'th element is excluded
            dp[i][j] = dp[i - 1][j]

            # If i'th element is included
            if a[i - 1] <= j:
                dp[i][j] |= dp[i - 1][j - a[i - 1]]

    # Initialize difference
    # of two sums.
    diff = sys.maxsize

    # Find the largest j such that dp[n][j]
    # is true where j loops from sum/2 t0 0
    for j in range(su // 2, -1, -1):
        if dp[n][j] == True:
            diff = su - (2 * j)
            break

    return diff

# Driver code
a = [3, 1, 4, 2, 2, 1]
n = len(a)

print("The minimum difference between "
      "2 sets is ", findMin(a, n))

# This code is contributed by Tokir Manva
```

## C#

```
// A Recursive C# program to solve
// minimum sum partition problem.
using System;

class GFG {

    // Returns the minimum value of
    // the difference of the two sets.
    static int findMin(int[] arr, int n)
    {

        // Calculate sum of all elements
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Create an array to store
        // results of subproblems
        bool[, ] dp = new bool[n + 1, sum + 1];

        // Initialize first column as true.
        // 0 sum is possible  with all elements.
        for (int i = 0; i <= n; i++)
            dp[i, 0] = true;

        // Initialize top row, except dp[0,0],
        // as false. With 0 elements, no other
        // sum except 0 is possible
        for (int i = 1; i <= sum; i++)
            dp[0, i] = false;

        // Fill the partition table
        // in bottom up manner
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {

                // If i'th element is excluded
                dp[i, j] = dp[i - 1, j];

                // If i'th element is included
                if (arr[i - 1] <= j)
                    dp[i, j] |= dp[i - 1, j - arr[i - 1]];
            }
        }

        // Initialize difference of two sums.
        int diff = int.MaxValue;

        // Find the largest j such that dp[n,j]
        // is true where j loops from sum/2 t0 0
        for (int j = sum / 2; j >= 0; j--) {

            // Find the
            if (dp[n, j] == true) {
                diff = sum - 2 * j;
                break;
            }
        }
        return diff;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 1, 4, 2, 2, 1 };
        int n = arr.Length;

        Console.WriteLine("The minimum difference "
                          + "between 2 sets is "
                          + findMin(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// A Recursive JavaScript program to solve minimum sum partition
// problem.

// Returns the minimum value of the difference of the two sets.
function findMin(arr, n)
{
    // Calculate sum of all elements
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += arr[i];

    // Create an array to store results of subproblems
    let dp = new Array(n + 1);

    // Initialize first column as true. 0 sum is possible
    // with all elements.
    for (let i = 0; i <= n; i++) {
        dp[i] = new Array(sum + 1);
        for(let j = 0; j <= sum; j++) {

            if(j == 0)
                dp[i][j] = true;
        }
    }

    // Initialize top row, except dp[0][0], as false. With
    // 0 elements, no other sum except 0 is possible
    for (let i = 1; i <= sum; i++)
        dp[0][i] = false;

    // Fill the partition table in bottom up manner
    for (let i=1; i<=n; i++)
    {
        for (let j=1; j<=sum; j++)
        {
            // If i'th element is excluded
            dp[i][j] = dp[i-1][j];

            // If i'th element is included
            if (arr[i-1] <= j)
                dp[i][j] |= dp[i-1][j-arr[i-1]];
        }
    }

    // Initialize difference of two sums.
    let diff = Number.MAX_VALUE;

    // Find the largest j such that dp[n][j]
    // is true where j loops from sum/2 t0 0
    for (let j=Math.floor(sum/2); j>=0; j--)
    {
        // Find the
        if (dp[n][j] == true)
        {
            diff = sum-2*j;
            break;
        }
    }
    return diff;
}

// Driver program to test above function

    let arr = [ 3, 1, 4, 2, 2, 1 ];
    let n = arr.length;
    document.write( "The minimum difference between 2 sets is "
         + findMin(arr, n));

    // This code is contributed by Dharanendra L V.

</script>
```

**输出:**

```
The minimum difference between 2 sets is 1
```

**时间复杂度** = O(n*sum)，其中 n 为元素个数，sum 为所有元素的和。

**空间复杂度更低的动态规划:**

我们可以使用 1D 阵列 dp[sum/2+1]来解决这个问题，而不是使用 2D 阵列。

假设集合 1 的元素之和是 x，那么集合 2 的元素之和将是 sm-x (sm 是 arr 的所有元素之和)。

所以我们必须最小化 abs(sm-2*x)。

因此，为了最小化两个集合之间的差异，我们需要知道一个刚好小于 sum/2 的数(sum 是数组中所有元素的和)，并且可以通过将数组中的元素相加来生成。

## C++

```
#include <iostream>
using namespace std;

int minDifference(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    int y = sum / 2 + 1;
    // dp[i] gives whether is it possible to get i as sum of
    // elements dd is helper variable
    // we use dd to ignoring duplicates
    bool dp[y], dd[y];

    // Initialising dp and dd
    for (int i = 0; i < y; i++) {
        dp[i] = dd[i] = false;
    }

    // sum = 0 is possible
    dd[0] = true;
    for (int i = 0; i < n; i++) {
        // updating dd[k] as true if k can be formed using
        // elements from 1 to i+1
        for (int j = 0; j + arr[i] < y; j++) {
            if (dp[j])
                dd[j + arr[i]] = true;
        }
        // updating dd
        for (int j = 0; j < y; j++) {
            if (dd[j])
                dp[j] = true;
            dd[j] = false; // reset dd
        }
    }
    // checking the number from sum/2 to 1 which is possible
    // to get as sum

    for (int i = y - 1; i >= 0; i--) {
        if (dp[i])
            return (sum - 2 * i);
        // since i is possible to form then another number
        // is sum-i
        // so mindifference is sum-i-i
    }
}
int main()
{

    int arr[] = { 1, 6, 11, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "The Minimum difference of 2 sets is "
         << minDifference(arr, n) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG {

    static int minDifference(int arr[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        int y = sum / 2 + 1;
        // dp[i] gives whether is it possible to get i as
        // sum of elements dd is helper variable we use dd
        // to ignoring duplicates
        boolean dp[] = new boolean[y], dd[]
                                       = new boolean[y];

        // Initialising dp and dd
        for (int i = 0; i < y; i++) {
            dp[i] = dd[i] = false;
        }

        // sum = 0 is possible
        dd[0] = true;
        for (int i = 0; i < n; i++) {
            // updating dd[k] as true if k can be formed
            // using elements from 1 to i+1
            for (int j = 0; j + arr[i] < y; j++) {
                if (dp[j])
                    dd[j + arr[i]] = true;
            }
            // updating dd
            for (int j = 0; j < y; j++) {
                if (dd[j])
                    dp[j] = true;
                dd[j] = false; // reset dd
            }
        }
        // checking the number from sum/2 to 1 which is
        // possible to get as sum

        for (int i = y - 1; i >= 0; i--) {
            if (dp[i])
                return (sum - 2 * i);
            // since i is possible to form then another
            // number is sum-i so mindifference is sum-i-i
        }
        return 0;
    }

    public static void main(String[] args)
    {

        int arr[] = { 1, 6, 11, 5 };
        int n = arr.length;
        System.out.print(
            "The Minimum difference of 2 sets is "
            + minDifference(arr, n) + '\n');
    }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
def minDifference(arr, n):
    sum = 0;
    for i in range(n):
        sum += arr[i];
    y = sum // 2 + 1;

    # dp[i] gives whether is it possible to get i as
    # sum of elements dd is helper variable we use dd
    # to ignoring duplicates
    dp = [False for i in range(y)]
    dd = [False for i in range(y)]

    # Initialising dp and dd

    # sum = 0 is possible
    dd[0] = True;
    for i in range(n):

        # updating dd[k] as True if k can be formed
        # using elements from 1 to i+1
        for j in range(y):
            if (j + arr[i] < y and dp[j]):
                dd[j + arr[i]] = True;

        # updating dd
        for j in range(y):
            if (dd[j]):
                dp[j] = True;
            dd[j] = False; # reset dd

    # checking the number from sum/2 to 1 which is
    # possible to get as sum
    for i in range(y-1, 0, -1):
        if (dp[i]):
            return (sum - 2 * i);

        # since i is possible to form then another
        # number is sum-i so mindifference is sum-i-i
    return 0;

if __name__ == '__main__':

    arr = [ 1, 6, 11, 5 ];
    n = len(arr);
    print("The Minimum difference of 2 sets is ", minDifference(arr, n));

# This code is contributed by umadevi9616
```

## C#

```
using System;

public class GFG {

    static int minDifference(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        int y = sum / 2 + 1;
        // dp[i] gives whether is it possible to get i as
        // sum of elements dd is helper variable we use dd
        // to ignoring duplicates
        bool []dp = new bool[y];bool []dd = new bool[y];

        // Initialising dp and dd
        for (int i = 0; i < y; i++) {
            dp[i] = dd[i] = false;
        }

        // sum = 0 is possible
        dd[0] = true;
        for (int i = 0; i < n; i++) {
            // updating dd[k] as true if k can be formed
            // using elements from 1 to i+1
            for (int j = 0; j + arr[i] < y; j++) {
                if (dp[j])
                    dd[j + arr[i]] = true;
            }
            // updating dd
            for (int j = 0; j < y; j++) {
                if (dd[j])
                    dp[j] = true;
                dd[j] = false; // reset dd
            }
        }
        // checking the number from sum/2 to 1 which is
        // possible to get as sum

        for (int i = y - 1; i >= 0; i--) {
            if (dp[i])
                return (sum - 2 * i);
            // since i is possible to form then another
            // number is sum-i so mindifference is sum-i-i
        }
        return 0;
    }

    public static void Main(String[] args)
    {

        int []arr = { 1, 6, 11, 5 };
        int n = arr.Length;
        Console.Write(
            "The Minimum difference of 2 sets is "
            + minDifference(arr, n) + '\n');
    }
}

// This code contributed by gauravrajput1
```

## java 描述语言

```
<script>
    function minDifference(arr , n) {
        var sum = 0;
        for (var i = 0; i < n; i++)
            sum += arr[i];
        var y = parseInt(sum / 2) + 1;

        // dp[i] gives whether is it possible to get i as
        // sum of elements dd is helper variable we use dd
        // to ignoring duplicates
        var dp = Array(y).fill(false), dd = Array(y).fill(false);

        // Initialising dp and dd
        for (var i = 0; i < y; i++) {
            dp[i] = dd[i] = false;
        }

        // sum = 0 is possible
        dd[0] = true;
        for ( var i = 0; i < n; i++)
        {

            // updating dd[k] as true if k can be formed
            // using elements from 1 to i+1
            for (var j = 0; j + arr[i] < y; j++) {
                if (dp[j])
                    dd[j + arr[i]] = true;
            }

            // updating dd
            for (var j = 0; j < y; j++) {
                if (dd[j])
                    dp[j] = true;
                dd[j] = false; // reset dd
            }
        }

        // checking the number from sum/2 to 1 which is
        // possible to get as sum
        for (var i = y - 1; i >= 0; i--) {
            if (dp[i])
                return (sum - 2 * i);
            // since i is possible to form then another
            // number is sum-i so mindifference is sum-i-i
        }
        return 0;
    }

        var arr = [ 1, 6, 11, 5 ];
        var n = arr.length;
        document.write("The Minimum difference of 2 sets is " + minDifference(arr, n) + '\n');

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
The Minimum difference of 2 sets is 1
```

**时间复杂度:**O(n * sum)
T3】辅助空间: O(sum)

请注意，上述解决方案是在伪多项式时间(时间复杂度取决于输入的数值)。本文由 Abhiraj Smit 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。