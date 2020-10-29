# 对的总数为 2 的幂| 设置 2

> 原文：[https://www.geeksforgeeks.org/number-of-pairs-whose-sum-is-a-power-of-2-set-2/](https://www.geeksforgeeks.org/number-of-pairs-whose-sum-is-a-power-of-2-set-2/)

给定由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，任务是计算对数**（arr [i]，arr [j]）**，使得 **arr [i] + arr [j]** 是[的 2](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 次方。

**示例**：

> **输入**：arr [] = {1，-1、2、3}
> **输出**：5
> **说明**：（1、1） ，（2、2），（1、3），（-1、3），（-1、2）是有效对，其和为 2 的幂。
> 
> **输入**：arr [] = {1，1，1}
> **输出**：6

**朴素的方法**：解决该问题的最简单方法是[从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)生成所有可能的对，并且对于每对，[检查该对的和是否是幂 是否为 2](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 。

***时间复杂度**：O（N <sup>2</sup> ）

**辅助空间**：`O(1)`*

**有效方法**：可以使用 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 优化上述方法。 请按照以下步骤解决问题：

*   创建 **[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)** ，以存储数组 **arr []** 的每个元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

*   初始化变量**和**以存储总和等于 2 的任何**幂的对的计数。**

*   遍历范围 **[0，31]** 并生成 2 的所有幂，即 **2 <sup>0</sup>** 至 **2 <sup>31</sup> [** 。

*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，每产生 2 次幂，并检查 **map [key-arr [j]]** 是否存在，其中**键**等于[ **2 <sup>i</sup>** 。

*   如果发现是真的，则将**计数**增加 **map [key – arr [j]]** ，成对**（arr [j]，key – arr [j ]）**的和等于**的 2 幂。**

*   最后，打印 **count / 2** 作为所需答案。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to count all pairs 
// whose sum is a power of two 
int countPair(int arr[], int n) 
{ 
    // Stores the frequency of 
    // each element of the array 
    map<int, int> m; 

    // Update frequency of 
    // array elements 
    for (int i = 0; i < n; i++) 
        m[arr[i]]++; 

    // Stores count of 
    // required pairs 
    int ans = 0; 

    for (int i = 0; i < 31; i++) { 

        // Current power of 2 
        int key = pow(2, i); 

        // Traverse the array 
        for (int j = 0; j < n; j++) { 

            int k = key - arr[j]; 

            // If pair does not exist 
            if (m.find(k) == m.end()) 
                continue; 

            // Increment count of pairs 
            else
                ans += m[k]; 

            if (k == arr[j]) 
                ans++; 
        } 
    } 

    // Return the count of pairs 
    return ans / 2; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 1, 8, 2, 10, 6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << countPair(arr, n) << endl; 

    return 0; 
}

```

## Java

```java

// Java program for above approach 
import java.util.*; 

class GFG { 
    // Function to count all pairs 
    // whose sum is power of two 
    static int countPair(int[] arr, int n) 
    { 
        // Stores the frequency of 
        // each element of the array 
        Map<Integer, Integer> m 
            = new HashMap<>(); 

        // Update the frequency of 
        // array elements 
        for (int i = 0; i < n; i++) 
            m.put(arr[i], m.getOrDefault( 
                              arr[i], 0) 
                              + 1); 

        // Stores the count of pairs 
        int ans = 0; 

        // Generate powers of 2 
        for (int i = 0; i < 31; i++) { 

            // Generate current power of 2 
            int key = (int)Math.pow(2, i); 

            // Traverse the array 
            for (int j = 0; j < arr.length; 
                 j++) { 

                int k = key - arr[j]; 

                // Increase ans by m[k], if 
                // pairs with sum 2^i exists 
                ans += m.getOrDefault(k, 0); 

                // Increase ans again if k = arr[j] 
                if (k == arr[j]) 
                    ans++; 
            } 
        } 

        // Return count of pairs 
        return ans / 2; 
    } 

    // Driver function 
    public static void main(String[] args) 
    { 
        int[] arr = { 1, -1, 2, 3 }; 
        int n = arr.length; 
        System.out.println(countPair(arr, n)); 
    } 
}

```

**Output:**

```
5

```

**时间复杂度**：`O(NlogN)`

**辅助空间**：`O(1)`



* * *

* * *



