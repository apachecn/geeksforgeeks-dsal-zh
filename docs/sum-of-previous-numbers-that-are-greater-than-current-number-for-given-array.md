# 给定数组中大于当前数的先前数之和

> 原文:[https://www . geeksforgeeks . org/给定数组大于当前数的前几个数之和/](https://www.geeksforgeeks.org/sum-of-previous-numbers-that-are-greater-than-current-number-for-given-array/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**，对于数组中的每个元素，任务是找出所有先前元素的和，这些元素的和**严格大于当前元素的**。

**示例:**

> **输入:** A[] = {2，6，4，1，7}
> **输出:** 0 0 6 12 0
> **解释:**
> 对于 2 和 6，左边没有比它大的元素。
> 4 有 6。
> 1 的总和是 12。
> 对于 7 来说，再没有比它更大的元素了。
> 
> **输入:** A[] = {7，3，6，2，1}
> **输出:** 0 7 7 16 18
> **解释:**
> 对于 7，左边没有比它大的元素。
> 3 有 7。
> 6 的总和是 7。
> 对于 2，它必须是 7 + 3 + 6 = 16。
> 对于 1，总和将是 7 + 3 + 6 + 2 = 18

**天真法:**对于每个元素，思路是找出严格大于其左侧当前元素的元素，然后找出所有这些元素的和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Max Element of the Array
const int maxn = 1000000;

// Function to find the sum of previous
// numbers that are greater than the
// current number for the given array
void sumGreater(int ar[], int N)
{

    // Loop to iterate over all
    // the elements of the array
    for (int i = 0; i < N; i++) {

        // Store the answer for
        // the current element
        int cur_sum = 0;

        // Iterate from (current index - 1)
        // to 0 and check if ar[j] is greater
        // than the current element and add
        // it to the cur_sum if so

        for (int j = i - 1; j >= 0; j--) {

            if (ar[j] > ar[i])
                cur_sum += ar[j];
        }

        // Print the answer for
        // current element
        cout << cur_sum << " ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int ar[] = { 7, 3, 6, 2, 1 };

    // Size of the array
    int N = sizeof ar / sizeof ar[0];

    // Function call
    sumGreater(ar, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Max Element of the Array
static int maxn = 1000000;

// Function to find the sum of previous
// numbers that are greater than the
// current number for the given array
static void sumGreater(int ar[], int N)
{

    // Loop to iterate over all
    // the elements of the array
    for(int i = 0; i < N; i++)
    {

        // Store the answer for
        // the current element
        int cur_sum = 0;

        // Iterate from (current index - 1)
        // to 0 and check if ar[j] is greater
        // than the current element and add
        // it to the cur_sum if so
        for(int j = i - 1; j >= 0; j--)
        {
            if (ar[j] > ar[i])
                cur_sum += ar[j];
        }

        // Print the answer for
        // current element
        System.out.print(cur_sum + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int ar[] = { 7, 3, 6, 2, 1 };

    // Size of the array
    int N = ar.length;

    // Function call
    sumGreater(ar, N);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Max Element of the Array
maxn = 1000000;

# Function to find the sum of previous
# numbers that are greater than the
# current number for the given array
def sumGreater(ar, N):

    # Loop to iterate over all
    # the elements of the array
    for i in range(N):

        # Store the answer for
        # the current element
        cur_sum = 0;

        # Iterate from (current index - 1)
        # to 0 and check if ar[j] is greater
        # than the current element and add
        # it to the cur_sum if so
        for j in range(i, -1, -1):
            if (ar[j] > ar[i]):
                cur_sum += ar[j];

        # Prthe answer for
        # current element
        print(cur_sum, end = " ");

# Driver Code
if __name__ == '__main__':

    # Given array arr
    ar = [ 7, 3, 6, 2, 1] ;

    # Size of the array
    N = len(ar);

    # Function call
    sumGreater(ar, N);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Max Element of the Array
//static int maxn = 1000000;

// Function to find the sum of previous
// numbers that are greater than the
// current number for the given array
static void sumGreater(int []ar, int N)
{

    // Loop to iterate over all
    // the elements of the array
    for(int i = 0; i < N; i++)
    {

        // Store the answer for
        // the current element
        int cur_sum = 0;

        // Iterate from (current index - 1)
        // to 0 and check if ar[j] is greater
        // than the current element and add
        // it to the cur_sum if so
        for(int j = i - 1; j >= 0; j--)
        {
            if (ar[j] > ar[i])
                cur_sum += ar[j];
        }

        // Print the answer for
        // current element
        Console.Write(cur_sum + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []ar = { 7, 3, 6, 2, 1 };

    // Size of the array
    int N = ar.Length;

    // Function call
    sumGreater(ar, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach   
// Max Element of the Array
var maxn = 1000000;

// Function to find the sum of previous
// numbers that are greater than the
// current number for the given array
function sumGreater(ar, N)
{

    // Loop to iterate over all
    // the elements of the array
    for(i = 0; i < N; i++)
    {

        // Store the answer for
        // the current element
        var cur_sum = 0;

        // Iterate from (current index - 1)
        // to 0 and check if ar[j] is greater
        // than the current element and add
        // it to the cur_sum if so
        for(j = i - 1; j >= 0; j--)
        {
            if (ar[j] > ar[i])
                cur_sum += ar[j];
        }

        // Print the answer for
        // current element
        document.write(cur_sum + " ");
    }
}

// Driver Code

// Given array arr
var ar = [ 7, 3, 6, 2, 1 ];

// Size of the array
var N = ar.length;

// Function call
sumGreater(ar, N);

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
0 7 7 16 18
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是使用 [**芬威克树**](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) 。以下是步骤:

1.  遍历给定的数组，找到芬威克树中存储的所有元素的和(比如 **total_sum** )。
2.  现在考虑每个元素(比如**arr【I】**)作为芬威克树的索引。
3.  现在使用存储在树中的值找到小于当前元素的所有元素的总和(比如 **curr_sum** )。
4.  **total _ sum–curr _ sum**的值将给出严格大于当前元素左侧元素的所有元素的总和。
5.  更新芬威克树中的当前元素。
6.  对数组中的所有元素重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Max Element of the Array
const int maxn = 1000000;

// Initializing Fenwick Tree
int Bit[maxn + 5];

// Function to calculate the sum of
// previous numbers that are greater
// than the current number in the array
void sum(int ar[], int N)
{

    // Iterate from 1 to N
    for (int i = 0; i < N; i++) {
        int index;
        int total_sum = 0;
        index = 100000;

        // If some greater values has
        // occured before current element
        // then it will be already stored
        // in Fenwick Tree
        while (index) {

            // Calculating sum of
            // all the elememts
            total_sum += Bit[index];
            index -= index & -index;
        }
        int cur_sum = 0;

        // Sum only smaller or equal
        // elements than current element
        index = ar[i];

        while (index) {

            // If some smaller values has
            // occured before it will be
            // already stored in Tree
            cur_sum += Bit[index];
            index -= (index & -index);
        }

        int ans = total_sum - cur_sum;
        cout << ans << " ";

        // Update the fenwick tree
        index = ar[i];
        while (index <= 100000) {

            // Updating The Fenwick Tree
            // for future values
            Bit[index] += ar[i];
            index += (index & -index);
        }
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int ar[] = { 7, 3, 6, 2, 1 };
    int N = sizeof ar / sizeof ar[0];

    // Function call
    sum(ar, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Max Element of the Array
static int maxn = 1000000;

// Initializing Fenwick Tree
static int []Bit = new int[maxn + 5];

// Function to calculate the sum of
// previous numbers that are greater
// than the current number in the array
static void sum(int ar[], int N)
{

    // Iterate from 1 to N
    for (int i = 0; i < N; i++)
    {
        int index;
        int total_sum = 0;
        index = 100000;

        // If some greater values has
        // occured before current element
        // then it will be already stored
        // in Fenwick Tree
        while (index > 0)
        {

            // Calculating sum of
            // all the elememts
            total_sum += Bit[index];
            index -= index & -index;
        }
        int cur_sum = 0;

        // Sum only smaller or equal
        // elements than current element
        index = ar[i];

        while (index > 0)
        {

            // If some smaller values has
            // occured before it will be
            // already stored in Tree
            cur_sum += Bit[index];
            index -= (index & -index);
        }

        int ans = total_sum - cur_sum;
        System.out.print(ans + " ");

        // Update the fenwick tree
        index = ar[i];
        while (index <= 100000)
        {

            // Updating The Fenwick Tree
            // for future values
            Bit[index] += ar[i];
            index += (index & -index);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int ar[] = { 7, 3, 6, 2, 1 };
    int N = ar.length;

    // Function call
    sum(ar, N);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Max Element of the Array
maxn = 1000000;

# Initializing Fenwick Tree
Bit = [0] * (maxn + 5);

# Function to calculate the sum of
# previous numbers that are greater
# than the current number in the array
def sum(ar, N):

    # Iterate from 1 to N
    for i in range(N):
        total_sum = 0;
        index = 100000;

        # If some greater values has
        # occured before current element
        # then it will be already stored
        # in Fenwick Tree
        while (index > 0):

            # Calculating sum of
            # all the elememts
            total_sum += Bit[index];
            index -= index & -index;

        cur_sum = 0;

        # Sum only smaller or equal
        # elements than current element
        index = ar[i];

        while (index > 0):

            # If some smaller values has
            # occured before it will be
            # already stored in Tree
            cur_sum += Bit[index];
            index -= (index & -index);

        ans = total_sum - cur_sum;
        print(ans, end=" ");

        # Update the fenwick tree
        index = ar[i];
        while (index <= 100000):

            # Updating The Fenwick Tree
            # for future values
            Bit[index] += ar[i];
            index += (index & -index);

# Driver Code
if __name__ == '__main__':
    # Given array arr
    arr = [7, 3, 6, 2, 1];
    N = len(arr);

    # Function call
    sum(arr, N);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Max Element of the Array
static int maxn = 1000000;

// Initializing Fenwick Tree
static int []Bit = new int[maxn + 5];

// Function to calculate the sum of
// previous numbers that are greater
// than the current number in the array
static void sum(int []ar, int N)
{

    // Iterate from 1 to N
    for (int i = 0; i < N; i++)
    {
        int index;
        int total_sum = 0;
        index = 100000;

        // If some greater values has
        // occured before current element
        // then it will be already stored
        // in Fenwick Tree
        while (index > 0)
        {

            // Calculating sum of
            // all the elememts
            total_sum += Bit[index];
            index -= index & -index;
        }
        int cur_sum = 0;

        // Sum only smaller or equal
        // elements than current element
        index = ar[i];

        while (index > 0)
        {

            // If some smaller values has
            // occured before it will be
            // already stored in Tree
            cur_sum += Bit[index];
            index -= (index & -index);
        }

        int ans = total_sum - cur_sum;
        Console.Write(ans + " ");

        // Update the fenwick tree
        index = ar[i];
        while (index <= 100000)
        {

            // Updating The Fenwick Tree
            // for future values
            Bit[index] += ar[i];
            index += (index & -index);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int []ar = { 7, 3, 6, 2, 1 };
    int N = ar.Length;

    // Function call
    sum(ar, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Max Element of the Array
    var maxn = 1000000;

    // Initializing Fenwick Tree
     var Bit = Array(maxn + 5).fill(0);

    // Function to calculate the sum of
    // previous numbers that are greater
    // than the current number in the array
    function sum(ar , N) {

        // Iterate from 1 to N
        for (i = 0; i < N; i++) {
            var index;
            var total_sum = 0;
            index = 100000;

            // If some greater values has
            // occured before current element
            // then it will be already stored
            // in Fenwick Tree
            while (index > 0) {

                // Calculating sum of
                // all the elememts
                total_sum += Bit[index];
                index -= index & -index;
            }
            var cur_sum = 0;

            // Sum only smaller or equal
            // elements than current element
            index = ar[i];

            while (index > 0) {

                // If some smaller values has
                // occured before it will be
                // already stored in Tree
                cur_sum += Bit[index];
                index -= (index & -index);
            }

            var ans = total_sum - cur_sum;
            document.write(ans + " ");

            // Update the fenwick tree
            index = ar[i];
            while (index <= 100000) {

                // Updating The Fenwick Tree
                // for future values
                Bit[index] += ar[i];
                index += (index & -index);
            }
        }
    }

    // Driver Code

        // Given array arr
        var ar = [ 7, 3, 6, 2, 1 ];
        var N = ar.length;

        // Function call
        sum(ar, N);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
0 7 7 16 18
```

***时间复杂度:**O(N * log(max _ element))*
***辅助空间:** O(max_element)*