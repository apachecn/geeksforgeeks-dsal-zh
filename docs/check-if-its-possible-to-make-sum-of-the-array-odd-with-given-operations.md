# 检查在给定的操作下是否可以使数组的和为奇数

> 原文:[https://www . geeksforgeeks . org/check-if-it-to-make-sum-of-the-array-odd-with-given-operations/](https://www.geeksforgeeks.org/check-if-its-possible-to-make-sum-of-the-array-odd-with-given-operations/)

给定一个数组**arr【】**，任务是检查是否有可能使数组的和为奇数，使得任意两个索引 **i** 和 **j** 可以被选择并且**arr【I】**可以被设置为等于**arr【j】**给定 **i！= j** 。
**示例:**

> **输入:** arr[] = { 5，4，4，5，1，3 }
> **输出:**是
> **说明:**
> 数组之和为 22。放入 arr[0] = arr[1]，其中 i=0，j=1。这个新数组的和是 21，这是奇数。
> **输入:** arr[] = { 2，2，8，8 }
> **输出:**否
> **说明:**
> 数组之和为 20。
> 数组的和不能变成奇数，因为所有元素都是偶数。将偶数加到偶数上总是得到偶数的结果。

**方法:**思路是找出数组中所有元素的和，同时检查数组中存在的偶数和奇数的个数。如果和是偶数，那么偶数中的一个可以用奇数代替，从而使阵列的和为奇数。如果数组中没有奇数元素，则数组的和不能为奇数。
以下是上述办法的实施情况:

## C++

```
// C++ program to check if the array
// with odd sum is possible
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// sum of the array can be made odd.
bool isOdd(int arr[], int n)
{
    int l, r, flag = 0, flag1 = 0, sum = 0;

    // Find sum of all elements and increment
    // check for odd or even elements in the array
    // so that by changing ai=aj,
    // the sum of the array can be made odd
    for (int i = 0; i < n; i++) {
        sum += arr[i];
        if (arr[i] % 2 == 0 && flag == 0) {
            flag = 1;
            l = arr[i];
        }
        if (arr[i] % 2 != 0 && flag1 == 0) {
            r = arr[i];
            flag1 = 1;
        }
    }

    // If the sum is already odd
    if (sum % 2 != 0) {
        return true;
    }

    // Else, then both the flags should be checked.
    // Here, flag1 and flag represent if there is
    // an odd-even pair which can be replaced.
    else {
        if (flag1 == 1 && flag == 1)
            return true;
        else
            return false;
    }
}

// Driver code
int main()
{
    int ar[] = { 5, 4, 4, 5, 1, 3 };
    int n = sizeof(ar) / sizeof(ar[0]);
    bool res = isOdd(ar, n);

    if (res)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the array
// with odd sum is possible
class GFG {

    // Function to check if the
    // sum of the array can be made odd.
    static boolean isOdd(int []arr, int n)
    {
        int l, r, flag = 0, flag1 = 0, sum = 0;

        // Find sum of all elements and increment
        // check for odd or even elements in the array
        // so that by changing ai=aj,
        // the sum of the array can be made odd
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            if (arr[i] % 2 == 0 && flag == 0) {
                flag = 1;
                l = arr[i];
            }
            if (arr[i] % 2 != 0 && flag1 == 0) {
                r = arr[i];
                flag1 = 1;
            }
        }

        // If the sum is already odd
        if (sum % 2 != 0) {
            return true;
        }

        // Else, then both the flags should be checked.
        // Here, flag1 and flag represent if there is
        // an odd-even pair which can be replaced.
        else {
            if (flag1 == 1 && flag == 1)
                return true;
            else
                return false;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int ar[] = { 5, 4, 4, 5, 1, 3 };
        int n = ar.length;
        boolean res = isOdd(ar, n);

        if (res == true)
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to check if the array
# with odd sum is possible

# Function to check if the
# sum of the array can be made odd.
def isOdd(arr,  n) :
    flag = 0; flag1 = 0; sum = 0;

    # Find sum of all elements and increment
    # check for odd or even elements in the array
    # so that by changing ai=aj,
    # the sum of the array can be made odd
    for i in range(n) :
        sum += arr[i];
        if (arr[i] % 2 == 0 and flag == 0) :
            flag = 1;
            l = arr[i];

        if (arr[i] % 2 != 0 and flag1 == 0) :
            r = arr[i];
            flag1 = 1;

    # If the sum is already odd
    if (sum % 2 != 0) :
        return True;

    # Else, then both the flags should be checked.
    # Here, flag1 and flag represent if there is
    # an odd-even pair which can be replaced.
    else :
        if (flag1 == 1 and flag == 1) :
            return True;
        else :
            return False;

# Driver code
if __name__ == "__main__" :

    arr = [ 5, 4, 4, 5, 1, 3 ];
    n = len(arr);

    res = isOdd(arr, n);

    if (res) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to check if the array
// with odd sum is possible
using System;

class GFG{
    // Function to check if the
    // sum of the array can be made odd.
    static bool isOdd(int[] arr, int n)
    {
        int flag = 0, flag1 = 0, sum = 0;

        // Find sum of all elements and increment
        // check for odd or even elements in the array
        // so that by changing ai=aj,
        // the sum of the array can be made odd
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            if (arr[i] % 2 == 0 && flag == 0) {
                flag = 1;
            }
            if (arr[i] % 2 != 0 && flag1 == 0) {
                flag1 = 1;
            }
        }

        // If the sum is already odd
        if (sum % 2 != 0) {
            return true;
        }

        // Else, then both the flags should be checked.
        // Here, flag1 and flag represent if there is
        // an odd-even pair which can be replaced.
        else {
            if (flag1 == 1 && flag == 1)
                return true;
            else
                return false;
        }
    }

    // Driver code  
    static public void Main ()
    {
        int[] ar = { 5, 4, 4, 5, 1, 3 };
        int n = ar.Length;
        bool res = isOdd(ar, n);

        if (res)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by shivanisingh
```

## java 描述语言

```
<script>

// Javascript program to check if the array
// with odd sum is possible

    // Function to check if the
    // sum of the array can be made odd.
    function isOdd(arr, n)
    {
        let l, r, flag = 0, flag1 = 0, sum = 0;

        // Find sum of all elements and increment
        // check for odd or even elements in the array
        // so that by changing ai=aj,
        // the sum of the array can be made odd
        for (let i = 0; i < n; i++) {
            sum += arr[i];
            if (arr[i] % 2 == 0 && flag == 0) {
                flag = 1;
                l = arr[i];
            }
            if (arr[i] % 2 != 0 && flag1 == 0) {
                r = arr[i];
                flag1 = 1;
            }
        }

        // If the sum is already odd
        if (sum % 2 != 0) {
            return true;
        }

        // Else, then both the flags should be checked.
        // Here, flag1 and flag represent if there is
        // an odd-even pair which can be replaced.
        else {
            if (flag1 == 1 && flag == 1)
                return true;
            else
                return false;
        }
    }

// Driver Code

          let ar = [ 5, 4, 4, 5, 1, 3 ];
        let n = ar.length;
        let res = isOdd(ar, n);

        if (res == true)
            document.write("Yes");
        else
            document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)