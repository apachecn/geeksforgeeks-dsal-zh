# 将数组中丑陋的数字按其相对位置排序

> 原文:[https://www . geeksforgeeks . org/sort-丑八怪-相对位置数组中的数字/](https://www.geeksforgeeks.org/sort-ugly-numbers-in-an-array-at-their-relative-positions/)

给定一个整数数组 **arr[]** ，任务是只对那些在数组中相对位置为难看数字的元素进行排序(其他元素的位置不得受到影响)。
丑陋的数字是唯一质因数为 **2** 、 **3** 或 **5** 的数字。
顺序 **1、2、3、4、5、6、8、9、10、12、15、…..**显示前几个难看的数字。按照惯例，包括 1。
**示例:**

> **输入:** arr[] = {13，9，11，3，2}
> 输出: 13 2 11 3 9
> 9，3 和 2 是给定数组中唯一难看的数字。
> **输入:** arr[] = {1，2，3，7，12，10}
> **输出:** 1 2 3 7 10 12

**进场:**

*   开始遍历数组，对于每个元素 **arr[i]** ，如果 **arr[i]** 是一个丑陋的数字，那么将其存储在[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)中，并更新 **arr[i] = -1**
*   所有难看的数字都存储在数组列表中后，[对更新后的数组列表进行排序](https://www.geeksforgeeks.org/quick-sort-vs-merge-sort/)。
*   再次遍历数组，对于每个元素，
    *   如果 **arr[i] = -1** ，那么打印数组列表中之前没有打印过的第一个元素。
    *   否则，打印 **arr[i]** 。

以下是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function that returns true if n is an ugly number
bool isUgly(int n)
{
    // While divisible by 2, keep dividing
    while (n % 2 == 0)
        n = n / 2;

    // While divisible by 3, keep dividing
    while (n % 3 == 0)
        n = n / 3;

    // While divisible by 5, keep dividing
    while (n % 5 == 0)
        n = n / 5;

    // n must be 1 if it was ugly
    if (n == 1)
        return true;
    return false;
}

// Function to sort ugly numbers
// in their relative positions
void sortUglyNumbers(int arr[], int n)
{

    // To store the ugly numbers from the array
    vector<int> list;

    int i;
    for (i = 0; i < n; i++)
    {

        // If current element is an ugly number
        if (isUgly(arr[i]))
        {

            // Add it to the ArrayList
            // and set arr[i] to -1
            list.push_back(arr[i]);
            arr[i] = -1;
        }
    }

    // Sort the ugly numbers
    sort(list.begin(),list.end());

    int j = 0;
    for (i = 0; i < n; i++)
    {

        // Position of an ugly number
        if (arr[i] == -1)
            cout << list[j++] << " ";
        else
            cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 7, 12, 10 };
    int n = sizeof(arr)/sizeof(arr[0]);
    sortUglyNumbers(arr, n);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.Collections;

class GFG {

    // Function that returns true if n is an ugly number
    static boolean isUgly(int n)
    {
        // While divisible by 2, keep dividing
        while (n % 2 == 0)
            n = n / 2;

        // While divisible by 3, keep dividing
        while (n % 3 == 0)
            n = n / 3;

        // While divisible by 5, keep dividing
        while (n % 5 == 0)
            n = n / 5;

        // n must be 1 if it was ugly
        if (n == 1)
            return true;
        return false;
    }

    // Function to sort ugly numbers
    // in their relative positions
    static void sortUglyNumbers(int arr[], int n)
    {

        // To store the ugly numbers from the array
        ArrayList<Integer> list = new ArrayList<>();

        int i;
        for (i = 0; i < n; i++) {

            // If current element is an ugly number
            if (isUgly(arr[i])) {

                // Add it to the ArrayList
                // and set arr[i] to -1
                list.add(arr[i]);
                arr[i] = -1;
            }
        }

        // Sort the ugly numbers
        Collections.sort(list);

        int j = 0;
        for (i = 0; i < n; i++) {

            // Position of an ugly number
            if (arr[i] == -1)
                System.out.print(list.get(j++) + " ");
            else
                System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 7, 12, 10 };
        int n = arr.length;
        sortUglyNumbers(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if n is an ugly number
def isUgly(n):

    # While divisible by 2, keep dividing
    while n % 2 == 0:
        n = n // 2

    # While divisible by 3, keep dividing
    while n % 3 == 0:
        n = n // 3

    # While divisible by 5, keep dividing
    while n % 5 == 0:
        n = n // 5

    # n must be 1 if it was ugly
    if n == 1:
        return True
    return False

# Function to sort ugly numbers
# in their relative positions
def sortUglyNumbers(arr, n):

    # To store the ugly numbers from the array
    list = []

    for i in range(0, n):

        # If current element is an ugly number
        if isUgly(arr[i]):

            # Add it to the ArrayList
            # and set arr[i] to -1
            list.append(arr[i])
            arr[i] = -1

    # Sort the ugly numbers
    list.sort()

    j = 0
    for i in range(0, n):

        # Position of an ugly number
        if arr[i] == -1:
            print(list[j], end = " ")
            j += 1
        else:
            print(arr[i], end = " ")

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 3, 7, 12, 10]
    n = len(arr)
    sortUglyNumbers(arr, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function that returns true
    // if n is an ugly number
    static bool isUgly(int n)
    {
        // While divisible by 2, keep dividing
        while (n % 2 == 0)
            n = n / 2;

        // While divisible by 3, keep dividing
        while (n % 3 == 0)
            n = n / 3;

        // While divisible by 5, keep dividing
        while (n % 5 == 0)
            n = n / 5;

        // n must be 1 if it was ugly
        if (n == 1)
            return true;
        return false;
    }

    // Function to sort ugly numbers
    // in their relative positions
    static void sortUglyNumbers(int []arr, int n)
    {

        // To store the ugly numbers from the array
        List<int> list = new List<int>();

        int i;
        for (i = 0; i < n; i++)
        {

            // If current element is an ugly number
            if (isUgly(arr[i]))
            {

                // Add it to the ArrayList
                // and set arr[i] to -1
                list.Add(arr[i]);
                arr[i] = -1;
            }
        }

        // Sort the ugly numbers
        list.Sort();

        int j = 0;
        for (i = 0; i < n; i++)
        {

            // Position of an ugly number
            if (arr[i] == -1)
                Console.Write(list[j++] + " ");
            else
                Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 3, 7, 12, 10 };
        int n = arr.Length;
        sortUglyNumbers(arr, n);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if n is an ugly number
function isUgly(n)
{
    // While divisible by 2, keep dividing
    while (n % 2 == 0)
        n = n / 2;

    // While divisible by 3, keep dividing
    while (n % 3 == 0)
        n = n / 3;

    // While divisible by 5, keep dividing
    while (n % 5 == 0)
        n = n / 5;

    // n must be 1 if it was ugly
    if (n == 1)
        return true;
    return false;
}

// Function to sort ugly numbers
// in their relative positions
function sortUglyNumbers(arr, n)
{

    // To store the ugly numbers from the array
    var list = [];

    var i;
    for (i = 0; i < n; i++)
    {

        // If current element is an ugly number
        if (isUgly(arr[i]))
        {

            // Add it to the ArrayList
            // and set arr[i] to -1
            list.push(arr[i]);
            arr[i] = -1;
        }
    }

    // Sort the ugly numbers
    list.sort((a,b)=>a-b);

    var j = 0;
    for (i = 0; i < n; i++)
    {

        // Position of an ugly number
        if (arr[i] == -1)
            document.write( list[j++] + " ");
        else
            document.write( arr[i] + " ");
    }
}

// Driver code
var arr = [1, 2, 3, 7, 12, 10 ];
var n = arr.length;
sortUglyNumbers(arr, n);

</script>
```

**Output:** 

```
1 2 3 7 10 12
```