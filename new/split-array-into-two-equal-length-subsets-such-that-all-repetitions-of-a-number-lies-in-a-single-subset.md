# 将数组拆分为两个相等长度的子集，其中一个数字的所有重复都位于单个子集中

> 原文：[https://www.geeksforgeeks.org/split-array-into-two-equal-length-subsets-such-that-all-repetitions-of-a-number-lies-in-a-single-subset/](https://www.geeksforgeeks.org/split-array-into-two-equal-length-subsets-such-that-all-repetitions-of-a-number-lies-in-a-single-subset/)

给定由 `N`个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，任务是检查是否有可能将整数分成两个等长的子集，以便任何数组元素的重复都属于同一子集。 如果发现是真的，则打印`Yes`。 否则，打印`No`。

**示例**：

> **输入**：`arr[] = {2, 1, 2, 3}`
> **输出**：`Yes`
> **说明**：
> 一种数组分割的可能方式是`{1, 3}`和`{2, 2}`。
> 
> **输入**：`arr [] = {1, 1, 1, 1}`
> **输出**：`No`

**朴素的方法**：解决该问题的最简单方法是尝试将数组分为两个相等子集的所有可能组合。 对于每个组合，检查每个重复是否仅属于两个集合之一。 如果发现是真的，则打印`Yes`。 否则，打印`No`。

**时间复杂度**：`O(2 ^ N`，其中`N`是给定整数的大小。

**辅助空间**：`O(n)`。

**有效方法**：可以通过将[给定数组](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的所有元素的频率存储在数组`freq[]`中来优化上述方法。 为了将元素分为两个相等的集合，每个集合中必须存在`N / 2`个元素。 因此，要将给定数组`arr[]`分为`2`个相等的部分，`freq[]`中必须有一些总和为`N / 2`的整数子集。 请按照以下步骤解决问题：

1.  将每个元素的频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) `M`中。

2.  现在，创建一个辅助数组`aux[]`并将所有从`Map`存储的频率插入其中。

3.  给定的问题简化为[在数组`aux[]`中找到具有给定总和`N / 2`的子集](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)。

4.  如果在上述步骤中存在任何此类子集，请打印`Yes`。 否则，打印`No`。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach 
import java.io.*; 
import java.util.*; 

class GFG { 

    // Function to create the frequency 
    // array of the given array arr[] 
    private static int[] findSubsets(int[] arr) 
    { 

        // Hashmap to store the frequencies 
        HashMap<Integer, Integer> M 
            = new HashMap<>(); 

        // Store freq for each element 
        for (int i = 0; i < arr.length; i++) { 
            M.put(arr[i], 
                  M.getOrDefault(arr[i], 0) + 1); 
        } 

        // Get the total frequencies 
        int[] subsets = new int[M.size()]; 
        int i = 0; 

        // Store frequencies in subset[] array 
        for ( 
            Map.Entry<Integer, Integer> playerEntry : 
            M.entrySet()) { 
            subsets[i++] 
                = playerEntry.getValue(); 
        } 

        // Return frequency array 
        return subsets; 
    } 

    // Function to check is sum N/2 can be 
    // formed using some subset 
    private static boolean
    subsetSum(int[] subsets, 
              int target) 
    { 

        // dp[i][j] store the answer to 
        // form sum j using 1st i elements 
        boolean[][] dp 
            = new boolean[subsets.length 
                          + 1][target + 1]; 

        // Initialize dp[][] with true 
        for (int i = 0; i < dp.length; i++) 
            dp[i][0] = true; 

        // Fill the subset table in the 
        // bottom up manner 
        for (int i = 1; 
             i <= subsets.length; i++) { 

            for (int j = 1; 
                 j <= target; j++) { 
                dp[i][j] = dp[i - 1][j]; 

                // If curren element is 
                // less than j 
                if (j >= subsets[i - 1]) { 

                    // Update current state 
                    dp[i][j] 
                        |= dp[i - 1][j 
                                     - subsets[i - 1]]; 
                } 
            } 
        } 

        // Return the result 
        return dp[subsets.length][target]; 
    } 

    // Function to check if the given 
    // array can be split into required sets 
    public static void
    divideInto2Subset(int[] arr) 
    { 
        // Store frequencies of arr[] 
        int[] subsets = findSubsets(arr); 

        // If size of arr[] is odd then 
        // print "Yes" 
        if ((arr.length) % 2 == 1) { 
            System.out.println("No"); 
            return; 
        } 

        // Check if answer is true or not 
        boolean isPossible 
            = subsetSum(subsets, 
                        arr.length / 2); 

        // Print the result 
        if (isPossible) { 
            System.out.println("Yes"); 
        } 
        else { 
            System.out.println("No"); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Given array arr[] 
        int[] arr = { 2, 1, 2, 3 }; 

        // Function Call 
        divideInto2Subset(arr); 
    } 
} 

```

**输出**：

```
Yes

```

**时间复杂度**：`O(N * M)`，其中`N`是数组的大小，`M`是给定数组中不同元素的总数。

**辅助空间**：`O(n)`。



* * *

* * *



