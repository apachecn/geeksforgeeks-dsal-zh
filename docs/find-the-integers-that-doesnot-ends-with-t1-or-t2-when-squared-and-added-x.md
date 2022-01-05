# 求平方加 X 时不以 T1 或 T2 结尾的整数

> 原文:[https://www . geesforgeks . org/find-the-integers-not-end-with-T1-or-T2-when-squared-and-add-x/](https://www.geeksforgeeks.org/find-the-integers-that-doesnot-ends-with-t1-or-t2-when-squared-and-added-x/)

给定一组 **N 个**整数。给定两个一位数的数字 T1 和 T2 以及一个数字 X。任务是找出其中不以 **T1** 或 **T2** 结束的整数，当它们被平方并且 **X** 被加到它们上面时。如果没有这样的整数，打印 **-1** 。
**举例:**

> **输入:** N = 4，arr[] = {3，1，4，7} X = 10，T1 = 5，T2 = 6
> **输出:** 19 11 59
> **解释:**
> 的修改值 **3** 为 **19** (3^2 + 10)。
> **1**的修正值为 **11** (1^2 + 10)。
> **4**的修正值为 **26** (4^2 + 10)。
> 7 的修正值为 **59** (7^2 + 10)。
> 不以 **5** 或 **6**
> 结尾的修改值为 **19、11、59** 。
> 因此输出为 **19 11 59** 。
> **输入:** N = 4，arr[] = {2，18，22，8} X = 2，T1 = 5，T2 = 6
> **输出:** -1
> **解释:**
> 的修改值 **2** 为 **6** (2^2 + 2)。
> 18 的修正值为 **326** (18^2 + 2)。
> **22**的修正值为 **486** (22^2 + 2)。
> **8**的修正值为 **66** (8^2 + 2)。
> As，没有以 **5** 或 **6** 结尾的修改值
> 。
> 因此输出为 **-1** 。

**进场:**

*   初始化一个布尔变量**标志**为**真**。
*   遍历数组中的元素**a【n】**。
*   将 **X** 和【I】的**平方之和存储在变量 **temp** 中。**
*   检查**温度**的最后一位数字是不是既不是 **T1** 也不是 **T2** 。
*   如果**是**，则打印**温度**中的值，并将**标志**更改为**假**。
*   遍历完数组**中的所有元素后，如果****标志**为**真**，则打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ program to find the integers
// that ends with either T1 or T2
// when squared and added X

#include <bits/stdc++.h>
using namespace std;

// Function to print the elements
// Not ending with T1 or T2
void findIntegers(int n, int a[],
                   int x, int t1, int t2)
{

    // Flag to check if none of the elements
    // Do not end with t1 or t2
    bool flag = true;

    // Traverse through all the elements
    for (int i = 0; i < n; i++) {

        // Temporary variable to store the value
        int temp = pow(a[i], 2) + x;

        // If the last digit is neither t1
        // nor t2 then
        if (temp % 10 != t1 && temp % 10 != t2) {

            // Print the number
            cout << temp << " ";

            // Set the flag as False
            flag = false;
        }
    }

    // If none of the elements
    // meets the specification
    if (flag)
        cout << "-1";
}

// Driver Code
int main()
{
    // Test case 1
    int N = 4, X = 10, T1 = 5, T2 = 6;
    int a[N] = { 3, 1, 4, 7 };

    // Call the function
    findIntegers(N, a, X, T1, T2);
    cout << endl;

    // Test case 2
    N = 4, X = 2, T1 = 5, T2 = 6;
    int b[N] = { 2, 18, 22, 8 };

    // Call the function
    findIntegers(N, b, X, T1, T2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the integers
// that ends with either T1 or T2
// when squared and added X
class GFG
{

    // Function to print the elements
    // Not ending with T1 or T2
    static void findIntegers(int n, int a[],
                             int x, int t1, int t2)
    {

        // Flag to check if none of the elements
        // Do not end with t1 or t2
        boolean flag = true;

        // Traverse through all the elements
        for (int i = 0; i < n; i++)
        {

            // Temporary variable to store the value
            int temp = (int)Math.pow(a[i], 2) + x;

            // If the last digit is neither t1
            // nor t2 then
            if (temp % 10 != t1 && temp % 10 != t2)
            {

                // Print the number
                System.out.print(temp + " ");

                // Set the flag as False
                flag = false;
            }
        }

        // If none of the elements
        // meets the specification
        if (flag)
        {
            System.out.println();
            System.out.print("-1");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        // Test case 1
        int N = 4;
        int X = 10;
        int T1 = 5;
        int T2 = 6;
        int a[] = { 3, 1, 4, 7 };

        // Call the function
        findIntegers(N, a, X, T1, T2);

        // Test case 2
        N = 4; X = 2; T1 = 5; T2 = 6;
        int b[] = { 2, 18, 22, 8 };

        // Call the function
        findIntegers(N, b, X, T1, T2);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the integers
# that ends with either T1 or T2
# when squared and added X

# Function to print the elements
# Not ending with T1 or T2
def findIntegers(n, a, x, t1, t2):

    # Flag to check if none of the elements
    # Do not end with t1 or t2
    flag = True

    # Traverse through all the elements
    for i in range(n):

        # Temporary variable to store the value
        temp = pow(a[i], 2) + x

        # If the last digit is neither t1
        # nor t2 then
        if(temp % 10 != t1 and
           temp % 10 != t2):

            # Print the number
            print(temp, end = " ")

            # Set the flag as False
            flag = False

    # If none of the elements
    # meets the specification
    if flag:
        print(-1)

# Driver Code

# Test case 1
N , X , T1 , T2 = 4 , 10 , 5 , 6
a = [ 3, 1, 4, 7 ]

# Call the function
findIntegers(N, a, X, T1, T2);
print()

# Test case 2
N , X , T1 , T2 = 4 , 2 , 5 , 6
b = [ 2, 18, 22, 8 ]

# Call the function
findIntegers(N, b, X, T1, T2)

# This code is contributed by divyamohan123
```

## C#

```
// C# program to find the integers
// that ends with either T1 or T2
// when squared and added X
using System;

class GFG
{

    // Function to print the elements
    // Not ending with T1 or T2
    static void findIntegers(int n, int []a,
                             int x, int t1, int t2)
    {

        // Flag to check if none of the elements
        // Do not end with t1 or t2
        bool flag = true;

        // Traverse through all the elements
        for (int i = 0; i < n; i++)
        {

            // Temporary variable to store the value
            int temp = (int)Math.Pow(a[i], 2) + x;

            // If the last digit is neither t1
            // nor t2 then
            if (temp % 10 != t1 &&
                temp % 10 != t2)
            {

                // Print the number
                Console.Write(temp + " ");

                // Set the flag as False
                flag = false;
            }
        }

        // If none of the elements
        // meets the specification
        if (flag)
        {
            Console.WriteLine();
            Console.Write("-1");
        }
    }

    // Driver Code
    public static void Main(String []args)
    {
        // Test case 1
        int N = 4;
        int X = 10;
        int T1 = 5;
        int T2 = 6;
        int []a = { 3, 1, 4, 7 };

        // Call the function
        findIntegers(N, a, X, T1, T2);

        // Test case 2
        N = 4; X = 2; T1 = 5; T2 = 6;
        int []b = { 2, 18, 22, 8 };

        // Call the function
        findIntegers(N, b, X, T1, T2);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find the integers
// that ends with either T1 or T2
// when squared and added X

// Function to print the elements
// Not ending with T1 or T2
function findIntegers(n, a, x, t1, t2)
{

    // Flag to check if none of the elements
    // Do not end with t1 or t2
    let flag = true;

    // Traverse through all the elements
    for (let i = 0; i < n; i++) {

        // Temporary variable to store the value
        let temp = Math.pow(a[i], 2) + x;

        // If the last digit is neither t1
        // nor t2 then
        if (temp % 10 != t1 && temp % 10 != t2) {

            // Print the number
            document.write(temp + " ");

            // Set the flag as False
            flag = false;
        }
    }

    // If none of the elements
    // meets the specification
    if (flag)
        document.write("-1");
}

// Driver Code
    // Test case 1
    let N = 4, X = 10, T1 = 5, T2 = 6;
    let a = [ 3, 1, 4, 7 ];

    // Call the function
    findIntegers(N, a, X, T1, T2);
    document.write("<br>");

    // Test case 2
    N = 4, X = 2, T1 = 5, T2 = 6;
    let b = [ 2, 18, 22, 8 ];

    // Call the function
    findIntegers(N, b, X, T1, T2);

</script>
```

**Output:** 

```
19 11 59 
-1
```