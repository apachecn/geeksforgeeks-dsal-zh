# 检查任一子阵列的和是否为回文

> 原文:[https://www . geesforgeks . org/check-if-sum-of-any-subarray-is-回文-or-not/](https://www.geeksforgeeks.org/check-if-sum-of-any-subarray-is-palindrome-or-not/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是检查是否存在大小至少为 2 的**子阵列，这样它的和就是回文。如果存在这样的子阵列，则打印**是**。否则，打印**否**。
**举例:**** 

> **输入:** arr[] = {10，6，7，9，12}
> **输出:**是
> **解释:**
> 求和为 22 的子阵【6，7，9】是回文。
> **输入:** arr[] = {15，4，8，2}
> **输出:**否
> **说明:**
> 不存在这样的子阵列。

**方法:**
按照以下步骤解决问题:

*   创建给定数组的 [**前缀和数组**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 。
*   使用嵌套 for 循环来迭代数组，以表示子数组的开始和结束。通过**pref[y]–pref[x–1]**可以获得索引[x，y]内的子阵列之和。
*   检查这个和是否是[回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。如果任何一个和如果回文打印“是”，否则打印“否”。

以下是上述方法的实现:

## C++

```
// C++ program to check if sum of any
// subarray of size atleast 2 is
// palindrome or not

#include <bits/stdc++.h>
using namespace std;

// Function which checks whether
// a given number is palindrome or not
bool checkPalindrome(int n)
{
    // Store the reverse of
    // the number n
    int rev = 0;
    for (int x = n; x != 0; x /= 10) {
        int d = x % 10;
        rev = rev * 10 + d;
    }
    if (rev == n)
        return true;

    else
        return false;
}

// Function which checks if the
// requires subarray exists or not
void findSubarray(int ar[], int n)
{
    // Making a prefix sum array of ar[]
    int pref[n];
    pref[0] = ar[0];

    for (int x = 1; x < n; x++)
        pref[x] = pref[x - 1] + ar[x];

    // Boolean variable that will store
    // whether such subarray exists or not
    bool found = false;
    for (int x = 0; x < n; x++) {
        for (int y = x + 1; y < n; y++) {
            // sum stores the sum of subarray
            // from index x to y of array
            int sum = pref[y];
            if (x > 0) {
                sum -= pref[x - 1];
            }
            if (checkPalindrome(sum)) {
                // Required subarray is found
                found = true;
                break;
            }
        }

        if (found)
            break;
    }
    if (found)
        cout << "Yes" << endl;

    else
        cout << "No" << endl;
}

// Driver code
int main()
{
    int ar[] = { 1, 11, 20, 35 };

    int n = sizeof(ar) / sizeof(ar[0]);

    findSubarray(ar, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if sum of any
// subarray of size atleast 2 is
// palindrome or not
class GFG{

// Function which checks whether
// a given number is palindrome or not
static boolean checkPalindrome(int n)
{

    // Store the reverse of
    // the number n
    int rev = 0;
    for(int x = n; x != 0; x /= 10)
    {
       int d = x % 10;
       rev = rev * 10 + d;
    }
    if (rev == n)
        return true;
    else
        return false;
}

// Function which checks if the
// requires subarray exists or not
static void findSubarray(int []ar, int n)
{

    // Making a prefix sum array of ar[]
    int []pref = new int[n];
    pref[0] = ar[0];

    for(int x = 1; x < n; x++)
    pref[x] = pref[x - 1] + ar[x];

    // Boolean variable that will store
    // whether such subarray exists or not
    boolean found = false;

    for(int x = 0; x < n; x++)
    {
       for(int y = x + 1; y < n; y++)
       {

          // sum stores the sum of subarray
          // from index x to y of array
          int sum = pref[y];
          if (x > 0)
          {
              sum -= pref[x - 1];
          }
          if (checkPalindrome(sum))
          {

              // Required subarray is found
              found = true;
              break;
          }
       }
       if (found)
           break;
    }
    if (found)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String args[])
{
    int []ar = { 1, 11, 20, 35 };
    int n = ar.length;

    findSubarray(ar, n);
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to check if sum of
# any subarray of size atleast 2 is
# palindrome or not

# Function which checks whether a
# given number is palindrome or not
def checkPalindrome(n):

    # Store the reverse
    # of the number n
    rev = 0
    x = n

    while(x != 0):
        d = x % 10
        rev = rev * 10 + d
        x = x // 10

    if (rev == n):
        return True
    else:
        return False

# Function which checks if the
# requires subarray exists or not
def findSubarray(ar, n):

    # Making a prefix sum array of ar[]
    pref = [0 for i in range(n)]
    pref[0] = ar[0]

    for x in range(1, n):
        pref[x] = pref[x - 1] + ar[x]

    # Boolean variable that will store
    # whether such subarray exists or not
    found = False

    for x in range(n):
        for y in range(x + 1, n, 1):

            # Sum stores the sum of subarray
            # from index x to y of array
            sum = pref[y]
            if (x > 0):
                sum -= pref[x - 1]

            if (checkPalindrome(sum)):

                # Required subarray is found
                found = True
                break

        if (found):
            break
    if (found):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':

    ar = [ 1, 11, 20, 35 ]
    n = len(ar)

    findSubarray(ar, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to check if sum of any
// subarray of size atleast 2 is
// palindrome or not
using System;

class GFG{

// Function which checks whether
// a given number is palindrome or not
static bool checkPalindrome(int n)
{
    // Store the reverse of
    // the number n
    int rev = 0;
    for(int x = n; x != 0; x /= 10)
    {
       int d = x % 10;
       rev = rev * 10 + d;
    }
    if (rev == n)
        return true;
    else
        return false;
}

// Function which checks if the
// requires subarray exists or not
static void findSubarray(int []ar, int n)
{
    // Making a prefix sum array of ar[]
    int []pref = new int[n];
    pref[0] = ar[0];

    for(int x = 1; x < n; x++)
       pref[x] = pref[x - 1] + ar[x];

    // Boolean variable that will store
    // whether such subarray exists or not
    bool found = false;
    for(int x = 0; x < n; x++)
    {
       for(int y = x + 1; y < n; y++)
       {
          // sum stores the sum of subarray
          // from index x to y of array
          int sum = pref[y];
          if (x > 0)
          {
              sum -= pref[x - 1];
          }
          if (checkPalindrome(sum))
          {

              // Required subarray is found
              found = true;
              break;
          }
       }
       if (found)
           break;
    }
    if (found)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
public static void Main()
{
    int []ar = { 1, 11, 20, 35 };
    int n = ar.Length;

    findSubarray(ar, n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to check if sum of any
// subarray of size atleast 2 is
// palindrome or not

// Function which checks whether
// a given number is palindrome or not
function checkPalindrome(n)
{
    // Store the reverse of
    // the number n
    var rev = 0;
    for (var x = n; x != 0; x = parseInt(x/10)) {
        var d = x % 10;
        rev = rev * 10 + d;
    }
    if (rev == n)
        return true;

    else
        return false;
}

// Function which checks if the
// requires subarray exists or not
function findSubarray(ar, n)
{
    // Making a prefix sum array of ar[]
    var pref = Array(n).fill(0);
    pref[0] = ar[0];

    for (var x = 1; x < n; x++)
        pref[x] = pref[x - 1] + ar[x];

    // Boolean variable that will store
    // whether such subarray exists or not
    var found = false;
    for (var x = 0; x < n; x++) {
        for (var y = x + 1; y < n; y++) {
            // sum stores the sum of subarray
            // from index x to y of array
            var sum = pref[y];
            if (x > 0) {
                sum -= pref[x - 1];
            }
            if (checkPalindrome(sum)) {
                // Required subarray is found
                found = true;
                break;
            }
        }

        if (found)
            break;
    }
    if (found)
        document.write( "Yes" );

    else
        document.write( "No" );
}

// Driver code
var ar = [1, 11, 20, 35];
var n = ar.length;
findSubarray(ar, n);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*