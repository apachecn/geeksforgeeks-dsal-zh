# 通过交换给定数组中奇数和偶数元素的位置来重新排列数组

> 原文:[https://www . geeksforgeeks . org/通过交换给定数组中奇偶元素的位置来重新排列数组/](https://www.geeksforgeeks.org/rearrange-array-by-interchanging-positions-of-even-and-odd-elements-in-the-given-array/)

给定一个由偶数和奇数元素相等的正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]****N**。任务是使用就地交换来交换数组中偶数和奇数元素的位置。

**示例:**

> **输入:** arr[] = {1，3，2，4}
> **输出:** 2 4 1 3
> **解释:**
> 在重新排列给定数组之前，索引 0 和 1 有奇数元素，索引 2 和 3 有偶数元素。
> 重排后，数组变成{2，4，1，3}，其中索引 0 和 1 有偶数元素，索引 2 和 3 有奇数元素。
> 
> **输入:** arr[] = {2，2，1，3}
> **输出:** 1 3 2 2
> **解释:**
> 在重新排列给定数组之前，索引 0 和 1 具有偶数元素，索引 2 和 3 具有奇数元素。
> 重排后，数组变成{1，3，2，2}，其中索引 0 和 1 有奇数元素，索引 2 和 3 有偶数元素。

**天真方法:**最简单的方法是[使用两个循环迭代数组元素](https://www.geeksforgeeks.org/iterating-arrays-java/)，外循环挑选数组的每个元素，内循环是为挑选的元素找到相反的奇偶元素并交换它们。交换元素后，将拾取的元素标记为负，以免再次拾取。最后，使所有元素都为正，并打印数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to replace each even
// element by odd and vice-versa
// in a given array
void replace(int arr[], int n)
{

    // Traverse array
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // If current element is even
            // then swap it with odd
            if (arr[i] >= 0 && arr[j] >= 0 &&
                arr[i] % 2 == 0 &&
                arr[j] % 2 != 0)
            {

                // Perform Swap
                int tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;

                // Change the sign
                arr[j] = -arr[j];

                break;
            }

            // If current element is odd
            // then swap it with even
            else if (arr[i] >= 0 && arr[j] >= 0 &&
                     arr[i] % 2 != 0 &&
                     arr[j] % 2 == 0)
            {

                // Perform Swap
                int tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;

                // Change the sign
                arr[j] = -arr[j];

                break;
            }
        }
    }

    // Marked element positive
    for(int i = 0; i < n; i++)
        arr[i] = abs(arr[i]);

    // Print final array
    for(int i = 0; i < n; i++)
         cout << arr[i] << " ";
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 1, 3, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    replace(arr,n);
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG {

    // Function to replace each even
    // element by odd and vice-versa
    // in a given array
    static void replace(int[] arr)
    {
        // Stores length of array
        int n = arr.length;

        // Traverse array
        for (int i = 0; i < n; i++) {

            for (int j = i + 1; j < n; j++) {

                // If current element is even
                // then swap it with odd
                if (arr[i] >= 0
                    && arr[j] >= 0
                    && arr[i] % 2 == 0
                    && arr[j] % 2 != 0) {

                    // Perform Swap
                    int tmp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tmp;

                    // Change the sign
                    arr[j] = -arr[j];

                    break;
                }

                // If current element is odd
                // then swap it with even
                else if (arr[i] >= 0
                         && arr[j] >= 0
                         && arr[i] % 2 != 0
                         && arr[j] % 2 == 0) {

                    // Perform Swap
                    int tmp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tmp;

                    // Change the sign
                    arr[j] = -arr[j];

                    break;
                }
            }
        }

        // Marked element positive
        for (int i = 0; i < n; i++)
            arr[i] = Math.abs(arr[i]);

        // Print final array
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int[] arr = { 1, 3, 2, 4 };

        // Function Call
        replace(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to replace each even
# element by odd and vice-versa
# in a given array
def replace(arr,  n):

    # Traverse array
    for i in range(n):
        for j in range(i + 1, n):

            # If current element is
            # even then swap it with odd
            if (arr[i] >= 0 and
                arr[j] >= 0 and
                arr[i] % 2 == 0 and
                arr[j] % 2 != 0):

                # Perform Swap
                tmp = arr[i]
                arr[i] = arr[j]
                arr[j] = tmp

                # Change the sign
                arr[j] = -arr[j]

                break

            # If current element is odd
            # then swap it with even
            elif (arr[i] >= 0 and
                  arr[j] >= 0 and
                  arr[i] % 2 != 0 and
                  arr[j] % 2 == 0):

                # Perform Swap
                tmp = arr[i]
                arr[i] = arr[j]
                arr[j] = tmp

                # Change the sign
                arr[j] = -arr[j]

                break

    # Marked element positive
    for i in range(n):
        arr[i] = abs(arr[i])

    # Print final array
    for i in range(n):
        print(arr[i], end = " ")

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 3, 2, 4]
    n = len(arr)

    # Function Call
    replace(arr, n)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to replace each even
// element by odd and vice-versa
// in a given array
static void replace(int[] arr)
{

    // Stores length of array
    int n = arr.Length;

    // Traverse array
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // If current element is even
            // then swap it with odd
            if (arr[i] >= 0 &&
                arr[j] >= 0 &&
                arr[i] % 2 == 0 &&
                arr[j] % 2 != 0)
            {

                // Perform Swap
                int tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;

                // Change the sign
                arr[j] = -arr[j];

                break;
            }

            // If current element is odd
            // then swap it with even
            else if (arr[i] >= 0 &&
                     arr[j] >= 0 &&
                     arr[i] % 2 != 0 &&
                     arr[j] % 2 == 0)
            {

                // Perform Swap
                int tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;

                // Change the sign
                arr[j] = -arr[j];

                break;
            }
        }
    }

    // Marked element positive
    for(int i = 0; i < n; i++)
        arr[i] = Math.Abs(arr[i]);

    // Print readonly array
    for(int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int[] arr = { 1, 3, 2, 4 };

    // Function Call
    replace(arr);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

    // Function to replace each even
    // element by odd and vice-versa
    // in a given array
    function replace(arr)
    {
        // Stores length of array
        let n = arr.length;

        // Traverse array
        for (let i = 0; i < n; i++) {

            for (let j = i + 1; j < n; j++) {

                // If current element is even
                // then swap it with odd
                if (arr[i] >= 0
                    && arr[j] >= 0
                    && arr[i] % 2 == 0
                    && arr[j] % 2 != 0) {

                    // Perform Swap
                    let tmp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tmp;

                    // Change the sign
                    arr[j] = -arr[j];

                    break;
                }

                // If current element is odd
                // then swap it with even
                else if (arr[i] >= 0
                         && arr[j] >= 0
                         && arr[i] % 2 != 0
                         && arr[j] % 2 == 0) {

                    // Perform Swap
                    let tmp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tmp;

                    // Change the sign
                    arr[j] = -arr[j];

                    break;
                }
            }
        }

        // Marked element positive
        for (let i = 0; i < n; i++)
            arr[i] = Math.abs(arr[i]);

        // Prlet final array
        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Driver Code

           // Given array arr[]
        let arr = [ 1, 3, 2, 4 ];

        // Function Call
        replace(arr);

</script>
```

**Output**

```
2 4 1 3 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效进场:**优化上述进场，思路是使用[双指针进场](https://www.geeksforgeeks.org/two-pointers-technique/)。[通过选取大于 **0** 的每个元素来遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并从当前索引到数组末尾搜索大于 **0** 的相反奇偶元素。如果找到，交换元素并用 **-1** 相乘。按照以下步骤解决问题:

*   用 **-1** 初始化变量 **e** 和 **o** ，分别存储当前找到的尚未取的偶数和奇数。
*   在范围**【0，N–1】**内遍历给定数组，并执行以下操作:
    *   如果大于 **0** ，则选择元素**arr【I】**。
    *   如果 **arr[i]** 为偶数，则将 **o + 1** 增加 **1** ，找到下一个尚未标记的奇数。用 **-1** 相乘标记当前和找到的号码，并交换。
    *   如果 **arr[i]** 为奇数，将 **e + 1** 增加 **1** ，找到下一个尚未标记的偶数。用 **-1** 相乘标记当前和找到的号码，并交换。
*   遍历整个数组后，将其元素与 **-1** 相乘，使其再次为正，并打印该数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define N 3
#define M 4

// Function to replace odd elements
// with even elements and vice versa
void swapEvenOdd(int arr[], int n)
{
    int o = -1, e = -1;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // If arr[i] is visited
        if (arr[i] < 0)
            continue;

        int r = -1;

        if (arr[i] % 2 == 0)
        {
            o++;

            // Find the next odd element
            while (arr[o] % 2 == 0 || arr[o] < 0)
                o++;

            r = o;
        }
        else
        {
            e++;

            // Find next even element
            while (arr[e] % 2 == 1 || arr[e] < 0)
                e++;

            r = e;
        }

        // Mark them visited
        arr[i] *= -1;
        arr[r] *= -1;

        // Swap them
        int tmp = arr[i];
        arr[i] = arr[r];
        arr[r] = tmp;
    }

    // Print the final array
    for(int i = 0; i < n; i++)
    {
        cout << (-1 * arr[i]) << " ";
    }
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 1, 3, 2, 4 };

    // Length of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    swapEvenOdd(arr, n);
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to replace odd elements
    // with even elements and vice versa
    static void swapEvenOdd(int arr[])
    {
        // Length of the array
        int n = arr.length;

        int o = -1, e = -1;

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // If arr[i] is visited
            if (arr[i] < 0)
                continue;

            int r = -1;

            if (arr[i] % 2 == 0) {
                o++;

                // Find the next odd element
                while (arr[o] % 2 == 0
                       || arr[o] < 0)
                    o++;
                r = o;
            }
            else {
                e++;

                // Find next even element
                while (arr[e] % 2 == 1
                       || arr[e] < 0)
                    e++;
                r = e;
            }

            // Mark them visited
            arr[i] *= -1;
            arr[r] *= -1;

            // Swap them
            int tmp = arr[i];
            arr[i] = arr[r];
            arr[r] = tmp;
        }

        // Print the final array
        for (int i = 0; i < n; i++) {
            System.out.print(
                (-1 * arr[i]) + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 1, 3, 2, 4 };

        // Function Call
        swapEvenOdd(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to replace odd elements
# with even elements and vice versa
def swapEvenOdd(arr):

    # Length of the array
    n = len(arr)

    o = -1
    e = -1

    # Traverse the given array
    for i in range(n):

        # If arr[i] is visited
        if (arr[i] < 0):
            continue

        r = -1

        if (arr[i] % 2 == 0):
            o += 1

            # Find the next odd element
            while (arr[o] % 2 == 0 or
                   arr[o] < 0):
                o += 1

            r = o
        else:
            e += 1

            # Find next even element
            while (arr[e] % 2 == 1 or
                   arr[e] < 0):
                e += 1

            r = e

        # Mark them visited
        arr[i] *= -1
        arr[r] *= -1

        # Swap them
        tmp = arr[i]
        arr[i] = arr[r]
        arr[r] = tmp

    # Print the final array
    for i in range(n):
        print((-1 * arr[i]), end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 1, 3, 2, 4 ]

    # Function Call
    swapEvenOdd(arr)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to replace odd elements
// with even elements and vice versa
static void swapEvenOdd(int []arr)
{

    // Length of the array
    int n = arr.Length;

    int o = -1, e = -1;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // If arr[i] is visited
        if (arr[i] < 0)
            continue;

        int r = -1;

        if (arr[i] % 2 == 0)
        {
            o++;

            // Find the next odd element
            while (arr[o] % 2 == 0 ||
                   arr[o] < 0)
                o++;

            r = o;
        }
        else
        {
            e++;

            // Find next even element
            while (arr[e] % 2 == 1 ||
                   arr[e] < 0)
                e++;

            r = e;
        }

        // Mark them visited
        arr[i] *= -1;
        arr[r] *= -1;

        // Swap them
        int tmp = arr[i];
        arr[i] = arr[r];
        arr[r] = tmp;
    }

    // Print the readonly array
    for(int i = 0; i < n; i++)
    {
        Console.Write((-1 * arr[i]) + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 3, 2, 4 };

    // Function Call
    swapEvenOdd(arr);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to replace odd elements
// with even elements and vice versa
function swapEvenOdd(arr, n)
{
    let o = -1, e = -1;

    // Traverse the given array
    for(let i = 0; i < n; i++)
    {

        // If arr[i] is visited
        if (arr[i] < 0)
            continue;

        let r = -1;

        if (arr[i] % 2 == 0)
        {
            o++;

            // Find the next odd element
            while (arr[o] % 2 == 0 || arr[o] < 0)
                o++;

            r = o;
        }
        else
        {
            e++;

            // Find next even element
            while (arr[e] % 2 == 1 || arr[e] < 0)
                e++;

            r = e;
        }

        // Mark them visited
        arr[i] *= -1;
        arr[r] *= -1;

        // Swap them
        let tmp = arr[i];
        arr[i] = arr[r];
        arr[r] = tmp;
    }

    // Print the final array
    for(let i = 0; i < n; i++)
    {
        document.write((-1 * arr[i]) + " ");
    }
}

// Driver Code

    // Given array arr[]
    let arr = [ 1, 3, 2, 4 ];

    // Length of the array
    let n = arr.length;

    // Function Call
    swapEvenOdd(arr, n);

//This code is contributed by Mayank Tyagi
</script>
```

**Output**

```
2 4 1 3 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**有效方法 2 :**

另一种方法是使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)。请遵循以下步骤:

1.  从数组 arr[]中取出索引处的元素，并推送到堆栈中
2.  从索引 i = 1 迭代 arr[]到结束，并执行以下操作:
    1.  如果 arr[i]和堆栈顶部的项目不都是偶数或不都是奇数，则弹出并交换
    2.  否则将项目推入堆栈

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace odd elements
// with even elements and vice versa
void swapEvenOdd(int arr[], int N)
{
  stack<pair<int, int> > stack;

  // Push the first element to stack
  stack.push({ 0, arr[0] });

  // iterate the array and swap even and odd
  for (int i = 1; i < N; i++)
  {
    if (!stack.empty())
    {
      if (arr[i] % 2 != stack.top().second % 2)
      {

        // pop and swap
        pair<int, int> pop = stack.top();
        stack.pop();

        int index = pop.first, val = pop.second;
        arr[index] = arr[i];
        arr[i] = val;
      }
      else
        stack.push({ i, arr[i] });
    }
    else
      stack.push({ i, arr[i] });
  }

  // print the arr[]
  for (int i = 0; i < N; i++)
    cout << arr[i] << " ";
}

// Driven Program
int main()
{

  // Given array arr[]
  int arr[] = { 1, 3, 2, 4 };

  // Stores the length of array
  int N = sizeof(arr) / sizeof(arr[0]);

  // Function Call
  swapEvenOdd(arr, N);
  return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to replace odd elements
  // with even elements and vice versa
  static void swapEvenOdd(int arr[], int N)
  {

    Stack<int[]> stack = new Stack<>();

    // Push the first element to stack
    stack.push(new int[] { 0, arr[0] });

    // iterate the array and swap even and odd
    for (int i = 1; i < N; i++)
    {
      if (!stack.isEmpty())
      {
        if (arr[i] % 2 != stack.peek()[1] % 2)
        {

          // pop and swap
          int pop[] = stack.pop();
          int index = pop[0], val = pop[1];
          arr[index] = arr[i];
          arr[i] = val;
        }
        else
          stack.push(new int[] { i, arr[i] });
      }
      else
        stack.push(new int[] { i, arr[i] });
    }

    // print the arr[]
    for (int i = 0; i < N; i++)
      System.out.print(arr[i] + " ");
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given array arr
    int arr[] = { 1, 3, 2, 4 };

    // length of the arr
    int N = arr.length;

    // Function Call
    swapEvenOdd(arr, N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to replace odd elements
# with even elements and vice versa
def swapEvenOdd(arr):
    stack = []

    # Push the first element to stack
    stack.append((0, arr[0],))

    # iterate the array and swap even and odd
    for i in range(1, len(arr)):
        if stack:
            if arr[i]%2 != stack[-1][1]%2:
                #pop and swap
                index, val = stack.pop(-1)
                arr[index] = arr[i]
                arr[i] = val
            else:
                stack.append((i, arr[i],))
        else:
            stack.append((i, arr[i],))
    return arr

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 1, 3, 2, 4 ]

    # Function Call
    print(swapEvenOdd(arr))

# This code is contributed by Arunabha Choudhury
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to replace odd elements
// with even elements and vice versa
function swapEvenOdd(arr, N)
{
    let stack = [];

    // Push the first element to stack
    stack.push([0, arr[0]]);

    // Iterate the array and swap even and odd
    for(let i = 1; i < N; i++)
    {
        if (stack.length != 0)
        {
            if (arr[i] % 2 !=
                stack[stack.length - 1][1] % 2)
            {

                // pop and swap
                let pop = stack.pop();
                let index = pop[0], val = pop[1];
                arr[index] = arr[i];
                arr[i] = val;
            }
            else
            stack.push([i, arr[i]]);
        }
        else
        stack.push([i, arr[i]]);
    }

    // print the arr[]
    for(let i = 0; i < N; i++)
        document.write(arr[i] + " ");
}

// Driver code

// Given array arr
let arr = [ 1, 3, 2, 4 ];

// Length of the arr
let N = arr.length;

// Function Call
swapEvenOdd(arr, N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
[4, 2, 3, 1]
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)