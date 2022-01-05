# 构造数组 B 作为每个后缀数组的最后一个元素，通过对给定数组的每个后缀执行给定操作获得

> 原文:[https://www . geeksforgeeks . org/construct-array-b-作为每个后缀左侧的最后一个元素-array-通过对给定数组的每个后缀执行给定操作获得/](https://www.geeksforgeeks.org/construct-array-b-as-last-element-left-of-every-suffix-array-obtained-by-performing-given-operations-on-every-suffix-of-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印每个[后缀数组](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)的最后一个元素，该元素是通过对数组的每个后缀执行以下操作获得的: **arr[]** :

1.  将后缀数组的元素复制到数组 **suff[]** 中。
2.  将 **i <sup>th</sup>** 后缀元素更新为**suf[I]=(suf[I]OR suf[I+1])–(suf[I]XOR suf[I+1])**将后缀数组的大小减少 **1** 。
3.  重复上述步骤，直到后缀数组的大小不是 **1** 。

**示例:**

> **输入:** arr[] = {2，3，6，5}
> **输出:** 0 0 4 5
> **解释:**
> 执行如下操作:
> 
> 1.  后缀数组{2，3，6，5}:
>     1.  在第一步中，数组修改为{2，2，4}。
>     2.  在第二步中，数组修改为{2，0}
>     3.  在第三步中，数组修改为{0}。
>     4.  因此，剩下的最后一个元素是 0。
> 2.  后缀数组{3，6，5}:
>     1.  在第一步中，数组修改为{2，4}。
>     2.  在第二步中，数组修改为{0}
>     3.  因此，剩下的最后一个元素是 0。
> 3.  后缀数组{6，5}:
>     1.  在第一步中，数组修改为{4}
>     2.  因此，剩下的最后一个元素是 4。
> 4.  后缀数组{5}:
>     1.  它只有一个元素。因此，剩下的最后一个元素是 5。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 0 0 0 4

**天真方法:**最简单的方法是遍历每个后缀数组，通过迭代后缀数组来执行上面给定的操作，然后打印得到的值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**给定的问题可以基于以下观察来解决:

> 1.  From [Bitwise attribute](https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/) :
>     *   **(x | y)—(x ^ y)=(x & y)**
> 2.  Therefore, the last value obtained from the above is the bitwise sum of [and](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) of all elements of the suffix array after the given operation is performed on the suffix array.

按照以下步骤解决问题:

*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-2】**中以相反的顺序迭代，并且在每次迭代中将 **arr[i]** 更新为 **arr[i] & arr[i+1]** 。
*   [在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并使用变量 **i** 执行以下步骤:
    *   打印存储在 **arr[i]** 中的值，作为后缀数组在**【I，N-1】范围内的答案。**

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the last element
// left of every suffix of the array
// after performing the given operati-
// ons on them

void performOperation(int arr[], int N)
{
    // Iterate until i is greater than
    // or equal to 0
    for (int i = N - 2; i >= 0; i--) {
        arr[i] = arr[i] & arr[i + 1];
    }

    // Print the array arr[]
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";
    cout << endl;
}
// Driver Code
int main()
{
    // Input
    int arr[] = { 2, 3, 6, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    performOperation(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the last element
    // left of every suffix of the array
    // after performing the given operati-
    // ons on them
    public static void performOperation(int arr[], int N)
    {

        // Iterate until i is greater than
        // or equal to 0
        for (int i = N - 2; i >= 0; i--) {
            arr[i] = arr[i] & arr[i + 1];
        }

        // Print the array arr[]
        for (int i = 0; i < N; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver Code
    public static void main(String args[])
    {

        // Input
        int arr[] = { 2, 3, 6, 5 };
        int N = arr.length;

        // Function call
        performOperation(arr, N);
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the last element
# left of every suffix of the array
# after performing the given operati-
# ons on them
def performOperation(arr, N):

    # Iterate until i is greater than
    # or equal to 0
    i = N - 2
    while(i >= 0):
        arr[i] = arr[i] & arr[i + 1]
        i -= 1

    # Print the array arr[]
    for i in range(N):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':
    # Input
    arr = [2, 3, 6, 5]
    N = len(arr)

    # Function call
    performOperation(arr, N)

    # This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the last element
// left of every suffix of the array
// after performing the given operati-
// ons on them
static void performOperation(int []arr, int N)
{

    // Iterate until i is greater than
    // or equal to 0
    for(int i = N - 2; i >= 0; i--)
    {
        arr[i] = arr[i] & arr[i + 1];
    }

    // Print the array arr[]
    for(int i = 0; i < N; i++)
        Console.Write(arr[i] + " ");

    Console.WriteLine();
}

// Driver Code
public static void Main()
{

    // Input
    int []arr = { 2, 3, 6, 5 };
    int N = arr.Length;

    // Function call
    performOperation(arr, N);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the last element
        // left of every suffix of the array
        // after performing the given operati-
        // ons on them

        function performOperation(arr, N) {
            // Iterate until i is greater than
            // or equal to 0
            for (let i = N - 2; i >= 0; i--) {
                arr[i] = arr[i] & arr[i + 1];
            }

            // Print the array arr[]
            for (let i = 0; i < N; i++)
                document.write(arr[i] + " ");

            document.write('<br>')
        }
        // Driver Code

        // Input
        let arr = [2, 3, 6, 5];
        let N = arr.length;

        // Function call
        performOperation(arr, N);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
0 0 4 5 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)