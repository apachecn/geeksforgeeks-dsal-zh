# 求距离 2 的两个连续幂等距离的所有数组元素的和

> 原文:[https://www . geeksforgeeks . org/find-所有数组元素的和与两个连续的 2 的幂等距/](https://www.geeksforgeeks.org/find-the-sum-of-all-array-elements-that-are-equidistant-from-two-consecutive-powers-of-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出与[两个连续 2 的幂](https://www.geeksforgeeks.org/check-number-can-expressed-sum-consecutive-numbers/)等距的数组元素[的和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {10，24，17，3，8}
> **输出:** 27
> **解释:**
> 以下数组元素与 2 的两个连续幂等距:
> 
> 1.  arr[1] (= 24)与 2 <sup>4</sup> 和 2 <sup>5</sup> 相等。
> 2.  arr[3] (= 3)与 2 <sup>1</sup> 和 2 <sup>2</sup> 相等。
> 
> 因此，24 和 3 的和是 27。
> 
> **输入:** arr[] = {17，5，6，35 }
> T3】输出: 6

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **res** ，它存储数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   找到 **log <sub>2</sub> (arr[i])** 的值并存储在变量中，比如 **power** 。
    *   找到 **2 <sup>(功率)</sup>** 和 **2 <sup>(功率+ 1)</sup>** 的值，并存储在变量中，分别说**leservalue**和 **LargerValue** 。
    *   如果**(arr[I]–减小值)**的值等于**(大值–arr[I])**，那么将 **res** 的值增加 **arr[i]** 。
*   完成上述步骤后，打印 **res** 的值作为结果总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the sum of array
// elements that are equidistant from
// two consecutive powers of 2
int FindSum(int arr[], int N)
{
    // Stores the resultant sum of the
    // array elements
    int res = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Stores the power of 2 of the
        // number arr[i]
        int power = log2(arr[i]);

        // Stores the number which is
        // power of 2 and lesser than
        // or equal to arr[i]
        int LesserValue = pow(2, power);

        // Stores the number which is
        // power of 2 and greater than
        // or equal to arr[i]
        int LargerValue = pow(2, power + 1);

        // If arr[i] - LesserValue is the
        // same as LargerValue-arr[i]
        if ((arr[i] - LesserValue)
            == (LargerValue - arr[i])) {

            // Increment res by arr[i]
            res += arr[i];
        }
    }

    // Return the resultant sum res
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 10, 24, 17, 3, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << FindSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to print the sum of array
    // elements that are equidistant from
    // two consecutive powers of 2
    static int FindSum(int[] arr, int N)
    {
        // Stores the resultant sum of the
        // array elements
        int res = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Stores the power of 2 of the
            // number arr[i]
            int power
                = (int)(Math.log(arr[i]) / Math.log(2));

            // Stores the number which is
            // power of 2 and lesser than
            // or equal to arr[i]
            int LesserValue = (int)Math.pow(2, power);

            // Stores the number which is
            // power of 2 and greater than
            // or equal to arr[i]
            int LargerValue = (int)Math.pow(2, power + 1);

            // If arr[i] - LesserValue is the
            // same as LargerValue-arr[i]
            if ((arr[i] - LesserValue)
                == (LargerValue - arr[i])) {

                // Increment res by arr[i]
                res += arr[i];
            }
        }

        // Return the resultant sum res
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 10, 24, 17, 3, 8 };
        int N = arr.length;
        System.out.println(FindSum(arr, N));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2

# Function to print sum of array
# elements that are equidistant from
# two consecutive powers of 2
def FindSum(arr, N):

    # Stores the resultant sum of the
    # array elements
    res = 0

    # Traverse the array arr[]
    for i in range(N):

        # Stores the power of 2 of the
        # number arr[i]
        power = int(log2(arr[i]))

        # Stores the number which is
        # power of 2 and lesser than
        # or equal to arr[i]
        LesserValue = pow(2, power)

        # Stores the number which is
        # power of 2 and greater than
        # or equal to arr[i]
        LargerValue = pow(2, power + 1)

        # If arr[i] - LesserValue is the
        # same as LargerValue-arr[i]
        if ((arr[i] - LesserValue) ==
            (LargerValue - arr[i])):

            # Increment res by arr[i]
            res += arr[i]

    # Return the resultant sum res
    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 10, 24, 17, 3, 8 ]
    N = len(arr)

    print (FindSum(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print the sum of array
// elements that are equidistant from
// two consecutive powers of 2
static int FindSum(int[] arr, int N)
{
    // Stores the resultant sum of the
    // array elements
    int res = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Stores the power of 2 of the
        // number arr[i]
        int power = (int)(Math.Log(arr[i]) / Math.Log(2));

        // Stores the number which is
        // power of 2 and lesser than
        // or equal to arr[i]
        int LesserValue = (int)Math.Pow(2, power);

        // Stores the number which is
        // power of 2 and greater than
        // or equal to arr[i]
        int LargerValue = (int)Math.Pow(2, power + 1);

        // If arr[i] - LesserValue is the
        // same as LargerValue-arr[i]
        if ((arr[i] - LesserValue)
            == (LargerValue - arr[i])) {

            // Increment res by arr[i]
            res += arr[i];
        }
    }

    // Return the resultant sum res
    return res;
}

// Driver Code
public static void Main()
{
   int[] arr= { 10, 24, 17, 3, 8 };
    int N = arr.Length;
     Console.WriteLine(FindSum(arr, N));

}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the sum of array
// elements that are equidistant from
// two consecutive powers of 2
function FindSum(arr, N)
{

    // Stores the resultant sum of
    // the array elements
    let res = 0;

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // Stores the power of 2 of the
        // number arr[i]
        let power = Math.floor(
            Math.log2(arr[i]));

        // Stores the number which is
        // power of 2 and lesser than
        // or equal to arr[i]
        let LesserValue = Math.pow(2, power);

        // Stores the number which is
        // power of 2 and greater than
        // or equal to arr[i]
        let LargerValue = Math.pow(2, power + 1);

        // If arr[i] - LesserValue is the
        // same as LargerValue-arr[i]
        if ((arr[i] - LesserValue) ==
            (LargerValue - arr[i]))
        {

            // Increment res by arr[i]
            res += arr[i];
        }
    }

    // Return the resultant sum res
    return res;
}

// Driver Code
let arr = [ 10, 24, 17, 3, 8 ];
let N = arr.length;

document.write(FindSum(arr, N));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
27
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)