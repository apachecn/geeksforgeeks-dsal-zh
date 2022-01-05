# 构建一个由 A 和 B 组成的 AP 序列，该序列具有最小可能的第 n 项

> 原文:[https://www . geesforgeks . org/construct-an-AP-series-compose-a-and-b-having-minimum-n-term/](https://www.geeksforgeeks.org/construct-an-ap-series-consisting-of-a-and-b-having-minimum-possible-nth-term/)

给定两个整数 **A、B** ，它们是算术级数的任意两个项，以及一个整数 **N** ，任务是构造一个大小为 **N** 的[算术级数](https://www.geeksforgeeks.org/arithmetic-progression/)系列，使得它必须包括 **A** 和 **B** ，并且 AP 的 **N** <sup>第</sup>项应该是最小的。

**示例:**

> **输入:** N = 5，A = 20，B = 50
> **输出:** 10 20 30 40 50
> **解释:**
> 可能的 AP 序列之一是{10，20，30，40，50}有 50 作为第 5 个<sup>的</sup>值，这是最小的可能。
> 
> **输入:** N = 2，A = 1，B = 49
> T3】输出: 1 49

**方法:**AP 的 **N <sup>第</sup>T5】项由**X<sub>N</sub>= X+(N–1)* d**给出，其中 **X** 为第一项， **d** 为共同区别。为了使最大的元素最小，最小化 **x** 和 **d** 。可以观察到 **X** 的值不能超过 **min(A，B)******d**的值不能超过**ABS(A–B)**。****

1.  **现在，使用相同的公式为 **x (** 从 **1** 到 **min(A，B)** )和 **d** (从 **1** 到**ABS(A–B)**)的每个可能值构造 AP。**
2.  **现在，将数组 **arr[]** 构造为 **{x，x + d，x + 2d，…，x+d *(N–1)}**。**
3.  **检查其中是否存在 **A** 和 **B** 以及**N<sup>th</sup>T7】元素是否为最小可能。如果发现为真，则通过构造的数组 **arr[]** 更新 **ans[]** 。****
4.  **否则，进一步迭代并检查 **x** 和 **d** 的其他值。**
5.  **最后打印**ans【】**作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if both a and
// b are present in the AP series or not
bool check_both_present(int arr[], int N,
                        int a, int b)
{
    bool f1 = false, f2 = false;

    // Iterate over the array arr[]
    for (int i = 0; i < N; i++) {

        // If a is present
        if (arr[i] == a) {
            f1 = true;
        }

        // If b is present
        if (arr[i] == b) {
            f2 = true;
        }
    }

    // If both are present
    if (f1 && f2) {
        return true;
    }

    // Otherwise
    else {
        return false;
    }
}

// Function to print all the elements
// of the Arithmetic Progression
void print_array(int ans[], int N)
{
    for (int i = 0; i < N; i++) {
        cout << ans[i] << " ";
    }
}

// Function to construct AP series
// consisting of A and B with
// minimum Nth term
void build_AP(int N, int a, int b)
{
    // Stores the resultant series
    int arr[N], ans[N];

    // Initialise ans[i] as INT_MAX
    for (int i = 0; i < N; i++)
        ans[i] = INT_MAX;

    int flag = 0;

 // Maintain a smaller than b
    if (a > b) {
        swap(a, b);
    }

    // Difference between a and b
    int diff = b - a;

    // Check for all possible combination
    // of start and common difference d
    for (int start = 1;
         start <= a; start++) {

        for (int d = 1;
             d <= diff; d++) {

            // Initialise arr[0] as start
            arr[0] = start;

            for (int i = 1; i < N; i++) {

                arr[i] = arr[i - 1] + d;
            }

            // Check if both a and b are
            // present or not and the Nth
            // term is the minimum or not
            if (check_both_present(arr, N, a, b)
                && arr[N - 1] < ans[N - 1]) {

                // Update the answer
                for (int i = 0; i < N; i++) {
                    ans[i] = arr[i];
                }
            }
        }
    }

    // Print the resultant array
    print_array(ans, N);
}

// Driver Code
int main()
{
    int N = 5, A = 20, B = 50;

    // Function Call
    build_AP(N, A, B);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if both a and
// b are present in the AP series or not
public static boolean check_both_present(int[] arr,
                                         int N, int a,
                                         int b)
{
    boolean f1 = false, f2 = false;

    // Iterate over the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If a is present
        if (arr[i] == a)
        {
            f1 = true;
        }

        // If b is present
        if (arr[i] == b)
        {
            f2 = true;
        }
    }

    // If both are present
    if (f1 && f2)
    {
        return true;
    }

    // Otherwise
    else
    {
        return false;
    }
}

// Function to print all the elements
// of the Arithmetic Progression
public static void print_array(int[] ans, int N)
{
    for(int i = 0; i < N; i++)
    {
        System.out.print(ans[i] + " ");
    }
}

// Function to construct AP series
// consisting of A and B with
// minimum Nth term
public static void build_AP(int N, int a, int b)
{

    // Stores the resultant series
    int[] arr = new int[N];
    int[] ans = new int[N];

    // Initialise ans[i] as INT_MAX
    for(int i = 0; i < N; i++)
        ans[i] = Integer.MAX_VALUE;

    int flag = 0;

    // Maintain a smaller than b
    if (a > b)
    {

        // swap(a and b)
        a += (b - (b = a));
    }

    // Difference between a and b
    int diff = b - a;

    // Check for all possible combination
    // of start and common difference d
    for(int start = 1; start <= a; start++)
    {
        for(int d = 1; d <= diff; d++)
        {

            // Initialise arr[0] as start
            arr[0] = start;

            for(int i = 1; i < N; i++)
            {
                arr[i] = arr[i - 1] + d;
            }

            // Check if both a and b are
            // present or not and the Nth
            // term is the minimum or not
            if (check_both_present(arr, N, a, b) &&
                arr[N - 1] < ans[N - 1])
            {

                // Update the answer
                for(int i = 0; i < N; i++)
                {
                    ans[i] = arr[i];
                }
            }
        }
    }

    // Print the resultant array
    print_array(ans, N);
}

// Driver Code
public static void main(String[] args)
{
    int N = 5, A = 20, B = 50;

    // Function call
    build_AP(N, A, B);
}
}

// This code is contributed by akhilsaini
```

## **蟒蛇 3**

```
# Python3 program for the above approach
import sys

# Function to check if both a and
# b are present in the AP series or not
def check_both_present(arr, N, a, b):

    f1 = False
    f2 = False

    # Iterate over the array arr[]
    for i in range(0, N):

        # If a is present
        if arr[i] == a:
            f1 = True

        # If b is present
        if arr[i] == b:
            f2 = True

    # If both are present
    if f1 and f2:
        return True

    # Otherwise
    else:
        return False

# Function to print all the elements
# of the Arithmetic Progression
def print_array(ans, N):

    for i in range(0, N):
        print(ans[i], end = " ")

# Function to construct AP series
# consisting of A and B with
# minimum Nth term
def build_AP(N, a, b):

    INT_MAX = sys.maxsize

    # Stores the resultant series
    arr = [None for i in range(N)]

    # Initialise ans[i] as INT_MAX
    ans = [INT_MAX for i in range(N)]

    flag = 0

    # Maintain a smaller than b
    if a > b:

        # Swap a and b
        a, b = b, a

    # Difference between a and b
    diff = b - a

    # Check for all possible combination
    # of start and common difference d
    for start in range(1, a + 1):
        for d in range(1, diff + 1):

            # Initialise arr[0] as start
            arr[0] = start

            for i in range(1, N):
                arr[i] = arr[i - 1] + d

            # Check if both a and b are
            # present or not and the Nth
            # term is the minimum or not
            if ((check_both_present(arr, N, a, b) and
                 arr[N - 1] < ans[N - 1])):

                # Update the answer
                for i in range(0, N):
                    ans[i] = arr[i]

    # Print the resultant array
    print_array(ans, N)

# Driver Code
if __name__ == "__main__":

    N = 5
    A = 20
    B = 50

    # Function call
    build_AP(N, A, B)

# This code is contributed by akhilsaini
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to check if both a and
// b are present in the AP series or not
static bool check_both_present(int[] arr, int N,
                               int a, int b)
{
    bool f1 = false, f2 = false;

    // Iterate over the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If a is present
        if (arr[i] == a)
        {
            f1 = true;
        }

        // If b is present
        if (arr[i] == b)
        {
            f2 = true;
        }
    }

    // If both are present
    if (f1 && f2)
    {
        return true;
    }

    // Otherwise
    else
    {
        return false;
    }
}

