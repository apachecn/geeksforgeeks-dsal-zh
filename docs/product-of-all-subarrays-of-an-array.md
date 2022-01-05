# 一个阵列的所有子阵列的乘积

> 原文:[https://www . geeksforgeeks . org/全阵列子阵列产品/](https://www.geeksforgeeks.org/product-of-all-subarrays-of-an-array/)

给定一个整数数组 **arr** 的大小 **N** ，任务是打印数组的所有[子数组的产品。](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)

**示例:**

> **输入:** arr[] = {2，4 }
> T3】输出: 64
> 这里，子阵是【2】、【2，4】、【4】
> 积是所有子阵的 2，8，4
> 积= 64
> 
> **输入:** arr[] = {10，3，7}
> **输出:** 27783000
> 这里，子阵是[10]，[10，3]，[10，3，7]，[3，7]，[7]
> 产品是所有子阵的 10，30，210，3，21，7
> 产品= 27783000

**天真方法:**一个简单的解决方案是[生成所有子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并计算它们的乘积。

## C++

```
// C++ program to find product
// of all subarray of an array

#include <bits/stdc++.h>
using namespace std;

// Function to find product of all subarrays
void product_subarrays(int arr[], int n)
{
    // Variable to store the product
    int product = 1;

    // Compute the product while
    // traversing for subarrays
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            for (int k = i; k <= j; k++)
                product *= arr[k];
        }
    }

    // Printing product of all subarray
    cout << product << "\n";
}

// Driver code
int main()
{
    int arr[] = { 10, 3, 7 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    product_subarrays(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product
// of all subarray of an array
import java.util.*;

class GFG {

    // Function to find product of all subarrays
    static void product_subarrays(int arr[], int n)
    {

        // Variable to store the product
        int product = 1;

        // Compute the product while
        // traversing for subarrays
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                for (int k = i; k <= j; k++)
                    product *= arr[k];
            }
        }

        // Printing product of all subarray
        System.out.print(product + "\n");
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 10, 3, 7 };
        int n = arr.length;

        // Function call
        product_subarrays(arr, n);
    }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to find product
# of all subarray of an array

# Function to find product of all subarrays
def product_subarrays(arr, n):

    # Variable to store the product
    product = 1;

    # Compute the product while
    # traversing for subarrays
    for i in range(0, n):
        for j in range(i, n):
            for k in range(i, j + 1):
                product *= arr[k];

    # Printing product of all subarray
    print(product, "\n");

# Driver code
arr = [ 10, 3, 7 ];

n = len(arr);

# Function call
product_subarrays(arr, n);

# This code is contributed by Code_Mech
```

## C#

```
// C# program to find product
// of all subarray of an array
using System;

class GFG {

    // Function to find product of all subarrays
    static void product_subarrays(int[] arr, int n)
    {

        // Variable to store the product
        int product = 1;

        // Compute the product while
        // traversing for subarrays
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                for (int k = i; k <= j; k++)
                    product *= arr[k];
            }
        }

        // Printing product of all subarray
        Console.Write(product + "\n");
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 10, 3, 7 };
        int n = arr.Length;

        // Function call
        product_subarrays(arr, n);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
  // Javascript program to find product
  // of all subarray of an array

  // Function to find product of all subarrays
  function product_subarrays(arr, n)
  {

      // Variable to store the product
      let product = 1;

      // Compute the product while
      // traversing for subarrays
      for (let i = 0; i < n; i++) {
          for (let j = i; j < n; j++) {
              for (let k = i; k <= j; k++)
                  product *= arr[k];
          }
      }

      // Printing product of all subarray
      document.write(product + "</br>");
  }

  let arr = [ 10, 3, 7 ];
  let n = arr.length;

  // Function call
  product_subarrays(arr, n);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
27783000
```

时间复杂度:O(n <sup>3</sup> )

辅助空间:0(1)

**有效方法:**一种有效方法是使用两个循环并在遍历子阵列时计算乘积。
以下是上述办法的实施情况:

## C++

```
// C++ program to find product
// of all subarray of an array

#include <bits/stdc++.h>
using namespace std;

// Function to find product of all subarrays
void product_subarrays(long long int arr[], int n)
{
    // Variable to store the product
    long long int res = 1;

    // Compute the product while
    // traversing for subarrays
    for (int i = 0; i < n; i++) {
        long long int product = 1;
        for (int j = i; j < n; j++) {
            product = product * arr[j];
            res *= product;
        }
    }
    // Printing product of all subarray
    cout << res << "\n";
}

// Driver code
int main()
{
    long long int arr[] = { 10, 3, 7 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    product_subarrays(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product
// of all subarray of an array
import java.util.*;

class GFG {

    // Function to find product of all subarrays
    static void product_subarrays(int arr[], int n)
    {
        // Variable to store the product
        int res = 1;

        // Compute the product while
        // traversing for subarrays
        for (int i = 0; i < n; i++) {
            int product = 1;
            for (int j = i; j < n; j++) {
                product = product * arr[j];
                res *= product;
            }
        }

        // Printing product of all subarray
        System.out.println(res + "\n");
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 10, 3, 7 };

        int n = arr.length;

        // Function call
        product_subarrays(arr, n);
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 program to find product
# of all subarray of an array

# Function to find product of all subarrays
def product_subarrays(arr, n):

    # Variable to store the product
    res = 1;

    # Compute the product while
    # traversing for subarrays
    for i in range(n):
        product = 1
        for j in range(i, n):
            product *= arr[j];
            res = res * product

    # Printing product of all subarray
    print(res);

# Driver code
if __name__ == '__main__':
    arr = [ 10, 3, 7 ];

    n = len(arr);

    # Function call
    product_subarrays(arr, n);

# This code is contributed by Princi Singh
```

## C#

```
// C# program to find product
// of all subarray of an array
using System;

class GFG {

    // Function to find product of all subarrays
    static void product_subarrays(int[] arr, int n)
    {
        // Variable to store the product
        int res = 1;

        // Compute the product while
        // traversing for subarrays
        for (int i = 0; i < n; i++) {
            int product = 1;
            for (int j = i; j < n; j++) {
                product *= arr[j];
                res = res * product;
            }
        }

        // Printing product of all subarray
        Console.WriteLine(res + "\n");
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 10, 3, 7 };

        int n = arr.Length;

        // Function call
        product_subarrays(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find product
// of all subarray of an array

// Function to find product of all subarrays
function product_subarrays(arr, n)
{
    // Variable to store the product
    var res = 1;

    // Compute the product while
    // traversing for subarrays
    for (var i = 0; i < n; i++) {
        var product = 1;
        for (var j = i; j < n; j++) {
            product = product * arr[j];
            res *= product;
        }
    }
    // Printing product of all subarray
    document.write( res );
}

// Driver code
var arr = [10, 3, 7];
var n = arr.length;
// Function call
product_subarrays(arr, n);

</script>
```

**Output:** 

```
27783000
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:0(1)