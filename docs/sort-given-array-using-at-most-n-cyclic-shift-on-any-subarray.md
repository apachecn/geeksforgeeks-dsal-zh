# 在任何子阵列上最多使用 N 次循环移位对给定阵列进行排序

> 原文:[https://www . geesforgeks . org/sort-给定数组-最多使用 n 个循环移位任意子数组/](https://www.geeksforgeeks.org/sort-given-array-using-at-most-n-cyclic-shift-on-any-subarray/)

给定一个包含 **N** 个整数的 [**数组**](https://www.geeksforgeeks.org/array-data-structure/)**【arr】**，重复。任务是在任何子阵列上使用**最多 N 个**循环移位对阵列进行递增排序。

> **任意子阵列上的循环移位**是指从给定阵列中切出任意子阵列，在其中使用任意偏移量的循环移位(旋转)，并将其放回阵列的相同位置。

打印排序数组所需的移位次数。可能有多种可能性。

**示例:**

> **输入:**arr[]=【1，3，2，8，5】
> **输出:** 2
> **解释:**考虑从**索引= 1 到索引= 2** 的段。[1、 **3、2** 、8、5]。现在将此线段旋转 1 个偏移量。新数组变成[1， **2，3** ，8，5]。
> 然后考虑从**索引= 3 到索引= 4、**【1、2、3、 **8、5** 的段。旋转 1 个偏移量，新数组变成[1，2，3，5，8]。
> 
> **输入:**arr[]=【2，4，1，3】
> **输出:** 2
> **解释:**从**索引= 0 到索引= 2，**【**2，4，1** ，3】。将此线段向左旋转 2 个偏移量，新数组变成[ **1，2，4，** 3]。
> 从偏移 1 的**索引** **= 2 到索引= 3** 取第二段，旋转它，新数组变成【1，2， **4，3** 】。

**进场:**可以有两种情况:

1.  **数组已经排序的情况:**那么我们不需要执行任何移位操作
2.  **数组未排序的情况:**为此，请执行以下步骤:
    *   创建变量**计数= 0** 来存储计数总数。
    *   从 **i = 0** 迭代到 **i = N-2** 。对于每次迭代，执行以下操作:
        *   创建一个变量 **minVal** 来存储本次迭代中找到的最小值，**用**arr【I】**的值初始化**。
        *   从 i+1 开始迭代**到 **N-1** 。如果**电流值小于**值，则**更新**值。**
        *   向右标记位置**以执行从 I 到右偏移 1 的循环移位。**
    *   **如果**没有这样正确的**值存在，那么只需**移动到下一个迭代**。**
    *   **否则，将阵列从 **i** 旋转至**右侧**1 位置**并将计数**增加 1。**
    *   **返回 count 的值作为您的答案。**

**下面是上述方法的 C++实现:**

## **C++**

```
// C++ code to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to Sort given Array using
// at most N cyclic shift on any subarray
int ShiftingSort(vector<int>& arr, int n)
{
    vector<int> temp(arr.begin(), arr.end());
    sort(temp.begin(), temp.end());

    // Variable to store count of
    // shifting operations
    int count = 0;

    // If the vector arr is already sorted
    // the 0 operations shift required
    if (arr == temp) {
        return 0;
    }
    else {
        // Run a loop from 0 to n-2 index
        for (int index1 = 0; index1 < n - 1; index1++) {
            int minval = arr[index1];
            int left = index1;
            int right = -1;

            // Loop from i+1 to n-1
            // to find the minimum value
            for (int index2 = index1 + 1; index2 < n;
                 index2++) {
                if (minval > arr[index2]) {
                    minval = arr[index2];
                    right = index2;
                }
            }

            // Check if the shifting is required
            if (right != -1) {
                // Increment count operations
                count++;

                int index = right;
                int tempval = arr[right];

                // Loop for shifting the array arr
                // from index = left to index = right
                while (index > left) {
                    arr[index] = arr[index - 1];
                    index--;
                }
                arr[index] = tempval;
            }
        }
    }

    // Return the total operations
    return count;
}

// Driver code
int main()
{
    vector<int> arr{ 1, 3, 2, 8, 5 };
    int N = 5;

    cout << ShiftingSort(arr, N) << "\n";

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to implement the above approach
import java.util.*;

public class GFG
{

// Function to Sort given Array using
// at most N cyclic shift on any subarray
static int ShiftingSort(ArrayList<Integer> arr, int n)
{
    ArrayList<Integer> temp = new ArrayList<Integer>();
    for(int i = 0; i < arr.size(); i++) {
        temp.add(arr.get(i));
    }

    Collections.sort(temp);

    // Variable to store count of
    // shifting operations
    int count = 0;

    // If the vector arr is already sorted
    // the 0 operations shift required
    if (arr.equals(temp)) {
        return 0;
    }
    else {
        // Run a loop from 0 to n-2 index
        for (int index1 = 0; index1 < n - 1; index1++) {
            int minval = arr.get(index1);
            int left = index1;
            int right = -1;

            // Loop from i+1 to n-1
            // to find the minimum value
            for (int index2 = index1 + 1; index2 < n;
                 index2++) {
                if (minval > arr.get(index2)) {
                    minval = arr.get(index2);
                    right = index2;
                }
            }

            // Check if the shifting is required
            if (right != -1) {
                // Increment count operations
                count++;

                int index = right;
                int tempval = arr.get(right);

                // Loop for shifting the array arr
                // from index = left to index = right
                while (index > left) {
                    arr.set(index, arr.get(index - 1));
                    index--;
                }
                arr.set(index, tempval);
            }
        }
    }

    // Return the total operations
    return count;
}

// Driver code
public static void main(String args[])
{
    ArrayList<Integer> arr = new ArrayList<Integer>();

    arr.add(1);
    arr.add(3);
    arr.add(2);
    arr.add(8);
    arr.add(5);

    int N = 5;

    System.out.println(ShiftingSort(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## **蟒蛇 3**

```
# Python Program to implement
# the above approach

# Function to Sort given Array using
# at most N cyclic shift on any subarray
def ShiftingSort(arr, n):
    temp = arr.copy()
    temp.sort()

    # Variable to store count of
    # shifting operations
    count = 0

    # If the vector arr is already sorted
    # the 0 operations shift required
    if (arr == temp):
        return 0
    else:

        # Run a loop from 0 to n-2 index
        for index1 in range(n - 1):
            minval = arr[index1]
            left = index1
            right = -1

            # Loop from i+1 to n-1
            # to find the minimum value
            for index2 in range(index1 + 1, n):
                if (minval > arr[index2]):
                    minval = arr[index2]
                    right = index2

            # Check if the shifting is required
            if (right != -1):

                # Increment count operations
                count += 1
                index = right
                tempval = arr[right]

                # Loop for shifting the array arr
                # from index = left to index = right
                while (index > left):
                    arr[index] = arr[index - 1]
                    index -= 1
                arr[index] = tempval

    # Return the total operations
    return count

# Driver code
arr = [1, 3, 2, 8, 5]
N = 5
print(ShiftingSort(arr, N))

# This code is contributed by gfgking
```

## **C#**

```
// C# code to implement the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to Sort given Array using
// at most N cyclic shift on any subarray
static int ShiftingSort(ArrayList arr, int n)
{
    ArrayList temp = new ArrayList();
    for(int i = 0; i < arr.Count; i++) {
        temp.Add(arr[i]);
    }

    temp.Sort();

    // Variable to store count of
    // shifting operations
    int count = 0;

    // If the vector arr is already sorted
    // the 0 operations shift required
    if (arr.Equals(temp)) {
        return 0;
    }
    else
    {

        // Run a loop from 0 to n-2 index
        for (int index1 = 0; index1 < n - 1; index1++) {
            int minval = (int)arr[index1];
            int left = index1;
            int right = -1;

            // Loop from i+1 to n-1
            // to find the minimum value
            for (int index2 = index1 + 1; index2 < n;
                 index2++) {
                if (minval > (int)arr[index2]) {
                    minval = (int)arr[index2];
                    right = index2;
                }
            }

            // Check if the shifting is required
            if (right != -1)
            {

                // Increment count operations
                count++;

                int index = right;
                int tempval = (int)arr[right];

                // Loop for shifting the array arr
                // from index = left to index = right
                while (index > left) {
                    arr[index] = arr[index - 1];
                    index--;
                }
                arr[index] = tempval;
            }
        }
    }

    // Return the total operations
    return count;
}

// Driver code
public static void Main()
{
    ArrayList arr = new ArrayList();

    arr.Add(1);
    arr.Add(3);
    arr.Add(2);
    arr.Add(8);
    arr.Add(5);

    int N = 5;

    Console.Write(ShiftingSort(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## **java 描述语言**

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to Sort given Array using
        // at most N cyclic shift on any subarray
        function ShiftingSort(arr, n) {
            let temp = [...arr];
            temp.sort(function (a, b) { return a - b })

            // Variable to store count of
            // shifting operations
            let count = 0;

            // If the vector arr is already sorted
            // the 0 operations shift required
            if (arr == temp) {
                return 0;
            }
            else {

                // Run a loop from 0 to n-2 index
                for (let index1 = 0; index1 < n - 1; index1++) {
                    let minval = arr[index1];
                    let left = index1;
                    let right = -1;

                    // Loop from i+1 to n-1
                    // to find the minimum value
                    for (let index2 = index1 + 1; index2 < n;
                        index2++) {
                        if (minval > arr[index2]) {
                            minval = arr[index2];
                            right = index2;
                        }
                    }

                    // Check if the shifting is required
                    if (right != -1)
                    {

                        // Increment count operations
                        count++;

                        let index = right;
                        let tempval = arr[right];

                        // Loop for shifting the array arr
                        // from index = left to index = right
                        while (index > left) {
                            arr[index] = arr[index - 1];
                            index--;
                        }
                        arr[index] = tempval;
                    }
                }
            }

            // Return the total operations
            return count;
        }

        // Driver code
        let arr = [1, 3, 2, 8, 5];
        let N = 5;
        document.write(ShiftingSort(arr, N) + '<br>');

    // This code is contributed by Potta Lokesh
    </script>
```

****Output**

```
2
```** 

****时间复杂度:**O(N<sup>2</sup>)
T5】空间复杂度: O(1)**