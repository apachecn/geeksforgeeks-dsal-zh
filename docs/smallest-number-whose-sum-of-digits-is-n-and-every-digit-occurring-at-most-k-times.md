# 位数之和为 N 的最小数，每个位数最多出现 K 次

> 原文:[https://www . geesforgeks . org/最小数字，其数字总和为 n，每个数字最多出现 k 次/](https://www.geeksforgeeks.org/smallest-number-whose-sum-of-digits-is-n-and-every-digit-occurring-at-most-k-times/)

给定两个正整数 **N** 和 **K** ，任务是找出最小的数，其位数之和为 **N** ，并且该数中每个不同的位数最多出现**K**次。如果没有这样的号码，打印【T8 "-1 "。

**示例:**

> **输入:** N = 25，K = 3
> **输出:** 799
> **说明:**数字的位数之和= (7 + 9 + 9) = 25 且为最小可能。
> 
> **输入:** N =100，K = 2
> **输出:** -1

**逼近:**给定的问题可以用[贪婪逼近](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。按照以下步骤解决问题:

*   每个数字最多出现 **K** 次的任意数字的最大可能位数[总和为 **K * 45** 。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)
*   初始化一个字符串，比如 **res** ，以存储形成的结果字符串。
*   如果 **N** 大于 **K * 45** ，则不能得到这样的数字。因此，打印**“-1”**。
*   否则，从 **9** 开始到 **1** 为止，从 **N** 、**开始，最多 K** 次，一直减去每一个数字。将当前数字添加到 **res** 。继续，直到 N 小于当前数字。
*   如果 **N** 小于当前数字，将 **N** 作为数字插入 **res** 。
*   完成上述步骤后，将[字符串 **res** 按照相反的顺序](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/)打印为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest number
// whose sum of digits is N and each
// digit occurring at most K times
void findSmallestNumberPossible(int N, int K)
{
    // Maximum sum possible using
    // each digit at most K times
    if (N > 45 * K) {
        cout << "-1";
        return;
    }

    // Append smallest number into
    // the resultant string
    string res = "";
    int count = 0;

    // Iterate over the range [9, 1]
    for (int i = 9; i >= 1;) {

        // If the count of the digit
        // is K, then update count and
        // check for the next digit
        if (count == K) {
            i--;
            count = 0;
        }

        // If N is greater than
        // current digit
        if (N > i) {

            // Subtract i from N
            N -= i;

            // Insert i as a digit
            res += (char)48 + i;
        }
        else {

            // Insert remaining N
            // as a digit
            res += (char)N + 48;
            N = 0;
            break;
        }

        // Increment count
        count++;
    }

    // Reverse the string
    reverse(res.begin(),
            res.end());

    // Print the answer
    cout << res;
}

// Driver Code
int main()
{
    int N = 25, K = 3;

    // Function Call
    findSmallestNumberPossible(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the smallest number
// whose sum of digits is N and each
// digit occurring at most K times
static void findSmallestNumberPossible(int N, int K)
{

    // Maximum sum possible using
    // each digit at most K times
    if (N > 45 * K)
    {
        System.out.print("-1");
        return;
    }

    // Append smallest number into
    // the resultant string
    StringBuilder res = new StringBuilder();
    int count = 0;

    // Iterate over the range [9, 1]
    for(int i = 9; i >= 1😉
    {

        // If the count of the digit
        // is K, then update count and
        // check for the next digit
        if (count == K)
        {
            i--;
            count = 0;
        }

        // If N is greater than
        // current digit
        if (N > i)
        {

            // Subtract i from N
            N -= i;

            // Insert i as a digit
            res.append((char)('0' + i));
        }
        else
        {

            // Insert remaining N
            // as a digit
            res.append((char)('0' + N));
            N = 0;
            break;
        }

        // Increment count
        count++;
    }

    // Reverse the string
    res.reverse();

    // Print the answer
    System.out.print(res.toString());
}

// Driver Code
public static void main(String[] args)
{
    int N = 25, K = 3;

    // Function Call
    findSmallestNumberPossible(N, K);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the smallest number
# whose sum of digits is N and each
# digit occurring at most K times
def findSmallestNumberPossible(N, K) :

    # Maximum sum possible using
    # each digit at most K times
    if (N > 45 * K) :
        print("-1", endl = "");
        return;

    # Append smallest number into
    # the resultant string
    res = "";
    count = 0;

    # Iterate over the range [9, 1]
    i = 9;   
    while i >= 1 :

        # If the count of the digit
        # is K, then update count and
        # check for the next digit
        if (count == K) :
            i -= 1;
            count = 0;

        # If N is greater than
        # current digit
        if (N > i) :

            # Subtract i from N
            N -= i;

            # Insert i as a digit
            res += chr(48 + i);

        else :

            # Insert remaining N
            # as a digit
            res += chr(N + 48);
            N = 0;
            break;

        # Increment count
        count += 1;

    # Reverse the string
    res = res[::-1]

    # Print the answer
    print(res, end = "");

# Driver Code
if __name__ == "__main__" :

    N = 25; K = 3;

    # Function Call
    findSmallestNumberPossible(N, K);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

// Function to find the smallest number
// whose sum of digits is N and each
// digit occurring at most K times
static void findSmallestNumberPossible(int N, int K)
{

    // Maximum sum possible using
    // each digit at most K times
    if (N > 45 * K)
    {
        Console.Write("-1");
        return;
    }

    // Append smallest number into
    // the resultant string
    string res = "" ;
    int count = 0;

    // Iterate over the range [9, 1]
    for (int i = 9; i >= 1;)
    {

        // If the count of the digit
        // is K, then update count and
        // check for the next digit
        if (count == K)
        {
            i--;
            count = 0;
        }

        // If N is greater than
        // current digit
        if (N > i)
        {

            // Subtract i from N
            N -= i;

            // Insert i as a digit
            res += (char)('0' + i);
        }
        else
        {

            // Insert remaining N
            // as a digit
            res += (char)('0' + N);
            N = 0;
            break;
        }

        // Increment count
        count++;
    }

     // Reverse the string
     string ans = "";
     for (int i = res.Length - 1; i >= 0; i--)
     {
         ans += res[i] + "";

     }

     // Print the answer
     Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{
    int N = 25, K = 3;

    // Function Call
    findSmallestNumberPossible(N, K);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach

      // Function to find the smallest number
      // whose sum of digits is N and each
      // digit occurring at most K times
      function findSmallestNumberPossible(N, K) {
        // Maximum sum possible using
        // each digit at most K times
        if (N > 45 * K) {
          document.write("-1");
          return;
        }

        // Append smallest number into
        // the resultant string
        var res = "";
        var count = 0;

        // Iterate over the range [9, 1]
        for (var i = 9; i >= 1; ) {
          // If the count of the digit
          // is K, then update count and
          // check for the next digit
          if (count === K) {
            i--;
            count = 0;
          }

          // If N is greater than
          // current digit
          if (N > i) {
            // Subtract i from N
            N -= i;

            // Insert i as a digit
            res += String.fromCharCode("0".charCodeAt(0) + i);
          } else {
            // Insert remaining N
            // as a digit
            res += String.fromCharCode("0".charCodeAt(0) + N);
            N = 0;
            break;
          }

          // Increment count
          count++;
        }

        // Reverse the string
        var ans = "";
        for (var i = res.length - 1; i >= 0; i--) {
          ans += res[i] + "";
        }

        // Print the answer
        document.write(ans);
      }

      // Driver Code
      var N = 25,
        K = 3;

      // Function Call
      findSmallestNumberPossible(N, K);

</script>
```

**Output:** 

```
799
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*