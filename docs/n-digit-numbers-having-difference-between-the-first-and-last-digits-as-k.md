# 第一个和最后一个数字之间有差异的 N 位数字为 K

> 原文:[https://www . geesforgeks . org/n-digits-numbers-first-and-last-digits-as-k/](https://www.geeksforgeeks.org/n-digit-numbers-having-difference-between-the-first-and-last-digits-as-k/)

给定两个整数 **N** 和 **K** ，任务是打印所有由 **N** 数字组成的正数，这些数字的[第一个数字和最后一个数字](https://www.geeksforgeeks.org/find-first-last-digits-number/)之差等于 **K** 。

**示例:**

> **输入:** N = 2，K = 0
> T3】输出: 11，22，33，44，55，66，77，88，99
> 
> **输入:** N = 2，K = 9
> T3】输出: 90

**方法:**想法是使用[递归](https://www.geeksforgeeks.org/recursion/)生成所有可能的 1 位数到 **N 位数**的数字，并检查该数字的第一个数字和最后一个数字之间的差值是否等于 **K** 。以下是步骤:

1.  生成长度为 1 的所有可能的数字。
2.  每一步，继续给数字加数字，直到数字的长度变成 **N** 。
3.  当数字的长度等于 **N** 时，计算数字的第一个数字和最后一个数字之间的差值，并检查差值是否等于 **N** 。如果发现是真的，打印该号码并继续生成下一个号码。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to store and check the
// difference of digits
void findNumbers(string st, vector<int>& result,
                 int prev, int n, int K)
{
    // Base Case
    if (st.length() == n) {
        result.push_back(stoi(st));
        return;
    }

    // Last digit of the number to
    // check the difference from the
    // first digit
    if (st.size() == n - 1) {

        // Condition to avoid
        // repeated values
        if (prev - K >= 0) {

            string pt = "";

            // Update the string pt
            pt += prev - K + 48;

            // Recursive Call
            findNumbers(st + pt, result,
                        prev - K, n, K);
        }

        if (K != 0 && prev + K < 10) {

            string pt = "";

            // Update the string pt
            pt += prev + K + 48;

            // Recursive Call
            findNumbers(st + pt, result,
                        prev + K, n, K);
        }
    }

    // Any number can come in between
    // first and last except the zero
    else {
        for (int j = 1; j <= 9; j++) {

            string pt = "";
            pt += j + 48;

            // Recursive Call
            findNumbers(st + pt, result,
                        prev, n, K);
        }
    }
}

// Function to place digit of the number
vector<int> numDifference(int N, int K)
{
    vector<int> res;
    string st = "";

    // When N is 1 and K > 0, then the
    // single number will be the first
    // and last digit it cannot have
    // difference greater than 0
    if (N == 1 && K == 0) {
        res.push_back(0);
    }

    else if (N == 1 && K > 0) {
        return res;
    }

    // This loop place the digit at the
    // starting
    for (int i = 1; i < 10; i++) {

        string temp = "";
        temp += 48 + i;

        // Recursive Call
        findNumbers(st + temp, res, i, N, K);
        st = "";
    }

    return res;
}

void numDifferenceUtil(int N, int K)
{

    // Vector to store results
    vector<int> res;

    // Generate all the resultant number
    res = numDifference(N, K);

    // Print the result
    for (int i = 0; i < res.size(); i++) {
        cout << res[i] << " ";
    }
}

// Driver Code
int main()
{
    int N = 2, K = 9;

    // Function Call
    numDifferenceUtil(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

@SuppressWarnings("unchecked")
class GFG{

// Function to store and check the
// difference of digits
static void findNumbers(String st, ArrayList result,
                        int prev, int n, int K)
{

    // Base Case
    if (st.length() == n)
    {
        result.add(Integer.parseInt(st));
        return;
    }

    // Last digit of the number to
    // check the difference from the
    // first digit
    if (st.length() == n - 1)
    {

        // Condition to avoid
        // repeated values
        if (prev - K >= 0)
        {
            String pt = "";

            // Update the String pt
            pt += (char)(prev - K + 48);

            // Recursive Call
            findNumbers(st + pt, result,
                      prev - K, n, K);
        }

        if (K != 0 && prev + K < 10)
        {
            String pt = "";

            // Update the String pt
            pt += (char)(prev + K + 48);

            // Recursive Call
            findNumbers(st + pt, result,
                      prev + K, n, K);
        }
    }

    // Any number can come in between
    // first and last except the zero
    else
    {
        for(int j = 1; j <= 9; j++)
        {
            String pt = "";
            pt += (char)(j + 48);

            // Recursive Call
            findNumbers(st + pt, result,
                        prev, n, K);
        }
    }
}

// Function to place digit of the number
static ArrayList numDifference(int N, int K)
{
    ArrayList res = new ArrayList();

    String st = "";

    // When N is 1 and K > 0, then the
    // single number will be the first
    // and last digit it cannot have
    // difference greater than 0
    if (N == 1 && K == 0)
    {
        res.add(0);
    }

    else if (N == 1 && K > 0)
    {
        return res;
    }

    // This loop place the digit at the
    // starting
    for(int i = 1; i < 10; i++)
    {
        String temp = "";
        temp += (char)(48 + i);

        // Recursive Call
        findNumbers(st + temp, res, i, N, K);
        st = "";
    }
    return res;
}

static void numDifferenceUtil(int N, int K)
{

    // Vector to store results
    ArrayList res = new ArrayList();

    // Generate all the resultant number
    res = numDifference(N, K);

    // Print the result
    for(int i = 0; i < res.size(); i++)
    {
        System.out.print(res.get(i) + " ");
    }
}

// Driver Code
public static void main(String []args)
{
    int N = 2, K = 9;

    // Function Call
    numDifferenceUtil(N, K);
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to store and
# check the difference
# of digits
result = []
def findNumbers(st, prev,
                n, K):

    global result

    # Base Case
    if (len(st) == n):
        result.append(int(st))
        return

    # Last digit of the number to
    # check the difference from the
    # first digit
    if(len(st) == n - 1):

        # Condition to avoid
        # repeated values
        if (prev - K >= 0):
            pt = ""

            # Update the string pt
            pt += prev - K + 48

            # Recursive Call
            findNumbers(st + pt,
                        prev - K,
                        n, K)

        if (K != 0 and
            prev + K < 10):
            pt = ""

            # Update the string pt
            pt += prev + K + 48

            # Recursive Call
            findNumbers(st + pt,
                        prev + K,
                        n, K)

    # Any number can come in between
    # first and last except the zero
    else:
        for j in range(1, 10, 1):
            pt = ""
            pt += j + 48

            # Recursive Call
            findNumbers(st + pt,
                        prev, n, K)

# Function to place digit
# of the number
def numDifference(N,K):
    global result
    st = ""

    # When N is 1 and K > 0,
    # then the single number
    # will be the first and
    # last digit it cannot have
    # difference greater than 0
    if (N == 1 and K == 0):
        result.append(0)

    elif(N == 1 and K > 0):
        return result

    # This loop place the
    # digit at the starting
    for i in range(1, 10, 1):
        temp = ""
        temp += str(48 + i)

        # Recursive Call
        findNumbers(st + temp,
                    i, N, K)
        st = ""
    return result

def numDifferenceUtil(N, K):

    # Vector to store results
    res = []

    # Generate all the
    # resultant number
    res = numDifference(N, K)

    # Print the result
    for i in range(1, len(res)):
        print(res[i] + 40,
              end = " ")
        break

# Driver Code
if __name__ == '__main__':

    N = 2
    K = 9

    # Function Call
    numDifferenceUtil(N, K)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach

using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to store and check the
// difference of digits
static void findNumbers(string st, ArrayList result,
                 int prev, int n, int K)
{
    // Base Case
    if (st.Length == n) {
        result.Add(Int32.Parse(st));
        return;
     }

    // Last digit of the number to
    // check the difference from the
    // first digit
    if (st.Length == n - 1) {

        // Condition to avoid
        // repeated values
        if (prev - K >= 0) {

            string pt = "";

            // Update the string pt
            pt += (char)(prev - K + 48);

            // Recursive Call
            findNumbers(st + pt, result,
                        prev - K, n, K);
        }

        if (K != 0 && prev + K < 10) {

            string pt = "";

            // Update the string pt
            pt += (char)(prev + K + 48);

            // Recursive Call
            findNumbers(st + pt, result,
                        prev + K, n, K);
        }
    }

    // Any number can come in between
    // first and last except the zero
    else {
        for (int j = 1; j <= 9; j++) {

            string pt = "";
            pt += (char)(j + 48);

            // Recursive Call
            findNumbers(st + pt, result,
                        prev, n, K);
        }
    }
}

// Function to place digit of the number
static ArrayList numDifference(int N, int K)
{
    ArrayList res=new ArrayList();

    string st = "";

    // When N is 1 and K > 0, then the
    // single number will be the first
    // and last digit it cannot have
    // difference greater than 0
    if (N == 1 && K == 0) {
        res.Add(0);
    }

    else if (N == 1 && K > 0) {
        return res;
    }

    // This loop place the digit at the
    // starting
    for (int i = 1; i < 10; i++) {

        string temp = "";
        temp += (char)(48 + i);

        // Recursive Call
        findNumbers(st + temp, res, i, N, K);
        st = "";
    }

    return res;
}

static void numDifferenceUtil(int N, int K)
{

    // Vector to store results
    ArrayList res=new ArrayList();

    // Generate all the resultant number
    res = numDifference(N, K);

    // Print the result
    for (int i = 0; i < res.Count; i++) {
        Console.Write(res[i]+" ");
    }
}

// Driver Code
public static void Main(string []args)
{
    int N = 2, K = 9;

    // Function Call
    numDifferenceUtil(N, K);

}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to store and check the
    // difference of digits
    function findNumbers(st, result, prev, n, K)
    {
        // Base Case
        if (st.length == n) {
            result.push(parseInt(st));
            return;
         }

        // Last digit of the number to
        // check the difference from the
        // first digit
        if (st.length == n - 1) {

            // Condition to avoid
            // repeated values
            if (prev - K >= 0) {

                let pt = "";

                // Update the string pt
                pt += String.fromCharCode(prev - K + 48);

                // Recursive Call
                findNumbers(st + pt, result,
                            prev - K, n, K);
            }

            if (K != 0 && prev + K < 10) {

                let pt = "";

                // Update the string pt
                pt += String.fromCharCode(prev + K + 48);

                // Recursive Call
                findNumbers(st + pt, result,
                            prev + K, n, K);
            }
        }

        // Any number can come in between
        // first and last except the zero
        else {
            for (let j = 1; j <= 9; j++) {

                let pt = "";
                pt += String.fromCharCode(j + 48);

                // Recursive Call
                findNumbers(st + pt, result,
                            prev, n, K);
            }
        }
    }

    // Function to place digit of the number
    function numDifference(N, K)
    {
        let res = [];

        let st = "";

        // When N is 1 and K > 0, then the
        // single number will be the first
        // and last digit it cannot have
        // difference greater than 0
        if (N == 1 && K == 0) {
            res.push(0);
        }

        else if (N == 1 && K > 0) {
            return res;
        }

        // This loop place the digit at the
        // starting
        for (let i = 1; i < 10; i++) {

            let temp = "";
            temp += String.fromCharCode(48 + i);

            // Recursive Call
            findNumbers(st + temp, res, i, N, K);
            st = "";
        }

        return res;
    }

    function numDifferenceUtil(N, K)
    {

        // Vector to store results
        let res = [];

        // Generate all the resultant number
        res = numDifference(N, K);

        // Print the result
        for (let i = 0; i < res.length; i++) {
            document.write(res[i]+" ");
        }
    }

    let N = 2, K = 9;

    // Function Call
    numDifferenceUtil(N, K);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
90
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*