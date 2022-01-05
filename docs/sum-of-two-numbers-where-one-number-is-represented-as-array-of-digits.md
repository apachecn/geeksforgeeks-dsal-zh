# 两个数字的和，其中一个数字表示为数字阵列

> 原文:[https://www . geeksforgeeks . org/两位数之和-其中一位数字表示为数字数组/](https://www.geeksforgeeks.org/sum-of-two-numbers-where-one-number-is-represented-as-array-of-digits/)

给定一个数字数组 **arr[]** 和一个整数 **K** ，任务是找到 **num(arr) + K** ，其中 **num(arr)** 是由数组的所有数字串联而成的数字。

**示例:**

> **输入:** arr[] = {2，7，4}，K = 181
> **输出:** 455
> 274 + 181 = 455
> 
> **输入:** arr[] = {6}，K = 815
> **输出:** 821
> 6 + 815 = 821

**方法:**从末尾开始遍历数字数组，开始将 K 的数字一个接一个地加到当前数字上，如果产生进位，则将其加到下一个数字的加法中。添加完 K 的所有数字后，开始从左边遍历数字数组，并开始打印元素，这些元素在连接时会给出结果数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the vector containing the answer
vector<int> addToArrayForm(vector<int>& A, int K)
{

    // Vector v is to store each digits sum
    // and vector ans is to store the answer
    vector<int> v, ans;

    // No carry in the beginning
    int rem = 0;

    int i = 0;

    // Start loop from the end
    // and take element one by one
    for (i = A.size() - 1; i >= 0; i--) {

        // Array index and last digit of number
        int my = A[i] + K % 10 + rem;
        if (my > 9) {

            // Maintain carry of summation
            rem = 1;

            // Push the digit value into the array
            v.push_back(my % 10);
        }
        else {
            v.push_back(my);
            rem = 0;
        }
        K = K / 10;
    }

    // K value is greater then 0
    while (K > 0) {

        // Push digits of K one by one in the array
        int my = K % 10 + rem;
        v.push_back(my % 10);

        // Also maintain carry with summation
        if (my / 10 > 0)
            rem = 1;
        else
            rem = 0;
        K = K / 10;
    }

    if (rem > 0)
        v.push_back(rem);

    // Reverse the elements of vector v
    // and store it in vector ans
    for (int i = v.size() - 1; i >= 0; i--)
        ans.push_back(v[i]);

    return ans;
}

// Driver code
int main()
{
    vector<int> A{ 2, 7, 4 };
    int K = 181;
    vector<int> ans = addToArrayForm(A, K);

    // Print the answer
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Function to return the vector containing the answer
    static ArrayList<Integer> addToArrayForm(ArrayList<Integer> A, int K)
    {

        // ArrayList v is to store each digits sum
        // and ArrayList ans is to store the answer
        ArrayList<Integer> v = new ArrayList<Integer>();
        ArrayList<Integer> ans = new ArrayList<Integer>();

        // No carry in the beginning
        int rem = 0;

        int i = 0;

        // Start loop from the end
        // and take element one by one
        for (i = A.size() - 1; i >= 0; i--)
        {

            // Array index and last digit of number
            int my = A.get(i) + K % 10 + rem;
            if (my > 9)
            {

                // Maintain carry of summation
                rem = 1;

                // Push the digit value into the array
                v.add(my % 10);
            }
            else
            {
                v.add(my);
                rem = 0;
            }
            K = K / 10;
        }

        // K value is greater then 0
        while (K > 0)
        {

            // Push digits of K one by one in the array
            int my = K % 10 + rem;
            v.add(my % 10);

            // Also maintain carry with summation
            if (my / 10 > 0)
                rem = 1;
            else
                rem = 0;
            K = K / 10;
        }

        if (rem > 0)
            v.add(rem);

        // Reverse the elements of vector v
        // and store it in vector ans
        for (int j = v.size() - 1; j >= 0; j--)
            ans.add(v.get(j));

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        ArrayList<Integer> A = new ArrayList<Integer>();
        A.add(2);
        A.add(7);
        A.add(4);

        int K = 181;
        ArrayList<Integer> ans = addToArrayForm(A, K);

        // Print the answer
        for (int i = 0; i < ans.size(); i++)
            System.out.print(ans.get(i));

    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the vector
# containing the answer
def addToArrayForm(A, K):

    # Vector v is to store each digits sum
    # and vector ans is to store the answer
    v, ans = [], []

    # No carry in the beginning
    rem, i = 0, 0

    # Start loop from the end
    # and take element one by one
    for i in range(len(A) - 1, -1, -1):

        # Array index and last digit of number
        my = A[i] + (K % 10) + rem
        if my > 9:

            # Maintain carry of summation
            rem = 1

            # Push the digit value into the array
            v.append(my % 10)

        else:
            v.append(my)
            rem = 0

        K = K // 10

    # K value is greater then 0
    while K > 0:

        # Push digits of K one by one in the array
        my = (K % 10) + rem
        v.append(my % 10)

        # Also maintain carry with summation
        if my // 10 > 0:
            rem = 1
        else:
            rem = 0

        K = K // 10

    if rem > 0:
        v.append(rem)

    # Reverse the elements of vector v
    # and store it in vector ans
    for i in range(len(v) - 1, -1, -1):
        ans.append(v[i])

    return ans

# Driver code
if __name__ == "__main__":

    A = [2, 7, 4]
    K = 181
    ans = addToArrayForm(A, K)

    # Print the answer
    for i in range(0, len(ans)):
        print(ans[i], end = "")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{
    // Function to return the vector containing the answer
    static ArrayList addToArrayForm(ArrayList A, int K)
    {

        // ArrayList v is to store each digits sum
        // and ArrayList ans is to store the answer
        ArrayList v = new ArrayList();
        ArrayList ans = new ArrayList();

        // No carry in the beginning
        int rem = 0;

        int i = 0;

        // Start loop from the end
        // and take element one by one
        for (i = A.Count - 1; i >= 0; i--)
        {

            // Array index and last digit of number
            int my = (int)A[i] + K % 10 + rem;
            if (my > 9)
            {

                // Maintain carry of summation
                rem = 1;

                // Push the digit value into the array
                v.Add(my % 10);
            }
            else
            {
                v.Add(my);
                rem = 0;
            }
            K = K / 10;
        }

        // K value is greater then 0
        while (K > 0)
        {

            // Push digits of K one by one in the array
            int my = K % 10 + rem;
            v.Add(my % 10);

            // Also maintain carry with summation
            if (my / 10 > 0)
                rem = 1;
            else
                rem = 0;
            K = K / 10;
        }

        if (rem > 0)
            v.Add(rem);

        // Reverse the elements of vector v
        // and store it in vector ans
        for (int j = v.Count - 1; j >= 0; j--)
            ans.Add((int)v[j]);

        return ans;
    }

    // Driver code
    static void Main()
    {
        ArrayList A = new ArrayList();
        A.Add(2);
        A.Add(7);
        A.Add(4);

        int K = 181;
        ArrayList ans = addToArrayForm(A, K);

        // Print the answer
        for (int i = 0; i < ans.Count; i++)
            Console.Write((int)ans[i]);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to return the vector containing the answer
function addToArrayForm($A, $K)
{

    // Vector v is to store each digits sum
    // and vector ans is to store the answer
    $v = array();
    $ans = array();

    // No carry in the beginning
    $rem = 0;

    $i = 0;

    // Start loop from the end
    // and take element one by one
    for ($i = count($A) - 1; $i >= 0; $i--)
    {

        // Array index and last digit of number
        $my = $A[$i] + $K % 10 + $rem;
        if ($my > 9)
        {

            // Maintain carry of summation
            $rem = 1;

            // Push the digit value into the array
            array_push($v,$my % 10);
        }
        else
        {
            array_push($v,$my);
            $rem = 0;
        }
        $K = floor($K / 10);
    }

    // K value is greater then 0
    while ($K > 0)
    {

        // Push digits of K one by one in the array
        $my = $K % 10 + $rem;

        array_push($v,$my % 10);

        // Also maintain carry with summation
        if ($my / 10 > 0)
            $rem = 1;
        else
            $rem = 0;

        $K = floor($K / 10);
    }

    if ($rem > 0)
        array_push($v,$rem);

    // Reverse the elements of vector v
    // and store it in vector ans
    for ($i = count($v) - 1; $i >= 0; $i--)
        array_push($ans,$v[$i]);

    return $ans;
}

// Driver code
$A = array( 2, 7, 4 );
$K = 181;
$ans = addToArrayForm($A, $K);

// Print the answer
for ($i = 0; $i < count($ans); $i++)
    echo $ans[$i];

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the vector
// containing the answer
function addToArrayForm(A, K)
{

    // ArrayList v is to store each digits sum
    // and ArrayList ans is to store the answer
    let v = [];
    let ans = [];

    // No carry in the beginning
    let rem = 0;

    let i = 0;

    // Start loop from the end
    // and take element one by one
    for(i = A.length - 1; i >= 0; i--)
    {

        // Array index and last digit of number
        let my = A[i] + K % 10 + rem;
        if (my > 9)
        {

            // Maintain carry of summation
            rem = 1;

            // Push the digit value into the array
            v.push(my % 10);
        }
        else
        {
            v.push(my);
            rem = 0;
        }
        K = parseInt(K / 10, 10);
    }

    // K value is greater then 0
    while (K > 0)
    {

        // Push digits of K one by one in the array
        let my = K % 10 + rem;
        v.push(my % 10);

        // Also maintain carry with summation
        if (parseInt(my / 10, 10) > 0)
            rem = 1;
        else
            rem = 0;

        K = parseInt(K / 10, 10);
    }

    if (rem > 0)
        v.push(rem);

    // Reverse the elements of vector v
    // and store it in vector ans
    for(let j = v.length - 1; j >= 0; j--)
        ans.push(v[j]);

    return ans;
}

// Driver code
let A = [];
A.push(2);
A.push(7);
A.push(4);

let K = 181;
let ans = addToArrayForm(A, K);

// Print the answer
for(let i = 0; i < ans.length; i++)
    document.write(ans[i]);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
455
```