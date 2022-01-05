# 最大不重复元素

> 原文:[https://www . geesforgeks . org/maximum-非重复元素/](https://www.geeksforgeeks.org/largest-non-repeating-element/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组中最大的[非重复元素](https://www.geeksforgeeks.org/non-repeating-element/)。如果不存在这样的元素，则打印 **-1** 。

**示例:**

> **输入:** arr[] = { 3，1，8，8，4 }
> **输出:** 4
> **解释:**
> 给定数组的非重复元素为{ 1，3，4 }
> 因此，给定数组最大的非重复元素为 4。
> 
> **输入:** arr[] = { 3，1，8，8，3 }
> **输出:** 1
> **解释:**
> 给定数组的非重复元素为{ 1 }
> 因此，给定数组最大的非重复元素为 1。

**方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以解决问题。按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如 **mp** ，来存储数组中每个不同元素的[频率。](https://www.geeksforgeeks.org/c-program-to-count-frequency-of-each-element-in-an-array/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并存储每个数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   初始化一个变量，比如说 **LNRElem** 来存储数组中最大的[非重复元素](https://www.geeksforgeeks.org/non-repeating-element/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个**I<sup>th</sup>T5】元素，检查数组中**arr【I】**的频率是否等于 **1** 。如果发现为真，则更新 **LNRElem = max(LNRElem，arr[i])** 。**
*   最后，打印 **LNRElem** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest unique
// element of the array
void LarUnEl(int arr[], int N)
{
    // Store frequency of each
    // distinct array element
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of arr[i]
        mp[arr[i]]++;
    }

    // Stores largest non-repeating
    // element present in the array
    int LNRElem = INT_MIN;

    // Stores index of the largest
    // unique element of the array
    int ind = -1;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If frequency of arr[i] is equal
        // to 1 and arr[i] exceeds LNRElem
        if (mp[arr[i]] == 1
            && arr[i] > LNRElem) {

            // Update ind
            ind = i;

            // Update LNRElem
            LNRElem = arr[i];
        }
    }

    // If no array element is found
    // with frequency equal to 1
    if (ind == -1) {
        cout << ind;
        return;
    }

    // Print the largest
    // non-repeating element
    cout << arr[ind];
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 8, 8, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    LarUnEl(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the largest unique
    // element of the array
    static void LarUnEl(int arr[], int N)
    {

        // Store frequency of each distinct
        // element of the array
        HashMap<Integer, Integer> map
            = new HashMap<Integer, Integer>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update frequency of arr[i]
            map.put(arr[i],
                    map.getOrDefault(arr[i], 0) + 1);
        }

        // Stores largest non-repeating
        // element present in the array
        int LNRElem = Integer.MIN_VALUE;

        // Stores index of the largest
        // non-repeating array element
        int ind = -1;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If frequency of arr[i] is equal
            // to 1 and arr[i] exceeds LNRElem
            if (map.get(arr[i]) == 1
                && arr[i] > LNRElem) {

                // Update ind
                ind = i;

                // Update LNRElem
                LNRElem = arr[i];
            }
        }

        // If no array element is found
        // with frequency equal to 1
        if (ind == -1) {
            System.out.println(ind);
            return;
        }

        // Print largest non-repeating element
        System.out.println(arr[ind]);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 1, 8, 8, 4 };
        int N = arr.length;
        LarUnEl(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python program to implement
# the above approach
import sys

# Function to find the largest unique
# element of the array
def LarUnEl(arr, N):

    # Store frequency of each distinct
    # element of the array
    map = dict.fromkeys(arr, 0);

    # Traverse the array
    for i in range(N):

        # Update frequency of arr[i]
        map[arr[i]] += 1;

    # Stores largest non-repeating
    # element present in the array
    LNRElem = -sys.maxsize;

    # Stores index of the largest
    # non-repeating array element
    ind = -1;

    # Traverse the array
    for i in range(N):

        # If frequency of arr[i] is equal
        # to 1 and arr[i] exceeds LNRElem
        if (map.get(arr[i]) == 1 and arr[i] > LNRElem):

            # Update ind
            ind = i;

            # Update LNRElem
            LNRElem = arr[i];

    # If no array element is found
    # with frequency equal to 1
    if (ind == -1):
        print(ind);
        return;

    # Prlargest non-repeating element
    print(arr[ind]);

# Driver Code
if __name__ == '__main__':
    arr = [3, 1, 8, 8, 4];
    N = len(arr);
    LarUnEl(arr, N);

    # This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach 
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the largest unique
    // element of the array
    static void LarUnEl(int[] arr, int N)
    {

        // Store frequency of each distinct
        // element of the array
        Dictionary<int,
               int> map = new Dictionary<int,
                                        int>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update frequency of arr[i]
            if (map.ContainsKey(arr[i]) == true)
                map[arr[i]] += 1;
            else
                map[arr[i]] = 1;
            }

        // Stores largest non-repeating
        // element present in the array
        int LNRElem = Int32.MinValue;

        // Stores index of the largest
        // non-repeating array element
        int ind = -1;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If frequency of arr[i] is equal
            // to 1 and arr[i] exceeds LNRElem
            if (map[arr[i]] == 1
                && arr[i] > LNRElem) {

                // Update ind
                ind = i;

                // Update LNRElem
                LNRElem = arr[i];
            }
        }

        // If no array element is found
        // with frequency equal to 1
        if (ind == -1) {
            Console.WriteLine(ind);
            return;
        }

        // Print largest non-repeating element
        Console.WriteLine(arr[ind]);
    }

    // Drivers Code
    public static void Main ()
    {
        int[] arr = { 3, 1, 8, 8, 4 };
        int N = arr.Length;
        LarUnEl(arr, N);
    }

}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the largest unique
// element of the array
function LarUnEl(arr, N)
{
    // Store frequency of each
    // distinct array element
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Update frequency of arr[i]
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else
            mp.set(arr[i], 1);
    }

    // Stores largest non-repeating
    // element present in the array
    var LNRElem = -1000000000;

    // Stores index of the largest
    // unique element of the array
    var ind = -1;

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // If frequency of arr[i] is equal
        // to 1 and arr[i] exceeds LNRElem
        if (mp.get(arr[i]) == 1
            && arr[i] > LNRElem) {

            // Update ind
            ind = i;

            // Update LNRElem
            LNRElem = arr[i];
        }
    }

    // If no array element is found
    // with frequency equal to 1
    if (ind == -1) {
        cout << ind;
        return;
    }

    // Print the largest
    // non-repeating element
    document.write( arr[ind]);
}

// Driver Code
var arr = [3, 1, 8, 8, 4 ];
var N = arr.length;
LarUnEl(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)