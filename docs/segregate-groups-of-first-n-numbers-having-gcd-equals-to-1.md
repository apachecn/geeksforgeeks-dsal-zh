# 将 GCD 等于 1 的前 N 个数字的组分开

> 原文:[https://www . geesforgeks . org/separate-group-of-first-n-numbers-having-gcd-equal-to-1/](https://www.geeksforgeeks.org/segregate-groups-of-first-n-numbers-having-gcd-equals-to-1/)

给定一个数字 **N** 。任务是将从 **1 到 N** 的所有数字分组，这样每组中所有数字的 GCD 为 1，因为组的数量必须最小化。

**示例:**

> **输入:** N = 3
> **输出:**
> 1 2 3
> **解释:**
> gcd(1，2，3) = 1
> 
> **输入:** N = 6
> **输出:**
> 1 2
> 3 4
> 5 6
> **解释:**
> gcd(1，2) = 1
> gcd(3，4) = 1
> gcd(5，6) = 1

**进场:**众所周知，每一个连续号码的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 都是 1。所以我们就用这个事实来解决这个问题。以下是步骤:

1.  如果数字是 3，那么只有一个组是可能的 **{1，2，3}** ，其 GCD(1，2，3)是 1。
2.  否则迭代(说 **i** )到**【1，N/2】**上，使用**(2 * I–1，2*i)** 组成组，并将其存储在[向量数组](https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/)中(说 **arr[][]** )。
3.  存储在 arr[][]中的组是所需的组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the groups
void printGroups(vector<int> A[], int N)
{

    // Iterate over [1, N/2];
    for (int i = 1; i <= N / 2 + 1; i++) {

        // Print all pairs
        for (int j = 0; j < A[i].size(); j++) {
            cout << A[i][j] << ' ';
        }
        cout << endl;
    }
}

// Function to form a groups with GCD 1
void formGroups(int N)
{
    int i;

    // Corner case
    if (N == 3) {
        cout << "1 2 3";
        return;
    }

    // Array of vectors to store the
    // possible pairs
    vector<int> arr[N / 2 + 2];

    for (i = 1; i <= N / 2; i++) {

        // Push the pair (2*i - 1, 2*i)
        arr[i].push_back(2 * i - 1);
        arr[i].push_back(2 * i);
    }

    // If N is odd then push the
    // last element N
    if (N & 1) {
        arr[i].push_back(N);
    }

    // Function Call
    printGroups(arr, N);

    return;
}

// Driver Code
int main()
{
    int N = 10;

    // Function Call
    formGroups(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the groups
static void printGroups(Vector<Integer> A[],
                        int N)
{

    // Iterate over [1, N/2];
    for(int i = 1; i <= N / 2 + 1; i++)
    {

        // Print all pairs
        for(int j = 0; j < A[i].size(); j++)
        {
            System.out.print(A[i].get(j) + " ");
        }
        System.out.println();
    }
}

// Function to form a groups with GCD 1
static void formGroups(int N)
{
    int i;

    // Corner case
    if (N == 3)
    {
        System.out.print("1 2 3");
        return;
    }

    // Array of vectors to store the
    // possible pairs
    @SuppressWarnings("unchecked")
    Vector<Integer> []arr = new Vector[N / 2 + 2];
    for(int k = 0; k < arr.length; k++)
        arr[k] = new Vector<Integer>();

    for(i = 1; i <= N / 2; i++)
    {

        // Push the pair (2*i - 1, 2*i)
        arr[i].add(2 * i - 1);
        arr[i].add(2 * i);
    }

    // If N is odd then push the
    // last element N
    if ((N & 1) != 0)
    {
        arr[i].add(N);
    }

    // Function call
    printGroups(arr, N);

    return;
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;

    // Function call
    formGroups(N);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to print the groups
def printGroups(A, N):

    # Iterate over [1, N / 2];
    for i in range (0, N // 2 ):

        # Print all pairs
        for j in range (len(A[i])):
            print (A[i][j], end = ' ')

        print ()

# Function to form a
# groups with GCD 1
def formGroups(N):

    # Corner case
    if (N == 3):
        print ("1 2 3")
        return

    # Array of vectors
    # to store the
    # possible pairs
    arr = []

    for i in range (1, N // 2 + 1):
        P = []

        # Push the pair
        # (2 * i - 1, 2 * i)
        P.append(2 * i - 1)
        P.append(2 * i)
        arr.append(P)

    # If N is odd then push the
    # last element N
    if (N & 1):
        arr.append(N)

    # Function Call
    printGroups(arr, N)

    return

# Driver Code
if __name__ == "__main__":

    N = 10

    # Function Call
    formGroups(N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the groups
static void printGroups(List<int> []A,
                        int N)
{

    // Iterate over [1, N/2];
    for(int i = 1; i <= N / 2 + 1; i++)
    {

        // Print all pairs
        for(int j = 0; j < A[i].Count; j++)
        {
            Console.Write(A[i][j] + " ");
        }
        Console.WriteLine();
    }
}

// Function to form a groups with GCD 1
static void formGroups(int N)
{
    int i;

    // Corner case
    if (N == 3)
    {
        Console.Write("1 2 3");
        return;
    }

    // Array of vectors to store the
    // possible pairs
    List<int> []arr = new List<int>[N / 2 + 2];
    for(int k = 0; k < arr.Length; k++)
        arr[k] = new List<int>();

    for(i = 1; i <= N / 2; i++)
    {

        // Push the pair (2*i - 1, 2*i)
        arr[i].Add(2 * i - 1);
        arr[i].Add(2 * i);
    }

    // If N is odd then push the
    // last element N
    if ((N & 1) != 0)
    {
        arr[i].Add(N);
    }

    // Function call
    printGroups(arr, N);

    return;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 10;

    // Function call
    formGroups(N);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the groups
function printGroups(A,N)
{
    // Iterate over [1, N/2];
    for(let i = 1; i <= N / 2 + 1; i++)
    {

        // Print all pairs
        for(let j = 0; j < A[i].length; j++)
        {
            document.write(A[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Function to form a groups with GCD 1
function formGroups(N)
{
    let i;

    // Corner case
    if (N == 3)
    {
        document.write("1 2 3");
        return;
    }

    // Array of vectors to store the
    // possible pairs
    let arr = new Array(Math.floor(N / 2) + 2);
    for(let k = 0; k < arr.length; k++)
        arr[k] = [];

    for(i = 1; i <= N / 2; i++)
    {

        // Push the pair (2*i - 1, 2*i)
        arr[i].push(2 * i - 1);
        arr[i].push(2 * i);
    }

    // If N is odd then push the
    // last element N
    if ((N & 1) != 0)
    {
        arr[i].push(N);
    }

    // Function call
    printGroups(arr, N);

    return;
}

// Driver Code
let N = 10;

// Function call
formGroups(N);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1 2 
3 4 
5 6 
7 8 
9 10
```

**时间复杂度:** O(N)，其中 N 为给定数。