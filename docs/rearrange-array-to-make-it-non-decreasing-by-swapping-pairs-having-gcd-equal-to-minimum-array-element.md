# 通过交换 GCD 等于最小数组元素的对，重新排列数组使其不减少

> 原文:[https://www . geeksforgeeks . org/rearray-array-to-make-it-非减交换-pairs-having-gcd-等于最小数组-element/](https://www.geeksforgeeks.org/rearrange-array-to-make-it-non-decreasing-by-swapping-pairs-having-gcd-equal-to-minimum-array-element/)

给定一个由 **N** 个正整数组成的[数组，](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过交换对 **(arr[i]，arr[j])** 使数组不递减，这样 **i！= j (1 ≤ i，j ≤ n)** 和[**GCD**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)**(arr[I]，arr[j])** 等于数组中存在的[最小元素。](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

**示例:**

> **输入:** arr[] = {4，3，6，6，2，9}
> **输出:**是
> **说明:**
> 最小阵元= 2。
> 交换 arr[0]和 arr[2]，因为 gcd(4，6) = 2。数组修改为{6，3，4，6，2，9}。
> 交换 arr[0]和 arr[4]，因为 gcd(6，2) = 2。
> 因此，修改后的数组{2，3，4，6，6，9}是非递减的。
> 
> **输入:** arr[] = {7，5，2，2，4}
> 输出:否

**进场:**

1.  首先[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)到[找到最小元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)。将所有这些元素存储在另一个数组中[对该数组进行排序](https://www.geeksforgeeks.org/sorting-algorithms/)。
2.  对于每个数组元素，检查它是否在正确的位置。如果发现为真，继续下一个元素。否则，检查它是否能被数组的最小元素整除，因为只有这些元素的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 与数组的[最小元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)相等。
3.  如果任何数组元素不在正确的位置，并且该元素不能被数组的最小元素整除，则打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the array
// can be made non-decreasing
bool check(int a[], int n)
{
    int b[n];
    int minElement = INT_MAX;

    // Iterate till N
    for(int i = 0; i < n; i++)
    {

        // Find the minimum element
        b[i] = a[i];
        minElement = min(minElement, a[i]);
    }

    // Sort the array
    sort(b, b + n);
    int k = 1;

    // Iterate till N
    for(int i = 0; i < n; i++)
    {

        // Check if the element is
        // at its correct position
        if (a[i] != b[i] &&
            a[i] % minElement != 0)
        {
            k = 0;
            break;
        }
    }

    // Return the answer
    return k == 1 ? true : false;
}

// Driver Code
int main()
{
    int a[] = { 4, 3, 6, 6, 2, 9 };

    int n = sizeof(a) / sizeof(a[0]);

    // Print the answer
    if (check(a, n) == true)
        cout << "Yes \n";
    else
        cout<<"No \n";

    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.io.*;
import java.util.*;
import java.math.*;

class GFG {

    // Function to check if the array
    // can be made non-decreasing
    public static boolean check(int[] a, int n)
    {
        int[] b = new int[n];
        int minElement = Integer.MAX_VALUE;

        // Iterate till N
        for (int i = 0; i < n; i++) {
            // Find the minimum element
            b[i] = a[i];
            minElement
                = Math.min(minElement, a[i]);
        }

        // Sort the array
        Arrays.sort(b);
        int k = 1;

        // Iterate till N
        for (int i = 0; i < n; i++) {
            // Check if the element is
            // at its correct position
            if (a[i] != b[i]
                && a[i] % minElement != 0) {
                k = 0;
                break;
            }
        }

        // Return the answer
        return k == 1 ? true : false;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] a = { 4, 3, 6, 6, 2, 9 };

        int n = a.length;

        // Print the answer
        if (check(a, n) == true) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach
import sys

# Function to check if the array
# can be made non-decreasing
def check(a, n):

    b = [None] * n
    minElement = sys.maxsize

    # Iterate till N
    for i in range(0, n):

        # Find the minimum element
        b[i] = a[i]
        minElement = min(minElement, a[i])

    # Sort the array
    b.sort()
    k = 1

    # Iterate till N
    for i in range(0, n):

        # Check if the element is
        # at its correct position
        if ((a[i] != b[i]) and
            (a[i] % minElement != 0)):
            k = 0
            break

    # Return the answer
    if k == 1:
        return True
    else:
        return False

# Driver Code
if __name__ == "__main__":

    a = [ 4, 3, 6, 6, 2, 9 ]

    n = len(a)

    # Print the answer
    if check(a, n) == True:
        print("Yes")
    else:
        print("No")

# This code is contributed by akhilsaini
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to check if the array
// can be made non-decreasing
static bool check(int[] a, int n)
{
    int[] b = new int[n];
    int minElement = int.MaxValue;

    // Iterate till N
    for(int i = 0; i < n; i++)
    {

        // Find the minimum element
        b[i] = a[i];
        minElement = Math.Min(minElement, a[i]);
    }

    // Sort the array
    Array.Sort(b);
    int k = 1;

    // Iterate till N
    for(int i = 0; i < n; i++)
    {

        // Check if the element is
        // at its correct position
        if (a[i] != b[i] &&
            a[i] % minElement != 0)
        {
            k = 0;
            break;
        }
    }

    // Return the answer
    return k == 1 ? true : false;
}

// Driver Code
static public void Main()
{
    int[] a = { 4, 3, 6, 6, 2, 9 };

    int n = a.Length;

    // Print the answer
    if (check(a, n) == true)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

   // Function to check if the array
    // can be made non-decreasing
    function check(a, n)
    {
        let b = new Array(n).fill(0);
        let minElement = Number.MAX_VALUE;

        // Iterate till N
        for (let i = 0; i < n; i++) {
            // Find the minimum element
            b[i] = a[i];
            minElement
                = Math.min(minElement, a[i]);
        }

        // Sort the array
        b.sort();
        let k = 1;

        // Iterate till N
        for (let i = 0; i < n; i++) {
            // Check if the element is
            // at its correct position
            if (a[i] != b[i]
                && a[i] % minElement != 0) {
                k = 0;
                break;
            }
        }

        // Return the answer
        return k == 1 ? true : false;
    }

// Driver Code

    let a = [ 4, 3, 6, 6, 2, 9 ];

        let n = a.length;

        // Prlet the answer
        if (check(a, n) == true) {
            document.write("Yes");
        }
        else {
           document.write("No");
        }

 // This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N logN)*
***辅助空间:** O(N)*