# 所有子集平均值之和

> 原文:[https://www.geeksforgeeks.org/sum-average-subsets/](https://www.geeksforgeeks.org/sum-average-subsets/)

给定一个由 N 个整数元素组成的数组，任务是找出这个数组所有子集的平均值之和。

**示例:**

```
Input  : arr[] = [2, 3, 5]
Output : 23.33 
Explanation : Subsets with their average are, 
[2]        average = 2/1 = 2
[3]        average = 3/1 = 3
[5]        average = 5/1 = 5
[2, 3]        average = (2+3)/2 = 2.5
[2, 5]        average = (2+5)/2 = 3.5
[3, 5]        average = (3+5)/2 = 4
[2, 3, 5]    average = (2+3+5)/3 = 3.33

Sum of average of all subset is, 
2 + 3 + 5 + 2.5 + 3.5 + 4 + 3.33 = 23.33 
```

一个天真的解决方案是迭代所有可能的子集，获得所有子集的平均值，然后逐个添加它们，但这将花费指数时间，并且对于更大的数组是不可行的。
我们可以通过举个例子得到一个模式，

```
arr = [a0, a1, a2, a3]
sum of average = 
a0/1 + a1/1 + a2/2 + a3/1 +
(a0+a1)/2 + (a0+a2)/2 + (a0+a3)/2 + (a1+a2)/2 +
 (a1+a3)/2 + (a2+a3)/2 + 
(a0+a1+a2)/3 + (a0+a2+a3)/3 + (a0+a1+a3)/3 + 
 (a1+a2+a3)/3 +
(a0+a1+a2+a3)/4

If S = (a0+a1+a2+a3), then above expression 
can be rearranged as below,
sum of average = (S)/1 + (3*S)/2 + (3*S)/3 + (S)/4
```

带记数器的系数可以解释如下，假设我们迭代具有 K 个元素的子集，那么分母将是 K，分子将是 r*S，其中“r”表示在迭代相同大小的子集时特定数组元素被添加的次数。通过检查，我们可以看到 r 将是 nCr(N–1，N–1)，因为在将一个元素放入求和后，我们需要从(N–1)个元素中选择(N–1)个元素，因此在考虑相同大小的子集时，每个元素都将具有 nCr(N–1，N–1)的频率，因为所有元素都以相等的次数参与求和，这也将是 S 的频率，并且将是最终表达式中的分子。
在下面的代码中 [nCr 是使用动态编程方法](https://www.geeksforgeeks.org/dynamic-programming-set-9-binomial-coefficient/)实现的，你可以在这里阅读更多相关内容，

## C++

```
// C++ program to get sum of average of all subsets
#include <bits/stdc++.h>
using namespace std;

// Returns value of Binomial Coefficient C(n, k)
int nCr(int n, int k)
{
    int C[n + 1][k + 1];
    int i, j;

    // Calculate value of Binomial Coefficient in bottom
    // up manner
    for (i = 0; i <= n; i++) {
        for (j = 0; j <= min(i, k); j++) {
            // Base Cases
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Calculate value using previously stored
            // values
            else
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
        }
    }
    return C[n][k];
}

// method returns sum of average of all subsets
double resultOfAllSubsets(int arr[], int N)
{
    double result = 0.0; // Initialize result

    // Find sum of elements
    int sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];

    // looping once for all subset of same size
    for (int n = 1; n <= N; n++)

        /* each element occurs nCr(N-1, n-1) times while
           considering subset of size n  */
        result += (double)(sum * (nCr(N - 1, n - 1))) / n;

    return result;
}

// Driver code to test above methods
int main()
{
    int arr[] = { 2, 3, 5, 7 };
    int N = sizeof(arr) / sizeof(int);
    cout << resultOfAllSubsets(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to get sum of
// average of all subsets
import java.io.*;

class GFG {

    // Returns value of Binomial
    // Coefficient C(n, k)
    static int nCr(int n, int k)
    {
        int C[][] = new int[n + 1][k + 1];
        int i, j;

        // Calculate value of Binomial
        // Coefficient in bottom up manner
        for (i = 0; i <= n; i++) {
            for (j = 0; j <= Math.min(i, k); j++) {
                // Base Cases
                if (j == 0 || j == i)
                    C[i][j] = 1;

                // Calculate value using
                // previously stored values
                else
                    C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
            }
        }
        return C[n][k];
    }

    // method returns sum of average of all subsets
    static double resultOfAllSubsets(int arr[], int N)
    {
        // Initialize result
        double result = 0.0;

        // Find sum of elements
        int sum = 0;
        for (int i = 0; i < N; i++)
            sum += arr[i];

        // looping once for all subset of same size
        for (int n = 1; n <= N; n++)

            /* each element occurs nCr(N-1, n-1) times while
            considering subset of size n */
            result += (double)(sum * (nCr(N - 1, n - 1))) / n;

        return result;
    }

    // Driver code to test above methods
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 5, 7 };
        int N = arr.length;
        System.out.println(resultOfAllSubsets(arr, N));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to get sum
# of average of all subsets

# Returns value of Binomial
# Coefficient C(n, k)
def nCr(n, k):

    C = [[0 for i in range(k + 1)]
            for j in range(n + 1)]

    # Calculate value of Binomial
    # Coefficient in bottom up manner
    for i in range(n + 1):

        for j in range(min(i, k) + 1):

            # Base Cases
            if (j == 0 or j == i):
                C[i][j] = 1

            # Calculate value using
            # previously stored values
            else:
                C[i][j] = C[i-1][j-1] + C[i-1][j]

    return C[n][k]

# Method returns sum of
# average of all subsets
def resultOfAllSubsets(arr, N):

    result = 0.0 # Initialize result

    # Find sum of elements
    sum = 0
    for i in range(N):
        sum += arr[i]

    # looping once for all subset of same size
    for n in range(1, N + 1):

        # each element occurs nCr(N-1, n-1) times while
        # considering subset of size n */
        result += (sum * (nCr(N - 1, n - 1))) / n

    return result

# Driver code
arr = [2, 3, 5, 7]
N = len(arr)
print(resultOfAllSubsets(arr, N))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to get sum of
// average of all subsets
using System;

class GFG {

    // Returns value of Binomial
    // Coefficient C(n, k)
    static int nCr(int n, int k)
    {
        int[, ] C = new int[n + 1, k + 1];
        int i, j;

        // Calculate value of Binomial
        // Coefficient in bottom up manner
        for (i = 0; i <= n; i++) {
            for (j = 0; j <= Math.Min(i, k); j++)
            {
                // Base Cases
                if (j == 0 || j == i)
                    C[i, j] = 1;

                // Calculate value using
                // previously stored values
                else
                    C[i, j] = C[i - 1, j - 1] + C[i - 1, j];
            }
        }
        return C[n, k];
    }

    // method returns sum of average
    // of all subsets
    static double resultOfAllSubsets(int[] arr, int N)
    {
        // Initialize result
        double result = 0.0;

        // Find sum of elements
        int sum = 0;
        for (int i = 0; i < N; i++)
            sum += arr[i];

        // looping once for all subset
        // of same size
        for (int n = 1; n <= N; n++)

            /* each element occurs nCr(N-1, n-1) times while
               considering subset of size n */
            result += (double)(sum * (nCr(N - 1, n - 1))) / n;

        return result;
    }

    // Driver code to test above methods
    public static void Main()
    {
        int[] arr = { 2, 3, 5, 7 };
        int N = arr.Length;
        Console.WriteLine(resultOfAllSubsets(arr, N));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get sum
// of average of all subsets

// Returns value of Binomial
// Coefficient C(n, k)
function nCr($n, $k)
{
    $C[$n + 1][$k + 1] = 0;
    $i; $j;

    // Calculate value of Binomial
    // Coefficient in bottom up manner
    for ($i = 0; $i <= $n; $i++)
    {
        for ($j = 0; $j <= min($i, $k); $j++)
        {
            // Base Cases
            if ($j == 0 || $j == $i)
                $C[$i][$j] = 1;

            // Calculate value using
            // previously stored values
            else
                $C[$i][$j] = $C[$i - 1][$j - 1] +
                             $C[$i - 1][$j];
        }
    }
    return $C[$n][$k];
}

// method returns sum of
// average of all subsets
function resultOfAllSubsets($arr, $N)
{
    // Initialize result
    $result = 0.0;

    // Find sum of elements
    $sum = 0;
    for ($i = 0; $i < $N; $i++)
        $sum += $arr[$i];

    // looping once for all
    // subset of same size
    for ($n = 1; $n <= $N; $n++)

        /* each element occurs nCr(N-1,
        n-1) times while considering
        subset of size n */
        $result += (($sum * (nCr($N - 1,
                                 $n - 1))) / $n);

    return $result;
}

// Driver Code
$arr = array( 2, 3, 5, 7 );
$N = sizeof($arr) / sizeof($arr[0]);
echo resultOfAllSubsets($arr, $N) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // javascript program to get sum of
    // average of all subsets

    // Returns value of Binomial
    // Coefficient C(n, k)
    function nCr(n, k)
    {
        let C = new Array(n + 1);
        for (let i = 0; i <= n; i++)
        {
            C[i] = new Array(k + 1);
            for (let j = 0; j <= k; j++)
            {
                C[i][j] = 0;
            }
        }
        let i, j;

        // Calculate value of Binomial
        // Coefficient in bottom up manner
        for (i = 0; i <= n; i++) {
            for (j = 0; j <= Math.min(i, k); j++) {
                // Base Cases
                if (j == 0 || j == i)
                    C[i][j] = 1;

                // Calculate value using
                // previously stored values
                else
                    C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
            }
        }
        return C[n][k];
    }

    // method returns sum of average of all subsets
    function resultOfAllSubsets(arr, N)
    {
        // Initialize result
        let result = 0.0;

        // Find sum of elements
        let sum = 0;
        for (let i = 0; i < N; i++)
            sum += arr[i];

        // looping once for all subset of same size
        for (let n = 1; n <= N; n++)

            /* each element occurs nCr(N-1, n-1) times while
            considering subset of size n */
            result += (sum * (nCr(N - 1, n - 1))) / n;

        return result;
    }

    let arr = [ 2, 3, 5, 7 ];
    let N = arr.length;
    document.write(resultOfAllSubsets(arr, N));

</script>
```

**输出:**

```
63.75
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。