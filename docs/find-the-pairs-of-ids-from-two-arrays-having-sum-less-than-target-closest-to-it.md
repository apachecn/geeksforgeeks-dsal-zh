# 从两个数组中找出和小于最接近的目标的 id 对

> 原文:[https://www . geeksforgeeks . org/从两个数组中找到最接近它的小于目标的 id 对/](https://www.geeksforgeeks.org/find-the-pairs-of-ids-from-two-arrays-having-sum-less-than-target-closest-to-it/)

给定两个尺寸分别为 **N** 和 **M** 的形式为 **{ID，value}** 的对的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr 1【】**和**arr 2【】**，以及一个整数**目标**，任务是从两个阵列中找到所有对的**ID**，使得对的值之和最大，并且最多具有值**M**

**示例:**

> **输入:** arr1[] = [[1，2000]，[2，3000]，[3，2000]]，arr2[] = [[1，2500]，[2，3000]，[3，3000]]，target = 6000
> **输出:**
> 2 2
> 2 3
> **解释:**
> 以下是来自两个数组 arr1[]和的元素对
> 
> *   **(arr1[2]，arr2[2]):** 元素 3000 + 3000 = 6000(=目标)之和，最接近值目标。将标识打印为(2，2)。
> *   **(arr1[2]，arr2[3]):** 元素 3000 + 3000 = 6000(=目标)之和，最接近值目标。将标识打印为(2，3)。
> 
> **输入:** arr1[] = [[1，2000]，[2，3000]，[3，2000]]，arr2[] = [[1，3000]，[2，3000]]，目标= 5500
> T3】输出:T5】1 1 1
> 1 2
> 3 1
> 3 2

**方法:**使用[树形图数据结构](https://www.geeksforgeeks.org/treemap-in-java/)存储数组元素**arr 1【】**并高效地为另一个数组**arr 2【】**中的每个元素找到配对，就可以解决给定的问题。以下是步骤:

*   创建一个树形图，其中键是数组元素的值，值是**标识列表**。
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr1[]** ，并将其元素插入树形图。
*   初始化一个变量，说 **closestTarget** 来跟踪最接近**目标**的值，并且不超过它。
*   初始化一个[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/) **结果**来存储所有可能的 id 对。
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr2[]** ，并为每个元素计算要在树形图中搜索的剩余值。
    *   如果剩余值，比如**(target–arr 2[I])**小于 **0** ，则不能形成对，所以[继续迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   使用树状图的[钻取键()功能找到小于或等于剩余值的值。如果上述函数的返回值为**空**，则找不到对应的元素。](https://www.geeksforgeeks.org/treemap-floorkey-in-java-with-examples/)
    *   如果返回值，说**当前目标**大于**关闭目标**，然后更新**关闭目标**并将数组列表**结果【】**重新初始化为新列表。
    *   遍历关键字为 **currentTarget** 的 id 列表，将所有可能的 id 对组合添加到**结果**列表中。
*   完成上述步骤后，打印数组列表**结果[]** 中存储的所有 id 对。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find pairs of ids with
    // sum of values closest to the target
    // but not exceeding the target
    public static void closestPair(
        int[][] arr1, int[][] arr2, int target)
    {

        // Initialize TreeMap having array
        // element value as key and list of
        // ids as value in the TreeMap
        TreeMap<Integer, List<Integer> > valueToIds
            = new TreeMap<>();

        // list to store all answer pairs
        List<int[]> result = new ArrayList<>();

        // Keeps the track of maximum sum
        // of pair values not exceeding target
        int closestTarget = 0;

        // Iterate through the array arr1 and
        // add all elements in the TreeMap
        for (int[] a : arr1) {

            int val = a[1], id = a[0];
            valueToIds.putIfAbsent(
                val, new ArrayList<>());
            valueToIds.get(val).add(id);
        }

        for (int[] b : arr2) {

            // Find the corresponding value
            // to be found
            int remaining = target - b[1];

            if (remaining < 0)
                continue;

            // Find a value which is close to
            // desired value, not exceeding it
            Integer floor = valueToIds.floorKey(
                remaining);

            // No value found which is less
            // than or equal to floor
            if (floor == null)
                continue;

            int currentTarget = b[1] + floor;

            if (currentTarget >= closestTarget) {
                if (currentTarget > closestTarget) {

                    // Update closeTarget and reset
                    // result list
                    closestTarget = currentTarget;
                    result = new ArrayList<>();
                }

                // Add all possible pairs in
                // result list
                for (int id : valueToIds.get(floor))
                    result.add(
                        new int[] { id, b[0] });
            }
        }

        // Print all the id pairs
        for (int[] ans : result) {
            System.out.println(
                ans[0] + " " + ans[1]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] arr1
            = { { 1, 2000 }, { 2, 3000 }, { 3, 2000 } };
        int[][] arr2 = { { 1, 3000 },
                         { 2, 3000 } };
        int target = 5500;

        closestPair(arr1, arr2, target);
    }
}
```

**Output:**

```
1 1
3 1
1 2
3 2

```

***时间复杂度:**O(N * log N+M)*
T5**辅助空间:** O(N*M)