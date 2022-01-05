# 与给定数组异或和为给定数 k 的数

> 原文:[https://www . geesforgeks . org/number-what-xor-sum-given-array-given-number-k/](https://www.geeksforgeeks.org/number-whose-xor-sum-given-array-given-number-k/)

给定一个由 N 个数字和 k 个数字组成的数组。任务是在给定的数组中插入一个数字，使新数组中所有元素的按位异或等于给定的输入 k。
**示例:**

```
Input:
a = {1, 2, 3, 4, 5}, k = 10
Output: 11 
Explanation: 1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 11 = 10

Input: A[] = { 12, 23, 34, 56, 78 }, k = 6
Output: 73 
```

**方法:**基本思想是使用简单的 XOR 属性，即如果 X ^ Y = Z，那么 X ^ Z = Y。让我们假设要插入数组中的数字是 x，使得(a[0]^ a[1]^…^ a[n–1])^ x = k。因此，要找到 x，我们可以使用关系(a[0]^ a[1]^…a[n–1])k = x。下面的
是上述方法的实现。

## C++

```
// CPP Program to find the number
// whose XOR sum with given array is
// equal to a given number k
#include <bits/stdc++.h>
using namespace std;

// This function returns the number to
// be inserted in the given array
int findEletobeInserted(int A[], int n, int k)
{
    // initialise the answer with k
    int ans = k;
    for (int i = 0; i < n; i++)
        ans ^= A[i]; // XOR of all elements in the array
    return ans;
}

// Driver Code to test above function
int main()
{
    int A[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(A) / sizeof(A[0]);
    int k = 10;

    cout << findEletobeInserted(A, n, k)
         << " has to be inserted"
         " in the given array to make xor sum of "
         << k << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the number
// whose XOR sum with given array is
// equal to a given number k
import java.io.*;

class GFG {

    // This function returns the number to
    // be inserted in the given array
    static int findEletobeInserted(int A[],
                              int n, int k)
    {

        // initialise the answer with k
        int ans = k;
        for (int i = 0; i < n; i++)

            // XOR of all elements in
            // the array
            ans ^= A[i];
        return ans;
    }

    // Driver Code to test above function
    public static void main (String[] args)
    {
        int A[] = { 1, 2, 3, 4, 5 };
        int n =A.length;
        int k = 10;

        System.out.println(
             findEletobeInserted(A, n, k)
              + " has to be inserted in "
              + "the given array to make"
                   + " xor sum of " + k);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 Program to find the number
# whose XOR sum with given array is
# equal to a given number k

# This function returns the number to
# be inserted in the given array
def findEletobeInserted(A, n, k):

    # initialise the answer with k
    ans = k
    for i in range(n):
        ans ^= A[i] # XOR of all elements
                    # in the array
    return ans

# Driver Code
if __name__ == '__main__':
    A = [1, 2, 3, 4, 5]
    n = len(A)
    k = 10

    print(findEletobeInserted(A, n, k),
          "has to be inserted in the given",
          "array to make xor sum of", k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to find the number
// whose XOR sum with given array is
// equal to a given number k
using System ;

class GFG {

    // This function returns the number to
    // be inserted in the given array
    static int findEletobeInserted(int []A,
                            int n, int k)
    {

        // initialise the answer with k
        int ans = k;
        for (int i = 0; i < n; i++)

            // XOR of all elements in
            // the array
            ans ^= A[i];
        return ans;
    }

    // Driver Code to test above function
    public static void Main ()
    {
        int []A = { 1, 2, 3, 4, 5 };
        int n =A.Length;
        int k = 10;

        Console.WriteLine(
            findEletobeInserted(A, n, k)
            + " has to be inserted in "
            + "the given array to make"
                + " xor sum of " + k);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the number
// whose XOR sum with given array is
// equal to a given number k

// This function returns the number to
// be inserted in the given array
function findEletobeInserted($A, $n, $k)
{
    // initialise the answer with k
    $ans = $k;
    for ( $i = 0; $i < $n; $i++)

        // XOR of all elements
        // in the array
        $ans ^= $A[$i];
    return $ans;
}

    // Driver Code
    $A = array(1, 2, 3, 4, 5);
    $n = count($A);
    $k = 10;

    echo findEletobeInserted($A, $n, $k) ;
    echo " has to be inserted";
    echo " in the given array to make xor sum of ";
    echo $k , "\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the number
// whose XOR sum with given array is
// equal to a given number k

// This function returns the number to
// be inserted in the given array
function findEletobeInserted(A, n, k)
{

    // initialise the answer with k
    var ans = k;
    for(var i = 0; i < n; i++)

        // XOR of all elements in
        // the array
        ans ^= A[i];

    return ans;
}
// Driver Code
var A = [ 1, 2, 3, 4, 5 ];
var n = A.length;
var k = 10;

document.write(findEletobeInserted(A, n, k) +
               " has to be inserted in " +
               "the given array to make" +
               " xor sum of " + k);

// This code is contributed by Khushboogoyal499

</script>
```

**输出:**

```
11 has to be inserted in the given array to make xor sum of 10
```