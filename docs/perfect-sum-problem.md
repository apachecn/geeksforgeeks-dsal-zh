# 完全数题

> 原文:[https://www.geeksforgeeks.org/perfect-sum-problem/](https://www.geeksforgeeks.org/perfect-sum-problem/)

给定一个整数数组 **arr[]** 和一个整数 **K** ，任务是打印给定数组的所有子集，其总和等于给定目标 K。
**示例:**

```
Input: arr[] = {5, 10, 12, 13, 15, 18}, K = 30
Output: {12, 18}, {5, 12, 13}, {5, 10, 15}
Explanation: 
Subsets with sum 30 are:
12 + 18 = 30
5 + 12 + 13 = 30
5 + 10 + 15 = 30

Input: arr[] = {1, 2, 3, 4}, K = 5
Output: {2, 3}, {1, 4}
```

**方法:**思路是利用[幂集](https://www.geeksforgeeks.org/power-set/)概念找出所有子集。对于每个集合，检查集合的和是否等于 K。如果相等，则打印该集合。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to print the subsets whose
// sum is equal to the given target K
void sumSubsets(vector<int> set, int n, int target)
{
    // Create the new array with size
    // equal to array set[] to create
    // binary array as per n(decimal number)
    int x[set.size()];
    int j = set.size() - 1;

    // Convert the array into binary array
    while (n > 0)
    {
        x[j] = n % 2;
        n = n / 2;
        j--;
    }

    int sum = 0;

    // Calculate the sum of this subset
    for (int i = 0; i < set.size(); i++)
        if (x[i] == 1)
            sum = sum + set[i];

    // Check whether sum is equal to target
    // if it is equal, then print the subset
    if (sum == target)
    {
        cout<<("{");
        for (int i = 0; i < set.size(); i++)
            if (x[i] == 1)
                cout << set[i] << ", ";
        cout << ("}, ");
    }
}

// Function to find the subsets with sum K
void findSubsets(vector<int> arr, int K)
{
    // Calculate the total no. of subsets
    int x = pow(2, arr.size());

    // Run loop till total no. of subsets
    // and call the function for each subset
    for (int i = 1; i < x; i++)
        sumSubsets(arr, i, K);
}

// Driver code
int main()
{
    vector<int> arr = { 5, 10, 12, 13, 15, 18 };
    int K = 30;
    findSubsets(arr, K);
    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG {

    // Function to print the subsets whose
    // sum is equal to the given target K
    public static void sumSubsets(
        int set[], int n, int target)
    {
        // Create the new array with size
        // equal to array set[] to create
        // binary array as per n(decimal number)
        int x[] = new int[set.length];
        int j = set.length - 1;

        // Convert the array into binary array
        while (n > 0) {
            x[j] = n % 2;
            n = n / 2;
            j--;
        }

        int sum = 0;

        // Calculate the sum of this subset
        for (int i = 0; i < set.length; i++)
            if (x[i] == 1)
                sum = sum + set[i];

        // Check whether sum is equal to target
        // if it is equal, then print the subset
        if (sum == target) {
            System.out.print("{");
            for (int i = 0; i < set.length; i++)
                if (x[i] == 1)
                    System.out.print(set[i] + ", ");
            System.out.print("}, ");
        }
    }

    // Function to find the subsets with sum K
    public static void findSubsets(int[] arr, int K)
    {
        // Calculate the total no. of subsets
        int x = (int)Math.pow(2, arr.length);

        // Run loop till total no. of subsets
        // and call the function for each subset
        for (int i = 1; i < x; i++)
            sumSubsets(arr, i, K);
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 5, 10, 12, 13, 15, 18 };
        int K = 30;

        findSubsets(arr, K);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to print the subsets whose
# sum is equal to the given target K
def sumSubsets(sets, n, target) :

    # Create the new array with size
    # equal to array set[] to create
    # binary array as per n(decimal number)
    x = [0]*len(sets);
    j = len(sets) - 1;

    # Convert the array into binary array
    while (n > 0) :

        x[j] = n % 2;
        n = n // 2;
        j -= 1;

    sum = 0;

    # Calculate the sum of this subset
    for i in range(len(sets)) :
        if (x[i] == 1) :
            sum += sets[i];

    # Check whether sum is equal to target
    # if it is equal, then print the subset
    if (sum == target) :

        print("{",end="");
        for i in range(len(sets)) :
            if (x[i] == 1) :
                print(sets[i],end= ", ");
        print("}, ",end="");

# Function to find the subsets with sum K
def findSubsets(arr, K) :

    # Calculate the total no. of subsets
    x = pow(2, len(arr));

    # Run loop till total no. of subsets
    # and call the function for each subset
    for i in range(1, x) :
        sumSubsets(arr, i, K);

# Driver code
if __name__ == "__main__" :

    arr = [ 5, 10, 12, 13, 15, 18 ];
    K = 30;
    findSubsets(arr, K);

# This code is contributed by Yash_R
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to print the subsets whose
    // sum is equal to the given target K
    public static void sumSubsets(
        int []set, int n, int target)
    {
        // Create the new array with size
        // equal to array set[] to create
        // binary array as per n(decimal number)
        int []x = new int[set.Length];
        int j = set.Length - 1;

        // Convert the array into binary array
        while (n > 0)
        {
            x[j] = n % 2;
            n = n / 2;
            j--;
        }

        int sum = 0;

        // Calculate the sum of this subset
        for (int i = 0; i < set.Length; i++)
            if (x[i] == 1)
                sum = sum + set[i];

        // Check whether sum is equal to target
        // if it is equal, then print the subset
        if (sum == target)
        {
            Console.Write("{");
            for (int i = 0; i < set.Length; i++)
                if (x[i] == 1)
                    Console.Write(set[i] + ", ");
            Console.Write("}, ");
        }
    }

    // Function to find the subsets with sum K
    public static void findSubsets(int[] arr, int K)
    {
        // Calculate the total no. of subsets
        int x = (int)Math.Pow(2, arr.Length);

        // Run loop till total no. of subsets
        // and call the function for each subset
        for (int i = 1; i < x; i++)
            sumSubsets(arr, i, K);
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 5, 10, 12, 13, 15, 18 };
        int K = 30;

        findSubsets(arr, K);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to print the subsets whose
// sum is equal to the given target K
function sumSubsets(set, n, target) {
    // Create the new array with length
    // equal to array set[] to create
    // binary array as per n(decimal number)
    let x = new Array(set.length);
    let j = set.length - 1;

    // Convert the array into binary array
    while (n > 0) {
        x[j] = n % 2;
        n = Math.floor(n / 2);
        j--;
    }

    let sum = 0;

    // Calculate the sum of this subset
    for (let i = 0; i < set.length; i++)
        if (x[i] == 1)
            sum = sum + set[i];

    // Check whether sum is equal to target
    // if it is equal, then print the subset
    if (sum == target) {
        document.write("{");
        for (let i = 0; i < set.length; i++)
            if (x[i] == 1)
                document.write(set[i] + ", ");
        document.write("}, ");
    }
}

// Function to find the subsets with sum K
function findSubsets(arr, K) {
    // Calculate the total no. of subsets
    let x = Math.pow(2, arr.length);

    // Run loop till total no. of subsets
    // and call the function for each subset
    for (let i = 1; i < x; i++)
        sumSubsets(arr, i, K);
}

// Driver code

let arr = [5, 10, 12, 13, 15, 18];
let K = 30;
findSubsets(arr, K);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
{12, 18, }, {5, 12, 13, }, {5, 10, 15, },
```

**时间复杂度:** 2 <sup>N</sup>

**辅助空间:** O(N)
**高效途径:**
这个问题也可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。参考[这篇](https://www.geeksforgeeks.org/perfect-sum-problem-print-subsets-given-sum/)文章。