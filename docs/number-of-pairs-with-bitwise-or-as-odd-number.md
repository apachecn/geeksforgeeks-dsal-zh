# 按位“或”为奇数的对的数量

> 原文:[https://www . geesforgeks . org/按位或奇数对数/](https://www.geeksforgeeks.org/number-of-pairs-with-bitwise-or-as-odd-number/)

给定一个大小为 n 的数组 A[]，任务是找出存在多少对(I，j)，使得 A[i]或 A[j]为奇数。
**例** :

```
Input : N = 4
            A[] = { 5, 6, 2, 8 }
Output : 3
Explanation :
Since pair of A[] = ( 5, 6 ), ( 5, 2 ), ( 5, 8 ),
( 6, 2 ), ( 6, 8 ), ( 2, 8 )
5 OR 6 = 7, 5 OR 2 = 7, 5 OR 8 = 13
6 OR 2 = 6, 6 OR 8 = 14, 2 OR 8 = 10
Total pair A( i, j ) = 6 and Odd = 3

Input : N = 7
            A[] = {8, 6, 2, 7, 3, 4, 9}
Output :15
```

一个**简单的解决方案**是检查每一对并找到按位或，然后用按位或计数所有这样的对为奇数。
以下是上述办法的实施情况:

## C++

```
// C++ program to count pairs with odd OR

#include <iostream>
using namespace std;

// Function to count pairs with odd OR
int findOddPair(int A[], int N)
{
    int oddPair = 0;
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N; j++) {

            // find OR operation
            // check odd or odd
            if ((A[i] | A[j]) % 2 != 0)
                oddPair++;
        }
    }

    // return count of odd pair
    return oddPair;
}

// Driver Code
int main()
{
    int A[] = { 5, 6, 2, 8 };

    int N = sizeof(A) / sizeof(A[0]);

    cout << findOddPair(A, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs
// with odd OR
class GFG
{
// Function to count pairs with odd OR
static int findOddPair(int A[], int N)
{
    int oddPair = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {

            // find OR operation
            // check odd or odd
            if ((A[i] | A[j]) % 2 != 0)
                oddPair++;
        }
    }

    // return count of odd pair
    return oddPair;
}

// Driver Code
public static void main(String []args)
{
    int A[] = { 5, 6, 2, 8 };

    int N = A.length;

    System.out.println(findOddPair(A, N));
}
}

// This code is contributed by ANKITRAI1
```

## 蟒蛇 3

```

# Python3 program to count pairs with odd OR

# Function to count pairs with odd OR
def findOddPair(A, N):

    oddPair = 0
    for i in range(0, N):
        for j in range(i+1, N):

            # find OR operation
            # check odd or odd
            if ((A[i] | A[j]) % 2 != 0):
                oddPair+=1

    # return count of odd pair
    return oddPair

# Driver Code
def main():

    A = [ 5, 6, 2, 8 ]

    N = len(A)

    print(findOddPair(A, N))

if __name__ == '__main__':
    main()
# This code is contributed by PrinciRaj1992 
```

## C#

```
// C#  program to count pairs
// with odd OR

using System;

public class GFG{

    // Function to count pairs with odd OR
static int findOddPair(int[] A, int N)
{
    int oddPair = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {

            // find OR operation
            // check odd or odd
            if ((A[i] | A[j]) % 2 != 0)
                oddPair++;
        }
    }

    // return count of odd pair
    return oddPair;
}

// Driver Code
    static public void Main (){
    int []A = { 5, 6, 2, 8 };
    int N = A.Length;

    Console.WriteLine(findOddPair(A, N));
    }
}

//This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to count pairs with odd OR

// Function to count pairs with odd OR
function  findOddPair($A, $N)
{
    $oddPair = 0;
    for ($i = 0; $i < $N; $i++) {
        for ($j = $i + 1; $j < $N; $j++) {

            // find OR operation
            // check odd or odd
            if (($A[$i] | $A[$j]) % 2 != 0)
                $oddPair++;
        }
    }

    // return count of odd pair
    return $oddPair;
}

// Driver Code
    $A = array (5, 6, 2, 8 );
    $N = sizeof($A) / sizeof($A[0]);

    echo findOddPair($A, $N),"\n";

#This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to count pairs with odd OR

// Function to count pairs with odd OR
function findOddPair(A, N)
{
    let oddPair = 0;
    for (let i = 0; i < N; i++)
    {
        for (let j = i + 1; j < N; j++)
        {

            // find OR operation
            // check odd or odd
            if ((A[i] | A[j]) % 2 != 0)
                oddPair++;
        }
    }

    // return count of odd pair
    return oddPair;
}

// Driver Code
let A = [ 5, 6, 2, 8 ];
let N = A.length;
document.write(findOddPair(A, N));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
3
```