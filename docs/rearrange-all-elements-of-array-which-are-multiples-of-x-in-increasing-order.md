# 按递增顺序重新排列数组中 x 的倍数的所有元素

> 原文:[https://www . geeksforgeeks . org/rearray-数组的所有元素都是 x 的倍数，以递增的顺序排列/](https://www.geeksforgeeks.org/rearrange-all-elements-of-array-which-are-multiples-of-x-in-increasing-order/)

给定一个整数数组“arr”和一个数字 x，任务是按照相对位置升序对数组中 x 的倍数的所有元素进行排序，即其他元素的其他位置不得受到影响。

**示例**:

> 输入:arr[] = {10，5，8，2，15}，x = 5
> 输出:5 10 8 2 15
> 我们按照递增的顺序重新排列所有 5 的倍数，保持其他元素不变。
> 
> 输入:arr[] = {100，12，25，50，5}，x = 5
> 输出:5 12 25 50 100

**进场:**

1.  遍历数组并检查该数是否是 x 的倍数。如果是，将其存储在向量中。
2.  然后，按升序对向量进行排序。
3.  再次遍历数组，用向量元素逐个替换 5 的倍数的元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort all the
// multiples of x from the
// array in ascending order
void sortMultiples(int arr[], int n, int x)
{
    vector<int> v;

    // Insert all multiples of 5 to a vector
    for (int i = 0; i < n; i++)
        if (arr[i] % x == 0)
            v.push_back(arr[i]);

    // Sort the vector
    sort(v.begin(), v.end());

    int j = 0;

    // update the array elements
    for (int i = 0; i < n; i++) {
        if (arr[i] % x == 0)
            arr[i] = v[j++];
    }
}

// Driver code
int main()
{
    int arr[] = { 125, 3, 15, 6, 100, 5 };
    int x = 5; 
    int n = sizeof(arr) / sizeof(arr[0]);

    sortMultiples(arr, n, x);

    // Print the result
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Collections;
import java.util.Vector;

// Java implementation of the approach
class GFG {

// Function to sort all the
// multiples of x from the
// array in ascending order
    static void sortMultiples(int arr[], int n, int x) {
        Vector<Integer> v = new Vector<Integer>();

        // Insert all multiples of 5 to a vector
        for (int i = 0; i < n; i++) {
            if (arr[i] % x == 0) {
                v.add(arr[i]);
            }
        }

        // Sort the vector
        Collections.sort(v);
        //sort(v.begin(), v.end());

        int j = 0;

        // update the array elements
        for (int i = 0; i < n; i++) {
            if (arr[i] % x == 0) {
                arr[i] = v.get(j++);
            }
        }
    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {125, 3, 15, 6, 100, 5};
        int x = 5;
        int n = arr.length;

        sortMultiples(arr, n, x);

        // Print the result
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i]+" ");
        }
    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to sort all the multiples of x
# from the array in ascending order
def sortMultiples(arr, n, x):
    v = []

    # Insert all multiples of 5 to a vector
    for i in range(0, n, 1):
        if (arr[i] % x == 0):
            v.append(arr[i])

    # Sort the vector
    v.sort(reverse=False)

    j = 0

    # update the array elements
    for i in range(0, n, 1):
        if (arr[i] % x == 0):
            arr[i] = v[j]
            j += 1

# Driver code
if __name__ == '__main__':
    arr = [ 125, 3, 15, 6, 100, 5]
    x = 5
    n = len(arr)

    sortMultiples(arr, n, x)

    # Print the result
    for i in range(0, n, 1):
        print(arr[i], end = " ")

# This code is contributed by
# Surendra _Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    // Function to sort all the
    // multiples of x from the
    // array in ascending order
    static void sortMultiples(int []arr,
                            int n, int x)
    {
        List<int> v = new List<int>();
        int i;

        // Insert all multiples of 5 to a vector
        for (i = 0; i < n; i++)
        if (arr[i] % x == 0)
            v.Add(arr[i]);

        // Sort the vector
        v.Sort();
        int j = 0;

        // update the array elements
        for (i = 0; i < n; i++)
        {
            if (arr[i] % x == 0)
                arr[i] = v[j++];
        }
    }

    // Driver code
    public static void Main()
    {
        int []arr = {125, 3, 15, 6, 100, 5};
        int x = 5;
        int n = arr.Length;
        sortMultiples(arr, n, x);

        // Print the result
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code is contributed by
// Shivi_Aggarwal
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to sort all the
// multiples of x from the
// array in ascending order
function sortMultiples(arr, n, x)
{
    var v = [];

    // Insert all multiples of 5 to a vector
    for(var i = 0; i < n; i++)
    {
        if (arr[i] % x == 0)
        {
            v.push(arr[i]);
        }
    }

    // Sort the vector
    v.sort((a, b) => a - b);

    var j = 0;

    // update the array elements
    for(var i = 0; i < n; i++)
    {
        if (arr[i] % x == 0)
            arr[i] = v[j++];
    }
}

// Driver code
var arr = [ 125, 3, 15, 6, 100, 5 ];
var x = 5;
var n = arr.length;

sortMultiples(arr, n, x);

// Print the result
for(var i = 0; i < n; i++)
{
    document.write(arr[i] + "  ");
}

// This code is contributed by rdtank

</script>
```

**Output:** 

```
5 3 15 6 100 125
```