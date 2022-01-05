# 每个数组元素出现的索引的绝对差之和|集合 2

> 原文:[https://www . geeksforgeeks . org/每个数组元素集出现的绝对差异指数之和-2/](https://www.geeksforgeeks.org/sum-of-absolute-differences-of-indices-of-occurrences-of-each-array-element-set-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** ，每个数组元素 **arr[i]** 的任务是打印所有可能索引 **j** 的**| I–j |**的和，使得 **arr[i] = arr[j]** 。

**示例:**

> ***输入:** arr[] = {1，3，1，1，2}*
> ***输出:** 5 0 3 4 0*
> ***解释:***
> *对于 arr[0]，求和= | 0–0 |+| 0–2 |+| 0–3 | = 5。*
> *对于 arr[1]，sum = | 1–1 | = 0。*
> *为 arr[2]，和= | 2–0 |+| 2–2 |+| 2–3 | = 3。*
> *对于 arr[3]，sum = | 3–0 |+| 3–2 |+| 3–3 | = 4。*
> *为 arr[4]，求和= | 4–4 | = 0。*
> *因此，所需输出为 5 0 3 4 0。*
> 
> ***输入:** arr[] = {1，1，1}*
> ***输出:** 3 2 3*

**天真的做法:**解决问题最简单的做法请参考本文[之前的帖子](https://www.geeksforgeeks.org/sum-of-absolute-differences-of-indices-of-occurrences-of-each-array-element/)。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

[**地图**](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **为主的方法:**使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)解决问题请参考本文[前一帖](https://www.geeksforgeeks.org/sum-of-absolute-differences-of-indices-of-occurrences-of-each-array-element/)。
***时间复杂度:** O(N*L)*
***辅助空间:** O(N)*

**有效方法:**上述方法也可以通过将每个元素的先前索引和[出现次数存储在](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)[哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中来优化。按照以下步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，说 **M** 存储**arr【I】**为键，**(计数，前一个索引)**为值。
*   初始化大小为 **N** 的两个[数组](https://www.geeksforgeeks.org/arrays-in-java/) **L[]** 和 **R[]** ，其中 **L[i]** 表示所有可能索引 **j < i** 和 **arr[i] = arr[j]** 的 **R[i]** 表示**| I–j |】的和**
*   [在范围**【0，N–1】**内遍历给定数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** ，并执行以下步骤:
    *   [如果地图](https://www.geeksforgeeks.org/hashmap-containskey-method-in-java/) **M** 中存在**arr【I】**，则将**L【I】**的值更新为 **0** 和**M【arr【I】】**以存储[对](https://www.geeksforgeeks.org/pair-class-in-java/) **{1，i}** ，其中第一个元素表示出现次数，第二个元素表示该元素的前一个索引。
    *   否则，从地图 **M** 中找到**arr【I】**的值，并将计数和先前的索引分别存储在变量 **cnt** 和 **j** 中。
    *   将**L【I】**的值更新为**(CNT *(I–j)+L【j】)**并将 **M** 中**arr【I】**的值更新为存储[对](https://www.geeksforgeeks.org/pair-class-in-java/) **(cnt + 1，i)** 。
*   重复同样的过程，更新数组 **R[]** 中的值。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/iterating-arrays-java/)**【0，N–1】**，并打印值 **(L[i] + R[i])** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the count of occurrences
// and previous index of every element
struct pairr
{
    int count, prevIndex;

    // Constructor
    pairr(int countt, int prevIndexx)
    {
        count = countt;
        prevIndex = prevIndexx;
    }
};

// Function to calculate the sum of
// absolute differences of indices
// of occurrences of array element
void findSum(int arr[], int n)
{

    // Stores the count of elements
    // and their previous indices
    map<int, pairr*> mapp;

    // Initialize 2 arrays left[]
    // and right[] of size N
    int left[n];
    int right[n];

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // If arr[i] is present in the Map
        if (mapp.find(arr[i]) == mapp.end())
        {

            // Update left[i] to 0
            // and update the value
            // of arr[i] in map
            left[i] = 0;
            mapp[arr[i]] = new pairr(1, i);
        }

        // Otherwise, get the value from
        // the map and update left[i]
        else
        {
            pairr* tmp = mapp[arr[i]];
            left[i] = (tmp->count) * (i - tmp->prevIndex) +
                   left[tmp->prevIndex];
            mapp[arr[i]] = new pairr(tmp->count + 1, i);
        }
    }

    // Clear the map to calculate right[] array
    mapp.clear();

    // Traverse the array arr[] in reverse
    for(int i = n - 1; i >= 0; i--)
    {

        // If arr[i] is present in theMap
        if (mapp.find(arr[i]) == mapp.end())
        {

            // Update right[i] to 0
            // and update the value
            // of arr[i] in the Map
            right[i] = 0;
            mapp[arr[i]] = new pairr(1, i);
        }

        // Otherwise get the value from
        // the map and update right[i]
        else
        {
            pairr* tmp = mapp[arr[i]];
            right[i] = (tmp->count) *
                       (abs(i - tmp->prevIndex)) +
                          right[tmp->prevIndex];

            mapp[arr[i]] = new pairr(tmp->count + 1, i);
        }
    }

    // Iterate in the range [0, N-1]
    // and print the sum of left[i]
    // and right[i] as the result
    for(int i = 0; i < n; i++)
        cout << left[i] + right[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 1, 1, 2 };
    int N = 5;

    findSum(arr, N);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Stores the count of occurrences
    // and previous index of every element
    static class pair {
        int count, prevIndex;

        // Constructor
        pair(int count, int prevIndex)
        {
            this.count = count;
            this.prevIndex = prevIndex;
        }
    }

    // Function to calculate the sum of
    // absolute differences of indices
    // of occurrences of array element
    static void findSum(int[] arr, int n)
    {
        // Stores the count of elements
        // and their previous indices
        Map<Integer, pair> map = new HashMap<>();

        // Initialize 2 arrays left[]
        // and right[] of size N
        int[] left = new int[n];
        int[] right = new int[n];

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // If arr[i] is present in the Map
            if (!map.containsKey(arr[i])) {

                // Update left[i] to 0
                // and update the value
                // of arr[i] in map
                left[i] = 0;
                map.put(arr[i], new pair(1, i));
            }

            // Otherwise, get the value from
            // the map and update left[i]
            else {
                pair tmp = map.get(arr[i]);
                left[i] = (tmp.count)
                              * (i - tmp.prevIndex)
                          + left[tmp.prevIndex];
                map.put(
                    arr[i], new pair(
                                tmp.count + 1, i));
            }
        }

        // Clear the map to calculate right[] array
        map.clear();

        // Traverse the array arr[] in reverse
        for (int i = n - 1; i >= 0; i--) {

            // If arr[i] is present in theMap
            if (!map.containsKey(arr[i])) {

                // Update right[i] to 0
                // and update the value
                // of arr[i] in the Map
                right[i] = 0;
                map.put(arr[i], new pair(1, i));
            }

            // Otherwise get the value from
            // the map and update right[i]
            else {

                pair tmp = map.get(arr[i]);
                right[i]
                    = (tmp.count)
                          * (Math.abs(i - tmp.prevIndex))
                      + right[tmp.prevIndex];

                map.put(
                    arr[i], new pair(
                                tmp.count + 1, i));
            }
        }

        // Iterate in the range [0, N-1]
        // and print the sum of left[i]
        // and right[i] as the result
        for (int i = 0; i < n; i++)
            System.out.print(
                left[i] + right[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 3, 1, 1, 2 };
        int N = arr.length;
        findSum(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Stores the count of occurrences
    # and previous index of every element
class pair:
    def __init__(self, count,prevIndex):
        self.count = count;
        self.prevIndex = prevIndex;

# Function to calculate the sum of
    # absolute differences of indices
    # of occurrences of array element
def findSum(arr,n):

    # Stores the count of elements
        # and their previous indices
        map = {};

        # Initialize 2 arrays left[]
        # and right[] of size N
        left = [0 for i in range(n)];
        right = [0 for i in range(n)];

        # Traverse the given array
        for i in range(n):

            # If arr[i] is present in the Map
            if (arr[i] not in map):

                # Update left[i] to 0
                # and update the value
                # of arr[i] in map
                left[i] = 0;
                map[arr[i]] =  pair(1, i);

            # Otherwise, get the value from
            # the map and update left[i]
            else:
                tmp = map[arr[i]];
                left[i] = (tmp.count) * (i - tmp.prevIndex) + left[tmp.prevIndex]
                map[arr[i]] = pair( tmp.count + 1, i);

        # Clear the map to calculate right[] array
        map.clear();

        # Traverse the array arr[] in reverse
        for i in range (n - 1, -1, -1):

            # If arr[i] is present in theMap
            if (arr[i] not in map):

                # Update right[i] to 0
                # and update the value
                # of arr[i] in the Map
                right[i] = 0;
                map[arr[i]] =  pair(1, i);

            # Otherwise get the value from
            # the map and update right[i]
            else:

                tmp = map[arr[i]];
                right[i] = (tmp.count) * (abs(i - tmp.prevIndex)) + right[tmp.prevIndex];

                map[arr[i]] =  pair(tmp.count + 1, i);

        # Iterate in the range [0, N-1]
        # and print the sum of left[i]
        # and right[i] as the result
        for i in range(n):
            print(left[i] + right[i], end=" ");

# Driver Code
arr=[1, 3, 1, 1, 2];
N = len(arr);
findSum(arr, N);

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Stores the count of occurrences
    // and previous index of every element
class pair
{
    constructor(count,prevIndex)
    {
        this.count = count;
            this.prevIndex = prevIndex;
    }
}

// Function to calculate the sum of
    // absolute differences of indices
    // of occurrences of array element
function findSum(arr,n)
{
    // Stores the count of elements
        // and their previous indices
        let map = new Map();

        // Initialize 2 arrays left[]
        // and right[] of size N
        let left = new Array(n);
        let right = new Array(n);

        // Traverse the given array
        for (let i = 0; i < n; i++) {

            // If arr[i] is present in the Map
            if (!map.has(arr[i])) {

                // Update left[i] to 0
                // and update the value
                // of arr[i] in map
                left[i] = 0;
                map.set(arr[i], new pair(1, i));
            }

            // Otherwise, get the value from
            // the map and update left[i]
            else {
                let tmp = map.get(arr[i]);
                left[i] = (tmp.count)
                              * (i - tmp.prevIndex)
                          + left[tmp.prevIndex];
                map.set(
                    arr[i], new pair(
                                tmp.count + 1, i));
            }
        }

        // Clear the map to calculate right[] array
        map.clear();

        // Traverse the array arr[] in reverse
        for (let i = n - 1; i >= 0; i--) {

            // If arr[i] is present in theMap
            if (!map.has(arr[i])) {

                // Update right[i] to 0
                // and update the value
                // of arr[i] in the Map
                right[i] = 0;
                map.set(arr[i], new pair(1, i));
            }

            // Otherwise get the value from
            // the map and update right[i]
            else {

                let tmp = map.get(arr[i]);
                right[i]
                    = (tmp.count)
                          * (Math.abs(i - tmp.prevIndex))
                      + right[tmp.prevIndex];

                map.set(
                    arr[i], new pair(
                                tmp.count + 1, i));
            }
        }

        // Iterate in the range [0, N-1]
        // and print the sum of left[i]
        // and right[i] as the result
        for (let i = 0; i < n; i++)
            document.write(
                left[i] + right[i] + " ");
}

// Driver Code
let arr=[1, 3, 1, 1, 2];
let N = arr.length;
findSum(arr, N);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
5 0 3 4 0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)