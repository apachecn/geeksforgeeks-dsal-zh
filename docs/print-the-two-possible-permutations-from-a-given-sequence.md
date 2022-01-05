# 打印给定序列的两种可能排列

> 原文:[https://www . geeksforgeeks . org/print-给定序列的两种可能排列/](https://www.geeksforgeeks.org/print-the-two-possible-permutations-from-a-given-sequence/)

给定一个包含 **N** 正整数的数组 **arr** ，任务是检查给定的数组是否可以分解成两个排列，如果可能的话打印排列。如果从 **1 到 M** 的所有整数恰好只包含一次，则一个 **M** 整数序列被称为置换。
**举例:**

> **输入:** arr[] = { 1，2，5，3，4，1，2 }，N = 7
> **输出:** {1 2 5 3 4}，{1 2}
> **输入:** arr[] = {2，1，1，3}，N = 4
> **输出:**不可能

**进场:**

*   首先，我们需要检查数组是否是两个排列的拼接。在[这篇](https://www.geeksforgeeks.org/check-if-a-sequence-is-a-concatenation-of-two-permutations/)文章中有解释。
*   如果是，找到数组中最大的元素，说 **x** 。
*   如果索引**【0，x-1】**和**【x，n-1】**处的元素形成两个有效排列，则打印它们。
*   否则，将索引**【0，n-1–x】**和**【n–x，n–1】**处的元素打印为两个有效排列。

以下是上述方法的实现:

## C++

```
// C++ program to print two
// permutations from a given sequence

#include <bits/stdc++.h>
using namespace std;

// Function to check if the sequence is
// concatenation of two permutations or not
bool checkPermutation(int arr[], int n)
{
    // Computing the sum of all the
    // elements in the array
    long long sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Computing the prefix sum
    // for all the elements in the array
    long long prefix[n + 1] = { 0 };
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Iterating through the i
    // from lengths 1 to n-1
    for (int i = 0; i < n - 1; i++) {

        // Sum of first i+1 elements
        long long lsum = prefix[i];

        // Sum of remaining n-i-1 elements
        long long rsum = sum - prefix[i];

        // Lengths of the 2 permutations
        long long l_len = i + 1,
                  r_len = n - i - 1;

        // Checking if the sums
        // satisfy the formula or not
        if (((2 * lsum)
             == (l_len * (l_len + 1)))
            && ((2 * rsum)
                == (r_len * (r_len + 1))))
            return true;
    }

    return false;
}

// Function to print the
// two permutations
void printPermutations(int arr[], int n,
                       int l1, int l2)
{
    // Print the first permutation
    for (int i = 0; i < l1; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    // Print the second permutation
    for (int i = l1; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Function to find the two permutations
// from the given sequence
void findPermutations(int arr[], int n)
{
    // If the sequence is not a
    // concatenation of two permutations
    if (!checkPermutation(arr, n)) {
        cout << "Not Possible";
        return;
    }

    int l1 = 0, l2 = 0;

    // Find the largest element in the
    // array and set the lengths of the
    // permutations accordingly
    l1 = *max_element(arr, arr + n);
    l2 = n - l1;

    set<int> s1, s2;
    for (int i = 0; i < l1; i++)
        s1.insert(arr[i]);

    for (int i = l1; i < n; i++)
        s2.insert(arr[i]);

    if (s1.size() == l1 && s2.size() == l2)
        printPermutations(arr, n, l1, l2);
    else {
        swap(l1, l2);
        printPermutations(arr, n, l1, l2);
    }
}

// Driver code
int main()
{
    int arr[] = { 2, 1, 3, 4, 5,
                  6, 7, 8, 9, 1,
                  10, 2 };
    int n = sizeof(arr) / sizeof(int);

    findPermutations(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print two
// permutations from a given sequence
import java.util.*;

class GFG{

// Function to check if the sequence is
// concatenation of two permutations or not
static boolean checkPermutation(int arr[], int n)
{
    // Computing the sum of all the
    // elements in the array
    long sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Computing the prefix sum
    // for all the elements in the array
    int []prefix = new int[n + 1];
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Iterating through the i
    // from lengths 1 to n-1
    for (int i = 0; i < n - 1; i++) {

        // Sum of first i+1 elements
        long lsum = prefix[i];

        // Sum of remaining n-i-1 elements
        long rsum = sum - prefix[i];

        // Lengths of the 2 permutations
        long l_len = i + 1,
                  r_len = n - i - 1;

        // Checking if the sums
        // satisfy the formula or not
        if (((2 * lsum)
             == (l_len * (l_len + 1)))
            && ((2 * rsum)
                == (r_len * (r_len + 1))))
            return true;
    }

    return false;
}

// Function to print the
// two permutations
static void printPermutations(int arr[], int n,
                       int l1, int l2)
{
    // Print the first permutation
    for (int i = 0; i < l1; i++) {
        System.out.print(arr[i]+ " ");
    }
    System.out.println();

    // Print the second permutation
    for (int i = l1; i < n; i++) {
        System.out.print(arr[i]+ " ");
    }
}

// Function to find the two permutations
// from the given sequence
static void findPermutations(int arr[], int n)
{
    // If the sequence is not a
    // concatenation of two permutations
    if (!checkPermutation(arr, n)) {
        System.out.print("Not Possible");
        return;
    }

    int l1 = 0, l2 = 0;

    // Find the largest element in the
    // array and set the lengths of the
    // permutations accordingly
    l1 = Arrays.stream(arr).max().getAsInt();
    l2 = n - l1;

    HashSet<Integer> s1 = new HashSet<Integer>(),
            s2 = new HashSet<Integer>();
    for (int i = 0; i < l1; i++)
        s1.add(arr[i]);

    for (int i = l1; i < n; i++)
        s2.add(arr[i]);

    if (s1.size() == l1 && s2.size() == l2)
        printPermutations(arr, n, l1, l2);
    else {
        l1 = l1+l2;
        l2 = l1-l2;
        l1 = l1-l2;
        printPermutations(arr, n, l1, l2);
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 3, 4, 5,
                  6, 7, 8, 9, 1,
                  10, 2 };
    int n = arr.length;

    findPermutations(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print two
# permutations from a given sequence

# Function to check if the sequence is
# concatenation of two permutations or not
def checkPermutation(arr, n):
    # Computing the sum of all the
    # elements in the array
    sum = 0
    for i in range(n):
        sum += arr[i]

    # Computing the prefix sum
    # for all the elements in the array
    prefix = [0 for i in range(n+1)]
    prefix[0] = arr[0]
    for i in range(1,n):
        prefix[i] = prefix[i - 1] + arr[i]

    # Iterating through the i
    # from lengths 1 to n-1
    for i in range(n - 1):

        # Sum of first i+1 elements
        lsum = prefix[i]

        # Sum of remaining n-i-1 elements
        rsum = sum - prefix[i]

        # Lengths of the 2 permutations
        l_len = i + 1
        r_len = n - i - 1

        # Checking if the sums
        # satisfy the formula or not
        if (((2 * lsum) == (l_len * (l_len + 1))) and
                ((2 * rsum) == (r_len * (r_len + 1)))):
            return True

    return False

# Function to print the
# two permutations
def printPermutations(arr,n,l1,l2):
    # Print the first permutation
    for i in range(l1):
        print(arr[i],end = " ")

    print("\n",end = "");

    # Print the second permutation
    for i in range(l1, n, 1):
        print(arr[i], end = " ")

# Function to find the two permutations
# from the given sequence
def findPermutations(arr,n):

    # If the sequence is not a
    # concatenation of two permutations
    if (checkPermutation(arr, n) == False):
        print("Not Possible")
        return

    l1 = 0
    l2 = 0

    # Find the largest element in the
    # array and set the lengths of the
    # permutations accordingly
    l1 = max(arr)
    l2 = n - l1

    s1 = set()
    s2 = set()
    for i in range(l1):
        s1.add(arr[i])

    for i in range(l1,n):
        s2.add(arr[i])

    if (len(s1) == l1 and len(s2) == l2):
        printPermutations(arr, n, l1, l2)
    else:
        temp = l1
        l1 = l2
        l2 = temp
        printPermutations(arr, n, l1, l2)

# Driver code
if __name__ == '__main__':
    arr = [2, 1, 3, 4, 5,6, 7, 8, 9, 1,10, 2]
    n = len(arr)

    findPermutations(arr, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to print two
// permutations from a given sequence
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{

// Function to check if the sequence is
// concatenation of two permutations or not
static bool checkPermutation(int []arr, int n)
{
    // Computing the sum of all the
    // elements in the array
    long sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Computing the prefix sum
    // for all the elements in the array
    int []prefix = new int[n + 1];
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Iterating through the i
    // from lengths 1 to n-1
    for (int i = 0; i < n - 1; i++) {

        // Sum of first i+1 elements
        long lsum = prefix[i];

        // Sum of remaining n-i-1 elements
        long rsum = sum - prefix[i];

        // Lengths of the 2 permutations
        long l_len = i + 1,
                  r_len = n - i - 1;

        // Checking if the sums
        // satisfy the formula or not
        if (((2 * lsum)
             == (l_len * (l_len + 1)))
            && ((2 * rsum)
                == (r_len * (r_len + 1))))
            return true;
    }

    return false;
}

// Function to print the
// two permutations
static void printPermutations(int []arr, int n,
                       int l1, int l2)
{
    // Print the first permutation
    for (int i = 0; i < l1; i++) {
        Console.Write(arr[i]+ " ");
    }
    Console.WriteLine();

    // Print the second permutation
    for (int i = l1; i < n; i++) {
        Console.Write(arr[i]+ " ");
    }
}

// Function to find the two permutations
// from the given sequence
static void findPermutations(int []arr, int n)
{
    // If the sequence is not a
    // concatenation of two permutations
    if (!checkPermutation(arr, n)) {
        Console.Write("Not Possible");
        return;
    }

    int l1 = 0, l2 = 0;

    // Find the largest element in the
    // array and set the lengths of the
    // permutations accordingly
    l1 = arr.Max();
    l2 = n - l1;

    HashSet<int> s1 = new HashSet<int>(),
            s2 = new HashSet<int>();
    for (int i = 0; i < l1; i++)
        s1.Add(arr[i]);

    for (int i = l1; i < n; i++)
        s2.Add(arr[i]);

    if (s1.Count == l1 && s2.Count == l2)
        printPermutations(arr, n, l1, l2);
    else {
        l1 = l1+l2;
        l2 = l1-l2;
        l1 = l1-l2;
        printPermutations(arr, n, l1, l2);
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 1, 3, 4, 5,
                  6, 7, 8, 9, 1,
                  10, 2 };
    int n = arr.Length;

    findPermutations(arr, n);
}
}

// This code contributed by Rajput-Ji
```

**Output:** 

```
2 1 
3 4 5 6 7 8 9 1 10 2
```

时间复杂度:0(N)

辅助空间:O(N)