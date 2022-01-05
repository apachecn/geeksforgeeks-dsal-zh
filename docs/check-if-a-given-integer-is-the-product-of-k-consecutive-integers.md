# 检查给定的整数是否是 K 个连续整数的乘积

> 原文:[https://www . geesforgeks . org/check-if-a-给定整数是 k 个连续整数的乘积/](https://www.geeksforgeeks.org/check-if-a-given-integer-is-the-product-of-k-consecutive-integers/)

给定两个正整数 **N** 和 **K** ，任务是检查给定的整数 **N** 是否可以表示为 **K** 连续整数的乘积。如果发现属实，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 210，K = 3
> **输出:**是
> **说明:** 210 可以表示为 5 * 6 * 7。
> 
> **输入:** N = 780，K = 4
> T3】输出:否

**方法:**给定的问题可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决。按照以下步骤解决问题:

*   初始化两个整数，比如 **Kthroot** 和**乘积**，分别存储整数 **N** 的[T5】K<sup>th</sup>T8】根和 **K** 的乘积。](https://www.geeksforgeeks.org/n-th-root-number/)
*   将**【1，K】**范围内整数的乘积存储在变量**乘积**中。
*   否则，[迭代范围](https://www.geeksforgeeks.org/python-program-to-print-all-positive-numbers-in-a-range/)**【2，Kthroot】**并执行以下步骤:
    *   如果产品价值等于 **N** ，则打印**“是”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   将产品价值更新为**(产品*(I+K–1))/(I–1)**。
*   完成上述步骤后，如果上述情况都不满足，则打印**“否”**为 **N** 不能表示为 **K** 连续整数的乘积。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be expressed
// as the product of K consecutive integers
string checkPro(int n, int k)
{
    double exp = 1.0 / k;

    // Stores the K-th root of N
    int KthRoot = (int)pow(n, exp);

    // Stores the product of K
    // consecutive integers
    int product = 1;

    // Traverse over the range [1, K]
    for(int i = 1; i < k + 1; i++)
    {

        // Update the product
        product = product * i;
    }

    // If product is N, then return "Yes"
    if (product == n)
        return "Yes";

    else
    {

        // Otherwise, traverse over
        // the range [2, Kthroot]
        for(int j = 2; j < KthRoot + 1; j++)
        {

            // Update the value of product
            product = product * (j + k - 1);
            product = product / (j - 1);

            // If product is equal to N
            if (product == n)
                return "Yes";
        } 
    }

    // Otherwise, return "No"
    return "No";
}

// Driver code
int main()
{
    int N = 210;
    int K = 3;

    cout << checkPro(N, K);

    return 0;
}

// This code is contributed by avijitmondal1998
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

  // Function to check if N can be expressed
  // as the product of K consecutive integers
  static String checkPro(int n, int k){

    double exp = 1.0 / k ;

    // Stores the K-th root of N
    int KthRoot = (int)Math.pow(n, exp);

    // Stores the product of K
    // consecutive integers
    int product = 1 ;

    // Traverse over the range [1, K]
    for (int i = 1; i < k + 1; i++){
      // Update the product
      product = product * i;
    }

    // If product is N, then return "Yes"
    if(product == n)
      return "Yes";

    else {
      // Otherwise, traverse over
      // the range [2, Kthroot]
      for (int j = 2; j < KthRoot + 1; j++) {

        // Update the value of product
        product = product * (j + k - 1) ;
        product = product / (j - 1) ;

        // If product is equal to N
        if(product == n)
          return "Yes" ;
      } 
    }

    // Otherwise, return "No"
    return "No" ;
  }

  // Driver Code
  public static void main (String[] args) {

    int N = 210;
    int K = 3;

    System.out.println(checkPro(N, K));
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if N can be expressed
# as the product of K consecutive integers
def checkPro(n, k):

    # Stores the K-th root of N
    KthRoot = int(n**(1 / k))

    # Stores the product of K
    # consecutive integers
    product = 1

    # Traverse over the range [1, K]
    for i in range(1, k + 1):

        # Update the product
        product = product * i

    print(product)
    # If product is N, then return "Yes"
    if(product == N):
        return ("Yes")

    # Otherwise, traverse over
    # the range [2, Kthroot]
    for i in range(2, KthRoot + 1):

        # Update the value of product
        product = product*(i + k-1)
        product = product/(i - 1)
        print(product)
        # If product is equal to N
        if(product == N):
            return ("Yes")

    # Otherwise, return "No"
    return ("No")

# Driver Code
N = 210
K = 3

# Function Call
print(checkPro(N, K))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if N can be expressed
// as the product of K consecutive integers
static string checkPro(int n, int k)
{
    double exp = 1.0 / k ;

    // Stores the K-th root of N
    int KthRoot = (int)Math.Pow(n, exp);

    // Stores the product of K
    // consecutive integers
    int product = 1 ;

    // Traverse over the range [1, K]
    for(int i = 1; i < k + 1; i++)
    {

        // Update the product
        product = product * i;
    }

    // If product is N, then return "Yes"
    if (product == n)
        return "Yes";

    else
    {

        // Otherwise, traverse over
        // the range [2, Kthroot]
        for(int j = 2; j < KthRoot + 1; j++)
        {

            // Update the value of product
            product = product * (j + k - 1);
            product = product / (j - 1);

            // If product is equal to N
            if (product == n)
                return "Yes";
        } 
    }

    // Otherwise, return "No"
    return "No";
}

// Driver Code
static public void Main()
{
    int N = 210;
    int K = 3;

    Console.WriteLine(checkPro(N, K));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to check if N can be expressed
    // as the product of K consecutive integers
    function checkPro(n , k) {

        var exp = 1.0 / k;

        // Stores the K-th root of N
        var KthRoot = parseInt( Math.pow(n, exp));

        // Stores the product of K
        // consecutive integers
        var product = 1;

        // Traverse over the range [1, K]
        for (i = 1; i < k + 1; i++) {

            // Update the product
            product = product * i;
        }

        // If product is N, then return "Yes"
        if (product == n)
            return "Yes";

        else {

            // Otherwise, traverse over
            // the range [2, Kthroot]
            for (j = 2; j < KthRoot + 1; j++) {

                // Update the value of product
                product = product * (j + k - 1);
                product = product / (j - 1);

                // If product is equal to N
                if (product == n)
                    return "Yes";
            }
        }

        // Otherwise, return "No"
        return "No";
    }

    // Driver Code

        var N = 210;
        var K = 3;

        document.write(checkPro(N, K));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(K+N<sup>(1/K)</sup>)*
***辅助空间:** O(1)*