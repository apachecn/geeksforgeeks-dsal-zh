# 在二进制数组中从 0 的相邻左边移除所有 1

> 原文:[https://www . geesforgeks . org/remove-all-1s-from-the-neighbor-of-0s-in-a-in-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a](https://www.geeksforgeeks.org/remove-all-1s-from-the-adjacent-left-of-0s-in-a-binary-array/)

给定一个二进制数组 **arr[]** ，任务是找出从相邻的 0 左边移除所有 1 所需的操作数。在每个操作中，0 左边的所有 1 都被更改为 0。

**示例:**

> **输入:** arr[] = { 1，0，0，1，1，0 }
> **输出:** 2
> **解释:**
> 操作 1:索引 0 和 4 的变化。arr[] = { 0，0，0，1，0，0 }
> 操作 2:索引 3 中的更改。arr[] = { 0，0，0，0，0，0 }
> 不需要更多操作。
> 
> **输入:** arr[] = { 0，1，0，1 }
> **输出:** 1
> **说明:**
> 操作 1:指标 1 变化。arr[] = { 0，0，0，1 }
> 不需要更多操作。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思想是在 **0** 之前计算**连续 1 的最大次数**，这给出了执行给定操作所需的次数，使得数组不能进一步改变。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of 1's before 0
void noOfMoves(int arr[], int n)
{
    int cnt = 0;
    int maxCnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If value is 1
        if (arr[i] == 1) {
            cnt++;
        }
        else {

            // If consecutive 1 followed
            // by 0, then update the maxCnt
            if (cnt != 0) {
                maxCnt = max(maxCnt, cnt);
                cnt = 0;
            }
        }
    }

    // Print the maximum consecutive 1's
    // followed by 0
    cout << maxCnt << endl;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 1, 1, 1, 0,
                  0, 1, 1, 0, 0, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    noOfMoves(arr, N);
    int arr1[] = { 1, 0, 1, 0, 1, 0, 1, 0 };
    N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    noOfMoves(arr1, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find the maximum number
// of 1's before 0
static void noOfMoves(int arr[], int n)
{
    int cnt = 0;
    int maxCnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If value is 1
        if (arr[i] == 1) {
            cnt++;
        }
        else {

            // If consecutive 1 followed
            // by 0, then update the maxCnt
            if (cnt != 0) {
                maxCnt = Math.max(maxCnt, cnt);
                cnt = 0;
            }
        }
    }

    // Print the maximum consecutive 1's
    // followed by 0
    System.out.print(maxCnt +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 1, 1, 1, 0,
                0, 1, 1, 0, 0, 1 };
    int N = arr.length;

    // Function Call
    noOfMoves(arr, N);
    int arr1[] = { 1, 0, 1, 0, 1, 0, 1, 0 };
    N = arr1.length;

    // Function Call
    noOfMoves(arr1, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to find the maximum number
# of 1's before 0
def noOfMoves(arr,n):
    cnt = 0
    maxCnt = 0

    # Traverse the array
    for i in range(n):
        # If value is 1
        if (arr[i] == 1):
            cnt += 1
        else:
            # If consecutive 1 followed
            # by 0, then update the maxCnt
            if (cnt != 0):
                maxCnt = max(maxCnt, cnt)
                cnt = 0

    # Print the maximum consecutive 1's
    # followed by 0
    print(maxCnt)

# Driver Code
if __name__ == '__main__':
    arr = [0, 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1]
    N = len(arr)

    # Function Call
    noOfMoves(arr, N)
    arr1 = [1, 0, 1, 0, 1, 0, 1, 0]
    N = len(arr1)

    # Function Call
    noOfMoves(arr1, N)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG{

// Function to find the maximum number
// of 1's before 0
static void noOfMoves(int []arr, int n)
{
    int cnt = 0;
    int maxCnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If value is 1
        if (arr[i] == 1) {
            cnt++;
        }
        else {

            // If consecutive 1 followed
            // by 0, then update the maxCnt
            if (cnt != 0) {
                maxCnt = Math.Max(maxCnt, cnt);
                cnt = 0;
            }
        }
    }

    // Print the maximum consecutive 1's
    // followed by 0
    Console.Write(maxCnt +"\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 1, 1, 1, 0,
                0, 1, 1, 0, 0, 1 };
    int N = arr.Length;

    // Function Call
    noOfMoves(arr, N);
    int []arr1 = { 1, 0, 1, 0, 1, 0, 1, 0 };
    N = arr1.Length;

    // Function Call
    noOfMoves(arr1, N);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to find the maximum number
// of 1's before 0
function noOfMoves(arr, n)
{
    let cnt = 0;
    let maxCnt = 0;

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // If value is 1
        if (arr[i] == 1) {
            cnt++;
        }
        else {

            // If consecutive 1 followed
            // by 0, then update the maxCnt
            if (cnt != 0) {
                maxCnt = Math.max(maxCnt, cnt);
                cnt = 0;
            }
        }
    }

    // Print the maximum consecutive 1's
    // followed by 0
    document.write( maxCnt + "<br>");
}

// Driver Code

    let arr = [ 0, 1, 1, 1, 1, 0,
                0, 1, 1, 0, 0, 1 ];
    let N = arr.length;

    // Function Call
    noOfMoves(arr, N);
    let arr1 = [ 1, 0, 1, 0, 1, 0, 1, 0 ];
    N = arr.length;

    // Function Call
    noOfMoves(arr1, N);

//This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
4
1
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。