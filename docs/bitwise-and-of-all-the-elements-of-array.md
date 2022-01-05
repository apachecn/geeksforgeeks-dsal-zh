# 数组所有元素的按位“与”

> 原文:[https://www . geeksforgeeks . org/数组元素的逐位与运算/](https://www.geeksforgeeks.org/bitwise-and-of-all-the-elements-of-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)， **arr[]** ，任务是找出数组所有元素的按位**和(& )** 。

**示例:**

> **输入:** arr[] = {1，3，5，9，11}
> **输出:** 1
> 
> **输入:** arr[] = {3，7，11，19，11 }
> T3】输出: 3

**方法:**思路是遍历所有数组元素，计算所有元素的逐位**和**，并打印得到的结果。

下面是上述方法的实现:

## C++14

```
// C++ program to find bitwise AND
// of all the elements in the array
#include <bits/stdc++.h>
using namespace std;

int find_and(int arr[], int len){

    // Initialise ans variable is arr[0]
    int ans = arr[0];

    // Traverse the array compute AND
    for (int i = 0; i < len; i++){
        ans = (ans&arr[i]);
    }
    // Return ans
    return ans;
}

// Driver function
int main()
{
    int arr[] = {1, 3, 5, 9, 11};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call to find AND
    cout << find_and(arr, n);
    return 0;
}

// This code is contributed by sapnasingh4991
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find bitwise AND
// of all the elements in the array
import java.util.*;
class GFG{
// Function to calculate bitwise AND
    static int find_and(int arr[]){

        // Initialise ans variable is arr[0]
        int ans = arr[0];

        // Traverse the array compute AND
        for (int i=0;i<arr.length;i++){
            ans = (ans&arr[i]);
        }
        // Return ans
        return ans;
    }   
    // Driver Code
    public static void main(String args[])
    {
        int arr[] = {1, 3, 5, 9, 11};

        // Function Call to find AND
        System.out.println(find_and(arr));
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python program to find bitwise AND
# of all the elements in the array

# Function to calculate bitwise AND
def find_and(arr):

    # Initialise ans variable is arr[0]
    ans = arr[0]

    # Traverse the array compute AND
    for i in range(1, len(arr)):
        ans = ans&arr[i]

    # Return ans
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [1, 3, 5, 9, 11]

    # Function Call to find AND
    print(find_and(arr))
```

## C#

```
// C# program to find bitwise AND
// of all the elements in the array
using System;
class GFG{
// Function to calculate bitwise AND
    static int find_and(int[] arr){

        // Initialise ans variable is arr[0]
        int ans = arr[0];

        // Traverse the array compute AND
        for (int i=0;i<arr.Length;i++){
            ans = (ans&arr[i]);
        }
        // Return ans
        return ans;
    }
    // Driver Code
    public static void Main()
    {
        int[] arr = {1, 3, 5, 9, 11};

        // Function Call to find AND
        Console.Write(find_and(arr));
    }
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// Javascript program to find bitwise AND
// of all the elements in the array

// Function to calculate bitwise AND
function find_and(arr)
{

    // Initialise ans variable is arr[0]
    let ans = arr[0];

    // Traverse the array compute AND
    for(let i = 0; i < arr.length; i++)
    {
        ans = (ans&arr[i]);
    }

    // Return ans
    return ans;
}

// Driver Code
let arr = [ 1, 3, 5, 9, 11 ];

// Function Call to find AND
document.write(find_and(arr));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
1
```