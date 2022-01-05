# 检查整数数组的异或是偶数还是奇数

> 原文:[https://www . geesforgeks . org/检查整数数组的异或是偶数还是奇数/](https://www.geeksforgeeks.org/check-if-the-xor-of-an-array-of-integers-is-even-or-odd/)

给定一个包含大小为 **N** 的整数的数组 **arr** ，任务是检查这个数组的[异或](https://www.geeksforgeeks.org/tag/xor/)是偶数还是奇数

**示例**:

> **输入:** arr[] = { 2，4，7}
> **输出:**奇数
> **解释:**
> 数组的 xor = 2 ^ 4 ^ 7 = 1，哪个是奇数
> 
> **输入:** arr[] = { 3，9，12，13，15 }
> 输出:偶数

**天真解:**先求给定整数数组的 XOR，然后检查这个 XOR 是偶数还是奇数。

***时间复杂度:** O(N)*

**高效解决方案:**更好的解决方案基于[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)事实，即:

*   [任意两个偶数或任意两个奇数的逐位异或](https://www.geeksforgeeks.org/tag/xor/)始终为**偶数**。
*   [一个偶数和一个奇数的逐位异或](https://www.geeksforgeeks.org/tag/xor/)是**总是奇数**。

因此如果数组中奇数的[计数是奇数，那么最终的异或将是奇数，如果是偶数，那么最终的异或将是偶数。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

下面是上述方法的实现:

## C++

```
// C++ program to check if the XOR
// of an array is Even or Odd

#include <bits/stdc++.h>
using namespace std;

// Function to check if the XOR of
// an array of integers is Even or Odd
string check(int arr[], int n)
{
    int count = 0;

    for (int i = 0; i < n; i++) {

        // Count the number
        // of odd elements
        if (arr[i] & 1)
            count++;
    }

    // If count of odd elements
    // is odd, then XOR will be odd
    if (count & 1)
        return "Odd";

    // Else even
    else
        return "Even";
}

// Driver Code
int main()
{
    int arr[] = { 3, 9, 12, 13, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << check(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the XOR
// of an array is Even or Odd
import java.util.*;

class GFG{

// Function to check if the XOR of
// an array of integers is Even or Odd
static String check(int []arr, int n)
{
    int count = 0;

    for (int i = 0; i < n; i++) {

        // Count the number
        // of odd elements
        if ((arr[i] & 1)!=0)
            count++;
    }

    // If count of odd elements
    // is odd, then XOR will be odd
    if ((count & 1)!=0)
        return "Odd";

    // Else even
    else
        return "Even";
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 3, 9, 12, 13, 15 };
    int n = arr.length;

    // Function call
    System.out.println(check(arr, n));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to check if the XOR
# of an array is Even or Odd

# Function to check if the XOR of
# an array of integers is Even or Odd
def check(arr, n):
    count = 0;

    for i in range(n):

        # Count the number
        # of odd elements
        if (arr[i] & 1):
            count = count + 1;

    # If count of odd elements
    # is odd, then XOR will be odd
    if (count & 1):
        return "Odd";

    # Else even
    else:
        return "Even";

# Driver Code
if __name__=='__main__':

    arr = [ 3, 9, 12, 13, 15 ]
    n = len(arr)

    # Function call
    print(check(arr, n))

# This code is contributed by Princi Singh
```

## C#

```
// C# program to check if the XOR
// of an array is Even or Odd
using System;
using System.Collections.Generic;
using System.Linq;

class GFG
{

// Function to check if the XOR of
// an array of integers is Even or Odd
static String check(int []arr, int n)
{
    int count = 0;

    for (int i = 0; i < n; i++) {

        // Count the number
        // of odd elements
        if (arr[i] == 1)
            count++;
    }

    // If count of odd elements
    // is odd, then XOR will be odd
    if (count == 1)
        return "Odd";

    // Else even
    else
        return "Even";
}

// Driver Code
    public static void Main(String[] args)
    {
    int []arr= { 3, 9, 12, 13, 15 };
    int n = arr.Length;

    // Function call
    Console.Write(check(arr, n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program to check if the XOR
// of an array is Even or Odd

// Function to check if the XOR of
// an array of integers is Even or Odd
function check(arr, n)
{
    let count = 0;

    for(let i = 0; i < n; i++)
    {

        // Count the number
        // of odd elements
        if (arr[i] & 1)
            count++;
    }

    // If count of odd elements
    // is odd, then XOR will be odd
    if (count & 1)
        return "Odd";

    // Else even
    else
        return "Even";
}

// Driver Code
let arr = [ 3, 9, 12, 13, 15 ];
let n = arr.length;

// Function call
document.write(check(arr, n));

// This code is contributed by subham348

</script>
```

**Output:** 

```
Even
```

***时间复杂度** : O(N)*
**辅助空间:** O(1)