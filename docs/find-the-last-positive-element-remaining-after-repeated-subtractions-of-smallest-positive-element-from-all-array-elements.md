# 从所有数组元素中找出最小正元素重复减法后剩余的最后一个正元素

> 原文:[https://www . geeksforgeeks . org/find-最后一个正元素-重复减去所有数组元素后剩余的最小正元素/](https://www.geeksforgeeks.org/find-the-last-positive-element-remaining-after-repeated-subtractions-of-smallest-positive-element-from-all-array-elements/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从所有数组元素中反复减去最小的正数组元素后，找出剩余的最后一个正数组元素。

**示例:**

> **输入:** arr[] = {3，5，4，7}
> **输出:** 2
> **解释:**
> 从数组中减去最小正元素，即 3，新数组为 arr[] = {0，2，1，4}
> 从数组中减去最小正元素，即 1，新数组为 arr[] = {0，1，0，3}
> 从数组中减去最小正元素，即
> 
> **输入:** arr[] = {2，6，7}
> **输出:** 1

**天真法:**解决给定问题最简单的方法是[遍历给定数组**arr【】**T5】找到数组中最小的正元素，从所有元素中减去。执行此操作，直到数组中只剩下一个正元素。完成上述步骤后，打印剩余的正数组元素。](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效法:**通过观察最后一个正元素将是 [**最大阵元**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) 和 [**第二大阵元**](https://www.geeksforgeeks.org/find-second-largest-element-array/) 的差值，可以优化上述方法。按照以下步骤解决问题:

*   如果 **N = 1** ，打印数组的第一个元素。
*   否则打印 [**最大**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) 和 [**第二大**](https://www.geeksforgeeks.org/find-second-largest-element-array/) 阵列元素之间的差异。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate last positive
// element of the array
int lastPositiveElement(vector<int> arr)
{
    int N = arr.size();

    // Return the first element if N = 1
    if (N == 1)
        return arr[0];

    // Stores the greatest and the second
    // greatest element
    int greatest = -1, secondGreatest = -1;

    // Traverse the array A[]
    for (int x : arr) {

        // If current element is greater
        // than the greatest element
        if (x >= greatest) {
            secondGreatest = greatest;
            greatest = x;
        }

        // If current element is greater
        // than second greatest element
        else if (x >= secondGreatest) {
            secondGreatest = x;
        }
    }

    // Return the final answer
    return greatest - secondGreatest;
}

// Driver Code
int main()
{
    vector<int> arr = { 3, 5, 4, 7 };
    cout << lastPositiveElement(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.util.*;
class GFG{

// Function to calculate last positive
// element of the array
static int lastPositiveElement(int[] arr)
{
    int N = arr.length;

    // Return the first element if N = 1
    if (N == 1)
        return arr[0];

    // Stores the greatest and the second
    // greatest element
    int greatest = -1, secondGreatest = -1;

    // Traverse the array A[]
    for (int x : arr) {

        // If current element is greater
        // than the greatest element
        if (x >= greatest) {
            secondGreatest = greatest;
            greatest = x;
        }

        // If current element is greater
        // than second greatest element
        else if (x >= secondGreatest) {
            secondGreatest = x;
        }
    }

    // Return the final answer
    return greatest - secondGreatest;
}

// Driver Code
public static void main(String[] args){

    int[] arr = { 3, 5, 4, 7 };
    System.out.print(lastPositiveElement(arr));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate last positive
# element of the array
def lastPositiveElement(arr) :

    N = len(arr);

    # Return the first element if N = 1
    if (N == 1) :
        return arr[0];

    # Stores the greatest and the second
    # greatest element
    greatest = -1; secondGreatest = -1;

    # Traverse the array A[]
    for x in arr :

        # If current element is greater
        # than the greatest element
        if (x >= greatest) :
            secondGreatest = greatest;
            greatest = x;

        # If current element is greater
        # than second greatest element
        elif (x >= secondGreatest) :
            secondGreatest = x;

    # Return the final answer
    return greatest - secondGreatest;

# Driver Code
if __name__ == "__main__" :

    arr = [ 3, 5, 4, 7 ];
    print(lastPositiveElement(arr));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to calculate last positive
    // element of the array
    static int lastPositiveElement(int[] arr)
    {
        int N = arr.Length;

        // Return the first element if N = 1
        if (N == 1)
            return arr[0];

        // Stores the greatest and the second
        // greatest element
        int greatest = -1, secondGreatest = -1;

        // Traverse the array A[]
        for (int x = 0; x < N; x++) {

            // If current element is greater
            // than the greatest element
            if (arr[x] >= greatest) {
                secondGreatest = greatest;
                greatest = arr[x];
            }

            // If current element is greater
            // than second greatest element
            else if (arr[x] >= secondGreatest) {
                secondGreatest = arr[x];
            }
        }

        // Return the final answer
        return greatest - secondGreatest;
    }

    // Driver Code
    public static void Main()
    {

        int[] arr = { 3, 5, 4, 7 };
        Console.Write(lastPositiveElement(arr));
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to calculate last positive
       // element of the array
       function lastPositiveElement(arr) {
           let N = arr.length;

           // Return the first element if N = 1
           if (N == 1)
               return arr[0];

           // Stores the greatest and the second
           // greatest element
           let greatest = -1, secondGreatest = -1;

           // Traverse the array A[]
           for (let x of arr) {

               // If current element is greater
               // than the greatest element
               if (x >= greatest) {
                   secondGreatest = greatest;
                   greatest = x;
               }

               // If current element is greater
               // than second greatest element
               else if (x >= secondGreatest) {
                   secondGreatest = x;
               }
           }

           // Return the final answer
           return greatest - secondGreatest;
       }

       // Driver Code

       let arr = [3, 5, 4, 7];
       document.write(lastPositiveElement(arr));

    // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)