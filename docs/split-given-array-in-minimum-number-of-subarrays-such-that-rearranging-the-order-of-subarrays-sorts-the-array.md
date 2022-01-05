# 以最小数量的子阵列分割给定的阵列，从而重新排列子阵列的顺序对阵列进行排序

> 原文:[https://www . geeksforgeeks . org/split-给定最小数量子阵列中的阵列-这样-重新排列子阵列的顺序-对阵列进行排序/](https://www.geeksforgeeks.org/split-given-array-in-minimum-number-of-subarrays-such-that-rearranging-the-order-of-subarrays-sorts-the-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到将数组元素拆分为子数组的最小数目，从而重新排列子数组的顺序[对给定数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序。

**示例:**

> ***输入:** arr[] = {6，3，4，2，1}*
> ***输出:** 4*
> ***解释:***
> *给定的阵列可以分为 4 个子阵列，分别为{6}、{3，4}、{2}、{1}，这些子阵列可以重新排列为{1}、{2}、{3，4}、{6}。得到的数组将是排序后的{1，2，3，4，6}。因此，给定数组可以划分的最小子数组是 4。*
> 
> ***输入:** arr[] = {1，-4，0，-2}*
> ***输出:** 4*

**方法:**给定的问题可以通过维护数组的排序版本 **arr[]** 并将原始数组中所有出现在排序数组中的整数按相同顺序分组来解决。以下是步骤:

*   维护一对 **V** 的[向量，该向量为给定数组中的所有元素存储当前元素的值和数组中当前元素的索引 **arr[]** 。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   [排序向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **V** 。
*   初始化一个变量，比如说 **cnt** 为 **1** ，它存储所需的最小数量的子阵列。
*   [在**【1，N–1】**范围内遍历 **i** 的向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **V** ，并执行以下步骤:
    *   如果原始阵列中第**I**元素的索引是原始阵列中第 **(1 +第(I–1)<sup>第</sup>元素的索引)**，则这两个元素可以在同一个子阵列中组合在一起。
    *   否则，这两个元素需要在单独的子阵列中，并将 **cnt** 的值增加 **1** 。
*   完成上述步骤后，打印 **cnt** 的值，作为子阵列可能断裂的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>

#include <iostream>
using namespace std;

// Function to find minimum number of
// subarrays such that rearranging the
// subarrays sort the array
int numberOfSubarrays(int arr[], int n)
{
    // Stores the minimum number of
    // subarrays
    int cnt = 1;

    // Stores all the elements in the
    // array with their indices
    vector<pair<int, int> > v(n);

    // Copy array elements in vector
    for (int i = 0; i < n; i++) {
        v[i].first = arr[i];
        v[i].second = i;
    }

    // Sort the vector v
    sort(v.begin(), v.end());

    // Iterate through vector v
    for (int i = 1; i < n; i++) {

        // If the (i)th and (i-1)th element
        // can be grouped in same subarray
        if (v[i].second == v[i - 1].second + 1) {
            continue;
        }
        else {
            cnt++;
        }
    }

    // Return resultant count
    return cnt;
}

// Driver Code
int main()
{
    int arr[] = { 6, 3, 4, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << numberOfSubarrays(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to find minimum number of
// subarrays such that rearranging the
// subarrays sort the array
static int numberOfSubarrays(int arr[], int n)
{

    // Stores the minimum number of
    // subarrays
    int cnt = 1;

    // Stores all the elements in the
    // array with their indices
    pair[] v = new pair[n];

    // Copy array elements in vector
    for (int i = 0; i < n; i++) {
        v[i] = new pair(0,0);
        v[i].first = arr[i];
        v[i].second = i;
    }

    // Sort the vector v
    Arrays.sort(v,(a,b)->a.first-b.first);

    // Iterate through vector v
    for (int i = 1; i < n; i++) {

        // If the (i)th and (i-1)th element
        // can be grouped in same subarray
        if (v[i].second == v[i - 1].second + 1) {
            continue;
        }
        else {
            cnt++;
        }
    }

    // Return resultant count
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 6, 3, 4, 2, 1 };
    int N = arr.length;
    System.out.print(numberOfSubarrays(arr, N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find minimum number of
# subarrays such that rearranging the
# subarrays sort the array
def numberOfSubarrays(arr, n):

    # Stores the minimum number of
    # subarrays
    cnt = 1

    # Stores all the elements in the
    # array with their indices
    v = []

    # Copy array elements in vector
    for i in range(n):
        v.append({'first': arr[i], 'second': i})

    # Sort the vector v
    v = sorted(v, key = lambda i: i['first'])

    # Iterate through vector v
    for i in range(1, n):

        # If the (i)th and (i-1)th element
        # can be grouped in same subarray
        if (v[i]['first'] == v[i - 1]['second']):
            continue
        else:
            cnt += 1

    # Return resultant count
    return cnt

# Driver Code
arr = [6, 3, 4, 2, 1]
N = len(arr)
print(numberOfSubarrays(arr, N))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

    class pair : IComparable<pair>
    {
        public int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }  
        public int CompareTo(pair other)
        {
            // return other.Salary.CompareTo(this.Salary);
            if (this.first < other.first)
            {
                return 1;
            }
            else if (this.first > other.first)
            {
                return -1;
            }
            else
            {
                return 0;
            }
        }
    }

// Function to find minimum number of
// subarrays such that rearranging the
// subarrays sort the array
static int numberOfSubarrays(int []arr, int n)
{

    // Stores the minimum number of
    // subarrays
    int cnt = 1;

    // Stores all the elements in the
    // array with their indices
    pair[] v = new pair[n];

    // Copy array elements in vector
    for (int i = 0; i < n; i++) {
        v[i] = new pair(0,0);
        v[i].first = arr[i];
        v[i].second = i;
    }

    // Sort the vector v
    Array.Sort(v);

    // Iterate through vector v
    for (int i = 1; i < n; i++) {

        // If the (i)th and (i-1)th element
        // can be grouped in same subarray
        if (v[i].second == v[i - 1].second + 1) {
            continue;
        }
        else {
            cnt++;
        }
    }

    // Return resultant count
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 6, 3, 4, 2, 1 };
    int N = arr.Length;
    Console.Write(numberOfSubarrays(arr, N));

}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
   <script>
        // JavaScript Program to implement
        // the above approach

        // Function to find minimum number of
        // subarrays such that rearranging the
        // subarrays sort the array
        function numberOfSubarrays(arr, n) {
            // Stores the minimum number of
            // subarrays
            let cnt = 1;

            // Stores all the elements in the
            // array with their indices
            let v = [];

            // Copy array elements in vector
            for (let i = 0; i < n; i++) {
                v.push({ first: arr[i], second: i })
            }

            // Sort the vector v
            v.sort(function (a, b) { return a.first - b.first })

            // Iterate through vector v
            for (let i = 1; i < n; i++) {

                // If the (i)th and (i-1)th element
                // can be grouped in same subarray
                if (v[i].second == v[i - 1].second + 1) {
                    continue;
                }
                else {
                    cnt++;
                }
            }

            // Return resultant count
            return cnt;
        }

        // Driver Code

        let arr = [6, 3, 4, 2, 1];
        let N = arr.length;
        document.write(numberOfSubarrays(arr, N));

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*