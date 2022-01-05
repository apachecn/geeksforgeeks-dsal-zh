# 从阵列中移除最少，使最大-最小< = K

> 原文:[https://www . geesforgeks . org/minimum-removes-array-make-max-min-k/](https://www.geeksforgeeks.org/minimum-removals-array-make-max-min-k/)

给定 N 个整数和 K，求应该移除的元素的最小数量，使得 A<sub>max</sub>-A<sub>min</sub><= K，移除元素后，剩余元素中考虑 A <sub>max</sub> 和 A <sub>min</sub> 。

**示例:**

```
Input : a[] = {1, 3, 4, 9, 10, 11, 12, 17, 20} 
          k = 4 
Output : 5 
Explanation: Remove 1, 3, 4 from beginning 
and 17, 20 from the end.

Input : a[] = {1, 5, 6, 2, 8}  K=2
Output : 3
Explanation: There are multiple ways to 
remove elements in this case.
One among them is to remove 5, 6, 8.
The other is to remove 1, 2, 5
```

**方法:**给定元素排序。使用贪婪方法，最好的方法是移除最小元素或最大元素，然后检查**A<sub>max</sub>-A<sub>min</sub><= K**。必须考虑各种清除组合。我们写一个递归关系来尝试每一种可能的组合。有两种可能的移除方式，要么我们移除最小值，要么我们移除最大值。**设(i…j)为去除元素后剩余元素的指数**。最初，我们从 i=0 和 j=n-1 开始，开始时移除的元素数为 0。**我们只在 a[j]-a[i] > k、**的情况下移除一个元素，两种可能的移除方式是 **(i+1…j)或(i…j-1)** 。考虑两者中的最小值。
让 DP <sub>i，j</sub> 为需要移除的元素数量，以便移除后 a[j]-a[i] < =k。

**排序数组的递归关系:**

```
DP<sub>i, j = 1+ (min(countRemovals(i+1, j), countRemovals(i, j-1))</sub>
```

下面是上述想法的实现:

## C++

```
// CPP program to find minimum removals
// to make max-min <= K
#include <bits/stdc++.h>
using namespace std;

#define MAX 100
int dp[MAX][MAX];

// function to check all possible combinations
// of removal and return the minimum one
int countRemovals(int a[], int i, int j, int k)
{
    // base case when all elements are removed
    if (i >= j)
        return 0;

    // if condition is satisfied, no more
    // removals are required
    else if ((a[j] - a[i]) <= k)
        return 0;

    // if the state has already been visited
    else if (dp[i][j] != -1)
        return dp[i][j];

    // when Amax-Amin>d
    else if ((a[j] - a[i]) > k) {

        // minimum is taken of the removal
        // of minimum element or removal
        // of the maximum element
        dp[i][j] = 1 + min(countRemovals(a, i + 1, j, k),
                           countRemovals(a, i, j - 1, k));
    }
    return dp[i][j];
}

// To sort the array and return the answer
int removals(int a[], int n, int k)
{
    // sort the array
    sort(a, a + n);

    // fill all stated with -1
    // when only one element
    memset(dp, -1, sizeof(dp));
    if (n == 1)
        return 0;
    else
        return countRemovals(a, 0, n - 1, k);
}

// Driver Code
int main()
{
    int a[] = { 1, 3, 4, 9, 10, 11, 12, 17, 20 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 4;
    cout << removals(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum removals
// to make max-min <= K
import java.util.Arrays;

class GFG
{
    static int MAX=100;
    static int dp[][]=new int[MAX][MAX];

    // function to check all possible combinations
    // of removal and return the minimum one
    static int countRemovals(int a[], int i, int j, int k)
    {
        // base case when all elements are removed
        if (i >= j)
            return 0;

        // if condition is satisfied, no more
        // removals are required
        else if ((a[j] - a[i]) <= k)
            return 0;

        // if the state has already been visited
        else if (dp[i][j] != -1)
            return dp[i][j];

        // when Amax-Amin>d
        else if ((a[j] - a[i]) > k) {

            // minimum is taken of the removal
            // of minimum element or removal
            // of the maximum element
            dp[i][j] = 1 + Math.min(countRemovals(a, i + 1, j, k),
                                    countRemovals(a, i, j - 1, k));
        }
        return dp[i][j];
    }

    // To sort the array and return the answer
    static int removals(int a[], int n, int k)
    {
        // sort the array
        Arrays.sort(a);

        // fill all stated with -1
        // when only one element
        for(int[] rows:dp)
        Arrays.fill(rows,-1);
        if (n == 1)
            return 0;
        else
            return countRemovals(a, 0, n - 1, k);
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 1, 3, 4, 9, 10, 11, 12, 17, 20 };
        int n = a.length;
        int k = 4;
        System.out.print(removals(a, n, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# minimum removals to
# make max-min <= K
MAX = 100
dp = [[0 for i in range(MAX)]
         for i in range(MAX)]
for i in range(0, MAX) :
    for j in range(0, MAX) :
        dp[i][j] = -1

# function to check all
# possible combinations
# of removal and return
# the minimum one
def countRemovals(a, i, j, k) :

    global dp

    # base case when all
    # elements are removed
    if (i >= j) :
        return 0

    # if condition is satisfied,
    # no more removals are required
    elif ((a[j] - a[i]) <= k) :
        return 0

    # if the state has
    # already been visited
    elif (dp[i][j] != -1) :
        return dp[i][j]

    # when Amax-Amin>d
    elif ((a[j] - a[i]) > k) :

        # minimum is taken of
        # the removal of minimum
        # element or removal of
        # the maximum element
        dp[i][j] = 1 + min(countRemovals(a, i + 1,
                                         j, k),
                           countRemovals(a, i,
                                         j - 1, k))
    return dp[i][j]

# To sort the array
# and return the answer
def removals(a, n, k) :

    # sort the array
    a.sort()

    # fill all stated
    # with -1 when only
    # one element
    if (n == 1) :
        return 0
    else :
        return countRemovals(a, 0,
                             n - 1, k)

# Driver Code
a = [1, 3, 4, 9, 10,
     11, 12, 17, 20]
n = len(a)
k = 4
print (removals(a, n, k))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to find minimum
// removals to make max-min <= K
using System;

class GFG
{
    static int MAX = 100;
    static int [,]dp = new int[MAX, MAX];

    // function to check all
    // possible combinations
    // of removal and return
    // the minimum one
    static int countRemovals(int []a, int i,
                             int j, int k)
    {
        // base case when all
        // elements are removed
        if (i >= j)
            return 0;

        // if condition is satisfied,
        // no more removals are required
        else if ((a[j] - a[i]) <= k)
            return 0;

        // if the state has
        // already been visited
        else if (dp[i, j] != -1)
            return dp[i, j];

        // when Amax-Amin>d
        else if ((a[j] - a[i]) > k)
        {

            // minimum is taken of the
            // removal of minimum element
            // or removal of the maximum
            // element
            dp[i, j] = 1 + Math.Min(countRemovals(a, i + 1,
                                                  j, k),
                                    countRemovals(a, i,
                                                  j - 1, k));
        }
        return dp[i, j];
    }

    // To sort the array and
    // return the answer
    static int removals(int []a,
                        int n, int k)
    {
        // sort the array
        Array.Sort(a);

        // fill all stated with -1
        // when only one element
        for(int i = 0; i < MAX; i++)
        {
            for(int j = 0; j < MAX; j++)
                dp[i, j] = -1;
        }
        if (n == 1)
            return 0;
        else
            return countRemovals(a, 0,
                                 n - 1, k);
    }

    // Driver code
    static void Main()
    {
        int []a = new int[]{ 1, 3, 4, 9, 10,
                             11, 12, 17, 20 };
        int n = a.Length;
        int k = 4;
        Console.Write(removals(a, n, k));
    }
}

// This code is contributed by
// ManishShaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// minimum removals to
// make max-min <= K
$MAX = 100;
$dp = array(array());
for($i = 0; $i < $MAX; $i++)
{
    for($j = 0; $j < $MAX; $j++)
        $dp[$i][$j] = -1;
}

// function to check all
// possible combinations
// of removal and return
// the minimum one
function countRemovals($a, $i,
                       $j, $k)
{
    global $dp;

    // base case when all
    // elements are removed
    if ($i >= $j)
        return 0;

    // if condition is satisfied,
    // no more removals are required
    else if (($a[$j] - $a[$i]) <= $k)
        return 0;

    // if the state has
    // already been visited
    else if ($dp[$i][$j] != -1)
        return $dp[$i][$j];

    // when Amax-Amin>d
    else if (($a[$j] - $a[$i]) > $k)
    {

        // minimum is taken of
        // the removal of minimum
        // element or removal of
        // the maximum element
        $dp[$i][$j] = 1 + min(countRemovals($a, $i + 1,
                                                $j, $k),
                              countRemovals($a, $i,
                                            $j - 1, $k));
    }
    return $dp[$i][$j];
}

// To sort the array
// and return the answer
function removals($a, $n, $k)
{
    // sort the array
    sort($a);

    // fill all stated with -1
    // when only one element
    if ($n == 1)
        return 0;
    else
        return countRemovals($a, 0,
                             $n - 1, $k);
}

// Driver Code
$a = array(1, 3, 4, 9, 10,
           11, 12, 17, 20);
$n = count($a);
$k = 4;
echo (removals($a, $n, $k));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find minimum removals
    // to make max-min <= K

    let MAX = 100;
    let dp = new Array(MAX);
    for(let i = 0; i < MAX; i++)
    {
        dp[i] = new Array(MAX);
    }
    // function to check all possible combinations
    // of removal and return the minimum one
    function countRemovals(a,i,j,k)
    {
        // base case when all elements are removed
        if (i >= j)
            return 0;

        // if condition is satisfied, no more
        // removals are required
        else if ((a[j] - a[i]) <= k)
            return 0;

        // if the state has already been visited
        else if (dp[i][j] != -1)
            return dp[i][j];

        // when Amax-Amin>d
        else if ((a[j] - a[i]) > k) {

            // minimum is taken of the removal
            // of minimum element or removal
            // of the maximum element
            dp[i][j] = 1 + Math.min(countRemovals(a, i + 1, j, k),
                            countRemovals(a, i, j - 1, k));
        }
        return dp[i][j];
    }

    // To sort the array and return the answer
    function removals(a,n,k)
    {
        // sort the array
        a.sort(function(a, b){return a - b});

        // fill all stated with -1
        // when only one element
        for(let i = 0; i < MAX; i++)
        {
            for(let j = 0; j < MAX; j++)
            {
                dp[i][j] = -1;
            }
        }
        if (n == 1)
            return 0;
        else
            return countRemovals(a, 0, n - 1, k);
    }

    // Driver Code

    let a = [ 1, 3, 4, 9, 10, 11, 12, 17, 20 ];
    let n = a.length;
    let k = 4;
    document.write(removals(a, n, k));

</script>
```

**Output**

```
5
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup>

该解决方案可以进一步优化。其思想是以递增的顺序对数组进行排序，遍历所有元素(比如索引 I)，并找到其右边的最大元素(索引 j)，这样 arr[j]–arr[I]< = k。因此，要移除的元素数量变为 n-(j-i+1)。元素的最小数量可以通过取 n-(j-i-1)个整体 I 的最小值来找到。索引 j 的值可以通过 start = i+1 和 end = n-1 之间的二分搜索法来找到；

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find
// rightmost index
// which satisfies the condition
// arr[j] - arr[i] <= k
int findInd(int key, int i,
            int n, int k, int arr[])
{
    int start, end, mid, ind = -1;

    // Initialising start to i + 1
    start = i + 1;

    // Initialising end to n - 1
    end = n - 1;

    // Binary search implementation
    // to find the rightmost element
    // that satisfy the condition
    while (start < end)
    {
        mid = start + (end - start) / 2;

        // Check if the condition satisfies
        if (arr[mid] - key <= k)
        {  

            // Store the position
            ind = mid;

            // Make start = mid + 1
            start = mid + 1;
        }
        else
        {
            // Make end = mid
            end = mid;
        }
    }

    // Return the rightmost position
    return ind;
}

// Function to calculate
// minimum number of elements
// to be removed
int removals(int arr[], int n, int k)
{
    int i, j, ans = n - 1;

    // Sort the given array
    sort(arr, arr + n);

    // Iterate from 0 to n-1
    for (i = 0; i < n; i++)
    {

        // Find j such that
        // arr[j] - arr[i] <= k
        j = findInd(arr[i], i, n, k, arr);

        // If there exist such j
        // that satisfies the condition
        if (j != -1)
        {
            // Number of elements
            // to be removed for this
            // particular case is
            // (j - i + 1)
            ans = min(ans, n - (j - i + 1));
        }
    }

    // Return answer
    return ans;
}

// Driver Code
int main()
{
    int a[] = {1, 3, 4, 9, 10,
               11, 12, 17, 20};
    int n = sizeof(a) / sizeof(a[0]);
    int k = 4;
    cout << removals(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find rightmost index
// which satisfies the condition
// arr[j] - arr[i] <= k
static int findInd(int key, int i,
                   int n, int k, int arr[])
{
    int start, end, mid, ind = -1;

    // Initialising start to i + 1
    start = i + 1;

    // Initialising end to n - 1
    end = n - 1;

    // Binary search implementation
    // to find the rightmost element
    // that satisfy the condition
    while (start < end)
    {
        mid = start + (end - start) / 2;

        // Check if the condition satisfies
        if (arr[mid] - key <= k)
        {

            // Store the position
            ind = mid;

            // Make start = mid + 1
            start = mid + 1;
        }
        else
        {

            // Make end = mid
            end = mid;
        }
    }

    // Return the rightmost position
    return ind;
}

// Function to calculate
// minimum number of elements
// to be removed
static int removals(int arr[], int n, int k)
{
    int i, j, ans = n - 1;

    // Sort the given array
    Arrays.sort(arr);

    // Iterate from 0 to n-1
    for(i = 0; i < n; i++)
    {

        // Find j such that
        // arr[j] - arr[i] <= k
        j = findInd(arr[i], i, n, k, arr);

        // If there exist such j
        // that satisfies the condition
        if (j != -1)
        {

            // Number of elements
            // to be removed for this
            // particular case is
            // (j - i + 1)
            ans = Math.min(ans,
                           n - (j - i + 1));
        }
    }

    // Return answer
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 1, 3, 4, 9, 10,
                11, 12, 17, 20 };
    int n = a.length;
    int k = 4;

    System.out.println(removals(a, n, k));
}
}

// This code is contributed by adityapande88
```

## 蟒蛇 3

```
# Python program for the
# above approach

# Function to find
# rightmost index
# which satisfies the condition
# arr[j] - arr[i] <= k
def findInd(key, i, n,
            k, arr):

     ind = -1

     # Initialising start
     # to i + 1
     start = i + 1

     # Initialising end
     # to n - 1
     end = n - 1;

     # Binary search implementation
     # to find the rightmost element
     # that satisfy the condition
     while (start < end):
          mid = int(start +
                   (end - start) / 2)

          # Check if the condition
          # satisfies
          if (arr[mid] - key <= k):

               # Store the position
               ind = mid

               # Make start = mid + 1
               start = mid + 1
          else:
               # Make end = mid
               end = mid

     # Return the rightmost position
     return ind

# Function to calculate
# minimum number of elements
# to be removed
def removals(arr, n, k):

     ans = n - 1

     # Sort the given array
     arr.sort()

     # Iterate from 0 to n-1
     for i in range(0, n):

          # Find j such that
          # arr[j] - arr[i] <= k
          j = findInd(arr[i], i,
                      n, k, arr)

          # If there exist such j
          # that satisfies the condition
          if (j != -1):

               # Number of elements
               # to be removed for this
               # particular case is
               # (j - i + 1)
               ans = min(ans, n -
                        (j - i + 1))

     # Return answer
     return ans

# Driver Code
a = [1, 3, 4, 9,
     10,11, 12, 17, 20]
n = len(a)
k = 4
print(removals(a, n, k))

# This code is contributed by Stream_Cipher
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find rightmost index
// which satisfies the condition
// arr[j] - arr[i] <= k
static int findInd(int key, int i,
                   int n, int k, int[] arr)
{
    int start, end, mid, ind = -1;

    // Initialising start to i + 1
    start = i + 1;

    // Initialising end to n - 1
    end = n - 1;

    // Binary search implementation
    // to find the rightmost element
    // that satisfy the condition
    while (start < end)
    {
        mid = start + (end - start) / 2;

        // Check if the condition satisfies
        if (arr[mid] - key <= k)
        {

            // Store the position
            ind = mid;

            // Make start = mid + 1
            start = mid + 1;
        }
        else
        {

            // Make end = mid
            end = mid;
        }
    }

    // Return the rightmost position
    return ind;
}

// Function to calculate minimum
// number of elements to be removed
static int removals(int[] arr, int n, int k)
{
    int i, j, ans = n - 1;

    // Sort the given array
    Array.Sort(arr);

    // Iterate from 0 to n-1
    for(i = 0; i < n; i++)
    {

        // Find j such that
        // arr[j] - arr[i] <= k
        j = findInd(arr[i], i, n, k, arr);

        // If there exist such j
        // that satisfies the condition
        if (j != -1)
        {

            // Number of elements
            // to be removed for this
            // particular case is
            // (j - i + 1)
            ans = Math.Min(ans,
                           n - (j - i + 1));
        }
    }

    // Return answer
    return ans;
}

// Driver code
static void Main()
{
    int[] a = { 1, 3, 4, 9, 10,
                11, 12, 17, 20 };
    int n = a.Length;
    int k = 4;

    Console.Write(removals(a, n, k));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
    // javascript program for the above approach

    // Function to find rightmost index
    // which satisfies the condition
    // arr[j] - arr[i] <= k
    function findInd(key , i , n , k , arr) {
        var start, end, mid, ind = -1;

        // Initialising start to i + 1
        start = i + 1;

        // Initialising end to n - 1
        end = n - 1;

        // Binary search implementation
        // to find the rightmost element
        // that satisfy the condition
        while (start < end) {
            mid = start + (end - start) / 2;

            // Check if the condition satisfies
            if (arr[mid] - key <= k) {

                // Store the position
                ind = mid;

                // Make start = mid + 1
                start = mid + 1;
            }
              else {

                // Make end = mid
                end = mid;
            }
        }

        // Return the rightmost position
        return ind;
    }

    // Function to calculate
    // minimum number of elements
    // to be removed
    function removals(arr , n , k) {
        var i, j, ans = n - 1;

        // Sort the given array
        arr.sort((a,b)=>a-b);

        // Iterate from 0 to n-1
        for (i = 0; i < n; i++) {

            // Find j such that
            // arr[j] - arr[i] <= k
            j = findInd(arr[i], i, n, k, arr);

            // If there exist such j
            // that satisfies the condition
            if (j != -1) {

                // Number of elements
                // to be removed for this
                // particular case is
                // (j - i + 1)
                ans = Math.min(ans, n - (j - i + 1));
            }
        }

        // Return answer
        return ans;
    }

    // Driver Code

    var a = [ 1, 3, 4, 9, 10, 11, 12, 17, 20 ];
    var n = a.length;
    var k = 4;

    document.write(removals(a, n, k));

// This code contributed by Rajput-Ji
</script>
```

**Output**

```
5
```

**时间复杂度:** O(nlogn)

**辅助空间:** O(n)

**进场:**

1.  该解决方案可以进一步优化。其思想是以递增的顺序对数组进行排序，遍历所有元素(比如索引 j)，找到其左边的最小元素(索引 I)，这样 arr[j]–arr[I]< = k，并将其存储在 dp[j]中。
2.  因此，要移除的元素数量变为 n-(j-i+1)。通过取 n-(j-i-1)个整体 j 的最小值，可以找到元素的最小数量。索引 I 的值可以通过其先前的 dp 数组元素值找到。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// To sort the array and return the answer
int removals(int arr[], int n, int k)
{

  // sort the array
  sort(arr, arr + n);
  int dp[n];

  // fill all stated with -1
  // when only one element
  for(int i = 0; i < n; i++)
    dp[i] = -1;

  // as dp[0] = 0 (base case) so min
  // no of elements to be removed are
  // n-1 elements
  int ans = n - 1;
  dp[0] = 0;
  for (int i = 1; i < n; i++)
  {
    dp[i] = i;
    int j = dp[i - 1];
    while (j != i && arr[i] - arr[j] > k)
    {
      j++;
    }
    dp[i] = min(dp[i], j);
    ans = min(ans, (n - (i - j + 1)));
  }
  return ans;
}

// Driver code   
int main()
{
  int a[] = { 1, 3, 4, 9, 10, 11, 12, 17, 20 };
  int n = sizeof(a) / sizeof(a[0]);
  int k = 4;
  cout<<removals(a, n, k);
  return 0;
}

// This code is contributed by Balu Nagar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // To sort the array and return the answer
    static int removals(int arr[], int n, int k)
    {
        // sort the array
        Arrays.sort(arr);

        // fill all stated with -1
        // when only one element
        int dp[] = new int[n];
        Arrays.fill(dp, -1);

        // as dp[0] = 0 (base case) so min
        // no of elements to be removed are
        // n-1 elements
        int ans = n - 1;
        dp[0] = 0;

        // Iterate from 1 to n - 1
        for (int i = 1; i < n; i++) {
            dp[i] = i;
            int j = dp[i - 1];
            while (j != i && arr[i] - arr[j] > k) {
                j++;
            }
            dp[i] = Integer.min(dp[i], j);
            ans = Integer.min(ans, (n - (i - j + 1)));
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 1, 3, 4, 9, 10, 11, 12, 17, 20 };
        int n = a.length;
        int k = 4;
        System.out.print(removals(a, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# To sort the array and return the answer
def removals(arr, n, k):

  # sort the array
  arr.sort()
  dp = [0 for i in range(n)]

  # Fill all stated with -1
  # when only one element
  for i in range(n):
    dp[i] = -1

  # As dp[0] = 0 (base case) so min
  # no of elements to be removed are
  # n-1 elements
  ans = n - 1
  dp[0] = 0

  for i in range(1, n):
    dp[i] = i
    j = dp[i - 1]

    while (j != i and arr[i] - arr[j] > k):
      j += 1

    dp[i] = min(dp[i], j)
    ans = min(ans, (n - (i - j + 1)))

  return ans

# Driver code   
a = [ 1, 3, 4, 9, 10, 11, 12, 17, 20 ]
n = len(a)
k = 4

print(removals(a, n, k))

# This code is contributed by rohan07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// To sort the array and return the answer
static int removals(int[] arr, int n, int k)
{

    // Sort the array
    Array.Sort(arr);
    int[] dp = new int[n];

    // Fill all stated with -1
    // when only one element
    for(int i = 0; i < n; i++)
        dp[i] = -1;

    // As dp[0] = 0 (base case) so min
    // no of elements to be removed are
    // n-1 elements
    int ans = n - 1;
    dp[0] = 0;

    // Iterate from 1 to n - 1
    for(int i = 1; i < n; i++)
    {
        dp[i] = i;
        int j = dp[i - 1];

        while (j != i && arr[i] - arr[j] > k)
        {
            j++;
        }
        dp[i] = Math.Min(dp[i], j);
        ans = Math.Min(ans, (n - (i - j + 1)));
    }
    return ans;
}

// Driver code
static public void Main()
{
    int[] a = { 1, 3, 4, 9, 10, 11, 12, 17, 20 };
    int n = a.Length;
    int k = 4;

    Console.Write(removals(a, n, k));
}
}

// This code is contributed by lokeshpotta20
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// To sort the array and return the answer
function removals(arr, n, k)
{

  // sort the array
  arr.sort((a,b)=>a-b);
  var dp = Array(n);

  // fill all stated with -1
  // when only one element
  for(var i = 0; i < n; i++)
    dp[i] = -1;

  // as dp[0] = 0 (base case) so min
  // no of elements to be removed are
  // n-1 elements
  var ans = n - 1;
  dp[0] = 0;
  for (var i = 1; i < n; i++)
  {
    dp[i] = i;
    var j = dp[i - 1];
    while (j != i && arr[i] - arr[j] > k)
    {
      j++;
    }
    dp[i] = Math.min(dp[i], j);
    ans = Math.min(ans, (n - (i - j + 1)));
  }
  return ans;
}

// Driver code   
var a = [1, 3, 4, 9, 10, 11, 12, 17, 20];
var n = a.length;
var k = 4;
document.write( removals(a, n, k));

</script>
```

**Output**

```
5
```

**时间复杂度** : O(nlog n)。因为外部循环要进行 n 次迭代。对于所有外部迭代，内部循环最多迭代 n 次。因为我们从 dp[i-1]开始 j 的值，并循环它，直到它到达 I，然后对于下一个元素，我们再次从先前的 dp[i]值开始。因此，如果我们不考虑排序的复杂性，总时间复杂度为 O(n)，因为在上述解决方案中也没有考虑排序的复杂性。

**辅助空间** : O(n)