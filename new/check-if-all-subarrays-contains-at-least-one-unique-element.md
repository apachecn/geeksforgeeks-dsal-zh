# 检查所有子数组是否至少包含一个唯一元素

> 原文：[https://www.geeksforgeeks.org/check-if-all-subarrays-contains-at-least-one-unique-element/](https://www.geeksforgeeks.org/check-if-all-subarrays-contains-at-least-one-unique-element/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，该数组由 **N** 个整数组成，任务是检查该数组的所有[个子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)是否至少具有一个 是否包含唯一元素。 如果发现是真的，则打印**“是”** 。 否则，打印**“否”** 。

**示例**：

> **输入**：arr [] = {1、2、1}
> **输出**：是
> **说明**：
> 对于大小为 1 的子阵列 ：{1}，{2}，{1}，条件将始终为 true。
> 对于大小为 2：{1、2}，{2、1}的子数组，每个子数组至少具有一个唯一元素。
> 对于大小为 3 = {1,2,1}的子数组，在此子数组中，我们只有 2 个唯一元素。
> 由于每个子数组都有至少一个唯一元素，因此请打印“是”。
> 
> **输入**：arr [] = {1、2、3、1、2、3}
> **输出**：否
> **说明**：
> 大小为 6 的子数组：{1、2、3、1、2、3}不包含唯一元素。 因此，打印“否”。

**天真的方法**：最简单的方法是[生成所有子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，并对每个子数组使用 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 来存储该子阵列每个元素的[频率。 如果任何子数组没有至少一个唯一元素，则打印**“否”** 。 否则，打印**“是”** 。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

下面是上述方法的实现：

## Java

```java

// Java program for above approach 

import java.util.*; 
import java.lang.*; 

class GFG { 

    // Function to check if all subarrays 
    // of array have at least one unique element 
    static String check(int arr[], int n) 
    { 
        // Stores frequency of subarray 
        // elements 
        Map<Integer, Integer> hm 
            = new HashMap<>(); 

        // Generate all subarrays 
        for (int i = 0; i < n; i++) { 

            // Insert first element in map 
            hm.put(arr[i], 1); 

            for (int j = i + 1; j < n; j++) { 

                // Update frequency of current 
                // subarray in the HashMap 
                hm.put( 
                    arr[j], 
                    hm.getOrDefault(arr[j], 0) + 1); 

                boolean flag = false; 

                // Check if at least one element 
                // occurs once in current subarray 
                for (Integer k : hm.values()) { 
                    if (k == 1) { 
                        flag = true; 
                        break; 
                    } 
                } 

                // If any subarray doesn't 
                // have unique element 
                if (!flag) 
                    return "No"; 
            } 

            // Clear map for next subarray 
            hm.clear(); 
        } 

        // Return Yes if all subarray 
        // having at least 1 unique element 
        return "Yes"; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Given array arr[] 
        int[] arr = { 1, 2, 1 }; 

        int N = arr.length; 

        // Function Call 
        System.out.println(check(arr, N)); 
    } 
} 

```

**Output:**

```
Yes

```

***时间复杂度**：O（N <sup>3</sup> ）*

***辅助空间**：`O(n)`*

**高效方法**：请按照以下步骤优化上述方法：

*   在 **[0，N – 1]** 范围内循环循环，并创建和[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，以存储当前子阵列中每个字符的频率。

*   创建一个变量**计数**，以检查子数组是否具有至少一个频率为 **1** 的元素。

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr []** ，并更新映射中每个元素的频率，并将计数更新为：

    *   如果元素的频率为 **1** ，则增加**计数**。

    *   如果元素的频率为 **2** ，则递减**计数**。

*   在上述步骤中，如果 **count** 的值为 **0** ，则打印**“否”** ，因为存在一个子数组，该子数组中没有任何唯一元素 它。

*   在所有迭代之后，如果**计数**的值始终为正，则打印**为“是”** 。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach 

import java.util.*; 
import java.lang.*; 

class GFG { 

    // Function to check if all subarrays 
    // have at least one unique element 
    static String check(int arr[], int n) 
    { 
        // Generate all subarray 
        for (int i = 0; i < n; i++) { 

            // Store frequency of 
            // subarray's elements 
            Map<Integer, Integer> hm 
                = new HashMap<>(); 

            int count = 0; 

            // Traverse the array over 
            // the range [i, N] 
            for (int j = i; j < n; j++) { 

                // Update frequency of 
                // current subarray in map 
                hm.put(arr[j], 
                       hm.getOrDefault(arr[j], 0) + 1); 

                // Increment count 
                if (hm.get(arr[j]) == 1) 
                    count++; 

                // Decrement count 
                if (hm.get(arr[j]) == 2) 
                    count--; 

                if (count == 0) 
                    return "No"; 
            } 
        } 

        // If all subarrays have at 
        // least 1 unique element 
        return "Yes"; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Given array arr[] 
        int[] arr = { 1, 2, 1 }; 
        int N = arr.length; 

        // Function Call 
        System.out.println(check(arr, N)); 
    } 
}

```

**Output:**

```
Yes

```

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：`O(n)`*



* * *

* * *



