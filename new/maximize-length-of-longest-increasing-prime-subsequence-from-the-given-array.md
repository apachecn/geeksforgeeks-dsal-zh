# 最大化给定数组

> 原文：[https://www.geeksforgeeks.org/maximize-length-of-longest-increasing-prime-subsequence-from-the-given-array/](https://www.geeksforgeeks.org/maximize-length-of-longest-increasing-prime-subsequence-from-the-given-array/)

中最长增加的素子序列的长度

给定大小为 **N** 的数组 **arr []** ，任务是通过执行以下操作来找到[最长增加素数子序列](https://www.geeksforgeeks.org/length-of-longest-prime-subsequence-in-an-array/)的长度。

*   如果 **arr [i]** 已经是[质数](https://www.geeksforgeeks.org/prime-numbers/)，则无需更新 **arr [i]** 。

*   将非质数 **arr [i]** 更新为小于 **arr [i]** 的最接近质数。

*   将非素数 **arr [i]** 更新为大于 **arr [i]** 的最接近素数。

**示例**：

> **输入**：arr [] = {8，6，9，2，5}
> **输出**：2
> **说明**：
> 可能 数组的重排为：{{7，5，2，5}，{7，7，2，5}，{11，5，2，5}，{1，7，2，5}}。
> 因此，最长递增的主要子序列的长度= 2。
> 
> **输入**：arr [] = {27，38，43，68，83，12，69，12}
> **输出**：5

**朴素的方法**：最简单的方法是将给定数组的所有元素更新为最接近的较小素数或最接近的较大素数，然后[生成给定数组的所有可能子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/) 排列并按升序打印由[质数](https://www.geeksforgeeks.org/prime-numbers/)组成的最长子序列的长度。

**时间复杂度**：O（2 <sup>N</sup> ）

**辅助空间**：`O(n)`

**高效方法**：的想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法来优化上述方法。 此问题是[最长增加质数子序列（LIPS）问题](https://www.geeksforgeeks.org/length-of-longest-increasing-prime-subsequence-from-a-given-array/)的基本变体。 请按照以下步骤解决问题。

1.  初始化[二维](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)数组，例如 **dp [] []** ，大小为 **N * 2** ，其中 **dp [i] [0]** 通过选择小于 **i <sup>th</sup>** 索引和 **dp []的 **arr [i]** 的最接近素数来存储最长增长素数子序列的长度。 i] [1]** 通过选择大于或等于 **i <sup>th</sup>** 索引处的 arr [i]的最接近质数来存储最长递增质数子序列的长度。 下面是递归关系：

    > *   如果最接近较小的素数与 arr [j] <最接近较小的素数与 arr [i]：dp [i] [0] = 1 + dp [j] [0]

    > *   如果最接近素数的值大于或等于 arr [j] <最接近素数的值最接近 arr [i]：dp [i] [0] = max（ dp [i] [0]，1 + dp [j] [1]）

    > *   如果最接近较小的素数与 arr [j] <最接近较小的素数与 arr [i]：dp [i ] [1] = 1 + dp [j] [0]

    > *   如果最接近或等于素数的素数等于 arr [j] <最接近或等于素数的素数，等于或等于 arr [i]：dp [ i] [1] = max（dp [i] [1]，1 + dp [j] [1]）

    > 

    > 这里 j 的值= 0，1，…，（i-1 ）

2.  使用 Eratosthenes 的[筛网有效地计算](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素数](https://www.geeksforgeeks.org/prime-numbers/)。

3.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr []** ，对于每个索引 **i** ，将 **arr [i]** 更新为最接近**的质数 ] arr [i]** 。

4.  对于每个索引 **i** ，最佳地找到以 **i** 结尾的最长递增质数子序列的长度。

5.  最后，返回最长的素数子序列的长度。

下面是上述方法的实现：

## Java

```java

// Java Program to implement 
// the above approach 

import java.util.*; 

public class Main { 

    // Stores the closest prime 
    // number for each array element 
    static TreeSet<Integer> set 
        = new TreeSet<>(); 

    // Function to find the length of longest 
    // increasing prime subsequence 
    public static int LIPS(int arr[], int N) 
    { 
        // Base case 
        if (arr.length == 0) 
            return 0; 

        int dp[][] = new int[N + 1][2]; 

        // Store the length of the longest 
        // increasing prime subsequence 
        int max_subsequence = 0; 
        for (int i = 0; i < arr.length; 
             i++) { 
            // Store the length of LIPS 
            // by choosing the closest prime 
            // number smaller than arr[i] 
            dp[i][0] = (arr[i] >= 2) ? 1 : 0; 

            // Store the length of longest LIPS 
            // by choosing the closest prime 
            // number greater than arr[i] 
            dp[i][1] = 1; 
            for (int j = 0; j < i; j++) { 

                // Store closest smaller 
                // prime number 
                Integer option1 = set.floor(arr[j]); 

                // Store closest prime number 
                // greater or equal 
                Integer option2 = set.ceiling(arr[j]); 

                // Recurrence relation 

                // Fill the value of dp[i][0] 
                if (option1 != null
                    && option1 < set.floor(arr[i])) 
                    dp[i][0] 
                        = Math.max(dp[i][0], dp[j][0] + 1); 

                if (option2 != null
                    && option2 < set.floor(arr[i])) 
                    dp[i][0] 
                        = Math.max(dp[i][0], dp[j][1] + 1); 

                // Fill the value of dp[i][1] 
                if (option1 != null
                    && option1 < set.ceiling(arr[i])) 
                    dp[i][1] 
                        = Math.max(dp[i][0], dp[j][0] + 1); 

                if (option2 != null
                    && option2 < set.ceiling(arr[i])) 
                    dp[i][1] 
                        = Math.max(dp[i][1], dp[j][1] + 1); 
            } 

            // Store the length of the longest 
            // increasing prime subsequence 
            max_subsequence 
                = Math.max(max_subsequence, dp[i][0]); 

            max_subsequence 
                = Math.max(max_subsequence, dp[i][1]); 
        } 

        return max_subsequence; 
    } 

    // Function to generate all prime numbers 
    public static void prime_sieve() 
    { 
        // Store all prime numbers 
        boolean primes[] 
            = new boolean[1000000 + 5]; 

        // Consider all prime numbers 
        // to be true initially 
        Arrays.fill(primes, true); 

        // Mark 0 and 1 non-prime 
        primes[0] = primes[1] = false; 

        // Set all even numbers to 
        // non-prime 
        for (int i = 4; i <= 1000000; 
             i += 2) 
            primes[i] = false; 

        for (int i = 3; i <= 1000000; 
             i += 2) { 

            // If current element is prime 
            if (primes[i]) { 

                // Update all its multiples 
                // as non-prime 
                for (int j = 2 * i; j <= 1000000; 
                     j += i) 
                    primes[j] = false; 
            } 
        } 

        // Mark 2 as prime 
        set.add(2); 

        // Add all primes to the set 
        for (int i = 3; i <= 1000000; 
             i += 2) 
            if (primes[i]) 
                set.add(i); 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        int N = 6; 
        int arr[] = { 6, 7, 8, 9, 10, 11 }; 

        prime_sieve(); 

        System.out.println(LIPS(arr, N)); 
    } 
} 

```

**Output:**

```
3

```

**时间复杂度**：O（N <sup>2</sup> logN）

**辅助空间**：`O(n)`



* * *

* * *



