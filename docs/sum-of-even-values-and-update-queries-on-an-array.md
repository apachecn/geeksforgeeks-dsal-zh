# 偶数值之和和对数组的更新查询

> 原文:[https://www . geeksforgeeks . org/偶数值和更新数组查询之和/](https://www.geeksforgeeks.org/sum-of-even-values-and-update-queries-on-an-array/)

给定整数数组 **arr[]** 和查询数组 **q[]** 。
对于 i <sup>第</sup>次查询，**索引= q[i][0]** 和**值= q[i][1]** 。任务是对于每个查询，更新 **arr[index] = arr[index] +值**，然后返回数组中所有偶数元素的总和。

**示例:**

> **输入:** arr[] = {1，2，3，4}，q[] = {{0，1}，{1，-3}，{0，-4}，{3，2 } }
> T3】输出: 8 6 2 4
> 一开始，数组是{1，2，3，4}。
> arr[0]加 1 后，数组变成{2，2，3，4}，偶数值之和为 2 + 2 + 4 = 8。
> 将-3 加到 arr[1]上，arr[] = {2，-1，3，4}，偶数值之和为 2 + 4 = 6。
> 将-4 加到 arr[0]上，arr[] = {-2，-1，3，4}偶数的和为-2 + 4 = 2。
> 在 arr[3]上加 2，arr[] = {-2，-1，3，6}偶数的和为-2 + 6 = 4。
> 
> **输入:** arr[] = {1，2，2，2}，q[] = {{0，1}，{1，1}}
> **输出:** 8 6

**天真方法:**对于每个查询，更新数组中的值，并计算数组中所有偶数值的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of even elements
// after updating value at given index
int EvenSum(vector<int>& A, int index, int value)
{
    // Add given value to A[index]
    A[index] = A[index] + value;

    // To store the sum of even elements
    int sum = 0;

    for (int i = 0; i < A.size(); i++)

        // If current element is even
        if (A[i] % 2 == 0)
            sum = sum + A[i];

    return sum;
}

// Function to print the result for every query
void BalanceArray(vector<int>& A, vector<vector<int> >& Q)
{

    // Resultant vector that stores
    // the result for every query
    vector<int> ANS;

    int i, sum;

    for (i = 0; i < Q.size(); i++) {

        int index = Q[i][0];
        int value = Q[i][1];

        // Get sum of even elements after updating
        // value at given index
        sum = EvenSum(A, index, value);

        // Store sum for each query
        ANS.push_back(sum);
    }

    // Print the result for every query
    for (i = 0; i < ANS.size(); i++)
        cout << ANS[i] << " ";
}

// Driver code
int main()
{
    vector<int> A = { 1, 2, 3, 4 };
    vector<vector<int> > Q = { { 0, 1 },
                               { 1, -3 },
                               { 0, -4 },
                               { 3, 2 } };
    BalanceArray(A, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to return the sum of even elements
    // after updating value at given index
    static int EvenSum(int [] A, int index, int value)
    {
        // Add given value to A[index]
        A[index] = A[index] + value;

        // To store the sum of even elements
        int sum = 0;

        for (int i = 0; i < A.length; i++)

            // If current element is even
            if (A[i] % 2 == 0)
                sum = sum + A[i];

        return sum;
    }

    // Function to print the result for every query
    static void BalanceArray(int [] A, int [][] Q)
    {

        // Resultant vector that stores
        // the result for every query
        int [] ANS = new int[Q.length];
        int i, sum;

        for (i = 0; i < Q.length; i++)
        {

            int index = Q[i][0];
            int value = Q[i][1];

            // Get sum of even elements after updating
            // value at given index
            sum = EvenSum(A, index, value);

            // Store sum for each query
            ANS[i] = sum;
        }

        // Print the result for every query
        for (i = 0; i < ANS.length; i++)
            System.out.print(ANS[i] + " ");
    }

    // Driver code
    public static void main(String []args)
    {
        int [] A = { 1, 2, 3, 4 };
        int [][] Q = { { 0, 1 },
                        { 1, -3 },
                        { 0, -4 },
                        { 3, 2 } };
        BalanceArray(A, Q);

    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of even elements
# after updating value at given index
def EvenSum(A, index, value):

    # Add given value to A[index]
    A[index] = A[index] + value

    # To store the sum of even elements
    sum = 0

    for i in A:

        # If current element is even
        if (i % 2 == 0):
            sum = sum + i

    return sum

# Function to print result for every query
def BalanceArray(A,Q):

    # Resultant vector that stores
    # the result for every query
    ANS = []

    i, sum = 0, 0

    for i in range(len(Q)):

        index = Q[i][0]
        value = Q[i][1]

        # Get sum of even elements after updating
        # value at given index
        sum = EvenSum(A, index, value)

        # Store sum for each query
        ANS.append(sum)

    # Print the result for every query
    for i in ANS:
        print(i, end = " ")

# Driver code
A = [1, 2, 3, 4]
Q = [ [0, 1 ],
    [1, -3],
    [0, -4],
    [3, 2 ] ]
BalanceArray(A, Q)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
public class GFG
{

  // Function to return the sum of even elements
  // after updating value at given index
  static int EvenSum(int[] A, int index, int value)
  {

    // Add given value to A[index]
    A[index] = A[index] + value;

    // To store the sum of even elements
    int sum = 0;

    for (int i = 0; i < A.Length; i++)

      // If current element is even
      if (A[i] % 2 == 0)
        sum = sum + A[i];

    return sum;
  }

  // Function to print the result for every query
  static void BalanceArray(int[] A, int[,] Q) {

    // Resultant vector that stores
    // the result for every query
    int[] ANS = new int[Q.GetLength(0)];
    int i, sum;

    for (i = 0; i < Q.GetLength(0); i++) {

      int index = Q[i,0];
      int value = Q[i,1];

      // Get sum of even elements after updating
      // value at given index
      sum = EvenSum(A, index, value);

      // Store sum for each query
      ANS[i] = sum;
    }

    // Print the result for every query
    for (i = 0; i < ANS.Length; i++)
      Console.Write(ANS[i] + " ");
  }

  // Driver code
  public static void Main(String[] args)
  {
    int[] A = { 1, 2, 3, 4 };
    int[,] Q = { { 0, 1 }, { 1, -3 }, { 0, -4 }, { 3, 2 } };
    BalanceArray(A, Q);
  }
}

// This code is contributed by Rajput-Ji.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the sum of even elements
// after updating value at given index
function EvenSum(A, index, value)
{
    // Add given value to A[index]
    A[index] = A[index] + value;

    // To store the sum of even elements
    var sum = 0;

    for (var i = 0; i < A.length; i++)

        // If current element is even
        if (A[i] % 2 == 0)
            sum = sum + A[i];

    return sum;
}

// Function to print the result for every query
function BalanceArray(A, Q)
{

    // Resultant vector that stores
    // the result for every query
    var ANS = [];

    var i, sum;

    for (i = 0; i < Q.length; i++) {

        var index = Q[i][0];
        var value = Q[i][1];

        // Get sum of even elements after updating
        // value at given index
        sum = EvenSum(A, index, value);

        // Store sum for each query
        ANS.push(sum);
    }

    // Print the result for every query
    for (i = 0; i < ANS.length; i++)
        document.write( ANS[i] + " ");
}

// Driver code
var A = [ 1, 2, 3, 4 ];
var Q = [ [ 0, 1 ],
          [ 1, -3 ],
          [ 0, -4 ],
          [ 3, 2 ] ];
BalanceArray(A, Q);

</script>
```

**Output:** 

```
8 6 2 4
```

**时间复杂度:** O(n <sup>2</sup>

**有效方法:**

*   计算 arr[]中的**偶数**值之和
*   现在，如果给定索引处 arr[]的值为偶数，即 arr[index] % 2 = 0，则从总和中减去 arr[index]。
*   将给定值加到 arr[index]上，即 arr[index] = arr[index] +值。
*   现在再次检查 arr[index]的值是否为偶数，如果是，则将 arr[index]加到总和中。
*   打印每个查询的 sum 值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the result for every query
void BalanceArray(vector<int>& A, vector<vector<int> >& Q)
{
    vector<int> ANS;

    int i, sum = 0;

    for (i = 0; i < A.size(); i++)

        // If current element is even
        if (A[i] % 2 == 0)
            sum = sum + A[i];

    for (i = 0; i < Q.size(); i++) {

        int index = Q[i][0];
        int value = Q[i][1];

        // If element is even then
        // remove it from sum
        if (A[index] % 2 == 0)
            sum = sum - A[index];

        A[index] = A[index] + value;

        // If the value becomes even after updating
        if (A[index] % 2 == 0)
            sum = sum + A[index];

        // Store sum for each query
        ANS.push_back(sum);
    }

    // Print the result for every query
    for (i = 0; i < ANS.size(); i++)
        cout << ANS[i] << " ";
}

// Driver code
int main()
{
    vector<int> A = { 1, 2, 3, 4 };
    vector<vector<int> > Q = { { 0, 1 },
                               { 1, -3 },
                               { 0, -4 },
                               { 3, 2 } };
    BalanceArray(A, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to print the result for every query
    static void BalanceArray(int [] A, int [][] Q)
    {
        int [] ANS = new int [A.length];

        int i, sum = 0;

        for (i = 0; i < A.length; i++)

            // If current element is even
            if (A[i] % 2 == 0)
                sum = sum + A[i];

        for (i = 0; i < Q.length; i++)
        {

            int index = Q[i][0];
            int value = Q[i][1];

            // If element is even then
            // remove it from sum
            if (A[index] % 2 == 0)
                sum = sum - A[index];

            A[index] = A[index] + value;

            // If the value becomes even after updating
            if (A[index] % 2 == 0)
                sum = sum + A[index];

            // Store sum for each query
            ANS[i]= sum;
        }

        // Print the result for every query
        for (i = 0; i < ANS.length; i++)
            System.out.print(ANS[i] + " ");
    }

    // Driver code
    public static void main(String [] args)
    {
        int [] A = { 1, 2, 3, 4 };
        int [][] Q = { { 0, 1 },
                                { 1, -3 },
                                { 0, -4 },
                                { 3, 2 } };
        BalanceArray(A, Q);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the result for
# every query
def BalanceArray(A, Q) :

    ANS = []
    sum = 0

    for i in range(len(A)) :

        # If current element is even
        if (A[i] % 2 == 0) :
            sum += A[i];

    for i in range(len(Q)) :

        index = Q[i][0];
        value = Q[i][1];

        # If element is even then
        # remove it from sum
        if (A[index] % 2 == 0) :
            sum -= A[index];

        A[index] += value;

        # If the value becomes even
        # after updating
        if (A[index] % 2 == 0) :
            sum += A[index];

        # Store sum for each query
        ANS.append(sum);

    # Print the result for every query
    for i in range(len(ANS)) :
        print(ANS[i], end = " ");

# Driver code
if __name__ == "__main__" :

    A = [ 1, 2, 3, 4 ];
    Q = [ [ 0, 1 ], [ 1, -3 ],
          [ 0, -4 ], [ 3, 2 ]];
    BalanceArray(A, Q);

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to print the result for every query
    static void BalanceArray(int [] A, int [, ] Q)
    {
        int [] ANS = new int [A.Length];

        int i, sum = 0;

        for (i = 0; i < A.Length; i++)

            // If current element is even
            if (A[i] % 2 == 0)
                sum = sum + A[i];

        for (i = 0; i < Q.GetLength(0); i++)
        {

            int index = Q[i, 0];
            int value = Q[i, 1];

            // If element is even then
            // remove it from sum
            if (A[index] % 2 == 0)
                sum = sum - A[index];

            A[index] = A[index] + value;

            // If the value becomes even after updating
            if (A[index] % 2 == 0)
                sum = sum + A[index];

            // Store sum for each query
            ANS[i]= sum;
        }

        // Print the result for every query
        for (i = 0; i < ANS.Length; i++)
            Console.Write(ANS[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int [] A = { 1, 2, 3, 4 };
        int [, ] Q = { { 0, 1 },
                                { 1, -3 },
                                { 0, -4 },
                                { 3, 2 } };
        BalanceArray(A, Q);
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the result for every query
function BalanceArray($A, &$Q)
{
    $ANS = array();

    $sum = 0;

    for ($i = 0; $i < count($A); $i++)

        // If current element is even
        if ($A[$i] % 2 == 0)
            $sum = $sum + $A[$i];

    for ($i = 0; $i < count($Q); $i++)
    {
        $index = $Q[$i][0];
        $value = $Q[$i][1];

        // If element is even then
        // remove it from sum
        if ($A[$index] % 2 == 0)
            $sum = $sum - $A[$index];

        $A[$index] = $A[$index] + $value;

        // If the value becomes even after updating
        if ($A[$index] % 2 == 0)
            $sum = $sum + $A[$index];

        // Store sum for each query
        array_push($ANS,$sum);
    }

    // Print the result for every query
    for ($i = 0; $i < count($ANS); $i++)
        echo $ANS[$i] . " ";
}

// Driver code
$A = array( 1, 2, 3, 4 );
$Q = array(array( 0, 1 ),
           array( 1, -3 ),
           array( 0, -4 ),
           array( 3, 2 ));
BalanceArray($A, $Q);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to print the result for every query
function BalanceArray(A, Q)
{
    var ANS = [];

    var i, sum = 0;

    for (i = 0; i < A.length; i++)

        // If current element is even
        if (A[i] % 2 == 0)
            sum = sum + A[i];

    for (i = 0; i < Q.length; i++) {

        var index = Q[i][0];
        var value = Q[i][1];

        // If element is even then
        // remove it from sum
        if (A[index] % 2 == 0)
            sum = sum - A[index];

        A[index] = A[index] + value;

        // If the value becomes even after updating
        if (A[index] % 2 == 0)
            sum = sum + A[index];

        // Store sum for each query
        ANS.push(sum);
    }

    // Print the result for every query
    for (i = 0; i < ANS.length; i++)
        document.write( ANS[i] + " ");
}

// Driver code
var A = [ 1, 2, 3, 4 ];
var Q = [ [ 0, 1 ],
         [ 1, -3 ],
         [ 0, -4 ],
          [ 3, 2 ] ];
BalanceArray(A, Q);

</script>
```

**Output:** 

```
8 6 2 4
```

**时间复杂度:** O(n)