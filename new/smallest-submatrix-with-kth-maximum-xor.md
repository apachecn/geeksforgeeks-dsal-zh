# 具有第`K`大 XOR 的最小子矩阵

> 原文：[https://www.geeksforgeeks.org/smallest-submatrix-with-kth-maximum-xor/](https://www.geeksforgeeks.org/smallest-submatrix-with-kth-maximum-xor/)

给定尺寸为`N×M`的[矩阵](https://www.geeksforgeeks.org/matrix/)`m[][]`和整数`K`， 对于矩阵的每个索引计算`XOR(i, j)`，它等于从索引`(1, 1)`到`(i, j)`的子矩阵所有元素的[按位 XOR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 。 任务是找到具有第`K`大`XOR(i, j)`值的子矩阵。 如果存在多个此类子矩阵，则打印最小的子矩阵。

**注意**：矩阵的起始索引是`(1, 1)`。

**示例**：

> **输入**：`m[][] = {{1, 2}, {2, 3}}, K = 2`
>
> **输出**：`1 2`
>
> **说明**：
>
> ```
> XOR(1, 1): m[1][1] = 1
> XOR(1, 2): m[1][1] xor m[1][2] = 3
> XOR(2, 1): m[1][1] xor m[2][1] = 3
> XOR(2, 2): m[1][1] xor m[1][2] xor m[2][1] xor m[2][2] = 2
> ```
> 
> 因此，第二个最大值在位置`[1, 2]`为 3。
> 
> **输入**：`m[][] = {{1, 2, 3}, {2, 2, 1}, {2, 4, 2}}, k = 1`
>
> **输出**：`3 2`

**方法**：的想法是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)查找`XOR(i, j)`。

*   根据`xor[i][j] = xor[i-1][j] ^ xor[i][j-1] ^ xor[i-1][j-1] ^ m[i][j]`，计算按位`XOR(i, j)`。

*   将针对各个索引`(i, j)`获得的`XOR(i, j)`值存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

*   使用大小为`K`的[最小堆](https://www.geeksforgeeks.org/min-heap-in-java/)，找到所有`XOR(i, j)`值的第`K`个最大值。

*   查找最小索引`(i, j)`，对于该索引， `XOR(i, j)`等于第`K`个最大值。 以上步骤使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。

下面是上述方法的实现：

## Java

```java

// Java Program for above approach 
import java.util.*; 
import java.lang.*; 

class GFG { 

    // Function to print smallest index of 
    // Kth maximum Xor value of submatrices 
    static void smallestPosition(int m[][], int k) 
    { 

        // Dimensions of matrix 
        int n = m.length; 
        int mm = m[0].length; 

        // Stores XOR values for every index 
        int[][] xor = new int[n][mm]; 

        // Min heap to find the 
        // kth maximum XOR value 
        PriorityQueue<Integer> minHeap 
            = new PriorityQueue<>(); 

        // Stores indices for 
        // corresponding XOR vlaues 
        Map<Integer, int[]> map 
            = new HashMap<>(); 

        // Traversing matrix to 
        // calculate XOR values 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < mm; j++) { 

                int a = i - 1 >= 0
                            ? xor[i - 1][j] 
                            : 0; 

                int b = j - 1 >= 0
                            ? xor[i][j - 1] 
                            : 0; 

                int c = (i - 1 >= 0 && j - 1 >= 0) 
                            ? xor[i - 1][j - 1] 
                            : 0; 

                xor[i][j] = m[i][j] ^ a ^ b ^ c; 

                // Insert calculated value 
                // in Min Heap 
                minHeap.add(xor[i][j]); 

                // If size exceeds k 
                if (minHeap.size() > k) { 

                    // Remove the minimum 
                    minHeap.poll(); 
                } 

                // Store smallest index 
                // containing xor[i][j] 
                if (!map.containsKey(xor[i][j])) 
                    map.put(xor[i][j], 
                            new int[] { i, j }); 
            } 
        } 

        // Stores the kth maximum element 
        int kth_max_e = minHeap.poll(); 

        // Print the required index 
        System.out.println( 
            (map.get(kth_max_e)[0] + 1) 
            + " " + (map.get(kth_max_e)[1] + 1)); 
    } 
    // Driver Code 
    public static void main(String[] args) 
    { 

        int m[][] = { { 1, 2, 3 }, 
                      { 2, 2, 1 }, 
                      { 2, 4, 2 } }; 
        int k = 1; 

        // Function call 
        smallestPosition(m, k); 
    } 
}

```

**Output:**

```
3 2

```

**时间复杂度**：`O(N * M * log K)`

**辅助空间**：`O(N * M)`



* * *

* * *



