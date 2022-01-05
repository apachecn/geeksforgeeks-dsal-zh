# 检查数组是否可以转换成严格递减的序列

> 原文:[https://www . geesforgeks . org/check-if-array-can-convert-in-严格递减序列/](https://www.geeksforgeeks.org/check-if-array-can-be-converted-into-strictly-decreasing-sequence/)

给定一个数组 **arr[]** ，任务是借助下面的操作检查给定的数组是否可以转换成严格递减的序列:

*   在一次操作中将任何元素(如果大于 1)减少 1

**例:**

> **输入:** arr[] = {11，11，11，11}
> **输出:**是
> **解释:**
> 给定的序列可以转换成
> arr[] = {11，10，9，8}
> **输入:** arr[] = {1，1}
> **输出:**否
> **解释:**
> 给定的

**方法:**思路是检查数组的每个元素是否大于等于(元素的 N-index)，因为如果大于等于(元素的 N-index)就意味着数组可以转换成【N，N-1，N-2，…1】
下面是上述方法的实现:

## C++

```
// C++ implementation to check that
// array can be converted into a
// strictly decreasing sequence
#include <bits/stdc++.h>
using namespace std;

// Function to check that array
// can be converted into a
// strictly decreasing sequence
bool check(int* arr, int n)
{
    bool flag = true;

    // Loop to check that each element is
    // greater than the (N - index)
    for (int i = 0; i < n; i++) {

        // If element is less than (N - index)
        if (arr[i] < n - i) {
            flag = false;
        }
    }

    // If array can be converted
    if (flag) {
        return true;
    }
    else {
        return false;
    }
}

// Driver Code
int main()
{
    int arr1[] = { 11, 11, 11, 11 };
    int n1 = sizeof(arr1) / sizeof(arr1[0]);

    // Function calling
    if (check(arr1, n1)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check that
// array can be converted into a
// strictly decreasing sequence
class GFG{

// Function to check that array
// can be converted into a
// strictly decreasing sequence
static boolean check(int []arr, int n)
{
    boolean flag = true;

    // Loop to check that each element is
    // greater than the (N - index)
    for (int i = 0; i < n; i++)
    {

        // If element is less than (N - index)
        if (arr[i] < n - i)
        {
            flag = false;
        }
    }

    // If array can be converted
    if (flag)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr1[] = { 11, 11, 11, 11 };
    int n1 = arr1.length;

    // Function calling
    if (check(arr1, n1))
    {
        System.out.print("Yes" + "\n");
    }
    else
    {
        System.out.print("No" + "\n");
    }
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to check that
# array can be converted into a
# strictly decreasing sequence

# Function to check that array
# can be converted into a
# strictly decreasing sequence
def check(arr, n):

    flag = True;

    # Loop to check that each element
    # is greater than the (N - index)
    for i in range(n):

        # If element is less than (N - index)
        if (arr[i] < n - i):
            flag = False;

    # If array can be converted
    if (flag):
        return True;
    else:
        return False;

# Driver Code
if __name__ == '__main__':

    arr1 = [ 11, 11, 11, 11 ];
    n1 = len(arr1);

    # Function calling
    if (check(arr1, n1)):
        print("Yes");
    else:
        print("No");

# This code is contributed by sapnasingh4991
```

## C#

```
// C# implementation to check that
// array can be converted into a
// strictly decreasing sequence
using System;

class GFG{

// Function to check that array
// can be converted into a
// strictly decreasing sequence
static bool check(int []arr, int n)
{
    bool flag = true;

    // Loop to check that each element is
    // greater than the (N - index)
    for(int i = 0; i < n; i++)
    {

       // If element is less than (N - index)
       if (arr[i] < n - i)
       {
           flag = false;
       }
    }

    // If array can be converted
    if (flag)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver Code
static public void Main(String[] args)
{
    int []arr1 = { 11, 11, 11, 11 };
    int n1 = arr1.Length;

    // Function calling
    if (check(arr1, n1))
    {
        Console.Write("Yes" + "\n");
    }
    else
    {
        Console.Write("No" + "\n");
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation to check that
// array can be converted into a
// strictly decreasing sequence

// Function to check that array
// can be converted into a
// strictly decreasing sequence
function check(arr,n)
{
    var flag = true;

    // Loop to check that each element is
    // greater than the (N - index)
    for (let i = 0; i < n; i++) {

        // If element is less than (N - index)
        if (arr[i] < n - i) {
            flag = false;
        }
    }

    // If array can be converted
    if (flag) {
        return true;
    }
    else {
        return false;
    }
}

    let arr1= [ 11, 11, 11, 11 ];
    let n1 = arr1.length;

    // Function calling
    if (check(arr1, n1)) {
     document.write("Yes");
     }
    else {
        document.write("No");
     }

     // This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
Yes
```