# 将二进制数组的所有元素转换为 K 所需的最小子数组翻转次数

> 原文:[https://www . geesforgeks . org/minimum-subarray-flips-required-convert-all-elements-of-a-binary-array-to-k/](https://www.geeksforgeeks.org/minimum-subarray-flips-required-to-convert-all-elements-of-a-binary-array-to-k/)

给定一个由 **N** 个整数组成的二进制数组 **arr[]** ，任务是计算将数组的所有元素转换为等于 **K** 所需的以下类型的最小运算次数:

*   从给定数组中选择任意索引 **X** 。
*   翻转子阵列**arr[X]…arr[N–1]**的所有元素，即如果 arr[i] = 1，则将 arr[i]设置为 0，反之亦然。

**示例:**

> **输入:** N = 8，arr[ ] = {1，0，1，0，1，1，1}，K = 0
> **输出:** 5
> **解释:**
> 运算 1: X = 0(选择的指标)。修改值后，更新后的数组 arr[]为[0，1，0，1，1，0，0，0]。
> 操作 2: X = 1(选择的索引)。修改值后，更新后的数组 arr[]为[0，0，1，0，0，1，1，1]。
> 操作 3: X = 2(选择的索引)。修改值后，更新后的数组 arr[]为[0，0，0，1，1，0，0，0]。
> 操作 4: X = 3(选择的索引)。修改值后，更新的数组 arr[]为[0，0，0，0，0，1，1，1]。
> 操作 5: X = 5(选择的索引)。修改值后，更新后的数组 arr[]为[0，0，0，0，0，0，0，0]。
> 
> **输入:** N = 8，arr[ ] = {1，0，1，0，1，1，1}，K = 1
> **输出:** 4

**方法:**进行以下观察:

> 由于对索引 **N-1** 的任何索引 X ( < N) can be chosen and each value from index **X** 都可以修改，所以可以发现该方法是对数组中的变化点进行计数。

按照以下步骤解决上述问题:

1.  将变量**标志**初始化为 **K** 的倒数。即如果 K = 0 则为 1，反之亦然，这表示当前值。
2.  将变量 **cnt** 初始化为 0，该变量记录数组 arr[]中变化点的数量。
3.  遍历数组**arr【】**并对每个索引 **i** 应用以下步骤:
    *   如果**标志**值和**arr【I】**值不同，则进行下一次迭代。
    *   如果**标记**和**标记**相等，则增加**计数**并将**标记**设置为**标记=(标记+ 1) % 2** 。
4.  打印**计数**的最终值。

下面是上述方法的实现:

## C++14

```
// C++14 Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of subarray flips required
int minSteps(int arr[], int n, int k)
{
    int i, cnt = 0;
    int flag;
    if (k == 1)
        flag = 0;
    else
        flag = 1;

    // Iterate the array
    for (i = 0; i < n; i++) {

        // If arr[i] and flag are equal
        if (arr[i] == flag) {
            cnt++;
            flag = (flag + 1) % 2;
        }
    }

    // Return the answer
    return cnt;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 1, 0, 0, 1, 1, 1 };
    int n = sizeof(arr)
            / sizeof(arr[0]);
    int k = 1;

    cout << minSteps(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count the minimum
// number of subarray flips required
static int minSteps(int arr[], int n, int k)
{
    int i, cnt = 0;
    int flag;

    if (k == 1)
        flag = 0;
    else
        flag = 1;

    // Iterate the array
    for(i = 0; i < n; i++)
    {

        // If arr[i] and flag are equal
        if (arr[i] == flag)
        {
            cnt++;
            flag = (flag + 1) % 2;
        }
    }

    // Return the answer
    return cnt;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 0, 1, 0, 0, 1, 1, 1 };
    int n = arr.length;
    int k = 1;

    System.out.print(minSteps(arr, n, k));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the minimum
# number of subarray flips required
def minSteps(arr, n, k):

    cnt = 0
    if(k == 1):
        flag = 0
    else:
        flag = 1

    # Iterate the array
    for i in range(n):

        # If arr[i] and flag are equal
        if(arr[i] == flag):
            cnt += 1
            flag = (flag + 1) % 2

    # Return the answer
    return cnt

# Driver Code
arr = [ 1, 0, 1, 0, 0, 1, 1, 1 ]
n = len(arr)
k = 1

# Function call
print(minSteps(arr, n, k))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the minimum
// number of subarray flips required
static int minSteps(int[] arr, int n, int k)
{
    int i, cnt = 0;
    int flag;

    if (k == 1)
        flag = 0;
    else
        flag = 1;

    // Iterate the array
    for(i = 0; i < n; i++)
    {

        // If arr[i] and flag are equal
        if (arr[i] == flag)
        {
            cnt++;
            flag = (flag + 1) % 2;
        }
    }

    // Return the answer
    return cnt;
}

// Driver code
public static void Main ()
{
    int[] arr = { 1, 0, 1, 0, 0, 1, 1, 1 };
    int n = arr.Length;
    int k = 1;

    Console.Write(minSteps(arr, n, k));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to count the minimum
// number of subarray flips required
function minSteps(arr, n, k)
{
    let i, cnt = 0;
    let flag;

    if (k == 1)
        flag = 0;
    else
        flag = 1;

    // Iterate the array
    for(i = 0; i < n; i++)
    {

        // If arr[i] and flag are equal
        if (arr[i] == flag)
        {
            cnt++;
            flag = (flag + 1) % 2;
        }
    }

    // Return the answer
    return cnt;
}

// Driver Code

    let arr = [ 1, 0, 1, 0, 0, 1, 1, 1 ];
    let n = arr.length;
    let k = 1;

    document.write(minSteps(arr, n, k));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*