# 最大化数组中连续减少的子序列数

给定由 **N** 个整数组成的数组 **arr []** ，任务是从满足以下条件的数组中找出**个递减子序列**的最大数量：

*   每个子序列都以其最长的形式存在。
*   子序列的相邻元素之间的差异始终为 **1** 。

**示例**：

> **输入**：arr [] = {2，1，5，4，3}
> **输出**：2
> **说明**：
> 可能 递减的子序列是{5，4，3}和{2，1}。
> 
> **输入**：arr [] = {4，5，2，1，4}
> **输出**：3
> **说明**：
> 可能 递减的子序列为{4}，{5，4}和{2，1}。

**方法**：
的想法是使用 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 解决该问题。 请按照以下步骤操作：

*   维护 **HashMap** 来存储数组元素可能的子序列数，并维护 **maxSubsequences** 来计算可能子序列的总数。
*   遍历数组，对于每个元素 **arr [i]** ，通过分配给**的计数，检查是否存在可以将 **arr [i]** 作为下一个元素的子序列。 **HashMap** 中的 arr [i]** 。
*   如果存在，请执行以下操作：
    *   将 **arr [i]** 分配为子序列的下一个元素。
    *   在 **HashMap** 中分配给 **arr [i]** 的减少计数，因为以 arr [i]作为下一个元素的可能子序列的数量减少了 **1** 。
    *   同样，在 **HashMap** 中分配给 **arr [i] – 1** 的增加计数，作为 **arr [i] – 1** 作为下一个的可能子序列数 元素增加了 **1** 。
*   否则，增加 **maxCount** ，因为需要一个新的子序列，然后重复上述步骤以修改 **HashMap** 。
*   完成数组的遍历后，打印 **maxCount** 的值。

下面是上述方法的实现：

## Java

```java

// Java program to implememt 
// the above approach 
import java.util.*; 

class GFG { 

    // Function to find the maximum number 
    // number of required subsequences 
    static int maxSubsequences(int arr[], int n) 
    { 

        // HashMap to store number of 
        // arrows available with 
        // height of arrow as key 
        HashMap<Integer, Integer> map 
            = new HashMap<>(); 

        // Stores the maximum count 
        // of possible subsequences 
        int maxCount = 0; 

        // Stores the count of 
        // possible subsequences 
        int count; 

        for (int i = 0; i < n; i++) { 

            // Check if i-th element can be 
            // part of any of the previous 
            // subsequence 
            if (map.containsKey(arr[i])) { 

                // Count  of subsequences 
                // possible with arr[i] as 
                // the next element 
                count = map.get(arr[i]); 

                // If more than one such 
                // subsequence exists 
                if (count > 1) { 

                    // Include arr[i] in a subsequence 
                    map.put(arr[i], count - 1); 
                } 

                // Otherwise 
                else
                    map.remove(arr[i]); 

                // Increase count of subsequence possible 
                // with arr[i] - 1 as the next element 
                if (arr[i] - 1 > 0) 
                    map.put(arr[i] - 1, 
                            map.getOrDefault(arr[i] - 1, 0) + 1); 
            } 
            else { 

                // Start a new subsequence 
                maxCount++; 

                // Increase count of subsequence possible 
                // with arr[i] - 1 as the next element 
                if (arr[i] - 1 > 0) 
                    map.put(arr[i] - 1, 
                            map.getOrDefault(arr[i] - 1, 0) + 1); 
            } 
        } 

        // Return the answer 
        return maxCount; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int n = 8; 
        int arr[] = { 4, 3, 4, 2, 3, 4, 2, 2 }; 
        System.out.println(maxSubsequences(arr, n)); 
    } 
} 

```

**Output:**

```
4

```

***时间复杂度**：O（N）
**辅助空间**：O（1）*



* * *

* * *



