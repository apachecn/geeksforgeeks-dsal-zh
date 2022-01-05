# 从数组中选择元素以使其平均值为 K 的方法数

> 原文:[https://www . geeksforgeeks . org/从数组中选择元素的方法数，这样它们的平均值为-k/](https://www.geeksforgeeks.org/number-of-ways-to-choose-elements-from-the-array-such-that-their-average-is-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的数组 **arr[]** 。任务是找到从数组中选择一个或多个元素的方法的数量，使得所选整数的平均值等于给定的数量 **K** 。

**示例:**

> **输入:** arr[] = {7，9，8，9}，K = 8
> **输出:** 5
> {8}、{7，9}、{7，9}、{7，8，9}和{7，8，9}
> **输入:** arr[] = {3，6，2，8，7，6，5，9}，K = 5
> **输出:** 19

****简单方法:**一个简单的解决方案是尝试所有可能性，因为 N 可以很大。时间复杂度可以是 2 <sup>N</sup> 。
**高效途径**:以上途径可以通过使用动态规划来优化解决这个问题。假设我们在第 I 个指数上，让*值*为该指数的当前值。我们有两种可能，要么选择答案中的那个元素，要么放弃这个元素。因此，我们现在结束了。我们还将跟踪当前所选元素集中的元素数量。** 

****下面是递归公式。****

```
ways(index, sum, count) 
      = ways(index - 1, sum, count) 
        + ways(index - 1, sum + arr[index], count + 1)
```

**以下是上述方法的实现:** 

## **C++**

```
#include <bits/stdc++.h>
using namespace std;

#define MAX_INDEX 51
#define MAX_SUM 2505

// This dp array is used to store our values
// so that we don't have to calculate same
// values again and again
int dp[MAX_INDEX][MAX_SUM][MAX_INDEX];

int waysutil(int index, int sum, int count,
             vector<int>& arr, int K)
{
    // Base cases
    // Index can't be less than 0
    if (index < 0)
        return 0;

    if (index == 0) {

        // No element is picked hence
        // average cannot be calculated
        if (count == 0)
            return 0;
        int remainder = sum % count;

        // If remainder is non zero, we cannot
        // divide the sum by count i.e. the average
        // will not be an integer
        if (remainder != 0)
            return 0;
        int average = sum / count;

        // If we find an average return 1
        if (average == K)
            return 1;
    }

    // If we have already calculated this function
    // simply return it instead of calculating it again
    if (dp[index][sum][count] != -1)
        return dp[index][sum][count];

    // If we don't pick the current element
    // simple recur for index -1
    int dontpick = waysutil(index - 1,
                            sum, count, arr, K);

    // If we pick the current element add it to
    // our current sum and increment count by 1
    int pick = waysutil(index - 1,
                        sum + arr[index],
                        count + 1, arr, K);
    int total = pick + dontpick;

    // Store the value for the current function
    dp[index][sum][count] = total;
    return total;
}

// Function to return the number of ways
int ways(int N, int K, int* arr)
{
    vector<int> Arr;

    // Push -1 at the beginning to
    // make it 1-based indexing
    Arr.push_back(-1);
    for (int i = 0; i < N; ++i) {
        Arr.push_back(arr[i]);
    }

    // Initialize dp array by -1
    memset(dp, -1, sizeof dp);

    // Call recursive function
    // waysutil to calculate total ways
    int answer = waysutil(N, 0, 0, Arr, K);
    return answer;
}

// Driver code
int main()
{
    int arr[] = { 3, 6, 2, 8, 7, 6, 5, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 5;
    cout << ways(N, K, arr);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    static int MAX_INDEX = 51;
    static int MAX_SUM = 2505;

    // This dp array is used to store our values
    // so that we don't have to calculate same
    // values again and again
    static int[][][] dp = new int[MAX_INDEX][MAX_SUM][MAX_INDEX];

    static int waysutil(int index, int sum, int count,
                        Vector<Integer> arr, int K)
    {
        // Base cases
        // Index can't be less than 0
        if (index < 0)
        {
            return 0;
        }

        if (index == 0)
        {

            // No element is picked hence
            // average cannot be calculated
            if (count == 0)
            {
                return 0;
            }
            int remainder = sum % count;

            // If remainder is non zero, we cannot
            // divide the sum by count i.e. the average
            // will not be an integer
            if (remainder != 0)
            {
                return 0;
            }
            int average = sum / count;

            // If we find an average return 1
            if (average == K)
            {
                return 1;
            }
        }

        // If we have already calculated this function
        // simply return it instead of calculating it again
        if (dp[index][sum][count] != -1)
        {
            return dp[index][sum][count];
        }

        // If we don't pick the current element
        // simple recur for index -1
        int dontpick = waysutil(index - 1,
                sum, count, arr, K);

        // If we pick the current element add it to
        // our current sum and increment count by 1
        int pick = waysutil(index - 1,
                sum + arr.get(index),
                count + 1, arr, K);
        int total = pick + dontpick;

        // Store the value for the current function
        dp[index][sum][count] = total;
        return total;
    }

    // Function to return the number of ways
    static int ways(int N, int K, int[] arr)
    {
        Vector<Integer> Arr = new Vector<>();

        // Push -1 at the beginning to
        // make it 1-based indexing
        Arr.add(-1);
        for (int i = 0; i < N; ++i)
        {
            Arr.add(arr[i]);
        }

        // Initialize dp array by -1
        for (int i = 0; i < MAX_INDEX; i++)
        {
            for (int j = 0; j < MAX_SUM; j++)
            {
                for (int l = 0; l < MAX_INDEX; l++)
                {
                    dp[i][j][l] = -1;
                }
            }
        }

        // Call recursive function
        // waysutil to calculate total ways
        int answer = waysutil(N, 0, 0, Arr, K);
        return answer;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {3, 6, 2, 8, 7, 6, 5, 9};
        int N = arr.length;
        int K = 5;
        System.out.println(ways(N, K, arr));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## **蟒蛇 3**

```
# Python implementation of above approach
import numpy as np

MAX_INDEX = 51
MAX_SUM = 2505

# This dp array is used to store our values
# so that we don't have to calculate same
# values again and again

# Initialize dp array by -1
dp = np.ones((MAX_INDEX,MAX_SUM,MAX_INDEX)) * -1;

def waysutil(index, sum, count, arr, K) :

    # Base cases
    # Index can't be less than 0
    if (index < 0) :
        return 0;

    if (index == 0) :

        # No element is picked hence
        # average cannot be calculated
        if (count == 0) :
            return 0;

        remainder = sum % count;

        # If remainder is non zero, we cannot
        # divide the sum by count i.e. the average
        # will not be an integer
        if (remainder != 0) :
            return 0;

        average = sum // count;

        # If we find an average return 1
        if (average == K) :
            return 1;

    # If we have already calculated this function
    # simply return it instead of calculating it again
    if (dp[index][sum][count] != -1) :
        return dp[index][sum][count];

    # If we don't pick the current element
    # simple recur for index -1
    dontpick = waysutil(index - 1,
                            sum, count, arr, K);

    # If we pick the current element add it to
    # our current sum and increment count by 1
    pick = waysutil(index - 1,
                        sum + arr[index],
                        count + 1, arr, K);

    total = pick + dontpick;

    # Store the value for the current function
    dp[index][sum][count] = total;

    return total;

# Function to return the number of ways
def ways(N, K, arr) :

    Arr = [];

    # Push -1 at the beginning to
    # make it 1-based indexing
    Arr.append(-1);
    for i in range(N) :
        Arr.append(arr[i]);

    # Call recursive function
    # waysutil to calculate total ways
    answer = waysutil(N, 0, 0, Arr, K);
    return answer;

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 6, 2, 8, 7, 6, 5, 9 ];
    N =len(arr);
    K = 5;
    print(ways(N, K, arr));

