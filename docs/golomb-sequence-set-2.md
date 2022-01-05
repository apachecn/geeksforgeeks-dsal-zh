# Golomb 序列|第 2 集

> 原文:[https://www.geeksforgeeks.org/golomb-sequence-set-2/](https://www.geeksforgeeks.org/golomb-sequence-set-2/)

给定一个数字 **N** 。任务是找到 [Golomb 序列](https://www.geeksforgeeks.org/golomb-sequence/)的第一个 **N** 术语。 [Golomb 序列](https://www.geeksforgeeks.org/golomb-sequence/)是一个非递减整数序列，其中第 n 项等于 n 在序列中出现的次数。

> **输入:** N = 11
> **输出:**1 2 2 3 4 4 5 5 5
> **说明:**
> 第一项为 1。1 只出现一次。
> 第二学期是 2。2 出现两次。
> 第三学期是 2。3 出现两次。
> 第四学期是 3。4 出现三次。
> 第五学期是 3。5 出现三次。
> 
> **输入:**N = 6
> T3】输出:1 2 3 3 4

**进场:**

1.  用[1]初始化[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，因为 Golomb 序列从 1 开始。
2.  将最后一个索引的值存储在**地图 M** 中。
3.  对于 Golomb 序列直到 **N** :
    *   初始化 cnt = 0 并映射。
    *   如果 cnt 不等于 0，则 Golomb 序列中的当前元素是序列中的前一个元素，并减少 cnt。
    *   否则 [Golomb 序列](https://www.geeksforgeeks.org/golomb-sequence/)中的当前元素等于 **1 +序列中的前一个元素**，并且 cnt 被更新为[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)在 Golomb 序列中的当前元素处的值并减少 cnt。
    *   将当前索引映射到 Golomb 序列的当前值。
4.  打印存储在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**中的 [Golomb 序列](https://www.geeksforgeeks.org/golomb-sequence/)的所有元素。

下面是上述方法的实现:

## C++

```
// C++ program to find the first
// N terms of Golomb Sequence
#include "bits/stdc++.h"
#define MAX 100001
using namespace std;

// Function to print the Golomb
// Sequence
void printGolombSequence(int N)
{

    // Initialise the array
    int arr[MAX];

    // Initialise the cnt to 0
    int cnt = 0;

    // First and second element
    // of Golomb Sequence is 0, 1
    arr[0] = 0;
    arr[1] = 1;

    // Map to store the count of
    // current element in Golomb
    // Sequence
    map<int, int> M;

    // Store the count of 2
    M[2] = 2;

    // Iterate over 2 to N
    for (int i = 2; i <= N; i++) {

        // If cnt is equals to 0
        // then we have new number
        // for Golomb Sequence
        // which is 1 + previous
        // element
        if (cnt == 0) {
            arr[i] = 1 + arr[i - 1];
            cnt = M[arr[i]];
            cnt--;
        }

        // Else the current element
        // is the previous element
        // in this Sequence
        else {
            arr[i] = arr[i - 1];
            cnt--;
        }

        // Map the current index to
        // current value in arr[]
        M[i] = arr[i];
    }

    // Print the Golomb Sequence
    for (int i = 1; i <= N; i++) {
        cout << arr[i] << ' ';
    }
}

// Driver Code
int main()
{
    int N = 11;
    printGolombSequence(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the first
// N terms of Golomb Sequence
import java.util.*;

class GFG{

static int MAX = 1000;

// Function to print the Golomb
// Sequence
static void printGolombSequence(int N)
{

    // Initialise the array
    int []arr = new int[MAX];
    for(int i = 0; i < MAX; i++)
    arr[i] = 0;

    // Initialise the cnt to 0
    int cnt = 0;

    // First and second element
    // of Golomb Sequence is 0, 1
    arr[0] = 0;
    arr[1] = 1;

    // Map to store the count of
    // current element in Golomb
    // Sequence
    Map<Integer,Integer> M=new HashMap<Integer,Integer>();

    // Store the count of 2
    M.put(2,2);

    // Iterate over 2 to N
    for (int i = 2; i <= N; i++) {

        // If cnt is equals to 0
        // then we have new number
        // for Golomb Sequence 1 2 2 3 3 4 4 4 5 5 5
        // which is 1 + previous
        // element
        if (cnt == 0) {
            arr[i] = 1 + arr[i - 1];
            cnt = M.get(arr[i]);
            cnt--;
        }

        // Else the current element
        // is the previous element
        // in this Sequence
        else {
            arr[i] = arr[i - 1];
            cnt--;
        }

        // Map the current index to
        // current value in arr[]
            M.put(i, arr[i]);
    }

    // Print the Golomb Sequence
    for (int i = 1; i <= N; i++)
    {
        System.out.print(arr[i]+" ");
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 11;
    printGolombSequence(N);
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find the first
# N terms of Golomb Sequence
MAX = 100001

# Function to print the Golomb
# Sequence
def printGolombSequence(N):

    # Initialise the array
    arr = [0] * MAX

    # Initialise the cnt to 0
    cnt = 0

    # First and second element
    # of Golomb Sequence is 0, 1
    arr[0] = 0
    arr[1] = 1

    # Map to store the count of
    # current element in Golomb
    # Sequence
    M = dict()

    # Store the count of 2
    M[2] = 2

    # Iterate over 2 to N
    for i in range(2, N + 1):

        # If cnt is equals to 0
        # then we have new number
        # for Golomb Sequence
        # which is 1 + previous
        # element
        if (cnt == 0):
            arr[i] = 1 + arr[i - 1]
            cnt = M[arr[i]]
            cnt -= 1

        # Else the current element
        # is the previous element
        # in this Sequence
        else:
            arr[i] = arr[i - 1]
            cnt -= 1

        # Map the current index to
        # current value in arr[]
        M[i] = arr[i]

    # Print the Golomb Sequence
    for i in range(1, N + 1):
        print(arr[i], end=" ")

# Driver Code
N = 11
printGolombSequence(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the first
// N terms of Golomb Sequence
using System;
using System.Collections.Generic;

class GFG{

static int MAX = 1000;

// Function to print the Golomb
// Sequence
static void printGolombSequence(int N)
{

    // Initialise the array
    int[] arr = new int[MAX];
    for(int i = 0; i < MAX; i++)
        arr[i] = 0;

    // Initialise the cnt to 0
    int cnt = 0;

    // First and second element
    // of Golomb Sequence is 0, 1
    arr[0] = 0;
    arr[1] = 1;

    // Map to store the count of
    // current element in Golomb
    // Sequence
    Dictionary<int,
               int> M = new Dictionary<int,
                                       int>(); 

    // Store the count of 2
    M.Add(2, 2);

    // Iterate over 2 to N
    for(int i = 2; i <= N; i++)
    {

        // If cnt is equals to 0
        // then we have new number
        // for Golomb Sequence 1 2 2 3 3 4 4 4 5 5 5
        // which is 1 + previous
        // element
        if (cnt == 0)
        {
            arr[i] = 1 + arr[i - 1];
            cnt = M[arr[i]];
            cnt--;
        }

        // Else the current element
        // is the previous element
        // in this Sequence
        else
        {
            arr[i] = arr[i - 1];
            cnt--;
        }

        // Map the current index to
        // current value in arr[]
        if(M.ContainsKey(i))
        {
            M[i] = arr[i];
        }
        else
        {
            M.Add(i, arr[i]);
        }
    }

    // Print the Golomb Sequence
    for(int i = 1; i <= N; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver Code
static void Main()
{
    int N = 11;

    printGolombSequence(N);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program to find the first
// N terms of Golomb Sequence
var MAX = 100001;

// Function to print the Golomb
// Sequence
function printGolombSequence(N)
{

    // Initialise the array
    var arr = Array(MAX);

    // Initialise the cnt to 0
    var cnt = 0;

    // First and second element
    // of Golomb Sequence is 0, 1
    arr[0] = 0;
    arr[1] = 1;

    // Map to store the count of
    // current element in Golomb
    // Sequence
    var M = new Map();

    // Store the count of 2
    M.set(2, 2);

    // Iterate over 2 to N
    for (var i = 2; i <= N; i++) {

        // If cnt is equals to 0
        // then we have new number
        // for Golomb Sequence
        // which is 1 + previous
        // element
        if (cnt == 0) {
            arr[i] = 1 + arr[i - 1];
            cnt = M.get(arr[i]);
            cnt--;
        }

        // Else the current element
        // is the previous element
        // in this Sequence
        else {
            arr[i] = arr[i - 1];
            cnt--;
        }

        // Map the current index to
        // current value in arr[]
        M.set(i, arr[i]);
    }

    // Print the Golomb Sequence
    for (var i = 1; i <= N; i++) {
        document.write( arr[i] + ' ');
    }
}

// Driver Code
var N = 11;
printGolombSequence(N);

</script>
```

**Output:** 

```
1 2 2 3 3 4 4 4 5 5 5
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)