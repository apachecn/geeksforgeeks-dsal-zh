# Sudo 放置|放置游

> 原文:[https://www . geesforgeks . org/sudo-placement-placement-tour/](https://www.geeksforgeeks.org/sudo-placement-placement-tour/)

给定一个由 N 个正整数组成的数组 A 和一个预算 b。您的任务是确定要从数组中挑选的元素的最大数量，以便所有挑选的元素的累计成本小于或等于预算 b。挑选第 I 个元素的成本由下式给出:A[i] + (i * K)，其中 K 是一个常数，其值等于挑选的元素数量。索引(I)基于 1。打印最大数量及其各自的累计成本。
**例:**

> **输入** : arr[] = { 2，3，5 }，B = 11
> **输出** : 2 11
> **解释**:拣货最大要素成本= {2 + (1 * 2) } + {3 + (2 * 2)} = 4 + 7 = 11(等于预算)
> **输入** : arr[] = { 1，2，5，6，3 }，B = 90
> **输出【T0**

**先决条件** : [二分搜索法](https://www.geeksforgeeks.org/binary-search/)T4】

**逼近**:这里的想法是在 K 的所有可能值上使用二分搜索法，即要拾取的元素的最佳数量。*以零为下限开始*，以元素总数即 N 为上限结束*。检查通过将 K 设置为当前*中间*，获得的累计成本是否小于或等于预算。如果满足条件，则通过将 *Start* 设置为 *(Mid + 1)* 来尝试增加 K，否则通过将 *End* 设置为*(Mid–1)*来尝试减少 K。
条件的检查可以通过蛮力的方式完成，只需根据给定的公式修改数组，并将 K(当前要拾取的元素数)个最小的修改值相加，即可得到累计成本。
以下是上述办法的实施情况。* 

## C++

```
// CPP Program to find the optimal number of
// elements such that the cumulative value
// should be less than given number
#include <bits/stdc++.h>

using namespace std;

// This function returns true if the value cumulative
// according to received integer K is less than budget
// B, otherwise returns false
bool canBeOptimalValue(int K, int arr[], int N, int B,
                       int& value)
{
    // Initialize a temporary array which stores
    // the cumulative value of the original array
    int tmp[N];

    for (int i = 0; i < N; i++)
        tmp[i] = (arr[i] + K * (i + 1));

    // Sort the array to find the smallest K values
    sort(tmp, tmp + N);

    value = 0;
    for (int i = 0; i < K; i++)
        value += tmp[i];

    // Check if the value is less than budget
    return value <= B;
}

// This function prints the optimal number of elements
// and respective cumulative value which is less than
// the given number
void findNoOfElementsandValue(int arr[], int N, int B)
{
    int start = 0; // Min Value or lower bound

    int end = N; // Max Value or upper bound

    // Initialize answer as zero as optimal value
    // may not exists
    int ans = 0;

    int cumulativeValue = 0;

    while (start <= end) {
        int mid = (start + end) / 2;

        // If the current Mid Value is an optimal
        // value, then try to maximize it
        if (canBeOptimalValue(mid, arr, N, B,
                              cumulativeValue)) {
            ans = mid;
            start = mid + 1;
        }
        else
            end = mid - 1;
    }
    // Call Again to set the corresponding cumulative
    // value for the optimal ans
    canBeOptimalValue(ans, arr, N, B, cumulativeValue);

    cout << ans << " " << cumulativeValue << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5, 6, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Budget
    int B = 90;
    findNoOfElementsandValue(arr, N, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the optimal number of
// elements such that the cumulative value
// should be less than given number
import java.util.*;

class GFG
{
    static int value;

    // This function returns true if
    // the value cumulative according to
    // received integer K is less than
    // budget B, otherwise returns false
    static boolean canBeOptimalValue(int K, int arr[],
                                     int N, int B)
    {
        // Initialize a temporary array
        // which stores the cumulative value
        // of the original array
        int[] tmp = new int[N];

        for (int i = 0; i < N; i++)
            tmp[i] = (arr[i] + K * (i + 1));

        // Sort the array to find the
        // smallest K values
        Arrays.sort(tmp);

        value = 0;
        for (int i = 0; i < K; i++)
            value += tmp[i];

        // Check if the value is less than budget
        return value <= B;
    }

    // This function prints the optimal number
    // of elements and respective cumulative value
    // which is less than the given number
    static void findNoOfElementsandValue(int arr[],
                                  int N, int B)
    {
        int start = 0; // Min Value or lower bound

        int end = N; // Max Value or upper bound

        // Initialize answer as zero as
        // optimal value may not exists
        int ans = 0;

        value = 0;

        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If the current Mid Value is an optimal
            // value, then try to maximize it
            if (canBeOptimalValue(mid, arr, N, B))
            {
                ans = mid;
                start = mid + 1;
            }
            else
                end = mid - 1;
        }

        // Call Again to set the corresponding
        // cumulative value for the optimal ans
        canBeOptimalValue(ans, arr, N, B);

        System.out.print(ans + " " +
                         value + "\n");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 5, 6, 3 };
        int N = arr.length;

        // Budget
        int B = 90;
        findNoOfElementsandValue(arr, N, B);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to find the optimal number of
# elements such that the cumulative value
# should be less than given number
value = 0

# This function returns true if the value cumulative
# according to received integer K is less than budget
# B, otherwise returns false
def canBeOptimalValue(K: int, arr: list, N: int, B: int) -> bool:
    global value

    # Initialize a temporary array which stores
    # the cumulative value of the original array
    tmp = [0] * N

    for i in range(N):
        tmp[i] = (arr[i] + K * (i + 1))

    # Sort the array to find the smallest K values
    tmp.sort()

    value = 0
    for i in range(K):
        value += tmp[i]

    # Check if the value is less than budget
    return value <= B

# This function prints the optimal number of elements
# and respective cumulative value which is less than
# the given number
def findNoOfElementsandValue(arr: list, N: int, B: int):
    global value
    start = 0 # Min Value or lower bound

    end = N # Max Value or upper bound

    # Initialize answer as zero as optimal value
    # may not exists
    ans = 0

    value = 0
    while start <= end:
        mid = (start + end) // 2

        # If the current Mid Value is an optimal
        # value, then try to maximize it
        if canBeOptimalValue(mid, arr, N, B):
            ans = mid
            start = mid + 1
        else:
            end = mid - 1

    # Call Again to set the corresponding cumulative
    # value for the optimal ans
    canBeOptimalValue(ans, arr, N, B)

    print(ans, value)

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 5, 6, 3]
    N = len(arr)

    # Budget
    B = 90
    findNoOfElementsandValue(arr, N, B)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# Program to find the optimal number of
// elements such that the cumulative value
// should be less than given number
using System;

class GFG
{
    static int value;

    // This function returns true if
    // the value cumulative according to
    // received integer K is less than
    // budget B, otherwise returns false
    static bool canBeOptimalValue(int K, int []arr,
                                  int N, int B)
    {
        // Initialize a temporary array
        // which stores the cumulative value
        // of the original array
        int[] tmp = new int[N];

        for (int i = 0; i < N; i++)
            tmp[i] = (arr[i] + K * (i + 1));

        // Sort the array to find the
        // smallest K values
        Array.Sort(tmp);

        value = 0;
        for (int i = 0; i < K; i++)
            value += tmp[i];

        // Check if the value is less than budget
        return value <= B;
    }

    // This function prints the optimal number
    // of elements and respective cumulative value
    // which is less than the given number
    static void findNoOfElementsandValue(int []arr,
                                  int N, int B)
    {
        int start = 0; // Min Value or lower bound

        int end = N; // Max Value or upper bound

        // Initialize answer as zero as
        // optimal value may not exists
        int ans = 0;

        value = 0;

        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If the current Mid Value is an optimal
            // value, then try to maximize it
            if (canBeOptimalValue(mid, arr, N, B))
            {
                ans = mid;
                start = mid + 1;
            }
            else
                end = mid - 1;
        }

        // Call Again to set the corresponding
        // cumulative value for the optimal ans
        canBeOptimalValue(ans, arr, N, B);

        Console.Write(ans + " " +
                    value + "\n");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 5, 6, 3 };
        int N = arr.Length;

        // Budget
        int B = 90;
        findNoOfElementsandValue(arr, N, B);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript Program to find the optimal number of
// elements such that the cumulative value
// should be less than given number

// This function returns true if the value cumulative
// according to received integer K is less than budget
// B, otherwise returns false

let cumulativeValue = 0;

function canBeOptimalValue(K, arr, N, B) {
    // Initialize a temporary array which stores
    // the cumulative value of the original array
    let tmp = new Array(N);

    for (let i = 0; i < N; i++)
        tmp[i] = (arr[i] + K * (i + 1));

    // Sort the array to find the smallest K values
    tmp.sort((a, b) => a - b);

    cumulativeValue = 0;
    for (let i = 0; i < K; i++)
        cumulativeValue += tmp[i];

    // Check if the value is less than budget
    return cumulativeValue <= B;
}

// This function prints the optimal number of elements
// and respective cumulative value which is less than
// the given number
function findNoOfElementsandValue(arr, N, B) {
    let start = 0; // Min Value or lower bound

    let end = N; // Max Value or upper bound

    // Initialize answer as zero as optimal value
    // may not exists
    let ans = 0;

    while (start <= end) {
        let mid = Math.floor((start + end) / 2);

        // If the current Mid Value is an optimal
        // value, then try to maximize it
        if (canBeOptimalValue(mid, arr, N, B)) {
            ans = mid;
            start = mid + 1;
        }
        else
            end = mid - 1;
    }
    // Call Again to set the corresponding cumulative
    // value for the optimal ans
    canBeOptimalValue(ans, arr, N, B, cumulativeValue);

    document.write(ans + " " + cumulativeValue + "<br>");
}

// Driver Code

let arr = [1, 2, 5, 6, 3];
let N = arr.length;

// Budget
let B = 90;
findNoOfElementsandValue(arr, N, B);

</script>
```

**输出:**

```
4 54
```

**时间复杂度** : O(N * (log N) <sup>2</sup> ，其中 N 为给定数组中的元素个数。