# This code is contributed by AnkitRai01
```

## **C#**

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

    static int MAX_INDEX = 51;
    static int MAX_SUM = 2505;

    // This dp array is used to store our values
    // so that we don't have to calculate same
    // values again and again
    static int[,,] dp = new int[MAX_INDEX, MAX_SUM, MAX_INDEX];

    static int waysutil(int index, int sum, int count,
                        List<int> arr, int K)
    {
        // Base cases
        // Index can't be less than 0
        if (index < 0)
        {
            return 0;
        }

        if (index == 0)
        {

            // No element is picked hence
            // average cannot be calculated
            if (count == 0)
            {
                return 0;
            }
            int remainder = sum % count;

            // If remainder is non zero, we cannot
            // divide the sum by count i.e. the average
            // will not be an integer
            if (remainder != 0)
            {
                return 0;
            }
            int average = sum / count;

            // If we find an average return 1
            if (average == K)
            {
                return 1;
            }
        }

        // If we have already calculated this function
        // simply return it instead of calculating it again
        if (dp[index,sum,count] != -1)
        {
            return dp[index, sum, count];
        }

        // If we don't pick the current element
        // simple recur for index -1
        int dontpick = waysutil(index - 1,
                sum, count, arr, K);

        // If we pick the current element add it to
        // our current sum and increment count by 1
        int pick = waysutil(index - 1,
                sum + arr[index],
                count + 1, arr, K);
        int total = pick + dontpick;

        // Store the value for the current function
        dp[index,sum,count] = total;
        return total;
    }

    // Function to return the number of ways
    static int ways(int N, int K, int[] arr)
    {
        List<int> Arr = new List<int>();

        // Push -1 at the beginning to
        // make it 1-based indexing
        Arr.Add(-1);
        for (int i = 0; i < N; ++i)
        {
            Arr.Add(arr[i]);
        }

        // Initialize dp array by -1
        for (int i = 0; i < MAX_INDEX; i++)
        {
            for (int j = 0; j < MAX_SUM; j++)
            {
                for (int l = 0; l < MAX_INDEX; l++)
                {
                    dp[i, j, l] = -1;
                }
            }
        }

        // Call recursive function
        // waysutil to calculate total ways
        int answer = waysutil(N, 0, 0, Arr, K);
        return answer;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = {3, 6, 2, 8, 7, 6, 5, 9};
        int N = arr.Length;
        int K = 5;
        Console.WriteLine(ways(N, K, arr));
    }
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>
// javascript implementation of the above approach

    var MAX_INDEX = 51;
    var MAX_SUM = 2505;

    // This dp array is used to store our values
    // so that we don't have to calculate same
    // values again and again
    var dp = Array(MAX_INDEX).fill().map(()=>Array(MAX_SUM).fill().map(()=>Array(MAX_INDEX).fill(0)));;

    function waysutil(index , sum , count, arr , K) {
        // Base cases
        // Index can't be less than 0
        if (index < 0) {
            return 0;
        }

        if (index == 0) {

            // No element is picked hence
            // average cannot be calculated
            if (count == 0) {
                return 0;
            }
            var remainder = sum % count;

            // If remainder is non zero, we cannot
            // divide the sum by count i.e. the average
            // will not be an integer
            if (remainder != 0) {
                return 0;
            }
            var average = sum / count;

            // If we find an average return 1
            if (average == K) {
                return 1;
            }
        }

        // If we have already calculated this function
        // simply return it instead of calculating it again
        if (dp[index][sum][count] != -1) {
            return dp[index][sum][count];
        }

        // If we don't pick the current element
        // simple recur for index -1
        var dontpick = waysutil(index - 1, sum, count, arr, K);

        // If we pick the current element add it to
        // our current sum and increment count by 1
        var pick = waysutil(index - 1, sum + arr[index], count + 1, arr, K);
        var total = pick + dontpick;

        // Store the value for the current function
        dp[index][sum][count] = total;
        return total;
    }

    // Function to return the number of ways
    function ways(N , K,  arr) {
        var Arr = [];

        // Push -1 at the beginning to
        // make it 1-based indexing
        Arr.push(-1);
        for (i = 0; i < N; ++i) {
            Arr.push(arr[i]);
        }

        // Initialize dp array by -1
        for (i = 0; i < MAX_INDEX; i++) {
            for (j = 0; j < MAX_SUM; j++) {
                for (l = 0; l < MAX_INDEX; l++) {
                    dp[i][j][l] = -1;
                }
            }
        }

        // Call recursive function
        // waysutil to calculate total ways
        var answer = waysutil(N, 0, 0, Arr, K);
        return answer;
    }

    // Driver code

        var arr = [ 3, 6, 2, 8, 7, 6, 5, 9 ];
        var N = arr.length;
        var K = 5;
        document.write(ways(N, K, arr));

// This code contributed by gauravrajput1
</script>
```

****Output:** 

```
19
```**