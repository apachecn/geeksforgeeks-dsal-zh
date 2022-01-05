# 求 N 个元素数组中所有可能对的和

> 原文:[https://www . geesforgeks . org/find-n 元素数组中所有可能对的总和/](https://www.geeksforgeeks.org/find-the-sum-of-all-possible-pairs-in-an-array-of-n-elements/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是从给定的数组中找出所有可能的对的和。请注意，

1.  **(arr[i]，arr[i])** 也被认为是有效对。
2.  **(arr[i]、arr[j])** 和 **(arr[j]、arr[i])** 被认为是两个不同的对。

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** 12
> 所有有效对为(1，1)、(1，2)、(2，1)和(2，2)。
> 1 + 1 + 1 + 2 + 2 + 1 + 2 + 2 = 12
> 
> **输入:** arr[] = {1，2，3，1，4}
> 输出: 110

**天真法:**找出所有可能的对，计算每对元素的和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of the elements
// of all possible pairs from the array
int sumPairs(int arr[], int n)
{

    // To store the required sum
    int sum = 0;

    // Nested loop for all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            // Add the sum of the elements
            // of the current pair
            sum += (arr[i] + arr[j]);
        }
    }
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sumPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the sum of the elements
    // of all possible pairs from the array
    static int sumPairs(int arr[], int n)
    {

        // To store the required sum
        int sum = 0;

        // Nested loop for all possible pairs
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                // Add the sum of the elements
                // of the current pair
                sum += (arr[i] + arr[j]);
            }
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3};
        int n = arr.length;

        System.out.println(sumPairs(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the summ of the elements
# of all possible pairs from the array
def summPairs(arr, n):

    # To store the required summ
    summ = 0

    # Nested loop for all possible pairs
    for i in range(n):
        for j in range(n):

            # Add the summ of the elements
            # of the current pair
            summ += (arr[i] + arr[j])

    return summ

# Driver code
arr = [1, 2, 3]
n = len(arr)

print(summPairs(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the sum of the elements
    // of all possible pairs from the array
    static int sumPairs(int []arr, int n)
    {

        // To store the required sum
        int sum = 0;

        // Nested loop for all possible pairs
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                // Add the sum of the elements
                // of the current pair
                sum += (arr[i] + arr[j]);
            }
        }
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {1, 2, 3};
        int n = arr.Length;

        Console.WriteLine(sumPairs(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum of the elements
// of all possible pairs from the array
function sumPairs(arr, n)
{

    // To store the required sum
    var sum = 0;
    var i, j;

    // Nested loop for all possible pairs
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < n; j++)
        {

            // Add the sum of the elements
            // of the current pair
            sum += (arr[i] + arr[j]);
        }
    }
    return sum;
}

// Driver code
var arr = [ 1, 2, 3 ];
var n = arr.length;

document.write(sumPairs(arr, n));

// This code is contributed by ipg2016107

</script>
```

**Output:** 

```
36
```

**时间复杂度:** O(N <sup>2</sup> )

**高效方法:**可以观察到，每个元素作为一对 **(x，y)** 的元素之一，恰好出现 **(2 * N)** 次。精确地 **N** 倍于 **x** ，精确地 **N** 倍于 **y** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of the elements
// of all possible pairs from the array
int sumPairs(int arr[], int n)
{

    // To store the required sum
    int sum = 0;

    // For every element of the array
    for (int i = 0; i < n; i++) {

        // It appears (2 * n) times
        sum = sum + (arr[i] * (2 * n));
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sumPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the sum of the elements
// of all possible pairs from the array
static int sumPairs(int arr[], int n)
{

    // To store the required sum
    int sum = 0;

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // It appears (2 * n) times
        sum = sum + (arr[i] * (2 * n));
    }

    return sum;
}

// Driver code
static public void main(String []arg)
{
    int arr[] = { 1, 2, 3 };
    int n = arr.length;

    System.out.println(sumPairs(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of the elements
# of all possible pairs from the array
def sumPairs(arr, n) :

    # To store the required sum
    sum = 0;

    # For every element of the array
    for i in range(n) :

        # It appears (2 * n) times
        sum = sum + (arr[i] * (2 * n));

    return sum;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3 ];
    n = len(arr);

    print(sumPairs(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;        

class GFG
{

// Function to return the sum of the elements
// of all possible pairs from the array
static int sumPairs(int []arr, int n)
{

    // To store the required sum
    int sum = 0;

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // It appears (2 * n) times
        sum = sum + (arr[i] * (2 * n));
    }

    return sum;
}

// Driver code
static public void Main(String []arg)
{
    int []arr = { 1, 2, 3 };
    int n = arr.Length;

    Console.WriteLine(sumPairs(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum of the elements
// of all possible pairs from the array
function sumPairs(arr, n)
{

    // To store the required sum
    let sum = 0;

    // For every element of the array
    for (let i = 0; i < n; i++) {

        // It appears (2 * n) times
        sum = sum + (arr[i] * (2 * n));
    }

    return sum;
}

// Driver code
    let arr = [ 1, 2, 3 ];
    let n = arr.length;

    document.write(sumPairs(arr, n));

</script>
```

**Output:** 

```
36
```

**时间复杂度:** O(N)