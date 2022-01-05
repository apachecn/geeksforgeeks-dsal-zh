# 检查给定的整数 a、b、c、d 是否成比例

> 原文:[https://www . geesforgeks . org/check-给定整数-a-b-c-d 是否成比例/](https://www.geeksforgeeks.org/check-whether-the-given-integers-a-b-c-and-d-are-in-proportion/)

给定四个整数 **a** 、 **b** 、 **c** 和 **d** 。任务是检查是否有可能将它们配对，使它们成比例。我们可以打乱数字的顺序。
**举例:**

> **输入:** arr[] = {1，2，4，2}
> **输出:**是
> 1 / 2 = 2 / 4
> **输入:** arr[] = {1，2，5，2}
> **输出:**否

**方法:**如果四个数字 **a、b、c、d** 成比例，那么 **a:b = c:d** 。解决方案是将四个数字排序，将前两个数字和后两个数字配对，并检查它们的比率。这是因为，为了使它们成比例，平均值的乘积必须等于极值的乘积。所以， **a * d** 必须等于 **c * b** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the
// given four integers are in proportion
bool inProportion(int arr[])
{

    // Array will consist of
    // only four integers
    int n = 4;

    // Sort the array
    sort(arr, arr + n);

    // Find the product of extremes and means
    long extremes = (long)arr[0] * (long)arr[3];
    long means = (long)arr[1] * (long)arr[2];

    // If the products are equal
    if (extremes == means)
        return true;
    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 2 };

    if (inProportion(arr))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if the
// given four integers are in proportion
static boolean inProportion(int []arr)
{

    // Array will consist of
    // only four integers
    int n = 4;

    // Sort the array
    Arrays.sort(arr);

    // Find the product of extremes and means
    long extremes = (long)arr[0] * (long)arr[3];
    long means = (long)arr[1] * (long)arr[2];

    // If the products are equal
    if (extremes == means)
        return true;
    return false;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 4, 2 };

    if (inProportion(arr))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the
# given four integers are in proportion
def inProportion(arr) :

    # Array will consist of
    # only four integers
    n = 4;

    # Sort the array
    arr.sort()

    # Find the product of extremes and means
    extremes = arr[0] * arr[3];
    means = arr[1] * arr[2];

    # If the products are equal
    if (extremes == means) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 4, 2 ];

    if (inProportion(arr)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if the
// given four integers are in proportion
static bool inProportion(int []arr)
{

    // Array will consist of
    // only four integers
    int n = 4;

    // Sort the array
    Array.Sort(arr);

    // Find the product of extremes and means
    long extremes = (long)arr[0] * (long)arr[3];
    long means = (long)arr[1] * (long)arr[2];

    // If the products are equal
    if (extremes == means)
        return true;
    return false;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 4, 2 };

    if (inProportion(arr))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if the
// given four integers are in proportion
function inProportion(arr)
{

    // Array will consist of
    // only four integers
    var n = 4;

    // Sort the array
    arr.sort();

    // Find the product of extremes and means
    var extremes = arr[0] * arr[3];
    var means = arr[1] * arr[2];

    // If the products are equal
    if (extremes == means)
        return true;
    return false;
}

// Driver code
var arr = [ 1, 2, 4, 2 ]
if (inProportion(arr))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(1)