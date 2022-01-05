# 检查所有子编号是否有不同的数字乘积

> 原文:[https://www . geesforgeks . org/check-if-all-sub-numbers-has-distinct-digital-product/](https://www.geeksforgeeks.org/check-if-all-sub-numbers-have-distinct-digit-product/)

给定一个数字 N，任务是检查这个数字的所有子数字是否有不同的数字乘积。
**注** :

*   一个 N 位数有 N*(N+1)/2 个子数。例如，975 所有可能的子数都是 9、7、5、97、75、975。
*   数字的乘积就是数字的乘积。

**例:**

```
Input : N = 324
Output : YES
Sub-numbers of 324 are 3, 2, 4, 32, 24 and 324 
and digit products are 3, 2, 4, 6, 8 and 24 
respectively. All the digit products are different.

Input : N = 323
Output : NO
Sub-numbers of 323 are 3, 2, 3, 32, 23 and 323
and digit products are 3, 2, 3, 6, 6 and 18 
respectively. Digit products 3 and 6 have occurred 
twice. 
```

**进场:**

1.  制作一个数字数组，即一个数组，其元素是给定数字 n 的数字
2.  现在找到 N 的子数类似于找到数字阵列的所有可能的子阵列。
3.  维护这些子阵列的数字产品列表。
4.  如果任何数字产品出现多次，请打印“否”
5.  否则打印“是”。

以下是上述方法的实现:

## C++

```
// C++ program to check if all sub-numbers
// have distinct Digit product
#include<bits/stdc++.h>
using namespace std;

// Function to calculate product of
// digits between given indexes
int digitProduct(int digits[], int start, int end)
{
    int pro = 1;
    for (int i = start; i <= end; i++) {
        pro *= digits[i];
    }
    return pro;
}

// Function to check if all sub-numbers
// have distinct Digit product
bool isDistinct(int N)
{
    string s = to_string(N);

    // Length of number N
    int len = s.length();

    // Digit array
    int digits[len];

    // set to maintain digit products
    unordered_set<int> products;

    for (int i = 0; i < len; i++) {
        digits[i] = s[i]-'0';
    }

    // Finding all possible subarrays
    for (int i = 0; i < len; i++) {
        for (int j = i; j < len; j++) {

            int val = digitProduct(digits, i, j);

            if (products.find(val)!=products.end())
                return false;
            else
                products.insert(val);
        }
    }

    return true;
}

// Driver code
int main()
{
    int N = 324;

    if (isDistinct(N))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if all sub-numbers
// have distinct Digit product
import java.io.*;
import java.util.*;

public class GFG {

    // Function to calculate product of
    // digits between given indexes
    static int digitProduct(int[] digits, int start, int end)
    {
        int pro = 1;
        for (int i = start; i <= end; i++) {
            pro *= digits[i];
        }
        return pro;
    }

    // Function to check if all sub-numbers
    // have distinct Digit product
    static boolean isDistinct(int N)
    {
        String s = "" + N;

        // Length of number N
        int len = s.length();

        // Digit array
        int[] digits = new int[len];

        // List to maintain digit products
        ArrayList<Integer> products = new ArrayList<>();

        for (int i = 0; i < len; i++) {
            digits[i] = Integer.parseInt("" + s.charAt(i));
        }

        // Finding all possible subarrays
        for (int i = 0; i < len; i++) {
            for (int j = i; j < len; j++) {

                int val = digitProduct(digits, i, j);

                if (products.contains(val))
                    return false;
                else
                    products.add(val);
            }
        }

        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 324;

        if (isDistinct(N))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if all
# sub-numbers have distinct Digit product

# Function to calculate product of
# digits between given indexes
def digitProduct(digits, start, end):

    pro = 1
    for i in range(start, end + 1):
        pro *= digits[i]

    return pro

# Function to check if all sub-numbers
# have distinct Digit product
def isDistinct(N):

    s = str(N)

    # Length of number N
    length = len(s)

    # Digit array
    digits = [None] * length

    # set to maintain digit products
    products = set()

    for i in range(0, length):
        digits[i] = int(s[i])

    # Finding all possible subarrays
    for i in range(0, length):
        for j in range(i, length):

            val = digitProduct(digits, i, j)

            if val in products:
                return False
            else:
                products.add(val)

    return True

# Driver Code
if __name__ == "__main__":

    N = 324

    if isDistinct(N) == True:
        print("YES")
    else:
        print("NO")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to check if all sub-numbers
// have distinct Digit product

using System;
using System.Collections;
using System.Collections.Generic;
public class GFG {

    // Function to calculate product of
    // digits between given indexes
    static int digitProduct(int[] digits, int start, int end)
    {
        int pro = 1;
        for (int i = start; i <= end; i++) {
            pro *= digits[i];
        }
        return pro;
    }

    // Function to check if all sub-numbers
    // have distinct Digit product
    static bool isDistinct(int N)
    {
        string s = N.ToString();

        // Length of number N
        int len = s.Length;

        // Digit array
        int[] digits = new int[len];

        // List to maintain digit products
        ArrayList products = new ArrayList();

        for (int i = 0; i < len; i++) {
            digits[i] = s[i]-'0';
        }

        // Finding all possible subarrays
        for (int i = 0; i < len; i++) {
            for (int j = i; j < len; j++) {

                int val = digitProduct(digits, i, j);

                if (products.Contains(val))
                    return false;
                else
                    products.Add(val);
            }
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        int N = 324;

        if (isDistinct(N))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}
// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP program to check if all sub-numbers
// have distinct Digit product

// Function to calculate product of
// digits between given indexes
function digitProduct($digits, $start, $end)
{
    $pro = 1;
    for ($i = $start; $i <= $end; $i++) {
        $pro *= $digits[$i];
    }
    return $pro;
}

// Function to check if all sub-numbers
// have distinct Digit product
function isDistinct($N)
{
    $s ="$N";

    // Length of number N
    $len = sizeof($s);

    // Digit array
    $digits=array();

    //  to maintain digit products
    $products=array();

    for ($i = 0; $i < $len; $i++) {
        $digits[$i] = $s[$i]-'0';
    }

    // Finding all possible subarrays
    for ($i = 0; $i < $len; $i++) {
        for ($j = $i; $j < $len; $j++) {

            $val = digitProduct($digits, $i, $j);

            if (in_array($val,$products))
                return false;
            else
                array_push($products,$val);
        }
    }

    return true;
}

// Driver code

$N = 324;

if (isDistinct($N))
    echo "YES";
else
    echo "NO";

// This code is contributed by ihritik

?>
```

## java 描述语言

```
<script>
// Javascript program to check if all sub-numbers
// have distinct Digit product

// Function to calculate product of
// digits between given indexes
function digitProduct(digits, start, end)
{
    let pro = 1;
    for (let i = start; i <= end; i++) {
        pro *= digits[i];
    }
    return pro;
}

// Function to check if all sub-numbers
// have distinct Digit product
function isDistinct(N)
{
    let s ="N";

    // Length of number N
    let len = s.length;

    // Digit array
    let digits = new Array();

    // to maintain digit products
    let products = new Array();

    for (let i = 0; i < len; i++) {
        digits[i] = s[i].charCodeAt(0) - '0'.charCodeAt(0);
    }

    // Finding all possible subarrays
    for (let i = 0; i < len; i++) {
        for (let j = i; j < len; j++) {

            let val = digitProduct(digits, i, j);

            if (products.includes(val))
                return false;
            else
                products.push(val);
        }
    }

    return true;
}

// Driver code

let N = 324;

if (isDistinct(N))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by gfgking
</script>
```

**Output:** 

```
YES
```