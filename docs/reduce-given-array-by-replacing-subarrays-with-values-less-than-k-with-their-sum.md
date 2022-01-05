# 通过将值小于 K 的子阵列替换为它们的和来减少给定的阵列

> 原文:[https://www . geeksforgeeks . org/通过将小于 k 的值替换为它们的和来减少给定的数组/](https://www.geeksforgeeks.org/reduce-given-array-by-replacing-subarrays-with-values-less-than-k-with-their-sum/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是通过用该子数组中元素的[和替换小于 **K** 的子数组来更新给定数组。](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)

**示例:**

> **输入:** arr[] = {200，6，36，612，121，66，63，39，668，108}，K = 100
> **输出:** 200 42 612 121 168 668 108
> **解释:**
> 子阵 **arr[1，2]** 即{6，36}元素较少因此，将它们相加并插入数组，如 6 + 36 = 42。
> 子阵列**arr【5，7】**即{66，63，39}具有小于 K(= 100)的元素。因此，将它们相加并插入数组，成为 66 + 63 + 39 = 168。
> 修改后的数组为{200，42，612，121，168，668，108}
> 
> **输入:** arr[] = {50，25，90，21，30}，K = 95
> **输出:** 216

**方法:**给定的问题可以通过[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并跟踪所有元素小于 **K** 的和并相应更新数组来解决。按照以下步骤解决问题:

*   初始化变量，将**总和**设为 **0** ，存储子阵列的总和。
*   初始化[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **res[]** ，它存储满足给定标准的更新数组 **arr[]** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果**arr【I】<K**的值，则更新 **sum** 的值为**sum+arr【I】**。否则，将**和**的值更新为 **0** ，并将值**和**和 **arr[i]** 添加到向量 **res[]** 。
*   完成上述步骤后，[打印矢量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)**RES【】**中存储的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to replace all the subarray
// having values < K with their sum
void updateArray(vector<int>& arr, int K)
{

    // Stores the sum of subarray having
    // elements less than K
    int sum = 0;

    // Stores the updated array
    vector<int> res;

    // Traverse the array
    for (int i = 0; i < (int)arr.size(); i++) {

        // Update the sum
        if (arr[i] < K) {
            sum += arr[i];
        }

        // Otherwise, update the vector
        else {
            if (sum != 0) {
                res.push_back(sum);
            }
            sum = 0;
            res.push_back(arr[i]);
        }
    }

    if (sum != 0)
        res.push_back(sum);

    // Print the result
    for (auto& it : res)
        cout << it << ' ';
}

// Driver Code
int main()
{

    vector<int> arr = { 200, 6, 36, 612, 121,
                        66, 63, 39, 668, 108 };
    int K = 100;
    updateArray(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to replace all the subarray
    // having values < K with their sum
    static void updateArray(int []arr, int K)
    {

        // Stores the sum of subarray having
        // elements less than K
        int sum = 0;

        // Stores the updated array
         ArrayList<Integer> res
            = new ArrayList<Integer>();

        // Traverse the array
        for (int i = 0; i < arr.length; i++) {

            // Update the sum
            if (arr[i] < K) {
                sum += arr[i];
            }

            // Otherwise, update the vector
            else {
                if (sum != 0) {
                    res.add(sum);
                }
                sum = 0;
                res.add(arr[i]);
            }
        }

        if (sum != 0)
            res.add(sum);

        // Print the result
        for (int i = 0; i < res.size(); i++)
            System.out.print(res.get(i) + " ");
    }

    // Driver Code
    public static void main(String []args)
    {

        int []arr = {200, 6,  36, 612, 121,
                             66,  63, 39, 668, 108 };
        int K = 100;
        updateArray(arr, K);
    }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to replace all the subarray
# having values < K with their sum
def updateArray(arr, K):

    # Stores the sum of subarray having
    # elements less than K
    sum = 0

    # Stores the updated array
    res = []

    # Traverse the array
    for i in range(0, int(len(arr))):

        # Update the sum
        if (arr[i] < K):
            sum += arr[i]

        # Otherwise, update the vector
        else:
            if (sum != 0):
                res.append(sum)

            sum = 0
            res.append(arr[i])

    if (sum != 0):
        res.append(sum)

    # Print the result
    for it in res:
        print(it, end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [200, 6, 36, 612, 121, 66, 63, 39, 668, 108]
    K = 100
    updateArray(arr, K)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;
class GFG {

    // Function to replace all the subarray
    // having values < K with their sum
    static void updateArray(List<int> arr, int K)
    {

        // Stores the sum of subarray having
        // elements less than K
        int sum = 0;

        // Stores the updated array
        List<int> res = new List<int>();

        // Traverse the array
        for (int i = 0; i < arr.Count; i++) {

            // Update the sum
            if (arr[i] < K) {
                sum += arr[i];
            }

            // Otherwise, update the vector
            else {
                if (sum != 0) {
                    res.Add(sum);
                }
                sum = 0;
                res.Add(arr[i]);
            }
        }

        if (sum != 0)
            res.Add(sum);

        // Print the result
        foreach(int it in res) Console.Write(it + " ");
    }

    // Driver Code
    public static void Main()
    {

        List<int> arr
            = new List<int>{ 200, 6,  36, 612, 121,
                             66,  63, 39, 668, 108 };
        int K = 100;
        updateArray(arr, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to replace all the subarray
        // having values < K with their sum
        function updateArray(arr, K) {

            // Stores the sum of subarray having
            // elements less than K
            let sum = 0;

            // Stores the updated array
            let res = [];

            // Traverse the array
            for (let i = 0; i < arr.length; i++) {

                // Update the sum
                if (arr[i] < K) {
                    sum += arr[i];
                }

                // Otherwise, update the vector
                else {
                    if (sum != 0) {
                        res.push(sum);
                    }
                    sum = 0;
                    res.push(arr[i]);
                }
            }

            if (sum != 0)
                res.push(sum);

            // Prlet the result
            for (let it of res)
                document.write(it + ' ');
        }

        // Driver Code

        let arr = [200, 6, 36, 612, 121,
            66, 63, 39, 668, 108];
        let K = 100;
        updateArray(arr, K);

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
200 42 612 121 168 668 108
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)