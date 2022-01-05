# 检查是否有可能对 N 个对象进行着色，以便对每个对象使用完全不同的颜色

> 原文:[https://www . geeksforgeeks . org/check-如果可能的话-给 n 个对象上色-这样-与对象完全一样-使用不同的颜色/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-color-n-objects-such-that-for-ith-object-exactly-arri-distinct-colors-are-used/)

给定由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是检查是否有可能对 **N** 对象进行着色，使得对于数组中的 **i <sup>th</sup>** 元素，除了 **i <sup>th</sup>** 对象之外，在对所有对象进行着色时，精确地存在**arr【I】**不同的颜色。

**示例:**

> **输入:** arr[] = {1，2，2}
> **输出:**是
> **解释:**
> 可能的配色方式之一是:{“红”“蓝”“蓝”}。
> 
> 1.  对于 arr[0](=1)，正好有一种不同的颜色，即“蓝色”。
> 2.  对于 arr[1](=2)，正好有两种不同的颜色，即“蓝色”和“红色”。
> 3.  对于 arr[2](=3)，正好有两种不同的颜色，即“蓝色”和“红色”。
> 
> **输入:** arr[] = {4，3，4，3，4}
> **输出:**否

**方法:**根据以下观察结果可以解决问题:

> 1.  For **2** objects, it is common to have **n-2** objects when calculating the number of different colors. Therefore, there can be at most a difference of **1** between the maximum element and the minimum element of [array](https://www.geeksforgeeks.org/array-data-structure/) **arr [].**
> 2.  There are two situations now:
>     1.  If the maximum element and the minimum element are equal, then the answer is **"Yes",** only when the element is **n–1** or the element is less than or equal to **n/2** , because each color can be used many times.
>     2.  If the difference between the maximum element and the minimum element is **1** , then the number of different colors in the **n** object must be equal to the maximum element, because the minimum element is less than the maximum element by **1** .
>         *   Now suppose that the frequency of the smallest element is **x** and the frequency of the largest element is **y** , then the answer is " **is** " if and only if **x+1 ≤ a ≤ x+y/2** (based on observation).

按照以下步骤解决问题:

*   首先[对数组进行升序排序。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   如果 **arr[N-1]** 和 **arr[0]** 的差值大于 **1、**则打印“ **No** ”。
*   否则，如果 **arr[N-1]** 等于 **arr[0]** ，则检查以下内容:
    *   如果 **arr[N-1] = N-1** 或 **2*arr[N-1] < = N** ，则打印“**是**”。
    *   否则，打印“**否**”。
*   否则，计算最小和最大元素的频率并将其存储在变量中，比如 **X** 和 **Y** ，然后执行以下操作:
    *   如果 **arr[N-1]** 大于 **X** ， **arr[N-1]** 小于或等于 **X+Y/2** ，则打印“**是**”。
    *   否则，打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if coloring is
// possible with give conditions
string checkValid(int arr[], int N)
{

    // Sort the vector
    sort(arr, arr + N);

    // Coloring not possible in case of
    // maximum - minimum element > 1
    if (arr[N - 1] - arr[0] > 1)
        return "No";

    // case 1
    else if (arr[N - 1] == arr[0]) {

        // If h is equal to N-1 or
        // N is greater than 2*h
        if (arr[N - 1] == N - 1
            || 2 * arr[N - 1] <= N)
            return "Yes";
        else
            return "No";
    }
    // Case 2
    else {
        // Stores frequency of minimum element
        int x = 0;

        for (int i = 0; i < N; i++) {

            // Frequency  of minimum element
            if (arr[i] == arr[0])
                x++;
        }

        // Stores frequency of maximum element
        int y = N - x;

        // Condition for case 2
        if ((arr[N - 1] >= x + 1)
            and (arr[N - 1] <= x + y / 2))
            return "Yes";
        else
            return "No";
    }
}

// Driver Code
int main()
{
    // GivenInput
    int arr[] = { 1, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << checkValid(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if coloring is
// possible with give conditions
static String checkValid(int arr[], int N)
{

    // Sort the vector
    Arrays.sort(arr);

    // Coloring not possible in case of
    // maximum - minimum element > 1
    if (arr[N - 1] - arr[0] > 1)
        return "No";

    // Case 1
    else if (arr[N - 1] == arr[0])
    {

        // If h is equal to N-1 or
        // N is greater than 2*h
        if (arr[N - 1] == N - 1
            || 2 * arr[N - 1] <= N)
            return "Yes";
        else
            return "No";
    }

    // Case 2
    else
    {

        // Stores frequency of minimum element
        int x = 0;

        for(int i = 0; i < N; i++)
        {

            // Frequency  of minimum element
            if (arr[i] == arr[0])
                x++;
        }

        // Stores frequency of maximum element
        int y = N - x;

        // Condition for case 2
        if ((arr[N - 1] >= x + 1) &&
            (arr[N - 1] <= x + y / 2))
            return "Yes";
        else
            return "No";
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int[] arr = { 1, 2, 2 };
    int N = arr.length;

    // Function Call
    System.out.print(checkValid(arr, N));
}   
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if coloring is
# possible with give conditions
def checkValid(arr, N):

    # Sort the vector
    arr = sorted(arr)

    # Coloring not possible in case of
    # maximum - minimum element > 1
    if (arr[N - 1] - arr[0] > 1):
        return "No"

    # case 1
    elif (arr[N - 1] == arr[0]):

        # If h is equal to N-1 or
        # N is greater than 2*h
        if (arr[N - 1] == N - 1 or
        2 * arr[N - 1] <= N):
            return "Yes"
        else:
            return "No"
    # Case 2
    else:

        # Stores frequency of minimum element
        x = 0

        for i in range(N):

            # Frequency of minimum element
            if (arr[i] == arr[0]):
                x += 1

        # Stores frequency of maximum element
        y = N - x

        # Condition for case 2
        if ((arr[N - 1] >= x + 1) and
            (arr[N - 1] <= x + y // 2)):
            return "Yes"
        else:
            return "No"

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 1, 2, 2 ]
    N = len(arr)

    # Function Call
    print (checkValid(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if coloring is
// possible with give conditions
static string checkValid(int []arr, int N)
{

    // Sort the vector
    Array.Sort(arr);

    // Coloring not possible in case of
    // maximum - minimum element > 1
    if (arr[N - 1] - arr[0] > 1)
        return "No";

    // case 1
    else if (arr[N - 1] == arr[0]) {

        // If h is equal to N-1 or
        // N is greater than 2*h
        if (arr[N - 1] == N - 1
            || 2 * arr[N - 1] <= N)
            return "Yes";
        else
            return "No";
    }
    // Case 2
    else {
        // Stores frequency of minimum element
        int x = 0;

        for (int i = 0; i < N; i++) {

            // Frequency  of minimum element
            if (arr[i] == arr[0])
                x++;
        }

        // Stores frequency of maximum element
        int y = N - x;

        // Condition for case 2
        if ((arr[N - 1] >= x + 1)
            && (arr[N - 1] <= x + y / 2))
            return "Yes";
        else
            return "No";
    }
}

// Driver Code
public static void Main()
{
    // GivenInput
    int []arr = { 1, 2, 2 };
    int N = arr.Length;

    // Function Call
    Console.Write(checkValid(arr, N));

}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if coloring is
// possible with give conditions
function checkValid(arr, N)
{

    // Sort the vector
    arr.sort((a, b) => a - b);

    // Coloring not possible in case of
    // maximum - minimum element > 1
    if (arr[N - 1] - arr[0] > 1)
        return "No";

    // Case 1
    else if (arr[N - 1] == arr[0])
    {

        // If h is equal to N-1 or
        // N is greater than 2*h
        if (arr[N - 1] == N - 1 ||
        2 * arr[N - 1] <= N)
            return "Yes";
        else
            return "No";
    }

    // Case 2
    else
    {

        // Stores frequency of minimum element
        let x = 0;

        for(let i = 0; i < N; i++)
        {

            // Frequency  of minimum element
            if (arr[i] == arr[0])
                x++;
        }

        // Stores frequency of maximum element
        let y = N - x;

        // Condition for case 2
        if ((arr[N - 1] >= x + 1) &&
            (arr[N - 1] <= x + y / 2))
            return "Yes";
        else
            return "No";
    }
}

// Driver Code

// GivenInput
let arr = [ 1, 2, 2 ];
let N = arr.length;

// Function Call
document.write(checkValid(arr, N));

// This code is contributed by gfgking

</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*