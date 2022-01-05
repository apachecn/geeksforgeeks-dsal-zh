# 检查数组所有元素的和与异或是否相等

> 原文:[https://www . geeksforgeeks . org/检查数组中所有元素的和与异或是否相等/](https://www.geeksforgeeks.org/check-if-sum-and-xor-of-all-elements-of-array-is-equal/)

给定一个数组 **arr[]** ，任务是检查一个数组所有元素的和是否等于数组所有元素的异或。
**例:**

> **输入:**arr[]=【1，2】
> **输出:** YES
> **解释:**
> sum =(1+2)= 3
> xor =(1^2)= 3
> **输入:**arr[]=【6，3，7，10】
> **输出:** NO
> **解释:**
> sum =(6+3+7+14)

**进场:**

1.  迭代数组，找到所有元素的和。
2.  同样，对数组的所有元素进行异或运算。
3.  检查和与异或值是否相等。

以下是上述方法的实现:

## C++

```
// C++ Implementation to Check
// if Sum and XOR of all Elements
// of Array is equal
#include <iostream>
using namespace std;

// Function to Check if Sum and XOR
// of all elements of array is equal
int equal_xor_sum(int arr[], int n)
{
    int Sum = 0;
    int Xor = 0;

    // Sum and XOR of all elements
    for (int i = 0; i < n; i++) {
        Sum = Sum + arr[i];
        Xor = Xor ^ arr[i];
    }

    // Checking Sum and XOR to be equal
    if (Sum == Xor)
        cout << "YES";
    else
        cout << "NO";

    return 0;
}

// Driver Function
int main()
{
    int arr[] = { 6, 3, 7, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Check Sum and XOR is equal
    equal_xor_sum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation to Check
// if Sum and XOR of all Elements
// of Array is equal
class GFG
{

    // Function to Check if Sum and XOR
    // of all elements of array is equal
    static void equal_xor_sum(int arr[], int n)
    {
        int Sum = 0;
        int Xor = 0;

        // Sum and XOR of all elements
        for (int i = 0; i < n; i++)
        {
            Sum = Sum + arr[i];
            Xor = Xor ^ arr[i];
        }

        // Checking Sum and XOR to be equal
        if (Sum == Xor)
            System.out.println("YES");
        else
            System.out.println("NO");

    }

    // Driver Function
    public static void main (String[] args)
    {
        int arr[] = { 6, 3, 7, 10 };
        int n = arr.length;

        // Check Sum and XOR is equal
        equal_xor_sum(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 Implementation to Check
# if Sum and XOR of all Elements
# of Array is equal

# Function to Check if Sum and XOR
# of all elements of array is equal
def equal_xor_sum(arr, n) :

    Sum = 0;
    Xor = 0;

    # Sum and XOR of all elements
    for i in range(n) :
        Sum = Sum + arr[i];
        Xor = Xor ^ arr[i];

    # Checking Sum and XOR to be equal
    if (Sum == Xor) :
        print("YES");
    else :
        print("NO");

# Driver Function
if __name__ == "__main__" :

    arr = [ 6, 3, 7, 10 ];
    n = len(arr);

    # Check Sum and XOR is equal
    equal_xor_sum(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# Implementation to Check
// if Sum and XOR of all Elements
// of Array is equal
using System;

class GFG
{

    // Function to Check if Sum and XOR
    // of all elements of array is equal
    static void equal_xor_sum(int []arr, int n)
    {
        int Sum = 0;
        int Xor = 0;

        // Sum and XOR of all elements
        for (int i = 0; i < n; i++)
        {
            Sum = Sum + arr[i];
            Xor = Xor ^ arr[i];
        }

        // Checking Sum and XOR to be equal
        if (Sum == Xor)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");

    }

    // Driver Function
    public static void Main()
    {
        int []arr = { 6, 3, 7, 10 };
        int n = arr.Length;

        // Check Sum and XOR is equal
        equal_xor_sum(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript Implementation to Check
// if Sum and XOR of all Elements
// of Array is equal

// Function to Check if Sum and XOR
// of all elements of array is equal
function equal_xor_sum(arr, n)
{
    let Sum = 0;
    let Xor = 0;

    // Sum and XOR of all elements
    for (let i = 0; i < n; i++) {
        Sum = Sum + arr[i];
        Xor = Xor ^ arr[i];
    }

    // Checking Sum and XOR to be equal
    if (Sum === Xor)
        document.write("YES");
    else
        document.write("NO");

}

// Driver Function

    let arr = [ 6, 3, 7, 10 ];
    let n = arr.length;

    // Check Sum and XOR is equal
    equal_xor_sum(arr, n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
NO
```

**时间复杂度:** O(n)