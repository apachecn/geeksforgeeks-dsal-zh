# N 个自然数的给定排列之间的绝对差

> 原文:[https://www . geesforgeks . org/n 个自然数的给定排列之间的绝对差/](https://www.geeksforgeeks.org/absolute-difference-between-given-permutations-of-n-natural-numbers/)

给定从 **1** 到 **N** 的第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的两个[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)数组**arr【】**和**brr【】**，任务是找出它们在字典顺序中的位置的绝对差异。

**示例:**

> **输入:** arr[] = {1，3，2}，brr[] = {3，1，2}
> **输出:** 3
> **解释:**
> 前 N(= 3)个自然数有 6 种可能的排列。它们是{{1，2，3}，{1，3，2}，{2，1，3}，{2，3，1}，{3，1，2}，{3，2，1}。arr[]的位置是 2，brr[]的位置是 5。因此，答案是| 2–5 | = 3。
> 
> **输入:** arr[] = {1，3，2，4}，brr[] = {1，3，2，4}
> **输出:** 0

**方法:**使用函数[下一个排列 STL](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/) 生成第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的下一个排列，即可解决给定的问题。思路是将 **arr[]** 作为基置换，执行**next _ arrangement()**直到 **arr[]** 不等于 **brr[]** 。在这一步之后，将 **arr[]** 转换为 **brr[]** 所需的步数是它们在字典顺序中的位置之间的绝对差的合成值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the distance between
// two permutations array arr[] and brr[]
// in lexicographical order
int permutationDiff(vector<int> arr,
                    vector<int> brr)
{

    // Check if both permutations are
    // already equal or not
    if (arr == brr) {
        return 0;
    }

    // Stores the distance between the
    // two permutations arr[] and brr[]
    int count = 0;

    while (arr != brr) {

        // Increment the count
        count++;

        // call next_permutation
        next_permutation(brr.begin(),
                         brr.end());
    }

    // Return the total count
    return count;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 3, 2 };
    vector<int> brr = { 3, 1, 2 };

    cout << permutationDiff(arr, brr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Utility function to find next permutation
public static void next_permutation(int nums[])
{
    int mark = -1;
    for (int i = nums.length - 1; i > 0; i--) {
        if (nums[i] > nums[i - 1]) {
            mark = i - 1;
            break;
        }
    }
    if (mark == -1) {
        reverse(nums, 0, nums.length - 1);
        return;
    }
    int idx = nums.length-1;
    for (int i = nums.length-1; i >= mark+1; i--) {
        if (nums[i] > nums[mark]) {
            idx = i;
            break;
        }
    }
    swap(nums, mark, idx);
    reverse(nums, mark + 1, nums.length - 1);
}

// Utility function to swap two elements in array
public static void swap(int nums[], int i, int j) {
    int t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
}
// Utility function to reverse the array in a range
public static void reverse(int nums[], int i, int j) {
    while (i < j) {
        swap(nums, i, j);
        i++;
        j--;
    }
}
// Function to find the distance between
// two permutations array arr[] and brr[]
// in lexicographical order
public static int permutationDiff(int arr[], int brr[])
{
    // Check if both permutations are
    // already equal or not
    if (Arrays.equals(arr, brr)) {
        return 0;
    }
    // Stores the distance between the
    // two permutations arr[] and brr[]
    int count = 0, flag = 0;
    while(!Arrays.equals(arr, brr))
    {
        // Increment the count
        count++;
        // call next_permutation
        next_permutation(brr);
    }
    // Return the total count
    return count;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 1, 3, 2 };
    int []brr = { 3, 1, 2 };

    System.out.println(permutationDiff(arr, brr));
    }
}
// This code is contributed by Samim Hossain Mondal
```

## 蟒蛇 3

```
# Python program for the above approach

# Function for next permutation
def next_permutation(arr):

    # find the length of the array
    n = len(arr)

    # start from the right most digit and find the first
    # digit that is smaller than the digit next to it.
    k = n - 2
    while k >= 0:
        if arr[k] < arr[k + 1]:
            break
        k -= 1

    # reverse the list if the digit that is smaller than the
    # digit next to it is not found.
    if k < 0:
        arr = arr[::-1]
    else:

        # find the first greatest element than arr[k] from the
        # end of the list
        for l in range(n - 1, k, -1):
            if arr[l] > arr[k]:
                break

        # swap the elements at arr[k] and arr[l
        arr[l], arr[k] = arr[k], arr[l]

        # reverse the list from k + 1 to the end to find the
        # most nearest greater number to the given input number
        arr[k + 1:] = reversed(arr[k + 1:])

    return arr

    # Function to find the distance between
    # two permutations array arr[] and brr[]
    # in lexicographical order

def permutationDiff(arr,
                    brr):

    # Check if both permutations are
    # already equal or not
    if (arr == brr):
        return 0

    # Stores the distance between the
    # two permutations arr[] and brr[]
    count = 0

    while (arr != brr):

        # Increment the count
        count = count+1

        # call next_permutation
        brr = next_permutation(brr)

    # Return the total count
    return count

arr = [1, 3, 2]
brr = [3, 1, 2]

print(permutationDiff(arr, brr))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG
{
// Utility function to find next permutation
static void next_permutation(int []nums)
{
    int mark = -1;
    for (int i = nums.Length - 1; i > 0; i--) {
        if (nums[i] > nums[i - 1]) {
            mark = i - 1;
            break;
        }
    }
    if (mark == -1) {
        reverse(nums, 0, nums.Length - 1);
        return;
    }
    int idx = nums.Length-1;
    for (int i = nums.Length-1; i >= mark+1; i--) {
        if (nums[i] > nums[mark]) {
            idx = i;
            break;
        }
    }
    swap(nums, mark, idx);
    reverse(nums, mark + 1, nums.Length - 1);
}

// Utility function to swap two elements in array
static void swap(int []nums, int i, int j) {
    int t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
}
// Utility function to reverse the array in a range
public static void reverse(int []nums, int i, int j) {
    while (i < j) {
        swap(nums, i, j);
        i++;
        j--;
    }
}
// Function to find the distance between
// two permutations array arr[] and brr[]
// in lexicographical order
public static int permutationDiff(int []arr, int []brr)
{
    // Check if both permutations are
    // already equal or not
    if (arr.SequenceEqual(brr)) {
        return 0;
    }
    // Stores the distance between the
    // two permutations arr[] and brr[]
    int count = 0, flag = 0;
    while(!arr.SequenceEqual(brr))
    {
        // Increment the count
        count++;
        // call next_permutation
        next_permutation(brr);
    }
    // Return the total count
    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 3, 2 };
    int []brr = { 3, 1, 2 };

    Console.Write(permutationDiff(arr, brr));
    }
}
// This code is contributed by Samim Hossain Mondal
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*