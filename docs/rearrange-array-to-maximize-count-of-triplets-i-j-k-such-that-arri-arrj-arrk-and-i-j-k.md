# 重新排列数组以最大化三元组(I，j，k)的计数，使得 arr[i] > arr[j] < arr[k]和 i < j < k

> 原文:[https://www . geesforgeks . org/rearray-array-to-max-count-of-triples-I-j-k-so-arri-arrj-arrk-and-I-j-k/](https://www.geeksforgeeks.org/rearrange-array-to-maximize-count-of-triplets-i-j-k-such-that-arri-arrj-arrk-and-i-j-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** ，任务是重新排列数组元素，以最大化满足条件**arr[I]>arr[j]<arr[k]**和 **i < j < k** 的三元组的数量。

**示例:**

> **输入:** arr[] = {1，4，3，3，2，2，5}
> **输出:**
> 三胞胎计数:3
> 数组:{3，1，3，2，4，2，5}
> **解释:**
> 将数组重新排列为{3，1，3，2，4，2，5}，即给出三胞胎的最大计数{(3，1，3)，(3，2，4)，(4，2，5))
> 因此，所需的三胞胎数为 3。
> 
> **输入:** arr[] = {1，2，3，4，5，6，7，7}
> **输出:**
> 三胞胎计数= 3
> 数组= {5，1，6，2，7，3，7，4}

**天真方法:**解决问题最简单的方法是[生成数组的所有可能排列](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)并计算满足给定条件的三元组的数量。最后，打印三元组的计数和给定数组的排列，该数组包含给定条件下三元组的最大计数。

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是首先[对给定数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序，将给定数组的前半部分放在临时数组的奇数索引处，后半部分放在偶数索引处。最后，打印给定条件下的临时数组和三元组数。按照以下步骤解决问题:

1.  初始化一个临时数组，比如 **temp[]** ，来存储给定数组的[排列](https://en.wikipedia.org/wiki/Permutation)。
2.  [给定数组排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)， **arr[]** 。
3.  将给定数组的前半部分放在 **temp** 数组的奇数索引处。
4.  将给定数组的最后一半放在 **temp** 数组的偶数索引处。
5.  最后，在 **temp[]** 和 **temp** 数组中打印给定条件下的三胞胎计数。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array
// to maximize the count of triplets
void ctTriplets(int arr[], int N)
{
    // Sort the given array
    sort(arr, arr + N);

    // Stores the permutations
    // of the given array
    vector<int> temp(N);

    // Stores the index
    // of the given array
    int index = 0;

    // Place the first half
    // of the given array
    for (int i = 1; i < N;
         i += 2) {
        temp[i]
            = arr[index++];
    }

    // Place the last half
    // of the given array
    for (int i = 0; i < N;
         i += 2) {
        temp[i]
            = arr[index++];
    }

    // Stores the count
    // of triplets
    int ct = 0;
    for (int i = 0; i < N; i++) {

        // Check the given conditions
        if (i > 0 && i + 1 < N) {
            if (temp[i] < temp[i + 1]
                && temp[i] < temp[i - 1]) {
                ct++;
            }
        }
    }
    cout << "Count of triplets:"
         << ct << endl;
    cout << "Array:";
    for (int i = 0; i < N;
         i++) {
        cout << temp[i] << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    ctTriplets(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to rearrange the array
// to maximize the count of triplets
static void ctTriplets(int arr[], int N)
{

    // Sort the given array
    Arrays.sort(arr);

    // Stores the permutations
    // of the given array
    int[] temp = new int[N];

    // Stores the index
    // of the given array
    int index = 0;

    // Place the first half
    // of the given array
    for(int i = 1; i < N; i += 2)
    {
        temp[i] = arr[index++];
    }

    // Place the last half
    // of the given array
    for(int i = 0; i < N; i += 2)
    {
        temp[i] = arr[index++];
    }

    // Stores the count
    // of triplets
    int ct = 0;

    for(int i = 0; i < N; i++)
    {

        // Check the given conditions
        if (i > 0 && i + 1 < N)
        {
            if (temp[i] < temp[i + 1] &&
                temp[i] < temp[i - 1])
            {
                ct++;
            }
        }
    }

    System.out.println("Count of triplets:" + ct );
    System.out.print("Array:");

    for(int i = 0; i < N; i++)
    {
        System.out.print(temp[i] + " ");
    }
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = arr.length;

    ctTriplets(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to rearrange the array
# to maximize the count of triplets
def ctTriplets(arr, N):

    # Sort the given array
    arr.sort()

    # Stores the permutations
    # of the given array
    temp = [0] * N

    # Stores the index
    # of the given array
    index = 0

    # Place the first half
    # of the given array
    for i in range(1, N, 2):
        temp[i] = arr[index]
        index += 1

    # Place the last half
    # of the given array
    for i in range(0, N, 2):
        temp[i] = arr[index]
        index += 1

    # Stores the count
    # of triplets
    ct = 0

    for i in range(N):

        # Check the given conditions
        if (i > 0 and i + 1 < N):
            if (temp[i] < temp[i + 1] and
                temp[i] < temp[i - 1]):
                ct += 1

    print("Count of triplets:", ct)
    print("Array:", end = "")

    for i in range(N):
        print(temp[i], end = " ")

# Driver Code
arr = [ 1, 2, 3, 4, 5, 6 ]
N = len(arr)

ctTriplets(arr, N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to rearrange the array
// to maximize the count of triplets
static void ctTriplets(int[] arr, int N)
{

    // Sort the given array
    Array.Sort(arr);

    // Stores the permutations
    // of the given array
    int[] temp = new int[N];

    // Stores the index
    // of the given array
    int index = 0;

    // Place the first half
    // of the given array
    for(int i = 1; i < N; i += 2)
    {
        temp[i] = arr[index++];
    }

    // Place the last half
    // of the given array
    for(int i = 0; i < N; i += 2)
    {
        temp[i] = arr[index++];
    }

    // Stores the count
    // of triplets
    int ct = 0;

    for(int i = 0; i < N; i++)
    {

        // Check the given conditions
        if (i > 0 && i + 1 < N)
        {
            if (temp[i] < temp[i + 1] &&
                temp[i] < temp[i - 1])
            {
                ct++;
            }
        }
    }

    Console.WriteLine("Count of triplets:" + ct );
    Console.Write("Array:");

    for(int i = 0; i < N; i++)
    {
        Console.Write(temp[i] + " ");
    }
}

// Driver Code
public static void Main ()
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int N = arr.Length;

    ctTriplets(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to rearrange the array
// to maximize the count of triplets
function ctTriplets(arr, N)
{

    // Sort the given array
    arr.sort();

    // Stores the permutations
    // of the given array
    let temp = [];

    // Stores the index
    // of the given array
    let index = 0;

    // Place the first half
    // of the given array
    for(let i = 1; i < N; i += 2)
    {
        temp[i] = arr[index++];
    }

    // Place the last half
    // of the given array
    for(let i = 0; i < N; i += 2)
    {
        temp[i] = arr[index++];
    }

    // Stores the count
    // of triplets
    let ct = 0;

    for(let i = 0; i < N; i++)
    {

        // Check the given conditions
        if (i > 0 && i + 1 < N)
        {
            if (temp[i] < temp[i + 1] &&
                temp[i] < temp[i - 1])
            {
                ct++;
            }
        }
    }

    document.write("Count of triplets:" + ct + "<br/>");
    document.write("Array:");

    for(let i = 0; i < N; i++)
    {
        document.write(temp[i] + " ");
    }
}

// Driver Code
    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let N = arr.length;

    ctTriplets(arr, N);

// This code is contributed by target_2.
</script>
```

**Output:** 

```
Count of triplets:2
Array:4 1 5 2 6 3 
```

***时间复杂度** : O(N)*
***辅助空间** : O(N)*