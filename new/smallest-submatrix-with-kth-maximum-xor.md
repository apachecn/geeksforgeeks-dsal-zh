# 最小子矩阵，XOR 最大为 Kth

给定尺寸为 **N×M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **m [] []** 和整数 **K** ，计算 **XOR（i， j）对于矩阵的每个索引，它等于从索引**（1，1）到（i，j））**的子矩阵所有元素的[按位 Xor 或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 。 任务是找到具有 **K** <sup>th</sup> 最大 **XOR（i ，j）**值。 如果存在多个此类子矩阵，则打印最小的子矩阵。
***注意：**考虑（1，1）中矩阵的起始索引。***

**示例：**

> **输入：** m [] [] = {{1，2}，{2，3}}，K = 2
> **输出：** 1 2
> **说明：**
> XOR（1，1）：m [1] [1] = 1
> XOR（1，2）：m [1] [1] xor m [1] [2] = 3
> XOR（2，1）：m [1] [1] xor m [2] [1] = 3
> XOR（2，2）：m [1] [1] xor m [1] [2] xor m [2] [1] xor m [2] [2] = 2
> 因此，第二个最大值在位置[1，2]为 3。
> 
> **输入：** m [] [] = {{1，2，3}，{2，2，1}，{2，4，2}}，k = 1
> **输出 ：** 3 2

**方法：**的想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)查找 XOR（i，j）。

*   按 xor [i] [j] = xor [i-1] [j] ^ xor [i] [j-1] ^ xor [i-1] [j-1] ^计算按位 XOR（i，j） m [i] [j]。
*   将针对各个索引**（i，j）**获得的 **XOR（i，j）**值存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   使用大小为 **K** 的[最小堆](https://www.geeksforgeeks.org/min-heap-in-java/)，找到所有 XOR（i，j）值的第 K <sup>个第</sup>个最大值。
*   查找最小索引**（i，j）**，对于该索引， **XOR（i，j）**等于 **K** <sup>th</sup> 最大值。 以上步骤使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。

下面是上述方法的实现：

## 爪哇

```

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

***时间复杂度：** O（N * M * log K）*
***辅助空间：** O（N * M）*

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。