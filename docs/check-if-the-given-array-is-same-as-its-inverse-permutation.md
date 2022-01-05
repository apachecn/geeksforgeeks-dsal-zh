# 检查给定的数组是否与其逆排列相同

> 原文:[https://www . geeksforgeeks . org/check-如果给定数组与其逆排列相同/](https://www.geeksforgeeks.org/check-if-the-given-array-is-same-as-its-inverse-permutation/)

给定一个由范围**【1，N】**内的整数组成的数组 **arr[]** ，任务是确定给定数组的 [**逆置换**](https://www.geeksforgeeks.org/inverse-permutation/) 是否与给定数组相同。

> **逆置换**是通过将所有元素的位置插入到等于数组中该元素的相应值的位置而获得的置换。
> **插图:**
> arr[] = {2，4，1，3，5}
> 数组的逆排列将等于{3，1，4，2，5}

**示例:**

> **输入:** N = 4，arr[] = {1，4，3，2}
> **输出:**是
> **说明:**
> 给定数组的逆排列是{1，4，3，2}，与给定数组相同。
> **输入:** N = 5，arr[] = {2，3，4，5，1}
> **输出:**否
> **说明:**
> 给定数组的逆排列是{5，1，2，3，4}，与给定数组不一样。

**方法 1 :**

在这种方法中，我们将生成数组的**逆排列**，然后检查它是否与原始数组相同。

按照以下步骤解决问题:

*   求给定数组的**逆排列**。
*   检查生成的数组是否与原始数组相同。
*   如果两者相同，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to check if the inverse
// permutation of the given array is
// same as the original array
void inverseEqual(int arr[], int n)
{

    // Stores the inverse
    // permutation
    int brr[n];

    // Generate the inverse permutation
    for (int i = 0; i < n; i++) {
        int present_index = arr[i] - 1;
        brr[present_index] = i + 1;
    }

    // Check if the inverse permutation
    // is same as the given array
    for (int i = 0; i < n; i++) {
        if (arr[i] != brr[i]) {
            cout << "No" << endl;
            return;
        }
    }

    cout << "Yes" << endl;
}

// Driver Code
int main()
{

    int n = 4;
    int arr[n] = { 1, 4, 3, 2 };

    inverseEqual(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if the inverse
// permutation of the given array is
// same as the original array
static void inverseEqual(int arr[], int n)
{

    // Stores the inverse
    // permutation
    int[] brr = new int[n];

    // Generate the inverse permutation
    for(int i = 0; i < n; i++)
    {
        int present_index = arr[i] - 1;
        brr[present_index] = i + 1;
    }

    // Check if the inverse permutation
    // is same as the given array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] != brr[i])
        {
            System.out.println("No");
            return;
        }
    }
    System.out.println("Yes");
}

// Driver code
public static void main(String[] args)
{
    int n = 4;
    int[] arr = { 1, 4, 3, 2 };

    inverseEqual(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if the inverse
# permutation of the given array is
# same as the original array
def inverseEqual(arr, n):

    # Stores the inverse
    # permutation
    brr = [0] * n

    # Generate the inverse permutation
    for i in range(n):
        present_index = arr[i] - 1
        brr[present_index] = i + 1

    # Check if the inverse permutation
    # is same as the given array
    for i in range(n):
        if arr[i] != brr[i]:
            print("NO")
            return

    print("YES")

# Driver code
n = 4
arr = [ 1, 4, 3, 2 ]

inverseEqual(arr, n)

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to check if the inverse
// permutation of the given array is
// same as the original array
static void inverseEqual(int []arr, int n)
{

    // Stores the inverse
    // permutation
    int[] brr = new int[n];

    // Generate the inverse permutation
    for(int i = 0; i < n; i++)
    {
        int present_index = arr[i] - 1;
        brr[present_index] = i + 1;
    }

    // Check if the inverse permutation
    // is same as the given array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] != brr[i])
        {
            Console.WriteLine("No");
            return;
        }
    }
    Console.WriteLine("Yes");
}

// Driver code
public static void Main(String[] args)
{
    int n = 4;
    int[] arr = { 1, 4, 3, 2 };

    inverseEqual(arr, n);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to check if the inverse
// permutation of the given array is
// same as the original array
function inverseEqual(arr, n)
{

    // Stores the inverse
    // permutation
    var brr = Array(n).fill(0);

    // Generate the inverse permutation
    for (var i = 0; i < n; i++) {
        var present_index = arr[i] - 1;
        brr[present_index] = i + 1;
    }

    // Check if the inverse permutation
    // is same as the given array
    for (var i = 0; i < n; i++) {
        if (arr[i] != brr[i]) {
            document.write( "No" );
            return;
        }
    }

    document.write( "Yes" );
}

// Driver Code
var n = 4;
var arr = [ 1, 4, 3, 2 ];
inverseEqual(arr, n);

// This code is contributed by noob2000.
</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**方法二:**

在这种方法中，我们逐个获取元素并检查元素**在(arr[i] -1)索引 i+1 处是否存在**。如果不是，则给定数组的**逆排列**与该数组不同。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the inverse
// permutation of the given array is
// same as the original array
bool inverseEqual(int arr[], int n)
{

    // Check the if inverse permutation is not same
    for (int i = 0; i < n; i++)
        if (arr[arr[i] - 1] != i + 1)
            return false;

    return true;
}

// Driver Code
int main()
{
    int n = 4;
    int arr[n] = { 1, 4, 3, 2 };

    // Function Call
    cout << (inverseEqual(arr, n) ? "Yes" : "No");

    return 0;
}
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if the inverse
// permutation of the given array is
// same as the original array
function inverseEqual(arr, n)
{

    // Check the if inverse permutation
    // is not same
    for (let i = 0; i < n; i++)
        if (arr[arr[i] - 1] != i + 1)
            return false;

    return true;
}

    // Driver Code

    let n = 4;
    let arr = [ 1, 4, 3, 2 ];

    // Function Call
    document.write(inverseEqual(arr, n) ? "Yes" : "No");

</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(N)

**辅助空间:** O(1)