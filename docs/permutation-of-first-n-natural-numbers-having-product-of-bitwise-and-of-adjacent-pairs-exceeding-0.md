# 相邻对的位与乘积超过 0 的前 N 个自然数的排列

> 原文:[https://www . geeksforgeeks . org/第一个 n 个自然数的排列-相邻对的位积超过-0/](https://www.geeksforgeeks.org/permutation-of-first-n-natural-numbers-having-product-of-bitwise-and-of-adjacent-pairs-exceeding-0/)

给定一个正整数 **N** ，任务是找到第一个 **N** 自然数的排列，使得相邻元素对的[位 AND( **&** )](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 的乘积大于 **0** 。如果没有找到这样的排列，则打印**“不可能”**。

**示例:**

> **输入:** N = 3
> **输出:** 1 3 2
> **解释:**
> 1&3 = 1
> 3&2 = 2
> 相邻元素按位 AND 的乘积= 1 * 2 = 2( > 0)
> 因此，所需的输出为 1 3 2
> 
> **输入:** 2
> **输出:**不可能
> **说明:**
> 前 N(= 2)个自然数的可能排列为:{ { 1，2 }、{ 2，1 } }
> 1&2 = 0
> 2&1 = 0
> 因此，要求的输出是不可能的。

**天真方法:**解决这个问题最简单的方法是[生成前 N 个自然数](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)的所有可能排列。对于每个排列，检查其相邻元素的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的乘积是否大于 **0** 。如果发现是真的，那么打印那个排列。否则，打印**“不可能”**。

***时间复杂度:** O(N * N！)*
***辅助空间:** O(1)*

**有效方法:**可以根据以下观察结果解决问题:

> 如果 [N 是 2 的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，那么 N 与任何小于 N 的数的按位“与”必须是 0。
> 
> 如果相邻元素的按位“与”等于 0，则相邻元素的按位“与”的乘积必须为 0。

按照以下步骤解决问题:

*   如果 [**N** 是**2**T5 的幂，那么打印**“不可能”**。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)
*   初始化一个数组，比如说， **arr[]** 来存储满足给定条件的第一个 **N** 个自然数的排列。
*   迭代范围**【1，N】**，更新**arr【I】= I**
*   更新数组的前三个元素，使其相邻元素的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)必须大于 **0** ，即 **arr[1] = 2** 、 **arr[2] = 3** 和 **arr[3] = 1**
*   迭代范围**【4，N】**。对于每个**I<sup>th</sup>T5】值，检查 **i** 是否为 **2** 的幂。如果发现为真，则**交换(arr[i]，arr[i+1])** 。**
*   最后，打印 **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is a power of 2 or not
bool isPowerOfTwo(int n)
{
    if (n == 0)
        return false;

    return (ceil(log2(n))
            == floor(log2(n)));
}

// Function to find the permutation of first N
// natural numbers such that the product of
// bitwise AND  of adjacent elements is > 0
void findThePermutation(int N)
{

    // Base Case, If N = 1, print 1
    if (N == 1) {
        cout << "1";
        return;
    }

    // If N is a power of 2,
    // print "Not Possible"
    if (isPowerOfTwo(N)) {
        cout << "Not Possible";
        return;
    }

    // Stores permutation of first N
    // natural numbers that satisfy
    // the condition
    int arr[N + 1];

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Update arr[i]
        arr[i] = i;
    }

    // Update arr[1], arr[2] and arr[3]
    arr[1] = 2, arr[2] = 3, arr[3] = 1;

    // Iterate over the range [4, N]
    for (int i = 4; i <= N; i++) {

        // If i is a power of 2
        if (isPowerOfTwo(i)) {

            // Swap adjacent elements
            swap(arr[i], arr[i + 1]);

            // Update i
            i++;
        }
    }

    // Print the array
    for (int i = 1; i <= N; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    // Input
    int N = 5;

    // Function Call
    findThePermutation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
class GFG
{

    // Function to calculate the
    // log base 2 of an integer
    public static int log2(int N)
    {

        // calculate log2 N indirectly
        // using log() method
        int result = (int)(Math.log(N) / Math.log(2));  
        return result;
    }

    // Function to check if a number
    // is a power of 2 or not
    static boolean isPowerOfTwo(int n)
    {
        if (n == 0)
            return false;   
        return Math.ceil(log2(n)) == Math.floor(log2(n));
    }

    // Function to find the permutation of first N
    // natural numbers such that the product of
    // bitwise AND  of adjacent elements is > 0
    static void findThePermutation(int N)
    {

        // Base Case, If N = 1, print 1
        if (N == 1)
        {
            System.out.print("1");
            return;
        }

        // If N is a power of 2,
        // print "Not Possible"
        if (isPowerOfTwo(N) == false)
        {
            System.out.print("Not Possible");
            return;
        }

        // Stores permutation of first N
        // natural numbers that satisfy
        // the condition
        int arr[] = new int[N + 1];

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++)
        {

            // Update arr[i]
            arr[i] = i;
        }

        // Update arr[1], arr[2] and arr[3]
        arr[1] = 2; arr[2] = 3; arr[3] = 1;  
        int temp;

        // Iterate over the range [4, N]
        for (int i = 4; i <= N; i++)
        {

            // If i is a power of 2
            if (isPowerOfTwo(i) == true)
            {

                // Swap adjacent elements
                temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp ;

                // Update i
                i++;
            }
        }

        // Print the array
        for (int i = 1; i <= N; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input
        int N = 5;

        // Function Call
        findThePermutation(N);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import ceil, floor, log2

# Function to check if a number
# is a power of 2 or not
def isPowerOfTwo(n):

    if (n == 0):
        return False

    return (ceil(log2(n)) == floor(log2(n)))

# Function to find the permutation of first N
# natural numbers such that the product of
# bitwise AND of adjacent elements is > 0
def findThePermutation(N):

    # Base Case, If N = 1, pr1
    if (N == 1):
        print("1")
        return

    # If N is a power of 2,
    # print "Not Possible"
    if (isPowerOfTwo(N)):
        print("Not Possible")
        return

    # Stores permutation of first N
    # natural numbers that satisfy
    # the condition
    arr = [i for i in range(N + 1)]

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Update arr[i]
        arr[i] = i

    # Update arr[1], arr[2] and arr[3]
    arr[1], arr[2], arr[3] = 2, 3, 1

    # Iterate over the range [4, N]
    for i in range(4, N + 1):

        # If i is a power of 2
        if (isPowerOfTwo(i)):

            # Swap adjacent elements
            arr[i], arr[i + 1] = arr[i + 1], arr[i]

            # Update i
            i += 1

    # Print the array
    for i in range(1, N + 1):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Input
    N = 5

    # Function Call
    findThePermutation(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement the above approach
using System;
class GFG
{

    // Function to calculate the
    // log base 2 of an integer
    public static int log2(int N)
    {

        // calculate log2 N indirectly
        // using log() method
        int result = (int)(Math.Log(N) / Math.Log(2));  
        return result;
    }

    // Function to check if a number
    // is a power of 2 or not
    static bool isPowerOfTwo(int n)
    {
        if (n == 0)
            return false;   
        return Math.Ceiling((double)log2(n)) ==
          Math.Floor((double)log2(n));
    }

    // Function to find the permutation of first N
    // natural numbers such that the product of
    // bitwise AND  of adjacent elements is > 0
    static void findThePermutation(int N)
    {

        // Base Case, If N = 1, print 1
        if (N == 1)
        {
            Console.Write("1");
            return;
        }

        // If N is a power of 2,
        // print "Not Possible"
        if (isPowerOfTwo(N) == false)
        {
            Console.Write("Not Possible");
            return;
        }

        // Stores permutation of first N
        // natural numbers that satisfy
        // the condition
        int []arr = new int[N + 1];

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++)
        {

            // Update arr[i]
            arr[i] = i;
        }

        // Update arr[1], arr[2] and arr[3]
        arr[1] = 2; arr[2] = 3; arr[3] = 1;  
        int temp;

        // Iterate over the range [4, N]
        for (int i = 4; i <= N; i++)
        {

            // If i is a power of 2
            if (isPowerOfTwo(i) == true)
            {

                // Swap adjacent elements
                temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp ;

                // Update i
                i++;
            }
        }

        // Print the array
        for (int i = 1; i <= N; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Input
        int N = 5;

        // Function Call
        findThePermutation(N);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach   

   // Function to calculate the
  // log base 2 of an integer
    function log2(N) {

        // calculate log2 N indirectly
        // using log() method
        var result = parseInt( (Math.log(N) / Math.log(2)));
        return result;
    }

    // Function to check if a number
    // is a power of 2 or not
    function isPowerOfTwo(n) {
        if (n == 0)
            return false;
        return Math.ceil(log2(n)) == Math.floor(log2(n));
    }

    // Function to find the permutation of first N
    // natural numbers such that the product of
    // bitwise AND of adjacent elements is > 0
    function findThePermutation(N) {

        // Base Case, If N = 1, print 1
        if (N == 1) {
            document.write("1");
            return;
        }

        // If N is a power of 2,
        // print "Not Possible"
        if (isPowerOfTwo(N) == false) {
            document.write("Not Possible");
            return;
        }

        // Stores permutation of first N
        // natural numbers that satisfy
        // the condition
        var arr = Array(N + 1).fill(0);

        // Iterate over the range [1, N]
        for (i = 1; i <= N; i++) {

            // Update arr[i]
            arr[i] = i;
        }

        // Update arr[1], arr[2] and arr[3]
        arr[1] = 2;
        arr[2] = 3;
        arr[3] = 1;
        var temp;

        // Iterate over the range [4, N]
        for (i = 4; i <= N; i++) {

            // If i is a power of 2
            if (isPowerOfTwo(i) == true) {

                // Swap adjacent elements
                temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp;

                // Update i
                i++;
            }
        }

        // Print the array
        for (i = 1; i <= N; i++)
            document.write(arr[i] + " ");
    }

    // Driver Code

        // Input
        var N = 5;

        // Function Call
        findThePermutation(N);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
2 3 1 5 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)