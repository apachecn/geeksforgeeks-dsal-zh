# 对数组进行排序，最小的在第 0 个索引处，次小的在最后一个索引处，以此类推

> 原文:[https://www . geeksforgeeks . org/sort-array-this-minist-at-0th-index-next-minist-it-at-last-index-等等/](https://www.geeksforgeeks.org/sort-array-such-that-smallest-is-at-0th-index-and-next-smallest-it-at-last-index-and-so-on/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、**arr【】**，任务是重新排列数组元素，使得最小元素位于**第 0 个**位置，第二小元素位于 **(N-1)个**位置，第三小元素位于**第 1 个**位置，**第 4 个**最小元素位于 **(N-2)个**位置，依此类推

**示例:**

> **输入:** arr[] = {10，23，12，17，9}
> **输出:** 9 12 23 17 10
> **解释:**
> 最小的元素是 9，放在索引 0 中。
> 那么第二小的元素是 10，放在最后一个位置。
> 第三小元素从开始放在第二个位置。
> 倒数第二位第四个最小的，以此类推。
> **输入:** arr[] = {1，3，3，4，5}
> **输出:** 1 3 5 4 3

**方法:**我们将使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。其思想是从数组的变量 ***i*** 标记的开始到变量 ***j*** 标记的结束交替迭代，直到它们在中间相遇，并不断更新这些索引处的最小值。以下是步骤:

1.  将索引 **i** 处的元素设置为*最小值。*迭代*T5【I，j】*并将该范围内的每个值与**arr【I】**进行比较，如果该范围内的值小于**arr【I】**，则在**arr【I】**和**当前元素**之间交换该值。增加 **i** 的值。
2.  将索引 **j** 处的元素设置为*最小值。*迭代*T5【I，j】*并将该范围内的每个值与**arr【j】**进行比较，如果该范围内的值小于**arr【j】**，则在**arr【j】**和**当前元素**之间交换该值。减少 **j** 的值。
3.  在第一次迭代时将最小元素放置在第***I*****<sup>th</sup>**位置，将下一个最小元素放置在第***j*****<sup>th</sup>**位置。这样做，直到 ***i*** 和 ***j*** 指向同一个位置。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the rearrangement
void rearrange(int a[], int N)
{

    // Initialize variables
    int i = 0, j = N - 1;
    int min = 0, k, x = 0, temp;

    // Loop until i crosses j
    while (i < j)
    {

        // This check is to find the
        // minimum values in the
        // ascending order
        for(k = i; k <= j; k++)
        {
            if (a[k] < a[min])
                min = k;
        }

        // Condition to alternatively
        // iterate variable i and j
        if (x % 2 == 0)
        {

            // Perform swap operation
            temp = a[i];
            a[i] = a[min];
            a[min] = temp;

            // Increment i
            i++;

            // Assign the value of min
            min = i;
        }
        else
        {

            // Perform swap
            temp = a[j];
            a[j] = a[min];
            a[min] = temp;

            // Decrement i
            j--;

            // Assign the value of min
            min = j;
        }
        x++;
    }

    // Print the array
    for(i = 0; i < N; i++)
        cout << a[i] << " ";
}

// Driver Code
int main()
{

    // Given Array arr[]
    int arr[] = { 1, 3, 3, 4, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    rearrange(arr, N);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

public class GFG {

    // Function to perform the rearrangement
    static void rearrange(int[] a)
    {
        // Initialize variables
        int i = 0, j = a.length - 1;
        int min = 0, k, x = 0, temp;

        // Loop until i crosses j
        while (i < j) {

            // This check is to find the
            // minimum values in the
            // ascending order

            for (k = i; k <= j; k++) {
                if (a[k] < a[min])
                    min = k;
            }

            // Condition to alternatively
            // iterate variable i and j
            if (x % 2 == 0) {

                // Perform swap operation
                temp = a[i];
                a[i] = a[min];
                a[min] = temp;

                // Increment i
                i++;

                // Assign the value of min
                min = i;
            }
            else {

                // Perform swap
                temp = a[j];
                a[j] = a[min];
                a[min] = temp;

                // Decrement i
                j--;

                // Assign the value of min
                min = j;
            }
            x++;
        }

        // Print the array
        for (i = 0; i < a.length; i++)
            System.out.print(a[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Array arr[]
        int arr[] = { 1, 3, 3, 4, 5 };

        // Function Call
        rearrange(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
# Function to perform
# the rearrangement
def rearrange(a, N):

    # Initialize variables
    i = 0
    j = N - 1
    min = 0
    x = 0

    # Loop until i crosses j
    while (i < j):

        # This check is to find the
        # minimum values in the
        # ascending order
        for k in range (i, j + 1):
            if (a[k] < a[min]):
                min = k

        # Condition to alternatively
        # iterate variable i and j
        if (x % 2 == 0):

            # Perform swap operation
            temp = a[i]
            a[i] = a[min]
            a[min] = temp

            # Increment i
            i += 1

            # Assign the value of min
            min = i

        else:

            # Perform swap
            temp = a[j]
            a[j] = a[min]
            a[min] = temp

            # Decrement i
            j -= 1

            # Assign the value of min
            min = j

        x += 1

    # Print the array
    for i in range (N):
        print (a[i] ,end = " ")

# Driver Code
if __name__ == "__main__":

    # Given Array arr[]
    arr = [1, 3, 3, 4, 5]

    N = len(arr)

    # Function call
    rearrange(arr, N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to perform the rearrangement
static void rearrange(int[] a)
{

    // Initialize variables
    int i = 0, j = a.Length - 1;
    int min = 0, k, x = 0, temp;

    // Loop until i crosses j
    while (i < j)
    {

        // This check is to find the
        // minimum values in the
        // ascending order

        for(k = i; k <= j; k++)
        {
            if (a[k] < a[min])
                min = k;
        }

        // Condition to alternatively
        // iterate variable i and j
        if (x % 2 == 0)
        {

            // Perform swap operation
            temp = a[i];
            a[i] = a[min];
            a[min] = temp;

            // Increment i
            i++;

            // Assign the value of min
            min = i;
        }
        else
        {

            // Perform swap
            temp = a[j];
            a[j] = a[min];
            a[min] = temp;

            // Decrement i
            j--;

            // Assign the value of min
            min = j;
        }
        x++;
    }

    // Print the array
    for(i = 0; i < a.Length; i++)
        Console.Write(a[i] + " ");
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = { 1, 3, 3, 4, 5 };

    // Function call
    rearrange(arr);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to perform the rearrangement
    function rearrange(a) {
        // Initialize variables
        var i = 0, j = a.length - 1;
        var min = 0, k, x = 0, temp;

        // Loop until i crosses j
        while (i < j) {

            // This check is to find the
            // minimum values in the
            // ascending order

            for (k = i; k <= j; k++) {
                if (a[k] < a[min])
                    min = k;
            }

            // Condition to alternatively
            // iterate variable i and j
            if (x % 2 == 0) {

                // Perform swap operation
                temp = a[i];
                a[i] = a[min];
                a[min] = temp;

                // Increment i
                i++;

                // Assign the value of min
                min = i;
            } else {

                // Perform swap
                temp = a[j];
                a[j] = a[min];
                a[min] = temp;

                // Decrement i
                j--;

                // Assign the value of min
                min = j;
            }
            x++;
        }

        // Prvar the array
        for (i = 0; i < a.length; i++)
            document.write(a[i] + " ");
    }

    // Driver Code

        // Given Array arr
        var arr = [ 1, 3, 3, 4, 5 ];

        // Function Call
        rearrange(arr);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
1 3 5 4 3
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*