// Function to print all the elements
// of the Arithmetic Progression
static void print_array(int[] ans, int N)
{
    for(int i = 0; i < N; i++)
    {
        Console.Write(ans[i] + " ");
    }
}

// Function to construct AP series
// consisting of A and B with
// minimum Nth term
static void build_AP(int N, int a, int b)
{

    // Stores the resultant series
    int[] arr = new int[N];
    int[] ans = new int[N];

    // Initialise ans[i] as INT_MAX
    for(int i = 0; i < N; i++)
        ans[i] = int.MaxValue;

    // Maintain a smaller than b
    if (a > b)
    {

        // Swap a and b
        a += (b - (b = a));
    }

    // Difference between a and b
    int diff = b - a;

    // Check for all possible combination
    // of start and common difference d
    for(int start = 1; start <= a; start++)
    {
        for(int d = 1; d <= diff; d++)
        {

            // Initialise arr[0] as start
            arr[0] = start;

            for(int i = 1; i < N; i++)
            {
                arr[i] = arr[i - 1] + d;
            }

            // Check if both a and b are
            // present or not and the Nth
            // term is the minimum or not
            if (check_both_present(arr, N, a, b) &&
                arr[N - 1] < ans[N - 1])
            {

                // Update the answer
                for(int i = 0; i < N; i++)
                {
                    ans[i] = arr[i];
                }
            }
        }
    }

    // Print the resultant array
    print_array(ans, N);
}

