# 计算除所有其他元素之和的数组元素

> 原文:[https://www . geesforgeks . org/count-array-elements-除以所有其他元素的和/](https://www.geeksforgeeks.org/count-array-elements-that-divide-the-sum-of-all-other-elements/)

给定一个数组 **arr[]** ，任务是计算数组中除所有其他元素之和的元素数量。

**示例:**

> **输入:** arr[] = {3，10，4，6，7}
> **输出:** 3
> 3 除(10 + 4 + 6 + 7)即 27
> 10 除(3 + 4 + 6 + 7)即 20
> 6 除(3 + 10 + 4 + 7)即 24
> 
> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10}
> **输出:** 2

**天真方法:**从 0 到 N 运行两个循环，计算除当前元素之外的所有元素的总和，如果该元素除以该总和，则增加计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count
// of the required numbers
int countNum(int N, int arr[])
{
    // To store the count of required numbers
    int count = 0;
    for (int i = 0; i < N; i++) {

        // Initialize sum to 0
        int sum = 0;
        for (int j = 0; j < N; j++) {

            // If current element and the
            // chosen element are same
            if (i == j)
                continue;

            // Add all other numbers of array
            else
                sum += arr[j];
        }

        // If sum is divisible by the chosen element
        if (sum % arr[i] == 0)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
int main()
{
    int arr[] = { 3, 10, 4, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countNum(n, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of the required numbers
static int countNum(int N, int arr[])
{
    // To store the count of required numbers
    int count = 0;
    for (int i = 0; i < N; i++)
    {

        // Initialize sum to 0
        int sum = 0;
        for (int j = 0; j < N; j++)
        {

            // If current element and the
            // chosen element are same
            if (i == j)
                continue;

            // Add all other numbers of array
            else
                sum += arr[j];
        }

        // If sum is divisible by the chosen element
        if (sum % arr[i] == 0)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 10, 4, 6, 7 };
    int n = arr.length;
    System.out.println(countNum(n, arr));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of the required numbers
def countNum(N, arr):

    # To store the count of
    # required numbers
    count = 0

    for i in range(N):

        # Initialize sum to 0
        Sum = 0
        for j in range(N):

            # If current element and the
            # chosen element are same
            if (i == j):
                continue

            # Add all other numbers of array
            else:
                Sum += arr[j]

        # If Sum is divisible by the
        # chosen element
        if (Sum % arr[i] == 0):
            count += 1

    # Return the count
    return count

# Driver code
arr = [3, 10, 4, 6, 7]
n = len(arr)
print(countNum(n, arr))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of the required numbers
static int countNum(int N, int []arr)
{
    // To store the count of required numbers
    int count = 0;
    for (int i = 0; i < N; i++)
    {

        // Initialize sum to 0
        int sum = 0;
        for (int j = 0; j < N; j++)
        {

            // If current element and the
            // chosen element are same
            if (i == j)
                continue;

            // Add all other numbers of array
            else
                sum += arr[j];
        }

        // If sum is divisible by the chosen element
        if (sum % arr[i] == 0)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
public static void Main()
{
    int []arr = { 3, 10, 4, 6, 7 };
    int n = arr.Length;
    Console.WriteLine(countNum(n, arr));
}
}

// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to return the count
// of the required numbers
function countNum($N, $arr)
{
// To store the count of
// required numbers
$count = 0;

for ($i=0;$i<$N;$i++) {
// Initialize sum to 0
    $Sum = 0;
    for ($j = 0; $j < $N; $j++) {
        // If current element and the
        // chosen element are same
        if ($i == $j)
            continue;

        // Add all other numbers of array
        else
            $Sum += $arr[$j];
    }
    // If Sum is divisible by the
    // chosen element
    if ($Sum % $arr[$i] == 0)
        $count += 1;
}
// Return the count
    return $count;
}
// Driver code
$arr = array(3, 10, 4, 6, 7);
$n = count($arr);
echo countNum($n, $arr);

// This code is contributed
// by Srathore
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count
    // of the required numbers
    function countNum(N, arr)
    {
        // To store the count of required numbers
        let count = 0;
        for (let i = 0; i < N; i++) {

            // Initialize sum to 0
            let sum = 0;
            for (let j = 0; j < N; j++) {

                // If current element and the
                // chosen element are same
                if (i == j)
                    continue;

                // Add all other numbers of array
                else
                    sum += arr[j];
            }

            // If sum is divisible by the chosen element
            if (sum % arr[i] == 0)
                count++;
        }

        // Return the count
        return count;
    }

    let arr = [ 3, 10, 4, 6, 7 ];
    let n = arr.length;
    document.write(countNum(n, arr));

    // This code is contributed by vaibhavrabadiya117
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N <sup>2</sup> )

**高效方法:**运行从 0 到 N 的单个循环，计算所有元素的总和。现在运行另一个从 0 到 N 的循环，如果**(sum–arr[I])% arr[I]= 0**，则递增计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count
// of the required numbers
int countNum(int N, int arr[])
{
    // Initialize sum and count to 0
    int sum = 0, count = 0;

    // Calculate sum of all
    // the array elements
    for (int i = 0; i < N; i++)
        sum += arr[i];

    for (int i = 0; i < N; i++)

        // If current element satisfies the condition
        if ((sum - arr[i]) % arr[i] == 0)
            count++;

    // Return the count of required elements
    return count;
}

// Driver code
int main()
{
    int arr[] = { 3, 10, 4, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countNum(n, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to return the count
    // of the required numbers
    static int countNum(int N, int arr[])
    {
        // Initialize sum and count to 0
        int sum = 0, count = 0;

        // Calculate sum of all
        // the array elements
        for (int i = 0; i < N; i++)
        {
            sum += arr[i];
        }

        // If current element satisfies the condition
        for (int i = 0; i < N; i++)
        {
            if ((sum - arr[i]) % arr[i] == 0)
            {
                count++;
            }
        }

        // Return the count of required elements
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {3, 10, 4, 6, 7};
        int n = arr.length;
        System.out.println(countNum(n, arr));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of the required numbers
def countNum(N, arr):

    # Initialize Sum and count to 0
    Sum, count = 0, 0

    # Calculate Sum of all the
    # array elements
    for i in range(N):
        Sum += arr[i]

    for i in range(N):

        # If current element satisfies
        # the condition
        if ((Sum - arr[i]) % arr[i] == 0):
            count += 1

    # Return the count of required
    # elements
    return count

# Driver code
arr = [ 3, 10, 4, 6, 7 ]
n = len(arr)
print(countNum(n, arr))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of the required numbers
    static int countNum(int N, int []arr)
    {
        // Initialize sum and count to 0
        int sum = 0, count = 0;

        // Calculate sum of all
        // the array elements
        for (int i = 0; i < N; i++)
        {
            sum += arr[i];
        }

        // If current element satisfies the condition
        for (int i = 0; i < N; i++)
        {
            if ((sum - arr[i]) % arr[i] == 0)
            {
                count++;
            }
        }

        // Return the count of required elements
        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {3, 10, 4, 6, 7};
        int n = arr.Length;
        Console.WriteLine(countNum(n, arr));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of the required numbers
function countNum($N, $arr)
{
    // Initialize sum and count to 0
    $sum = 0; $count = 0;

    // Calculate sum of all
    // the array elements
    for ($i = 0; $i < $N; $i++)
        $sum += $arr[$i];

    for ($i = 0; $i < $N; $i++)

        // If current element satisfies
        // the condition
        if (($sum - $arr[$i]) % $arr[$i] == 0)
            $count++;

    // Return the count of required elements
    return $count;
}

// Driver code
$arr = array(3, 10, 4, 6, 7);
$n = count($arr);
echo countNum($n, $arr);

// This code contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>   
    // Javascript implementation of the approach

    // Function to return the count
    // of the required numbers
    function countNum(N, arr)
    {
        // Initialize sum and count to 0
        let sum = 0, count = 0;

        // Calculate sum of all
        // the array elements
        for (let i = 0; i < N; i++)
        {
            sum += arr[i];
        }

        // If current element satisfies the condition
        for (let i = 0; i < N; i++)
        {
            if ((sum - arr[i]) % arr[i] == 0)
            {
                count++;
            }
        }

        // Return the count of required elements
        return count;
    }

    let arr = [3, 10, 4, 6, 7];
    let n = arr.length;
    document.write(countNum(n, arr));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)