# 给定大小的所有子集之和(=K)

> 原文:[https://www . geesforgeks . org/给定大小的所有子集之和/](https://www.geeksforgeeks.org/sum-of-all-subsets-of-a-given-size/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出大小为 **K** 的所有[子集](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)的和。

**示例:**

> **输入:** arr[] = {1，2，4，5}，K = 2
> **输出:** 36
> **解释:**
> 大小为 K(= 2)的子集为= {1，2}、{1，4}、{1，5}、{2，4}、{2，5}、{4，5}。现在，所有子集总和总和= 3 + 5 + 6 + 6 + 7 + 9 = 36。
> 
> **输入:** arr[] = {2，4，5，6，8}，K = 3
> T3】输出: 150

**天真方法:**解决给定问题的最简单方法是[生成给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的所有可能子集，并找到那些大小为 **K** 的子集的[元素之和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。找到所有 **K 个大小子集**的总和后，打印得到的所有总和的总和作为结果。

***时间复杂度:**O(K * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**通过观察求和序列中每个元素**arr【I】**的出现次数取决于 N 和 k 的值，也可以优化上述方法

让我们找出求和级数中一般元素 x 的出现:

*   x 在所有大小的求和序列中的出现=k 个子集= <sup>n-1</sup> C <sub>k-1</sub>

因此，arr[]的每个元素的频率在求和公式中是相同的= <sup>n-1</sup> C <sub>k-1</sub> 。因此，所有子集的和=(数组所有元素的和)* <sup>n-1</sup> C <sub>k-1</sub> 。

按照以下步骤解决给定的问题:

*   初始化变量，将 **freq** 设为 0，计算 <sup>n-1</sup> C <sub>k-1</sub>
*   初始化变量，将**和**设为 **0** 来存储所有数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   执行上述步骤后，打印**总和*freq** 的值作为结果总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of all
// sub-sets of size K
void findSumOfAllSubsets(int arr[], int n, int k)
{

    // Frequency of each array element
    // in summation equation.
    int factorial_N=1, factorial_d=1, factorial_D=1;

    //calculate factorial of n-1
    for(int i=1; i<=n-1; i++)
      factorial_N*=i;
    //calculate factorial of k-1
    for(int i=1; i<=k-1; i++)
      factorial_d*=i;
    //calculate factorial of n-k
    for(int i=1; i<=n-k; i++)
      factorial_D*=i;

    int freq = factorial_N/(factorial_d * factorial_D);

    // Calculate sum of array.
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Sum of all subsets of size k.
    sum = sum * freq;

    cout <<"Sum of all subsets of size = "<<k<<" is => "<< sum << endl;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 4, 5 };
    int n = 4, k = 2;

    findSumOfAllSubsets(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG
{

    // Function to find the sum of all
    // sub-sets of size K
    static void findSumOfAllSubsets(int[] arr, int n, int k)
    {

        // Frequency of each array element
        // in summation equation.
        int factorial_N = 1, factorial_d = 1,
            factorial_D = 1;

        // calculate factorial of n-1
        for (int i = 1; i <= n - 1; i++)
            factorial_N *= i;

        // calculate factorial of k-1
        for (int i = 1; i <= k - 1; i++)
            factorial_d *= i;

        // calculate factorial of n-k
        for (int i = 1; i <= n - k; i++)
            factorial_D *= i;

        int freq
            = factorial_N / (factorial_d * factorial_D);

        // Calculate sum of array.
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Sum of all subsets of size k.
        sum = sum * freq;

        System.out.println("Sum of all subsets of size = "
                           + k + " is => " + sum);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = { 1, 2, 4, 5 };
        int n = 4, k = 2;

        findSumOfAllSubsets(arr, n, k);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the sum of all
# sub-sets of size K
def findSumOfAllSubsets(arr, n, k):

    # Frequency of each array element
    # in summation equation.
    factorial_N = 1
    factorial_d = 1
    factorial_D = 1

    # calculate factorial of n-1
    for i in range(1, n, 1):
        factorial_N *= i

    # calculate factorial of k-1
    for i in range(1, k, 1):
        factorial_d *= i

    # calculate factorial of n-k
    for i in range(1, n - k + 1, 1):
        factorial_D *= i

    freq = factorial_N//(factorial_d * factorial_D)

    # Calculate sum of array.
    sum = 0
    for i in range(n):
        sum += arr[i]

    # Sum of all subsets of size k.
    sum = sum * freq
    print("Sum of all subsets of size = ",k," is =>",sum)

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 4, 5]
    n = 4
    k = 2

    findSumOfAllSubsets(arr, n, k)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the sum of all
    // sub-sets of size K
    static void findSumOfAllSubsets(int[] arr, int n, int k)
    {

        // Frequency of each array element
        // in summation equation.
        int factorial_N = 1, factorial_d = 1,
            factorial_D = 1;

        // calculate factorial of n-1
        for (int i = 1; i <= n - 1; i++)
            factorial_N *= i;
        // calculate factorial of k-1
        for (int i = 1; i <= k - 1; i++)
            factorial_d *= i;
        // calculate factorial of n-k
        for (int i = 1; i <= n - k; i++)
            factorial_D *= i;

        int freq
            = factorial_N / (factorial_d * factorial_D);

        // Calculate sum of array.
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Sum of all subsets of size k.
        sum = sum * freq;

        Console.WriteLine("Sum of all subsets of size = "
                          + k + " is => " + sum);
    }

    // Driver Code
    public static void Main()
    {

        int[] arr = { 1, 2, 4, 5 };
        int n = 4, k = 2;

        findSumOfAllSubsets(arr, n, k);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the sum of all
        // sub-sets of size K
        function findSumOfAllSubsets(arr, n, k) {

            // Frequency of each array element
            // in summation equation.
            let factorial_N = 1, factorial_d = 1, factorial_D = 1;

            // calculate factorial of n-1
            for (let i = 1; i <= n - 1; i++)
                factorial_N *= i;

            // calculate factorial of k-1
            for (let i = 1; i <= k - 1; i++)
                factorial_d *= i;

            // calculate factorial of n-k
            for (let i = 1; i <= n - k; i++)
                factorial_D *= i;

            let freq = factorial_N / (factorial_d * factorial_D);

            // Calculate sum of array.
            let sum = 0;
            for (let i = 0; i < n; i++)
                sum += arr[i];

            // Sum of all subsets of size k.
            sum = sum * freq;

            document.write("Sum of all subsets of size = " + k + " is => " + sum + "<br>");
        }

        // Driver Code
        let arr = [1, 2, 4, 5];
        let n = 4, k = 2;

        findSumOfAllSubsets(arr, n, k);

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
36
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)