// Driver Code
static public void Main()
{
    int N = 5, A = 20, B = 50;

    // Function call
    build_AP(N, A, B);
}
}

// This code is contributed by akhilsaini
```

## **java 描述语言**

```
<script>
// javascript program for the
// above approach

// Function to check if both a and
// b are present in the AP series or not
function check_both_present(arr, N, a, b)
{
    let f1 = false, f2 = false;

    // Iterate over the array arr[]
    for(let i = 0; i < N; i++)
    {

        // If a is present
        if (arr[i] == a)
        {
            f1 = true;
        }

        // If b is present
        if (arr[i] == b)
        {
            f2 = true;
        }
    }

    // If both are present
    if (f1 && f2)
    {
        return true;
    }

    // Otherwise
    else
    {
        return false;
    }
}

// Function to print all the elements
// of the Arithmetic Progression
function print_array(ans, N)
{
    for(let i = 0; i < N; i++)
    {
        document.write(ans[i] + " ");
    }
}

// Function to construct AP series
// consisting of A and B with
// minimum Nth term
function build_AP(N, a, b)
{

    // Stores the resultant series
    let arr = Array(N).fill(0);
    let ans = Array(N).fill(0);

    // Initialise ans[i] as let_MAX
    for(let i = 0; i < N; i++)
        ans[i] = Number.MAX_VALUE;

    let flag = 0;

    // Maintain a smaller than b
    if (a > b)
    {

        // swap(a and b)
        a += (b - (b = a));
    }

    // Difference between a and b
    let diff = b - a;

    // Check for all possible combination
    // of start and common difference d
    for(let start = 1; start <= a; start++)
    {
        for(let d = 1; d <= diff; d++)
        {

            // Initialise arr[0] as start
            arr[0] = start;

            for(let i = 1; i < N; i++)
            {
                arr[i] = arr[i - 1] + d;
            }

            // Check if both a and b are
            // present or not and the Nth
            // term is the minimum or not
            if (check_both_present(arr, N, a, b) &&
                arr[N - 1] < ans[N - 1])
            {

                // Update the answer
                for(let i = 0; i < N; i++)
                {
                    ans[i] = arr[i];
                }
            }
        }
    }

    // Print the resultant array
    print_array(ans, N);
}

// Driver Code

     let N = 5, A = 20, B = 50;

    // Function call
    build_AP(N, A, B);

  // This code is contributed by avijitmondal1998.
</script>
```

****Output:** 

```
10 20 30 40 50
```** 

*****时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)***