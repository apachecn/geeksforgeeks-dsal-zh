# 在排序生成的数组中找到第 k 个最小的元素

> 原文:[https://www . geeksforgeeks . org/find-the-kth-排序生成数组中的最小元素/](https://www.geeksforgeeks.org/find-the-kth-smallest-element-in-the-sorted-generated-array/)

给定一个由 **N** 元素和一个整数 **K** 组成的数组 **arr[]** ，任务是生成一个具有以下规则的**B[]【T7:** 

1.  复制元素**arr【1…N】**、 **N** 次来排列 **B[]** 。
2.  复制元素**arr【1…N/2】**、 **2*N** 次以排列 **B[]** 。
3.  复制元素**arr【1…N/4】**， **3*N** 次以排列 **B[]** 。
4.  同样，直到没有元素可以复制到数组 B[]。

最后从阵 **B[]** 中打印出 **K <sup>th</sup>** 最小元素。如果 **K** 超出 **B[]** 的范围，则返回 **-1** 。
**示例:**

> **输入:** arr[] = {1，2，3}，K = 4
> **输出:** 1
> {1，2，3，1，2，3，1，2，3，1，1，1，1，1}是排序形式中所需的数组 B[]
> {1，1，1，1，1，1，1，1，1，1，2，2，2，3，3，3}其中
> 1 是第四个最小元素。
> **输入:** arr[] = {2，4，5，1}，K = 13
> **输出:** 2

**进场:**

1.  维护一个 Count_Array，其中我们必须存储数组 B[]中每个元素出现的次数。可以通过在起始索引处增加计数并在结束索引+ 1 位置减去相同的计数来对元素范围进行此操作。
2.  取计数数组的累计和。
3.  维护 arr[]的所有元素及其在数组 B[]中的计数，并根据元素值对它们进行排序。
4.  遍历向量，根据它们各自的计数，看看哪个元素在 B[]中有 Kth 位置。
5.  如果 K 超出了 B[]的界限，则返回-1。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the Kth element in B[]
int solve(int Array[], int N, int K)
{

    // Initialize the count Array
    int count_Arr[N + 1] = { 0 };
    int factor = 1;
    int size = N;

    // Reduce N repeatedly to half its value
    while (size) {
        int start = 1;
        int end = size;

        // Add count to start
        count_Arr[1] += factor * N;

        // Subtract same count after end index
        count_Arr[end + 1] -= factor * N;
        factor++;
        size /= 2;
    }

    for (int i = 2; i <= N; i++)
        count_Arr[i] += count_Arr[i - 1];

    // Store each element of Array[] with their count
    vector<pair<int, int> > element;
    for (int i = 0; i < N; i++) {
        element.push_back({ Array[i], count_Arr[i + 1] });
    }

    // Sort the elements wrt value
    sort(element.begin(), element.end());

    int start = 1;
    for (int i = 0; i < N; i++) {
        int end = start + element[i].second - 1;

        // If Kth element is in range of element[i]
        // return element[i]
        if (K >= start && K <= end) {
            return element[i].first;
        }

        start += element[i].second;
    }

    // If K is out of bound
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 5, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 13;

    cout << solve(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Vector;

class GFG
{

    // Pair class implementation to use Pair
    static class Pair
    {
        private int first;
        private int second;

        Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }

        public int getFirst()
        {
            return first;
        }

        public int getSecond()
        {
            return second;
        }
    }

    // Function to return the Kth element in B[]
    static int solve(int[] Array, int N, int K)
    {

        // Initialize the count Array
        int[] count_Arr = new int[N + 2];
        int factor = 1;
        int size = N;

        // Reduce N repeatedly to half its value
        while (size > 0)
        {
            int start = 1;
            int end = size;

            // Add count to start
            count_Arr[1] += factor * N;

            // Subtract same count after end index
            count_Arr[end + 1] -= factor * N;
            factor++;
            size /= 2;
        }

        for (int i = 2; i <= N; i++)
            count_Arr[i] += count_Arr[i - 1];

        // Store each element of Array[]
        // with their count
        Vector<Pair> element = new Vector<>();
        for (int i = 0; i < N; i++)
        {
            Pair x = new Pair(Array[i],
                              count_Arr[i + 1]);
            element.add(x);
        }

        int start = 1;
        for (int i = 0; i < N; i++)
        {
            int end = start + element.elementAt(0).getSecond() - 1;

            // If Kth element is in range of element[i]
            // return element[i]
            if (K >= start && K <= end)
                return element.elementAt(i).getFirst();

            start += element.elementAt(i).getSecond();
        }

        // If K is out of bound
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 2, 4, 5, 1 };
        int N = arr.length;
        int K = 13;
        System.out.println(solve(arr, N, K));
    }
}   

// This code is contiributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the Kth element in B[]
def solve(Array, N, K) :

    # Initialize the count Array
    count_Arr = [0]*(N + 2) ;
    factor = 1;
    size = N;

    # Reduce N repeatedly to half its value
    while (size) :
        start = 1;
        end = size;

        # Add count to start
        count_Arr[1] += factor * N;

        # Subtract same count after end index
        count_Arr[end + 1] -= factor * N;
        factor += 1;
        size //= 2;

    for i in range(2, N + 1) :
        count_Arr[i] += count_Arr[i - 1];

    # Store each element of Array[] with their count
    element = [];

    for i in range(N) :
        element.append(( Array[i], count_Arr[i + 1] ));

    # Sort the elements wrt value
    element.sort();

    start = 1;
    for i in range(N) :
        end = start + element[i][1] - 1;

        # If Kth element is in range of element[i]
        # return element[i]
        if (K >= start and K <= end) :
            return element[i][0];

        start += element[i][1];

    # If K is out of bound
    return -1;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 4, 5, 1 ];
    N = len(arr);
    K = 13;

    print(solve(arr, N, K));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Pair class implementation to use Pair
    public class Pair
    {
        public int first;
        public int second;

        public Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }

        public int getFirst()
        {
            return first;
        }

        public int getSecond()
        {
            return second;
        }
    }

    // Function to return the Kth element in B[]
    static int solve(int[] Array, int N, int K)
    {

        // Initialize the count Array
        int[] count_Arr = new int[N + 2];
        int factor = 1;
        int size = N;

        // Reduce N repeatedly to half its value
        while (size > 0)
        {
            int end = size;

            // Add count to start
            count_Arr[1] += factor * N;

            // Subtract same count after end index
            count_Arr[end + 1] -= factor * N;
            factor++;
            size /= 2;
        }

        for (int i = 2; i <= N; i++)
            count_Arr[i] += count_Arr[i - 1];

        // Store each element of Array[]
        // with their count
        List<Pair> element = new List<Pair>();
        for (int i = 0; i < N; i++)
        {
            Pair x = new Pair(Array[i],
                              count_Arr[i + 1]);
            element.Add(x);
        }

        int start = 1;
        for (int i = 0; i < N; i++)
        {
            int end = start + element[0].getSecond() - 1;

            // If Kth element is in range of element[i]
            // return element[i]
            if (K >= start && K <= end)
                return element[i].getFirst();

            start += element[i].getSecond();
        }

        // If K is out of bound
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 2, 4, 5, 1 };
        int N = arr.Length;
        int K = 13;
        Console.WriteLine(solve(arr, N, K));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the Kth element in B[]
function solve(arr, N, K) {

    // Initialize the count Array
    let count_Arr = new Array(N + 1).fill(0);
    let factor = 1;
    let size = N;

    // Reduce N repeatedly to half its value
    while (size) {
        let start = 1;
        let end = size;

        // Add count to start
        count_Arr[1] += factor * N;

        // Subtract same count after end index
        count_Arr[end + 1] -= factor * N;
        factor++;
        size = Math.floor(size / 2);
    }

    for (let i = 2; i <= N; i++)
        count_Arr[i] += count_Arr[i - 1];

    // Store each element of Array[] with their count
    let element = [];
    for (let i = 0; i < N; i++) {
        element.push([arr[i], count_Arr[i + 1]]);
    }

    // Sort the elements wrt value
    element.sort((a, b) => a - b);

    let start = 1;
    for (let i = 0; i < N; i++) {
        let end = start + element[i][1] - 1;

        // If Kth element is in range of element[i]
        // return element[i]
        if (K >= start && K <= end) {
            return element[i][0];
        }

        start += element[i][1];
    }

    // If K is out of bound
    return -1;
}

// Driver code

let arr = [2, 4, 5, 1];
let N = arr.length;
let K = 13;

document.write(solve(arr, N, K));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
```