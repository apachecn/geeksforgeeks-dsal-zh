# 由两个相同元素重复组合而成的给定数组中的最大数

> 原文:[https://www . geeksforgeeks . org/给定数组中重复组合两个相同元素形成的最大数量/](https://www.geeksforgeeks.org/largest-number-in-given-array-formed-by-repeatedly-combining-two-same-elements/)

给定一个数组 **arr[]** ，任务是找出给定数组中最大的数，该数组是由两个相同的元素重复组合而成的。如果数组中最初没有相同的元素，则将输出打印为-1。
**例:**

> **输入:** arr = {1，1，2，4，7，8}
> **输出:** 16
> **解释:**
> 重复 1:将数组中的 1 组合起来，在其中插入和 2。更新的数组= {2，2，4，7，8}
> 重复 2:组合数组中的 2s，并在其中插入和 4。更新的数组= {4，4，7，8}
> 重复 3:组合数组中的 4 个，并在其中插入总和 8。更新后的数组= {8，7，8}
> 重复 4:将数组中的 8s 合并，并将总和 16 插入其中。更新数组= {7，16}
> 最大和= 16
> **输入:** arr = {1，2，3}
> **输出:** -1
> **说明:**
> 数组中最初没有重复的元素。因此不能进行任何组合。

**方法:**这个问题可以用给定数组中元素的频率来解决。

*   在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中找到并存储给定数组中每个元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   遍历每个不同元素的频率图时，如果频率大于 1 的频率图中有任何重复元素 **K** ，则将元素 **2*K** 的频率增加 **K** 元素频率的一半。

*   最后，从地图上找到最大数量。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the largest sum
int largest_sum(int arr[], int n)
{
    // Variable to store the largest sum
    int maximum = -1;

    // Map to store the frequencies
    // of each element
    map<int, int> m;

    // Store the Frequencies
    for (int i = 0; i < n; i++) {
        m[arr[i]]++;
    }

    // Loop to combine duplicate elements
    // and update the sum in the map
    for (auto j : m) {

        // If j is a duplicate element
        if (j.second > 1) {

            // Update the frequency of 2*j
            m[2 * j.first]
                = m[2 * j.first]
                  + j.second / 2;

            // If the new sum is greater than
            // maximum value, Update the maximum
            if (2 * j.first > maximum)
                maximum = 2 * j.first;
        }
    }

    // Returns the largest sum
    return maximum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 4, 7, 8 };
    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function Calling
    cout << largest_sum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG {

    // Function to return the largest sum
    static int largest_sum(int arr[], int n)
    {
        // Variable to store the largest sum
        int maximum = -1;

        // Map to store the frequencies
        // of each element
        HashMap<Integer, Integer> m = new HashMap<Integer, Integer>();

        // Store the Frequencies
        for (int i = 0; i < n; i++) {

            if (m.containsKey(arr[i])){
            m.put(arr[i], m.get(arr[i]) + 1);
            }
            else{
                m.put(arr[i], 1);
            }
        }

        // Loop to combine duplicate elements
        // and update the sum in the map
        for(int i = 0; i < n; i++){

            // If j is a duplicate element
            if (m.get(arr[i]) > 1) {

                if (m.containsKey(2*arr[i]))
                {
                    // Update the frequency of 2*j
                    m.put(2*arr[i],m.get(2 * arr[i])+ m.get(arr[i]) / 2);
                }
                else
                {
                    m.put(2*arr[i],m.get(arr[i]) / 2);
                }

                // If the new sum is greater than
                // maximum value, Update the maximum
                if (2 * arr[i] > maximum)
                    maximum = 2 * arr[i];
            }
            }

        // Returns the largest sum
        return maximum;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 1, 1, 2, 4, 7, 8 };
        int n = arr.length;

        // Function Calling
        System.out.println(largest_sum(arr, n));
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the largest sum
def largest_sum(arr, n):

    # Variable to store the largest sum
    maximum = -1

    # Map to store the frequencies
    # of each element
    m = dict()

    # Store the Frequencies
    for i in arr:
        m[i] = m.get(i,0) + 1

    # Loop to combine duplicate elements
    # and update the sum in the map
    for j in list(m):

        # If j is a duplicate element
        if ((j in m) and m[j] > 1):

            # Update the frequency of 2*j
            x, y = 0, 0
            if 2*j in m:
                m[2*j] = m[2 * j]+ m[j]// 2
            else:
                m[2*j] = m[j]//2

            # If the new sum is greater than
            # maximum value, Update the maximum
            if (2 * j > maximum):
                maximum = 2 * j

    # Returns the largest sum
    return maximum

# Driver Code
if __name__ == '__main__':
    arr= [1, 1, 2, 4, 7, 8]
    n = len(arr)

    # Function Calling
    print(largest_sum(arr, n))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to return the largest sum
    static int largest_sum(int []arr, int n)
    {
        // Variable to store the largest sum
        int maximum = -1;

        // Map to store the frequencies
        // of each element
        Dictionary<int, int> m = new Dictionary<int, int>();

        // Store the Frequencies
        for (int i = 0; i < n; i++) {

            if (m.ContainsKey(arr[i])){
                m[arr[i]]++;
            }
            else{
                m.Add(arr[i] , 1);
            }
        }

        // Loop to combine duplicate elements
        // and update the sum in the map
        for(int i = 0; i < n; i++){

            // If j is a duplicate element
            //Console.Write(m[arr[i]]);

            if (m[arr[i]] > 1) {

                if (m.ContainsKey(2*arr[i]))
                {
                    // Update the frequency of 2*j
                    m[2*arr[i]] = m[2 * arr[i]]+ m[arr[i]] / 2;
                }
                else
                {
                    m.Add(2*arr[i],m[arr[i]] / 2);
                }

                // If the new sum is greater than
                // maximum value, Update the maximum
                if (2 * arr[i] > maximum)
                    maximum = 2 * arr[i];
            }

            }

        // Returns the largest sum
        return maximum;
    }

    // Driver Code
    public static void Main ()
    {
        int[] arr = { 1, 1, 2, 4, 7, 8 };
        int n = arr.Length;

        // Function Calling
        Console.Write(largest_sum(arr, n));
    }
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the largest sum
    function largest_sum(arr, n)
    {
        // Variable to store the largest sum
        let maximum = -1;

        // Map to store the frequencies
        // of each element
        let m = new Map();

        // Store the Frequencies
        for (let i = 0; i < n; i++) {

            if (m.has(arr[i])){
            m.set(arr[i], m.get(arr[i]) + 1);
            }
            else{
                m.set(arr[i], 1);
            }
        }

        // Loop to combine duplicate elements
        // and update the sum in the map
        for(let i = 0; i < n; i++){

            // If j is a duplicate element
            if (m.get(arr[i]) > 1) {

                if (m.has(2*arr[i]))
                {
                    // Update the frequency of 2*j
                    m.set(2*arr[i],m.get(2 * arr[i])+ m.get(arr[i]) / 2);
                }
                else
                {
                    m.set(2*arr[i],m.get(arr[i]) / 2);
                }

                // If the new sum is greater than
                // maximum value, Update the maximum
                if (2 * arr[i] > maximum)
                    maximum = 2 * arr[i];
            }
            }

        // Returns the largest sum
        return maximum;
    }

// Driver code

          let arr = [ 1, 1, 2, 4, 7, 8 ];
        let n = arr.length;

        // Function Calling
        document.write(largest_sum(arr, n));

</script>
```

**Output:** 

```
16
```

时间复杂度:0(n)

辅助空间:O(n)