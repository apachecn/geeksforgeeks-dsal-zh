# 不超过 N 的最大回文，可以表示为两个 3 位数的乘积

> 原文:[https://www . geesforgeks . org/maximum-回文-不超过-n-可表示为两个 3 位数的乘积/](https://www.geeksforgeeks.org/largest-palindrome-not-exceeding-n-which-can-be-expressed-as-product-of-two-3-digit-numbers/)

给定一个正整数 **N** ，任务是找到小于 **N** 的最大[回文号](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)，可以表示为两个 3 位数的乘积。

**示例:**

> **输入:** N = 101110
> **输出:** 101101
> **说明:**数字 101101 ( = 143 * 707)是满足条件的最大可能回文数。
> 
> **输入:** N = 800000
> **输出:** 793397
> **说明:**数字 793397 ( = 869 × 913)是满足条件的最大可能回文数。

**天真方法:**最简单的从范围**【100，999】**生成所有可能的对，并且对于每个对，检查它们的乘积是否是回文并且是否小于 **N** 。打印所有此类产品的最大数量，作为所需答案。

***时间复杂度:**O(N * 900<sup>2</sup>)*
***辅助空间:** O(1)*

**交替逼近:**基于[所有 11 的倍数](https://www.geeksforgeeks.org/sum-multiples-number-n/)都是回文的观察，这个问题也可以解决。因此，迭代范围**【100，999】**，对于范围内的每个值，迭代范围**【121，999】**内的 **11** 的倍数，并在每次迭代中检查所需条件。按照以下步骤解决问题:

*   初始化一个变量，比如 **num** ，来存储满足给定条件的最大回文数。
*   使用变量迭代范围**【100，999】**，说 **i** ，并执行以下步骤:
    *   使用一个变量迭代范围**【121，999】**，用 11 的倍数表示 **j** 。
        *   将 **i** 和 **j** 的产品存放在串 **x** 中。
        *   如果 **X** 的值小于 **N** ， **X** 是[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)，那么如果 **X > num** 更新 **num** 的值。
        *   否则，继续迭代下一对整数。
*   完成上述步骤后，打印 **num** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest palindrome
// not exceeding N which can be expressed
// as the product of two 3-digit numbers
void palindrome_prod(string N){

      // Stores all palindromes
    vector<int> palindrome_list;

    for (int i = 101; i < 1000; i++)
    {
        for (int j = 121; j < 1000;
             j += (i % 11 == 0) ? 1 : 11)
        {

            // Stores the product
            int n = i * j;
            string x = to_string(n);
            string y = x;
            reverse(y.begin(), y.end());

            // Check if X is palindrome
            if (x == y){

                  // Check n is less than N
                if (n < stoi(N)){

                    // If true, append it
                    // in the list
                    palindrome_list.push_back(i * j);
                     }
                  }
              }
          }

    // Print the largest palindrome
    cout << (*max_element(palindrome_list.begin(),
                          palindrome_list.end()));
}

// Driver Code
int main()
{

  string N = "101110";

  // Function Call
  palindrome_prod(N);

  return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find the largest palindrome
// not exceeding N which can be expressed
// as the product of two 3-digit numbers
static void palindrome_prod(String N){

      // Stores all palindromes
    Vector<Integer> palindrome_list = new Vector<Integer>();

    for (int i = 101; i < 1000; i++)
    {
        for (int j = 121; j < 1000;
             j += (i % 11 == 0) ? 1 : 11)
        {

            // Stores the product
            int n = i * j;
            String x = String.valueOf(n);
            String y = x;
            reverse(y);

            // Check if X is palindrome
            if (x == y){

                  // Check n is less than N
                if (n < Integer.valueOf(N)){

                    // If true, append it
                    // in the list
                    palindrome_list.add(i * j);
                     }
                  }
              }
          }

    // Print the largest palindrome
    System.out.print(Collections.max(palindrome_list));
}

static String reverse(String input)
{
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{
  String N = "101110";

  // Function Call
  palindrome_prod(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the largest palindrome
# not exceeding N which can be expressed
# as the product of two 3-digit numbers
def palindrome_prod(N):

      # Stores all palindromes
    palindrome_list = []

    for i in range(101, 1000):
        for j in range(121, 1000, (1 if i % 11 == 0 else 11)):

            # Stores the product
            n = i * j
            x = str(n)

            # Check if X is palindrome
            if x == x[::-1]:

                  # Check n is less than N
                if n < N:

                    # If true, append it
                    # in the list
                    palindrome_list.append(i * j)

    # Print the largest palindrome
    print(max(palindrome_list))

# Driver Code

N = 101110

# Function Call
palindrome_prod(N)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG
{

// Function to find the largest palindrome
// not exceeding N which can be expressed
// as the product of two 3-digit numbers
static void palindrome_prod(String N){

      // Stores all palindromes
    List<int> palindrome_list = new List<int>();

    for (int i = 101; i < 1000; i++)
    {
        for (int j = 121; j < 1000;
             j += (i % 11 == 0) ? 1 : 11)
        {

            // Stores the product
            int n = i * j;
            String x = String.Join("", n);
            String y = x;
            reverse(y);

            // Check if X is palindrome
            if (x == y)
            {

                  // Check n is less than N
                if (n < Int32.Parse(N))
                {

                    // If true, append it
                    // in the list
                    palindrome_list.Add(i * j);
                }
            }
        }
    }

    // Print the largest palindrome
    Console.Write(palindrome_list.Max());
}

static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("", a);
}

// Driver Code
public static void Main(String[] args)
{
  String N = "101110";

  // Function Call
  palindrome_prod(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the largest palindrome
// not exceeding N which can be expressed
// as the product of two 3-digit numbers
function palindrome_prod(N){

    // Stores all palindromes
    var palindrome_list = [];
    var i,j;
    for (i = 101; i < 1000; i++)
    {
        for (j = 121; j < 1000;
             j += (i % 11 == 0) ? 1 : 11)
        {

            // Stores the product
            var n = i * j;
            var x = n.toString();
            var y = x;
            y = y.split("").reverse().join("");

            // Check if X is palindrome
            if (x == y){

                // Check n is less than N
                if (n < Number(N)){

                    // If true, append it
                    // in the list
                    palindrome_list.push(i * j);
                }
             }
          }
       }

    // Print the largest palindrome
    document.write(Math.max.apply(null, palindrome_list));
}

// Driver Code
  var N = "101110";

  // Function Call
  palindrome_prod(N);

</script>
```

**Output:** 

```
101101
```

***时间复杂度:**O(N * 900<sup>2</sup>)*
***辅助空间:** O(1)*