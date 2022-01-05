# 在叠加序列中找到给定和的子序列

> 原文:[https://www . geesforgeks . org/find-the-subsequence-with-given-sum-in-a-superincreasing-sequence/](https://www.geeksforgeeks.org/find-the-subsequence-with-given-sum-in-a-superincreasing-sequence/)

正实数序列 **S <sub>1</sub>** 、 **S <sub>2</sub>** 、 **S <sub>3</sub>** 、…、 **S <sub>N</sub>** 如果序列的每个元素都大于序列中所有先前元素的和，则称为**叠加序列**。例如 **1，3，6，13，27，52** 就是这样的子序列。
现在，给定一个叠加序列 **S** 和该序列的一个子序列的**和**，任务是找到该子序列。
**举例:**

> **输入:** S[] = {17，25，46，94，201，400}，和= 272
> **输出:**25 46 201
> 25+46+201 = 272
> **输入:** S[] = {1，2，4，8，16}，和= 12
> **输出:** 4 8

**进场:**这个问题可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。从数组的最后一个元素开始到第一个元素，有两种情况:

1.  **总和< arr[i]:** 在这种情况下，当前元素不能是所需子序列的一部分，因为包含它之后，子序列的总和将超过给定的总和。所以丢弃当前元素。
2.  **sum ≥ arr[i]:** 在这种情况下，当前元素必须包含在所需的子序列中。这是因为如果不包括当前元素，那么数组中先前元素的总和将小于当前元素(因为它是一个叠加序列)，而当前元素又将小于所需的总和。所以取当前元素，更新总和为**总和=总和–arr[I]**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required subsequence
void findSubSeq(int arr[], int n, int sum)
{

    for (int i = n - 1; i >= 0; i--) {

        // Current element cannot be a part
        // of the required subsequence
        if (sum < arr[i])
            arr[i] = -1;

        // Include current element in
        // the required subsequence
        // So update the sum
        else
            sum -= arr[i];
    }

    // Print the elements of the
    // required subsequence
    for (int i = 0; i < n; i++) {

        // If the current element was
        // included in the subsequence
        if (arr[i] != -1)
            cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 17, 25, 46, 94, 201, 400 };
    int n = sizeof(arr) / sizeof(int);
    int sum = 272;

    findSubSeq(arr, n, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find the required subsequence
    static void findSubSeq(int arr[], int n, int sum)
    {
        for (int i = n - 1; i >= 0; i--)
        {

            // Current element cannot be a part
            // of the required subsequence
            if (sum < arr[i])
                arr[i] = -1;

            // Include current element in
            // the required subsequence
            // So update the sum
            else
                sum -= arr[i];
        }

        // Print the elements of the
        // required subsequence
        for (int i = 0; i < n; i++)
        {

            // If the current element was
            // included in the subsequence
            if (arr[i] != -1)
                System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 17, 25, 46, 94, 201, 400 };
        int n = arr.length;
        int sum = 272;

        findSubSeq(arr, n, sum);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required subsequence
def findSubSeq(arr, n, sum) :

    for i in range(n - 1, -1, -1) :

        # Current element cannot be a part
        # of the required subsequence
        if (sum < arr[i]) :
            arr[i] = -1;

        # Include current element in
        # the required subsequence
        # So update the sum
        else :
            sum -= arr[i];

    # Print the elements of the
    # required subsequence
    for i in range(n) :

        # If the current element was
        # included in the subsequence
        if (arr[i] != -1) :
            print(arr[i], end = " ");

# Driver code
if __name__ == "__main__" :

    arr = [ 17, 25, 46, 94, 201, 400 ];
    n = len(arr);
    sum = 272;

    findSubSeq(arr, n, sum);

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the required subsequence
    static void findSubSeq(int []arr,
                           int n, int sum)
    {
        for (int i = n - 1; i >= 0; i--)
        {

            // Current element cannot be a part
            // of the required subsequence
            if (sum < arr[i])
                arr[i] = -1;

            // Include current element in
            // the required subsequence
            // So update the sum
            else
                sum -= arr[i];
        }

        // Print the elements of the
        // required subsequence
        for (int i = 0; i < n; i++)
        {

            // If the current element was
            // included in the subsequence
            if (arr[i] != -1)
                Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 17, 25, 46, 94, 201, 400 };
        int n = arr.Length;
        int sum = 272;

        findSubSeq(arr, n, sum);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find the required subsequence
function findSubSeq(arr, n, sum) {

    for (let i = n - 1; i >= 0; i--) {

        // Current element cannot be a part
        // of the required subsequence
        if (sum < arr[i])
            arr[i] = -1;

        // Include current element in
        // the required subsequence
        // So update the sum
        else
            sum -= arr[i];
    }

    // Prlet the elements of the
    // required subsequence
    for (let i = 0; i < n; i++) {

        // If the current element was
        // included in the subsequence
        if (arr[i] != -1)
            document.write(arr[i] + " ");
    }
}

// Driver code

let arr = [17, 25, 46, 94, 201, 400];
let n = arr.length;
let sum = 272;

findSubSeq(arr, n, sum);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
25 46 201
```

**时间复杂度:** O(n)