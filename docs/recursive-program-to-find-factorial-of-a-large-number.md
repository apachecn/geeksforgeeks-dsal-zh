# 求大数阶乘的递归程序

> 原文:[https://www . geesforgeks . org/递归程序查找大数阶乘/](https://www.geeksforgeeks.org/recursive-program-to-find-factorial-of-a-large-number/)

给定一个大数 **N** ，任务是使用[递归](http://www.geeksforgeeks.org/recursion/)求 **N** 的阶乘。

> [非负整数的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)是所有小于或等于 n 的整数的乘积，例如 6 的阶乘是 6*5*4*3*2*1，是 720。

**示例:**

> **输入:** N = 100
> **输出:**933262154439441526816992388562667004-907159682643816214685929638952175999-93291560841463976 1565182866
> 
> **输入:**N = 50
> T3】输出:3041409320171337804361260816606476884-4377641568960512000000000000

**迭代方法:**本文的[第 1 集讨论了迭代方法。这里，我们已经讨论了递归方法。](https://www.geeksforgeeks.org/factorial-large-number/)

**递归方法:**为了递归地解决这个问题，算法改变了递归调用同一个函数[的方式](https://www.geeksforgeeks.org/recursion/)并将结果乘以数字 **n.** 按照下面的步骤解决问题:

*   如果 **n** 小于或等于 **2、**，则将 **n** 乘以 **1** ，并将结果存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。
*   否则，调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **相乘(n，阶乘递归算法(n–1))**找到答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// MUltiply the number x with the number
// represented by res array
vector<int> multiply(long int n, vector<int> digits)
{

    // Initialize carry
    long int carry = 0;

    // One by one multiply n with
    // individual digits of res[]
    for (long int i = 0; i < digits.size(); i++) {
        long int result
          = digits[i] * n + carry;

        // Store last digit of 'prod' in res[]
        digits[i] = result % 10;

        // Put rest in carry
        carry = result / 10;
    }

    // Put carry in res and increase result size
    while (carry) {
        digits.push_back(carry % 10);
        carry = carry / 10;
    }

    return digits;
}

// Function to recursively calculate the
// factorial of a large number
vector<int> factorialRecursiveAlgorithm(
  long int n)
{
    if (n <= 2) {
        return multiply(n, { 1 });
    }

    return multiply(
      n, factorialRecursiveAlgorithm(n - 1));
}

// Driver Code
int main()
{
    long int n = 50;

    vector<int> result
      = factorialRecursiveAlgorithm(n);

    for (long int i = result.size() - 1; i >= 0; i--) {
        cout << result[i];
    }

    cout << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// MUltiply the number x with the number
// represented by res array
static Integer []multiply(int n, Integer []digits)
{

    // Initialize carry
    int carry = 0;

    // One by one multiply n with
    // individual digits of res[]
    for (int i = 0; i < digits.length; i++) {
        int result
          = digits[i] * n + carry;

        // Store last digit of 'prod' in res[]
        digits[i] = result % 10;

        // Put rest in carry
        carry = result / 10;
    }

    // Put carry in res and increase result size
    LinkedList<Integer> v = new LinkedList<Integer>();
    v.addAll(Arrays.asList(digits));
    while (carry>0) {
        v.add(new Integer(carry % 10));
        carry = carry / 10;
    }

    return v.stream().toArray(Integer[] ::new);
}

// Function to recursively calculate the
// factorial of a large number
static Integer []factorialRecursiveAlgorithm(
  int n)
{
    if (n <= 2) {
        return multiply(n, new Integer[]{ 1 });
    }

    return multiply(
      n, factorialRecursiveAlgorithm(n - 1));
}

// Driver Code
public static void main(String[] args)
{
    int n = 50;

    Integer []result
      = factorialRecursiveAlgorithm(n);

    for (int i = result.length - 1; i >= 0; i--) {
        System.out.print(result[i]);
    }

    System.out.print("\n");

}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG
{

    // MUltiply the number x with the number
    // represented by res array
    static int[] multiply(int n, int[] digits)
    {

        // Initialize carry
        int carry = 0;

        // One by one multiply n with
        // individual digits of res[]
        for (int i = 0; i < digits.Length; i++)
        {
            int result
              = digits[i] * n + carry;

            // Store last digit of 'prod' in res[]
            digits[i] = result % 10;

            // Put rest in carry
            carry = result / 10;
        }

        // Put carry in res and increase result size
        LinkedList<int> v = new LinkedList<int>();
        foreach (int i in digits)
        {
            v.AddLast(i);
        }
        while (carry > 0)
        {
            v.AddLast((int)(carry % 10));
            carry = carry / 10;
        }

        return v.ToArray();
    }

    // Function to recursively calculate the
    // factorial of a large number
    static int[] factorialRecursiveAlgorithm(
      int n)
    {
        if (n <= 2)
        {
            return multiply(n, new int[] { 1 });
        }

        return multiply(
          n, factorialRecursiveAlgorithm(n - 1));
    }

    // Driver Code
    public static void Main()
    {
        int n = 50;
        int[] result = factorialRecursiveAlgorithm(n);
        for (int i = result.Length - 1; i >= 0; i--)
        {
            Console.Write(result[i]);
        }

        Console.Write("\n");

    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
// javascript program for the above approach
// MUltiply the number x with the number
// represented by res array
function multiply(n, digits)
{

    // Initialize carry
    var carry = 0;

    // One by one multiply n with
    // individual digits of res
    for (var i = 0; i < digits.length; i++) {
        var result
          = digits[i] * n + carry;

        // Store last digit of 'prod' in res
        digits[i] = result % 10;

        // Put rest in carry
        carry = parseInt(result / 10);
    }

    // Put carry in res and increase result size
    while (carry>0) {
        digits.push(carry % 10);
        carry = parseInt(carry / 10);
    }

    return digits;
}

// Function to recursively calculate the
// factorial of a large number
function factorialRecursiveAlgorithm(
  n)
{
    if (n <= 2) {
        return multiply(n, [ 1 ]);
    }

    return multiply(
      n, factorialRecursiveAlgorithm(n - 1));
}

// Driver Code
    var n = 50;

    var result = factorialRecursiveAlgorithm(n);

    for (var i = result.length - 1; i >= 0; i--) {
        document.write(result[i]);
    }

    document.write("<br>");

// This code is contributed by shikhasingrajput
</script>
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# MUltiply the number x with the number
# represented by res array

def multiply(n, digits):

    # Initialize carry
    carry = 0

    # One by one multiply n with
    # individual digits of res[]
    for i in range(len(digits)):
        result = digits[i] * n + carry

        # Store last digit of 'prod' in res[]
        digits[i] = result % 10

        # Put rest in carry
        carry = result // 10

    # Put carry in res and increase result size
    while (carry):
        digits.append(carry % 10)
        carry = carry // 10

    return digits

# Function to recursively calculate the
# factorial of a large number
def factorialRecursiveAlgorithm(n):
    if (n <= 2):
        return multiply(n, [1])

    return multiply(
        n, factorialRecursiveAlgorithm(n - 1))

# Driver Code
if __name__ == "__main__":

    n = 50

    result = factorialRecursiveAlgorithm(n)

    for i in range(len(result) - 1, -1, -1):
        print(result[i], end="")
```

**Output**

```
30414093201713378043612608166064768844377641568960512000000000000
```

***时间复杂度:** O(n)*
***辅助空间:** O(K)，其中 K 是*输出*中的最大位数*