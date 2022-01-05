# 需要翻转的最小索引数组元素，使数组的和等于 0

> 原文:[https://www . geesforgeks . org/最小索引数组元素需要翻转才能使数组之和等于 0/](https://www.geeksforgeeks.org/smallest-indexed-array-element-required-to-be-flipped-to-make-sum-of-array-equal-to-0/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到符号需要翻转的最小索引[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)元素，使得给定数组的[和变为 **0** 。如果无法使数组之和等于 **0** ，则打印 **-1** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {1，3，-5，3，4}
> **输出:** 1
> **解释:**
> 翻转 arr[1]的符号将 arr[]修改为{1，-3，-5，3，4}
> 由于数组的和修改为 0，因此需要的输出为 1。
> 
> **输入:** arr[] = {1，2，4}
> **输出:** -1

**天真法:**解决这个问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，翻转数组元素的符号，检查数组的[和是否变为 **0** 。如果发现为真，则打印当前元素的索引。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest indexed
// array element required to be flipped to
// make sum of the given array equal to 0
int smallestIndexArrayElementsFlip(
    int arr[], int N)
{

    // Stores the required index
    int pos = -1;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Flip the sign of current element
        arr[i] *= -1;

        // Stores the sum of array elements
        int sum = 0;

        // Find the sum of the array
        for (int j = 0; j < N; j++) {

            // Update sum
            sum += arr[j];
        }

        // If sum is equal to 0
        if (sum == 0) {

            // Update pos
            pos = i;
            break;
        }

        // Reset the current element
        // to its original value
        else {

            // Reset the value of arr[i]
            arr[i] *= -1;
        }
    }

    return pos;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, -5, 3, 4 };
    int N = sizeof(arr)
            / sizeof(arr[0]);
    cout << smallestIndexArrayElementsFlip(
        arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
class GFG {

    // Function to find the smallest indexed
    // array element required to be flipped to
    // make sum of the given array equal to 0
    static int smallestIndexArrayElementsFlip(int arr[], int N)
    {

        // Stores the required index
        int pos = -1;

        // Traverse the given array
        for (int i = 0; i < N; i++)
        {

            // Flip the sign of current element
            arr[i] *= -1;

            // Stores the sum of array elements
            int sum = 0;

            // Find the sum of the array
            for (int j = 0; j < N; j++)
            {

                // Update sum
                sum += arr[j];
            }

            // If sum is equal to 0
            if (sum == 0) {

                // Update pos
                pos = i;
                break;
            }

            // Reset the current element
            // to its original value
            else {

                // Reset the value of arr[i]
                arr[i] *= -1;
            }
        }

        return pos;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 1, 3, -5, 3, 4 };
        int N = arr.length;               
        System.out.println(smallestIndexArrayElementsFlip(arr, N));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the smallest indexed
# array element required to be flipped to
# make sum of the given array equal to 0
def smallestIndexArrayElementsFlip(arr, N):

    # Stores the required index
    pos = -1

    # Traverse the given array
    for i in range(N):

        # Flip the sign of current element
        arr[i] *= -1

        # Stores the sum of array elements
        sum = 0

        # Find the sum of the array
        for j in range(N):

            # Update sum
            sum += arr[j]

        # If sum is equal to 0
        if (sum == 0):

            # Update pos
            pos = i
            break

        # Reset the current element
        # to its original value
        else:

            # Reset the value of arr[i]
            arr[i] *= -1

    return pos

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 3, -5, 3, 4 ]
    N = len(arr)

    print(smallestIndexArrayElementsFlip(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to find the smallest indexed
    // array element required to be flipped to
    // make sum of the given array equal to 0
    static int smallestIndexArrayElementsFlip(int []arr, int N)
    {

        // Stores the required index
        int pos = -1;

        // Traverse the given array
        for (int i = 0; i < N; i++)
        {

            // Flip the sign of current element
            arr[i] *= -1;

            // Stores the sum of array elements
            int sum = 0;

            // Find the sum of the array
            for (int j = 0; j < N; j++)
            {

                // Update sum
                sum += arr[j];
            }

            // If sum is equal to 0
            if (sum == 0)
            {

                // Update pos
                pos = i;
                break;
            }

            // Reset the current element
            // to its original value
            else
            {

                // Reset the value of arr[i]
                arr[i] *= -1;
            }
        }   
        return pos;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 1, 3, -5, 3, 4 };
        int N = arr.Length;               
        Console.WriteLine(smallestIndexArrayElementsFlip(arr, N));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the smallest indexed
// array element required to be flipped to
// make sum of the given array equal to 0
function smallestIndexArrayElementsFlip(arr, N)
{

    // Stores the required index
    var pos = -1;

    var i,j;
    // Traverse the given array
    for (i = 0; i < N; i++) {

        // Flip the sign of current element
        arr[i] *= -1;

        // Stores the sum of array elements
        var sum = 0;

        // Find the sum of the array
        for (j = 0; j < N; j++) {

            // Update sum
            sum += arr[j];
        }

        // If sum is equal to 0
        if (sum == 0) {

            // Update pos
            pos = i;
            break;
        }

        // Reset the current element
        // to its original value
        else {

            // Reset the value of arr[i]
            arr[i] *= -1;
        }
    }

    return pos;
}

// Driver Code

    var arr = [1, 3, -5, 3, 4];
    var N = arr.length;
    document.write(smallestIndexArrayElementsFlip(arr, N));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 让给定数组的[和为 **ArrSum**
> 翻转任意数组元素符号后的数组和**UpdatedSum = ArrSum–2 * arr[I]**
> 如果 **UpdatedSum = 0** ，那么 **arr[i]** 必须为 **ArrSum / 2** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

按照以下步骤解决问题:

*   初始化一个变量，比如 **ArrSum** ，来存储给定数组的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，检查 **(2 * arr[i] == ArrSum)** 的值是否为真。如果发现为真，则打印当前元素的索引。
*   否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest indexed
// array element required to be flipped to
// make sum of the given array equal to 0
int smallestIndexArrayElementsFlip(
    int arr[], int N)
{

    // Stores the required index
    int pos = -1;

    // Stores the sum of the array
    int ArrSum = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Update ArrSum
        ArrSum += arr[i];
    }

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // If sum of array elements double
        // the value of the current element
        if (2 * arr[i] == ArrSum) {

            // Update pos
            pos = i;
            break;
        }
    }

    return pos;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, -5, 3, 4 };
    int N = sizeof(arr)
            / sizeof(arr[0]);

    cout << smallestIndexArrayElementsFlip(
        arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

  // Function to find the smallest indexed
  // array element required to be flipped to
  // make sum of the given array equal to 0
  static int smallestIndexArrayElementsFlip(
    int arr[], int N)
  {

    // Stores the required index
    int pos = -1;

    // Stores the sum of the array
    int ArrSum = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++)
    {

      // Update ArrSum
      ArrSum += arr[i];
    }

    // Traverse the given array
    for (int i = 0; i < N; i++)
    {

      // If sum of array elements double
      // the value of the current element
      if (2 * arr[i] == ArrSum)
      {

        // Update pos
        pos = i;
        break;
      }
    }
    return pos;
  }

  // Driver function
  public static void main (String[] args)
  {
    int arr[] = { 1, 3, -5, 3, 4 };
    int N = arr.length;

    System.out.println(smallestIndexArrayElementsFlip(
      arr, N));
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the smallest indexed
# array element required to be flipped to
# make sum of the given array equal to 0
def smallestIndexArrayElementsFlip(arr, N):

    # Stores the required index
    pos = -1

    # Stores the sum of the array
    ArrSum = 0

    # Traverse the given array
    for i in range(N):

        # Update ArrSum
        ArrSum += arr[i]

    # Traverse the given array
    for i in range(N):

        # If sum of array elements double
        # the value of the current element
        if (2 * arr[i] == ArrSum):

            # Update pos
            pos = i
            break
    return pos

# Driver Code
arr = [1, 3, -5, 3, 4]
N = len(arr)
print(smallestIndexArrayElementsFlip(
    arr, N))

# This code is contributed by Dharanendra L V
```

## C#

```
// C# program for above approach
using System;

class GFG {

    // Function to find the smallest indexed
    // array element required to be flipped to
    // make sum of the given array equal to 0
    static int smallestIndexArrayElementsFlip(int[] arr,
                                              int N)
    {

        // Stores the required index
        int pos = -1;

        // Stores the sum of the array
        int ArrSum = 0;

        // Traverse the given array
        for (int i = 0; i < N; i++) {

            // Update ArrSum
            ArrSum += arr[i];
        }

        // Traverse the given array
        for (int i = 0; i < N; i++) {

            // If sum of array elements double
            // the value of the current element
            if (2 * arr[i] == ArrSum) {

                // Update pos
                pos = i;
                break;
            }
        }
        return pos;
    }

    // Driver function
    static public void Main()
    {

        int[] arr = new int[] { 1, 3, -5, 3, 4 };
        int N = arr.Length;

        Console.WriteLine(
            smallestIndexArrayElementsFlip(arr, N));
    }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// javascript program for the above approach

  // Function to find the smallest indexed
  // array element required to be flipped to
  // make sum of the given array equal to 0
  function smallestIndexArrayElementsFlip(
    arr, N)
  {

    // Stores the required index
    let pos = -1;

    // Stores the sum of the array
    let ArrSum = 0;

    // Traverse the given array
    for (let i = 0; i < N; i++)
    {

      // Update ArrSum
      ArrSum += arr[i];
    }

    // Traverse the given array
    for (let i = 0; i < N; i++)
    {

      // If sum of array elements double
      // the value of the current element
      if (2 * arr[i] == ArrSum)
      {

        // Update pos
        pos = i;
        break;
      }
    }
    return pos;
  }

// Driver Code

    let arr = [ 1, 3, -5, 3, 4 ];
    let N = arr.length;

    document.write(smallestIndexArrayElementsFlip(
      arr, N));

</script>

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)