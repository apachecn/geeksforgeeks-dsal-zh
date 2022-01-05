# 检查是否可以通过增加和减少相邻对来严格增加数组

> 原文:[https://www . geesforgeks . org/check-一个数组是否可以被严格递增和递减相邻对/](https://www.geeksforgeeks.org/check-whether-an-array-can-be-made-strictly-increasing-by-incrementing-and-decrementing-adjacent-pairs/)

给定一个由非负整数组成的大小为 **N** 的 [**数组**](https://www.geeksforgeeks.org/array-data-structure/)**【arr】**。在一次移动中，阵列的第**个**索引元素减少 1，第 **(i+1)个**索引增加 1。任务是检查是否有任何**的可能性，通过任意次数的移动，使给定数组严格增加**(仅包含非负整数)。

**示例:**

> **输入:** arr[3] = [1，2，3]
> **输出:**是
> **说明:**数组已经按照严格递增顺序排序。
> 
> **输入:** arr[2] = [2，0]
> **输出:**是
> **解释**:考虑 **i = 0** 第一次移动 arr[0] = 2-1 = 1，arr[1] = 0 + 1 = 1。现在数组变成了[1，1]。
> 在第二步中，考虑 **i = 0。**所以现在 arr[0]= 1–1 = 0，arr[1] = 1 + 1 = 2。
> 最后的数组变成，arr[2] = [0，2]严格递增。
> 
> **输入:** arr[3] = [0，1，0]
> **输出:**否
> **说明**:这个数组不能通过执行任意次数的移动来严格递增只包含非负整数。

**方法:**问题可以用下面的数学观察来解决。

*   由于所有数组元素都是非负的，因此大小为 **N** 的数组的**最小严格递增顺序**可以是: **0，1，2，3。。。(N-1)** 。
*   因此**的第 I 个**元素的**最小和(min_sum)** 任何这样的数组都是 **min_sum = (i*(i-1))/2。**
*   因此，**给定数组(cur_sum)** 的前 I 个元素之和必须满足条件 **cur_sum ≥ min_sum** 。
*   如果条件为**不满足**，则**不可能**使给定数组严格递增。考虑以下示例

> 插图 1:
> 
> **arr[]**= 4 5 1 2 3
> **min _ sum**= 0 1 3 6 10
> **sum(arr)**= 4 9 10 12 15
> 
> 因为这个数组满足每个 I 的条件，所以可以将这个数组转换成严格递增的数组

> **插图 2:**
> 
> **arr[]**= 2 3 1 0 2
> **min _ sum**= 0 1 3 6 10
> **sum(arr)**= 2 5 6 8
> 
> 这里，在索引 4 处，数组的和不满足最小和为 10 的条件。所以不可能把数组变成严格递增的。

按照下面提到的步骤来实现这个概念:

*   从**索引= 0** 到**索引= N–1**遍历，对于每个**I**检查总和是否大于或等于 **(i*(i+1))/2** 。
*   如果条件满足**，则可以使阵**严格递增。**否则**，不能使**严格递增。******

****对于上述方法，请遵循以下实施方式:****

## ****C++****

```
**// C++ code to check if the given array
// can be made strictly increasing
#include <bits/stdc++.h>
using namespace std;

// Function to check if
// the array can be made strictly increasing
void CheckStrictlyIncreasing(int arr[],
                             int N)
{
    // variable to store sum till current
    // index element
    int cur_sum = 0;
    bool possible = true;
    for (int index = 0;
         index < N; index++) {
        cur_sum += arr[index];

        // Sum of 0, 1, ...(i)th element
        int req_sum = (index * (index + 1)) / 2;

        // Check if valid or not
        if (req_sum > cur_sum) {
            possible = false;
            break;
        }
    }

    // If can be made strictly increasing
    if (possible)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    int arr[3] = { 1, 2, 3 };
    int N = 3;

    CheckStrictlyIncreasing(arr, N);
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java code to check if the given array
// can be made strictly increasing
import java.util.*;

class GFG{

// Function to check if
// the array can be made strictly increasing
static void CheckStrictlyIncreasing(int arr[],
                             int N)
{
    // variable to store sum till current
    // index element
    int cur_sum = 0;
    boolean possible = true;
    for (int index = 0;
         index < N; index++) {
        cur_sum += arr[index];

        // Sum of 0, 1, ...(i)th element
        int req_sum = (index * (index + 1)) / 2;

        // Check if valid or not
        if (req_sum > cur_sum) {
            possible = false;
            break;
        }
    }

    // If can be made strictly increasing
    if (possible)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int N = 3;

    CheckStrictlyIncreasing(arr, N);
}
}

// This code is contributed by shikhasingrajput**
```

## ****蟒蛇 3****

```
**# Python 3 code to check if the given array
# can be made strictly increasing

# Function to check if
# the array can be made strictly increasing
def CheckStrictlyIncreasing(arr,
                            N):

    # variable to store sum till current
    # index element
    cur_sum = 0
    possible = True
    for index in range(N):
        cur_sum += arr[index]

        # Sum of 0, 1, ...(i)th element
        req_sum = (index * (index + 1)) // 2

        # Check if valid or not
        if (req_sum > cur_sum):
            possible = False
            break

    # If can be made strictly increasing
    if (possible):
        print("Yes")

    else:
        print("No")

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 3]
    N = 3

    CheckStrictlyIncreasing(arr, N)

    # This code is contributed by ukasp.**
```

## ****C#****

```
**// C# code to check if the given array
// can be made strictly increasing
using System;

class GFG{

// Function to check if the array can
// be made strictly increasing
static void CheckStrictlyIncreasing(int []arr,
                                    int N)
{

    // Variable to store sum till current
    // index element
    int cur_sum = 0;
    bool possible = true;
    for(int index = 0;
            index < N; index++)
    {
        cur_sum += arr[index];

        // Sum of 0, 1, ...(i)th element
        int req_sum = (index * (index + 1)) / 2;

        // Check if valid or not
        if (req_sum > cur_sum)
        {
            possible = false;
            break;
        }
    }

    // If can be made strictly increasing
    if (possible)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3 };
    int N = 3;

    CheckStrictlyIncreasing(arr, N);
}
}

// This code is contributed by shikhasingrajput**
```

## ****java 描述语言****

```
**<script>
       // JavaScript code for the above approach

       // Function to check if
       // the array can be made strictly increasing
       function CheckStrictlyIncreasing(arr, N)
       {

           // variable to store sum till current
           // index element
           let cur_sum = 0;
           let possible = true;
           for (let index = 0;
               index < N; index++) {
               cur_sum += arr[index];

               // Sum of 0, 1, ...(i)th element
               let req_sum = (index * (index + 1)) / 2;

               // Check if valid or not
               if (req_sum > cur_sum) {
                   possible = false;
                   break;
               }
           }

           // If can be made strictly increasing
           if (possible)
               document.write("Yes");
           else
               document.write("No");
       }

       // Driver code
       let arr = [1, 2, 3];
       let N = 3;

       CheckStrictlyIncreasing(arr, N);

 // This code is contributed by Potta Lokesh
   </script>**
```

******Output**

```
Yes
```**** 

******时间复杂度:**O(N)
T3】空间复杂度: O(1)****