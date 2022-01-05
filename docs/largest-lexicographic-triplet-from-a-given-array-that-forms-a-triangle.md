# 形成三角形的给定数组中最大的字典三元组

> 原文:[https://www . geeksforgeeks . org/最大字典顺序三元组从给定数组形成三角形/](https://www.geeksforgeeks.org/largest-lexicographic-triplet-from-a-given-array-that-forms-a-triangle/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在该数组中找到字典上最大的可以形成三角形的三元组。如果不存在这样的三元组，打印 ***-1*** 。
**例:**

> **输入:** arr[] = { 4，2，10，3，5 }
> **输出:** 3 4 5
> **解释:**
> 字典上最大的三元组是(4，5，10)。但它并不构成三角形。
> 下一个字典序上最大的三元组是(3，4，5)。
> 既然形成三角形，就是必答。
> **输入:** arr[] = { 20，12，120，3，15 }
> **输出:** 12 15 20

**方法:**
一个三元组可以形成一个三角形，当且仅当它遵循下面给出的条件:

> 如果 A、B、C 形成一个三元组，那么如果
> T1】A<b+ C 或 **B < A + C** 或**C<A+B**T7】则三元组可以形成一个三角形

思路是用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。按升序对数组进行排序。从数组的末尾开始遍历，检查是否有任何三元组满足上述条件。打印满足条件的第一个三元组，作为输出。如果找不到这样的三联，那么打印 **-1** 。
以下是上述办法的实施情况:

## C++

```
// C++ Program to implement
// the the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find lexicographically
// largest triplet that forms a
// triangle in the given array
void findTriplet(int arr[], int N)
{

    // Sort the array
    sort(arr, arr + N);

    int flag = 0, i;

    // Iterate from the end of the array
    for (i = N - 1; i - 2 >= 0; i--) {

        // If the triplet forms a triangle
        if (arr[i - 2] + arr[i - 1] > arr[i]) {
            flag = 1;
            break;
        }
    }

    // If triplet found
    if (flag) {

        // Print the triplet
        cout << arr[i - 2] << " "
             << arr[i - 1] << " "
             << arr[i] << endl;
    }

    // Otherwise
    else {
        cout << -1 << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 2, 10, 3, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    findTriplet(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the the above approach
import java.util.*;

class GFG{

// Function to find lexicographically
// largest triplet that forms a
// triangle in the given array
static void findTriplet(int arr[], int N)
{

    // Sort the array
    Arrays.sort(arr);

    int flag = 0, i;

    // Iterate from the end of the array
    for(i = N - 1; i - 2 >= 0; i--)
    {

        // If the triplet forms a triangle
        if (arr[i - 2] + arr[i - 1] > arr[i])
        {
            flag = 1;
            break;
        }
    }

    // If triplet found
    if (flag != 0)
    {

        // Print the triplet
        System.out.println(arr[i - 2] + " " +
                           arr[i - 1] + " " +
                           arr[i] );
    }

    // Otherwise
    else
    {
        System.out.println(-1);
    }
}

// Driver Code
public static void main (String []args)
{
    int arr[] = { 4, 2, 10, 3, 5 };

    int N = arr.length;

    findTriplet(arr, N);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to find lexicographically
# largest triplet that forms a
# triangle in the given array
def findTriplet(arr, N):

    # Sort the array
    arr.sort()

    # Iterate from the end of the array
    i = N - 1
    while i - 2 >= 0:

        # If the triplet forms a triangle
        if(arr[i - 2] + arr[i - 1] > arr[i]):
            flag = 1
            break

        i -= 1

    # If triplet found
    if(flag):

        # Print the triplet
        print(arr[i - 2],
              arr[i - 1],
              arr[i])

    # Otherwise
    else:
        print(-1)

# Driver Code
if __name__ == '__main__':

    arr = [ 4, 2, 10, 3, 5 ]

    N = len(arr)

    findTriplet(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the the above approach
using System;
class GFG{

// Function to find lexicographically
// largest triplet that forms a
// triangle in the given array
static void findTriplet(int []arr, int N)
{

    // Sort the array
    Array.Sort(arr);

    int flag = 0, i;

    // Iterate from the end of the array
    for(i = N - 1; i - 2 >= 0; i--)
    {

        // If the triplet forms a triangle
        if (arr[i - 2] + arr[i - 1] > arr[i])
        {
            flag = 1;
            break;
        }
    }

    // If triplet found
    if (flag != 0)
    {

        // Print the triplet
        Console.Write(arr[i - 2] + " " +
                      arr[i - 1] + " " +
                      arr[i] );
    }

    // Otherwise
    else
    {
        Console.Write(-1);
    }
}

// Driver Code
public static void Main (string []args)
{
    int []arr = { 4, 2, 10, 3, 5 };

    int N = arr.Length;

    findTriplet(arr, N);
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the the above approach
      // Function to find lexicographically
      // largest triplet that forms a
      // triangle in the given array
      function findTriplet(arr, N) {
        // Sort the array
        arr.sort((a, b) => a - b);

        var flag = 0,
          i;

        // Iterate from the end of the array
        for (i = N - 1; i - 2 >= 0; i--) {
          // If the triplet forms a triangle
          if (arr[i - 2] + arr[i - 1] > arr[i]) {
            flag = 1;
            break;
          }
        }

        // If triplet found
        if (flag) {
          // Print the triplet
          document.write(
            arr[i - 2] +
              "  " +
              arr[i - 1] +
              "  " +
              arr[i] +
              "<br>"
          );
        }

        // Otherwise
        else {
          document.write(-1 + "<br>");
        }
      }

      // Driver Code
      var arr = [4, 2, 10, 3, 5];
      var N = arr.length;
      findTriplet(arr, N);

</script>
```

**Output:** 

```
3 4 5
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*