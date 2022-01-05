# 计算数组中整数的位数的倍数

> 原文:[https://www . geesforgeks . org/count-数组中的整数是其位数的倍数/](https://www.geeksforgeeks.org/count-integers-in-an-array-which-are-multiples-their-bits-counts/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是对所有元素进行计数，这些元素是其设定位数的倍数。
**例:**

```
Input : arr[] = { 1, 2, 3, 4, 5, 6 }
Output : 4
Explanation :
There numbers which are multiple of their setbits count are { 1, 2, 4, 6 }.

Input : arr[] = {10, 20, 30, 40}
Output : 3
Explanation :
There numbers which are multiple of their setbits count are { 10, 20, 40 }
```

**方法:**逐个循环遍历每个数组元素。计算数组中每个数字的设定位。检查当前整数是否是其设置位数的倍数。如果“是”，则将计数器增加 1，否则跳过该整数。
以下是上述办法的实施:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of numbers
// which are multiple of its set bits count
int find_count(vector<int>& arr)
{
    // variable to store count
    int ans = 0;

    // iterate over elements of array
    for (int i : arr) {

        // Get the set-bits count of each element
        int x = __builtin_popcount(i);

        // Check if the setbits count
        // divides the integer i
        if (i % x == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

// Driver code
int main()
{
    vector<int> arr
        = { 1, 2, 3, 4, 5, 6 };

    cout << find_count(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

// Function to find the count of numbers
// which are multiple of its set bits count
static int find_count(int []arr)
{
    // variable to store count
    int ans = 0;

    // iterate over elements of array
    for (int i : arr) {

        // Get the set-bits count of each element
        int x = Integer.bitCount(i);

        // Check if the setbits count
        // divides the integer i
        if (i % x == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int []arr
        = { 1, 2, 3, 4, 5, 6 };

    System.out.print(find_count(arr));

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# function to return set bits count
def bitsoncount(x):
    return bin(x).count('1')

# Function to find the count of numbers
# which are multiple of its set bits count
def find_count(arr) :
    # variable to store count
    ans = 0

    # iterate over elements of array
    for i in arr :

        # Get the set-bits count of each element
        x = bitsoncount(i)

        # Check if the setbits count
        # divides the integer i
        if (i % x == 0):

            # Increment the count
            # of required numbers by 1
            ans += 1

    return ans

# Driver code
arr = [ 1, 2, 3, 4, 5, 6 ]

print(find_count(arr))

# This code is contributed by Sanjit_Prasad
```

## C#

```
using System;

public class GFG{

// Function to find the count of numbers
// which are multiple of its set bits count
static int find_count(int []arr)
{
    // Variable to store count
    int ans = 0;

    // Iterate over elements of array
    foreach (int i in arr) {

        // Get the set-bits count of each element
        int x = bitCount(i);

        // Check if the setbits count
        // divides the integer i
        if (i % x == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}
static int bitCount(long x)
{
    int setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
public static void Main(String[] args)
{
    int []arr
        = { 1, 2, 3, 4, 5, 6 };

    Console.Write(find_count(arr));

}
}
// This code contributed by Princi Singh
```

## java 描述语言

```
<script>

// Function to find the count of numbers
// which are multiple of its set bits count
function find_count(arr)
{
    // Variable to store count
    var ans = 0;

    // Iterate over elements of array
    for (var i=0;i<=arr.length;i++) {

        // Get the set-bits count of each element
        var x = bitCount(i);

        // Check if the setbits count
        // divides the integer i
        if (i % x == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}
function bitCount( x)
{
    var setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}
var arr = [ 1, 2, 3, 4, 5, 6 ];
  document.write(find_count(arr));

  // This code contributed by SoumikMondal
</script>
```

**输出:**

```
4
```

**时间复杂度:-** O(nlog(max(arr[]))，其中 n 是数组的大小，
T3】空间复杂度:- O(1)