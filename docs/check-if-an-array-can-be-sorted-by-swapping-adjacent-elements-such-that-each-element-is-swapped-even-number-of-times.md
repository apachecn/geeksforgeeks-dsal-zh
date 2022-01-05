# 检查一个数组是否可以通过交换相邻元素进行排序，使得每个元素被交换偶数次

> 原文:[https://www . geesforgeks . org/check-if-a-array-可以通过交换相邻元素进行排序-这样-每个元素被交换-偶数次/](https://www.geeksforgeeks.org/check-if-an-array-can-be-sorted-by-swapping-adjacent-elements-such-that-each-element-is-swapped-even-number-of-times/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是[检查数组是否可以通过任意次交换相邻元素来排序](https://www.geeksforgeeks.org/check-if-array-can-be-sorted-with-one-swap/)，使得每个数组元素被交换偶数次。

**示例:**

> **输入:** arr[] = {4，3，2，5}
> **输出:**是
> **解释:**
> 下面是可能的交换顺序，使数组排序:
> 
> 1.  选择索引 0 和 1 会将数组修改为[3，4，2，5]。现在，{2，3，4，5}的交换频率分别为{0，1，1，0}。
> 2.  选择索引 1 和 2 将数组修改为[3，2，4，5]。现在，{2，3，4，5}的交换频率分别为{1，1，2，0}。
> 3.  选择索引 0 和 1 会将数组修改为[2，3，4，5]。现在，{2，3，4，5}的交换频率分别为{2，2，2，0}。
> 
> 因此，每个数组元素被交换偶数次，并且给定的数组被排序。因此，打印“是”。
> 
> **输入:** arr[] = {1，2，3，5，4}
> 输出:否

**方法:**给定的问题可以通过观察两个相邻的偶数或奇数索引元素可以交换的事实来解决，因为在不改变中间元素的情况下，交换的数量没有限制。因此，想法是[在各自的偶数和奇数索引](https://www.geeksforgeeks.org/even-numbers-even-index-odd-numbers-odd-index/)处重新排列数组元素，并检查所形成的数组是否已排序。按照以下步骤解决给定的问题:

*   将所有数组元素**arr【I】**存储在另一个数组的奇数索引处，比如**奇数[]** 。
*   将所有数组元素**存储在另一个数组的偶数索引处，比如**偶数[]** 。**
*   [将数组](https://www.geeksforgeeks.org/sorting-algorithms/) **奇数[]** 和**偶数[]** 按递增顺序排序。
*   初始化两个变量，将 **j** 和 **k** 表示为 **0** ，用于[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **奇数[]** 和**偶数[]** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   如果 **i** 的值为奇数，则推数组**RES【】**中的元素**奇数【j】**，并将 **j** 的值增加 **1** 。
    *   [如果 **i** 的值为偶数](https://www.geeksforgeeks.org/check-if-a-number-is-odd-or-even-using-bitwise-operators/)，则推数组**RES【】**中的元素**偶数【k】**，将 **j** 的值增加 **1** 。
*   完成以上步骤后，如果数组 **res[]** 排序，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to check if the array can be
// made sorted by adjacent swapping of
// element such that each array element
// is swapped even number of times
bool isSorted(int arr[], int n)
{
    vector<int> evenArr, oddArr;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // Stores all the even positions
        // elements
        if (i % 2 == 0)
            evenArr.push_back(arr[i]);

        // Stores all the odd positions
        // elements
        else
            oddArr.push_back(arr[i]);
    }

    // Sort the array evenArr[]
    sort(evenArr.begin(), evenArr.end());

    // Sort the array oddArr[]
    sort(oddArr.begin(), oddArr.end());

    int j = 0, k = 0;
    vector<int> res;

    // Combine the elements from evenArr
    // and oddArr in the new array res[]
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0)
            res.push_back(evenArr[j]), j++;
        else
            res.push_back(oddArr[k]), k++;
    }

    // Check if the array res[] is
    // sorted or not
    for (int i = 0; i < n - 1; i++) {
        if (res[i] > res[i + 1])
            return false;
    }

    // Otherwise, return true
    return true;
}

// Driver Code
int main()
{
    int arr[] = { 4, 3, 2, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    if (isSorted(arr, N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if the array can be
// made sorted by adjacent swapping of
// element such that each array element
// is swapped even number of times
static boolean isSorted(int arr[], int n)
{
    Vector<Integer> evenArr = new Vector<Integer>();
    Vector<Integer> oddArr = new Vector<Integer>();

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // Stores all the even positions
        // elements
        if (i % 2 == 0)
            evenArr.add(arr[i]);

        // Stores all the odd positions
        // elements
        else
            oddArr.add(arr[i]);
    }

    // Sort the array evenArr[]
    Collections.sort(evenArr);

    // Sort the array oddArr[]
    Collections.sort(oddArr);

    int j = 0, k = 0;
    Vector<Integer> res=new Vector<Integer>();;

    // Combine the elements from evenArr
    // and oddArr in the new array res[]
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0) {
            res.add(evenArr.get(j)); j++;
        }
        else {
            res.add(oddArr.get(k)); k++;
        }
    }

    // Check if the array res[] is
    // sorted or not
    for (int i = 0; i < n - 1; i++) {
        if (res.get(i) > res.get(i + 1))
            return false;
    }

    // Otherwise, return true
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 3, 2, 5 };
    int N = arr.length;

    if (isSorted(arr, N)) {
        System.out.print("Yes");
    }
    else {
        System.out.print("No");
    }

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the array can be
# made sorted by adjacent swapping of
# element such that each array element
# is swapped even number of times
def isSorted(arr, n):

    evenArr = []
    oddArr = []

    # Traverse the given array
    for i in range(n):

        # Stores all the even positions
        # elements
        if (i % 2 == 0):
            evenArr.append(arr[i])

        # Stores all the odd positions
        # elements
        else:
            oddArr.append(arr[i])

    # Sort the array evenArr[]
    evenArr.sort()

    # Sort the array oddArr[]
    oddArr.sort()

    j = 0
    k = 0
    res = []

    # Combine the elements from evenArr
    # and oddArr in the new array res[]
    for i in range(n):
        if (i % 2 == 0):
            res.append(evenArr[j])
            j += 1
        else:
            res.append(oddArr[k])
            k += 1

    # Check if the array res[] is
    # sorted or not
    for i in range(n - 1):
        if (res[i] > res[i + 1]):
            return False

    # Otherwise, return true
    return True

# Driver Code
if __name__ == '__main__':

    arr = [ 4, 3, 2, 5 ]
    N = len(arr)

    if (isSorted(arr, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to check if the array can be
    // made sorted by adjacent swapping of
    // element such that each array element
    // is swapped even number of times
    static bool isSorted(int[] arr, int n)
    {
        List<int> evenArr = new List<int>();
        List<int> oddArr = new List<int>();

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // Stores all the even positions
            // elements
            if (i % 2 == 0)
                evenArr.Add(arr[i]);

            // Stores all the odd positions
            // elements
            else
                oddArr.Add(arr[i]);
        }

        // Sort the array evenArr[]
        evenArr.Sort();

        // Sort the array oddArr[]
        oddArr.Sort();

        int j = 0, k = 0;
        List<int> res = new List<int>();

        // Combine the elements from evenArr
        // and oddArr in the new array res[]
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                res.Add(evenArr[j]);
                j++;
            }
            else {
                res.Add(oddArr[k]);
                k++;
            }
        }

        // Check if the array res[] is
        // sorted or not
        for (int i = 0; i < n - 1; i++) {
            if (res[i] > res[i + 1])
                return false;
        }

        // Otherwise, return true
        return true;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 4, 3, 2, 5 };
        int N = arr.Length;

        if (isSorted(arr, N)) {
            Console.Write("Yes");
        }
        else {
            Console.Write("No");
        }
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to check if the array can be
        // made sorted by adjacent swapping of
        // element such that each array element
        // is swapped even number of times
        function isSorted(arr, n) {
            let evenArr = [], oddArr = [];

            // Traverse the given array
            for (let i = 0; i < n; i++) {

                // Stores all the even positions
                // elements
                if (i % 2 == 0)
                    evenArr.push(arr[i]);

                // Stores all the odd positions
                // elements
                else
                    oddArr.push(arr[i]);
            }

            // Sort the array evenArr[]
            evenArr.sort(function (a, b) { return a - b });

            // Sort the array oddArr[]
            oddArr.sort(function (a, b) { return a - b });

            let j = 0, k = 0;
            let res = [];

            // Combine the elements from evenArr
            // and oddArr in the new array res[]
            for (let i = 0; i < n; i++) {
                if (i % 2 == 0)
                    res.push(evenArr[j]), j++;
                else
                    res.push(oddArr[k]), k++;
            }

            // Check if the array res[] is
            // sorted or not
            for (let i = 0; i < n - 1; i++) {
                if (res[i] > res[i + 1])
                    return false;
            }

            // Otherwise, return true
            return true;
        }

        // Driver Code

        let arr = [4, 3, 2, 5];
        let N = arr.length;

        if (isSorted(arr, N)) {
            document.write("Yes");
        }
        else {
            document.write("No");
        }

   // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

**时间完成** ***存在:** O(N*log N)*
***辅助空间:** O(N)*