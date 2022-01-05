# 一组大数之和

> 原文:[https://www . geeksforgeeks . org/大数之和/](https://www.geeksforgeeks.org/sum-of-an-array-of-large-numbers/)

给定一个整数 **K** 和一个由字符串形式的 **N** 个大数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是求数组中所有大数的和。

**示例:**

> **输入:** K = 50，arr[]=
> {“01234567890123456789012345678901234567890123456789”，
> “01234567890123456789012345679012345679012456790125、567890123579012325、579012345456789”
> ”

**做法:**思路是把所有数字对应位置的数字相加。创建一个大小为 **K + 1** 的数组**结果[]** 来存储结果。从头到尾遍历所有字符串，继续将所有数字的数字加在同一个位置，并插入**结果[]** 中对应的索引中。以下是步骤:

1.  初始化一个数组**结果[]** 来存储数字的总和。
2.  迭代从索引 **K 到 0** 的字符串，对于每个索引，执行以下操作:
    *   遍历所有数组元素，计算当前索引处所有数字的和，比如说 **idx** ，存储在一个变量中，比如说 **sum** 。
    *   将上述**和**的数字放在**结果【idx】**的位置。
    *   存储**和/ 10** 的值作为下一个指标的进位。
3.  对所有数组的整个长度重复上述步骤后，反转存储在**结果【】**中的所有数字，得到给定 **N** 个数字的合成总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the result of the
// summation of numbers having K-digit
void printResult(vector<int> result)
{
    // Reverse the array to
    // obtain the result
    reverse(result.begin(), result.end());

    int i = 0;

    while (i < result.size()) {

        // Print every digit
        // of the answer
        cout << result[i];
        i++;
    }
}

// Function to calculate the total sum
void sumOfLargeNumbers(string v[], int k, int N)
{
    // Stores the array of large
    // numbers in integer format
    vector<vector<int> > x(1000);

    for (int i = 0; i < k; i++) {

        for (int j = 0; j < N; j++) {

            // Convert each element
            // from character to integer
            x[i].push_back(v[i][j] - '0');
        }
    }

    // Stores the carry
    int carry = 0;

    // Stores the result
    // of summation
    vector<int> result;

    for (int i = N - 1; i >= 0; i--) {

        // Initialize the sum
        int sum = 0;

        for (int j = 0; j < k; j++)

            // Calculate sum
            sum += x[j][i];

        // Update the sum by adding
        // existing carry
        sum += carry;
        int temp = sum;

        // Store the number of digits
        int count = 0;
        while (temp > 9) {
            temp = temp % 10;

            // Increase count of digits
            count++;
        }

        long long int l = pow(10, count);
        if (l != 1)

            // If the number exceeds 9,
            // Store the unit digit in carry
            carry = (double)sum / l;

        // Store the rest of the sum
        sum = sum % 10;

        // Append digit by digit
        // into result array
        result.push_back(sum);
    }
    while (carry != 0) {
        int a = carry % 10;

        // Append result until
        // carry is 0
        result.push_back(a);
        carry = carry / 10;
    }

    // Print the result
    printResult(result);
}

// Driver Code
int main()
{
    int K = 10;
    int N = 5;

    // Given N array of large numbers
    string arr[]
        = { "1111111111", "1111111111",
            "1111111111", "1111111111",
            "1111111111" };

    sumOfLargeNumbers(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to print the result of the
// summation of numbers having K-digit
static void printResult(ArrayList<Integer> result)
{

    // Reverse the array to
    // obtain the result
    Collections.reverse(result);

    int i = 0;

    while (i < result.size())
    {

        // Print every digit
        // of the answer
        System.out.print(result.get(i));
        i++;
    }
}

// Function to calculate the total sum
static void sumOfLargeNumbers(String v[],
                              int k, int N)
{

    // Stores the array of large
    // numbers in integer format
    ArrayList<
    ArrayList<Integer>> x = new ArrayList<>(1000);

    for(int i = 0; i < k; i++)
        x.add(new ArrayList<Integer>());

    for(int i = 0; i < k; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Convert each element
            // from character to integer
            x.get(i).add(v[i].charAt(j) - '0');
        }
    }

    // Stores the carry
    int carry = 0;

    // Stores the result
    // of summation
    ArrayList<Integer> result = new ArrayList<>();

    for(int i = N - 1; i >= 0; i--)
    {

        // Initialize the sum
        int sum = 0;

        for(int j = 0; j < k; j++)

            // Calculate sum
            sum += x.get(j).get(i);

        // Update the sum by adding
        // existing carry
        sum += carry;
        int temp = sum;

        // Store the number of digits
        int count = 0;
        while (temp > 9)
        {
            temp = temp % 10;

            // Increase count of digits
            count++;
        }

        long l = (long)Math.pow(10, count);
        if (l != 1)

            // If the number exceeds 9,
            // Store the unit digit in carry
            carry = (int)(sum / l);

        // Store the rest of the sum
        sum = sum % 10;

        // Append digit by digit
        // into result array
        result.add(sum);
    }
    while (carry != 0)
    {
        int a = carry % 10;

        // Append result until
        // carry is 0
        result.add(a);
        carry = carry / 10;
    }

    // Print the result
    printResult(result);
}

// Driver Code
public static void main (String[] args)
{
    int K = 10;
    int N = 5;

    // Given N array of large numbers
    String arr[]  = { "1111111111", "1111111111",
                      "1111111111", "1111111111",
                      "1111111111" };

    sumOfLargeNumbers(arr, N, K);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the result of the
# summation of numbers having K-digit
def printResult(result):

    # Reverse the array to
    # obtain the result
    result = result[::-1]

    i = 0
    while (i < len(result)):

        # Print every digit
        # of the answer
        print(result[i], end = "")
        i += 1

# Function to calculate the total sum
def sumOfLargeNumbers(v, k, N):

    # Stores the array of large
    # numbers in integer format
    x = [[] for i in range(1000)]

    for i in range(k):
        for j in range(N):

            # Convert each element
            # from character to integer
            x[i].append(ord(v[i][j]) - ord('0'))

    # Stores the carry
    carry = 0

    # Stores the result
    # of summation
    result = []

    for i in range(N - 1, -1, -1):

        # Initialize the sum
        sum = 0

        for j in range(k):

            # Calculate sum
            sum += x[j][i]

        # Update the sum by adding
        # existing carry
        sum += carry
        temp = sum

        # Store the number of digits
        count = 0
        while (temp > 9):
            temp = temp % 10

            # Increase count of digits
            count += 1

        l = pow(10, count)
        if (l != 1):

            # If the number exceeds 9,
            # Store the unit digit in carry
            carry = sum / l

        # Store the rest of the sum
        sum = sum % 10

        # Append digit by digit
        # into result array
        result.append(sum)

    while (carry != 0):
        a = carry % 10

        # Append result until
        # carry is 0
        result.append(a)
        carry = carry // 10

    # Print the result
    printResult(result)

# Driver Code
if __name__ == '__main__':

    K = 10
    N = 5

    # Given N array of large numbers
    arr= [ "1111111111", "1111111111",
           "1111111111", "1111111111",
           "1111111111" ]

    sumOfLargeNumbers(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to print the result of the
// summation of numbers having K-digit
static void printResult(List<int> result)
{
  // Reverse the array to
  // obtain the result
  result.Reverse();

  int i = 0;

  while (i < result.Count)
  {

    // Print every digit
    // of the answer
    Console.Write(result[i]);
    i++;
  }
}

// Function to calculate the total sum
static void sumOfLargeNumbers(String []v,
                              int k, int N)
{  
  // Stores the array of large
  // numbers in integer format
  List<List<int>> x =
            new List<List<int>>(1000);

  for(int i = 0; i < k; i++)
    x.Add(new List<int>());

  for(int i = 0; i < k; i++)
  {
    for(int j = 0; j < N; j++)
    {
      // Convert each element
      // from character to integer
      x[i].Add(v[i][j] - '0');
    }
  }

  // Stores the carry
  int carry = 0;

  // Stores the result
  // of summation
  List<int> result = new List<int>();

  for(int i = N - 1; i >= 0; i--)
  {
    // Initialize the sum
    int sum = 0;

    for(int j = 0; j < k; j++)

      // Calculate sum
      sum += x[j][i];

    // Update the sum by adding
    // existing carry
    sum += carry;
    int temp = sum;

    // Store the number of digits
    int count = 0;
    while (temp > 9)
    {
      temp = temp % 10;

      // Increase count of digits
      count++;
    }

    long l = (long)Math.Pow(10, count);
    if (l != 1)

      // If the number exceeds 9,
      // Store the unit digit in carry
      carry = (int)(sum / l);

    // Store the rest of the sum
    sum = sum % 10;

    // Append digit by digit
    // into result array
    result.Add(sum);
  }

  while (carry != 0)
  {
    int a = carry % 10;

    // Append result until
    // carry is 0
    result.Add(a);

    carry = carry / 10;
  }

  // Print the result
  printResult(result);
}

// Driver Code
public static void Main(String[] args)
{
  int K = 10;
  int N = 5;

  // Given N array of large numbers
  String []arr  = {"1111111111",
                   "1111111111",
                   "1111111111",
                   "1111111111",
                   "1111111111"};

  sumOfLargeNumbers(arr, N, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the result of the
// summation of numbers having K-digit
function printResult(result)
{
    // Reverse the array to
    // obtain the result
    result.reverse();

    let i = 0;

    while (i < result.length)
    {

        // Print every digit
        // of the answer
        document.write(result[i]);
        i++;
    }
}

// Function to calculate the total sum
function sumOfLargeNumbers(v,k,N)
{
    // Stores the array of large
    // numbers in integer format
    let x = [];

    for(let i = 0; i < k; i++)
        x.push([]);

    for(let i = 0; i < k; i++)
    {
        for(let j = 0; j < N; j++)
        {

            // Convert each element
            // from character to integer
            x[i].push(v[i][j].charCodeAt(0) - '0'.charCodeAt(0));
        }
    }

    // Stores the carry
    let carry = 0;

    // Stores the result
    // of summation
    let result = [];

    for(let i = N - 1; i >= 0; i--)
    {

        // Initialize the sum
        let sum = 0;

        for(let j = 0; j < k; j++)

            // Calculate sum
            sum += x[j][i];

        // Update the sum by adding
        // existing carry
        sum += carry;
        let temp = sum;

        // Store the number of digits
        let count = 0;
        while (temp > 9)
        {
            temp = temp % 10;

            // Increase count of digits
            count++;
        }

        let l = Math.pow(10, count);
        if (l != 1)

            // If the number exceeds 9,
            // Store the unit digit in carry
            carry = Math.floor(sum / l);

        // Store the rest of the sum
        sum = sum % 10;

        // Append digit by digit
        // into result array
        result.push(sum);
    }
    while (carry != 0)
    {
        let a = carry % 10;

        // Append result until
        // carry is 0
        result.push(a);
        carry = Math.floor(carry / 10);
    }

    // Print the result
    printResult(result);
}

// Driver Code
let K = 10;
let N = 5;

// Given N array of large numbers
let arr  = [ "1111111111", "1111111111",
                 "1111111111", "1111111111",
                 "1111111111" ];

sumOfLargeNumbers(arr, N, K);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
5555555555
```

***时间复杂度:** O(N*K)*
***辅助空间:** O(K)*