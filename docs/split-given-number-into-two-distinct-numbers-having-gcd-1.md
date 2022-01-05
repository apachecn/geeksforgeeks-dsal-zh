# 将给定的数字分成两个不同的数字，GCD 为 1

> 原文:[https://www . geesforgeks . org/split-给定数字-分成两个不同的数字-having-gcd-1/](https://www.geeksforgeeks.org/split-given-number-into-two-distinct-numbers-having-gcd-1/)

给定一个整数为 **N** ，任务是将 **N** 转换成两个数字 **a** 和 **b** ，使得 **a < b** 和 **GCD(a，b)** 等于 1。

**示例:**

> **输入:**N = 12
> T3】输出: 5 7
> 
> **输入:**N = 9
> T3】输出: 4 5

**方法:**想法是从循环的后面开始[迭代](https://www.geeksforgeeks.org/iterator-invalidation-cpp/)从数字本身开始。按照下面给出的步骤解决问题。

*   如果 **N** 小于等于 **2，**答案不存在。
*   否则[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N/2，0)** ，并执行以下任务:
    *   如果 **i** 和 **N-i** 的 [gcd](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 **1** ，则打印此作为答案并返回。

下面是上述方法的实现:

## C++

```
/// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split N into two numbers
void find(int n)
{

    // Base Case
    if (n <= 2) {
        cout << "-1";
    }
    else {

        // Since a < b
        // start from n/2
        for (int i = n / 2; i > 0; i--) {

            // Sum of a and b is n
            int a = i, b = n - i;

            // Check the gcd
            if (__gcd(a, b) == 1 && a < b) {
                cout << a <<", " << b;
                return;
            }
        }
    }
}

// Driver Code
int main()
{

    int N = 9;

    find(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/// Java program for the above approach
class GFG {

  // Function to split N into two numbers
  public static void find(int n) {

    // Base Case
    if (n <= 2) {
      System.out.println("-1");
    } else {

      // Since a < b
      // start from n/2
      for (int i = n / 2; i > 0; i--) {

        // Sum of a and b is n
        int a = i, b = n - i;

        // Check the gcd
        if (__gcd(a, b) == 1 && a < b) {
          System.out.println(a + ", " + b);
          return;
        }
      }
    }
  }

  static int __gcd(int a, int b) {
    if (b == 0)
      return a;
    return __gcd(b, a % b);
  }

  // Driver Code
  public static void main(String args[]) {
    int N = 9;
    find(N);
  }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import math

# Function to split N into two numbers
def find(n):

    # Base Case
    if (n <= 2):
        print("-1")

    else:

        # Since a < b
        # start from n/2
        for i in range(n // 2, -1, -1):

            # Sum of a and b is n
            a = i
            b = n - i

            # Check the gcd
            if (math.gcd(a, b) == 1 and a < b):
                print(a,",", b)
                return

# Driver Code
if __name__ == "__main__":

    N = 9
    find(N)

    #vThis code is contributed by ukasp.
```

## C#

```
/// C# program for the above approach
using System;
public class GFG {

  // Function to split N into two numbers
  public static void find(int n) {

    // Base Case
    if (n <= 2) {
      Console.WriteLine("-1");
    } else {

      // Since a < b
      // start from n/2
      for (int i = n / 2; i > 0; i--) {

        // Sum of a and b is n
        int a = i, b = n - i;

        // Check the gcd
        if (__gcd(a, b) == 1 && a < b) {
          Console.WriteLine(a + ", " + b);
          return;
        }
      }
    }
  }

  static int __gcd(int a, int b) {
    if (b == 0)
      return a;
    return __gcd(b, a % b);
  }

  // Driver Code
  public static void Main(String []args) {
    int N = 9;
    find(N);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Recursive function to return gcd of a and b
       function __gcd(a, b) {
           // Everything divides 0
           if (a == 0)
               return b;
           if (b == 0)
               return a;

           // base case
           if (a == b)
               return a;

           // a is greater
           if (a > b)
               return __gcd(a - b, b);
           return __gcd(a, b - a);
       }
       // Function to split N into two numbers
       function find(n) {

           // Base Case
           if (n <= 2) {
               document.write("-1");
           }
           else {

               // Since a < b
               // start from n/2
               for (let i = Math.floor(n / 2); i > 0; i--) {

                   // Sum of a and b is n
                   let a = i, b = n - i;

                   // Check the gcd
                   if (__gcd(a, b) == 1 && a < b) {
                       document.write(a + ", " + b);
                       return;
                   }
               }
           }
       }

       // Driver Code
       let N = 9;
       find(N);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
4, 5
```

***时间复杂度:** O(N log(N))*
***辅助空间:** O(1)*