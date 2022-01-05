# 通过给定的操作减少给定的数字形成一个键

> 原文:[https://www . geesforgeks . org/按给定的操作将给定的数字减少到给定的形式/键/](https://www.geeksforgeeks.org/reduce-a-given-number-to-form-a-key-by-the-given-operations/)

给定一个整数 **N** ，任务是按照下面给出的操作减少数字并形成一个键:

*   提取数字的[最高有效位:](https://www.geeksforgeeks.org/steps-to-reduce-n-to-zero-by-subtracting-its-most-significant-digit-at-every-step/)
    *   **如果数字为偶数:**将连续的数字相加，直到数字之和为奇数。
    *   **如果数字为奇数:**将连续的数字相加，直到数字之和为偶数。
*   对所有剩余的数字重复该过程。
*   最后，将计算的总和连接在一起以获得密钥。

**示例:**

> **输入:** N = 1667848270
> **输出:** 20290
> **解释:**
> **第一步:**第一位数字(= 1)为奇数。所以，把后面的数字加起来，直到总和是偶数。
> 因此，数字 1、6、6 和 7 相加形成 20。
> **第二步:**下一位数字(= 8)为偶数。所以，把接下来的数字加起来，直到总和为奇数。
> 所以数字 8、4、8、2、7 加起来就是 29。
> **第三步:**最后一位数字(= 0)为偶数。
> 因此，串联结果后的最终答案将是:20290
> 
> **输入:** N = 7246262412
> **输出:** 342
> **说明:**
> **第一步:**第一位数字(= 7)为奇数。所以，把后面的数字加起来，直到总和是偶数。
> 所以数字 7、2、4、6、2、6、2、4、1 加起来就是 34。
> **第二步:**最后一位数字(= 2)为偶数。
> 因此，串联结果后的最终答案将是:342。

**方法:**思路是迭代数字的位数，[检查数字的奇偶性](https://www.geeksforgeeks.org/finding-the-parity-of-a-number-efficiently/)。如果是偶数，则继续下一个数字，直到遇到奇数。对于奇数，添加连续的数字，直到数字之和为偶数。最后，连接计算出的总和以获得所需的密钥。

下面是上述方法的实现:

## C++

```
// C++ program of the
// above approach
#include <bits/stdc++.h>
using namespace std;

 // Function to find the key
// of the given number
int key(int N)
{

    // Convert the integer
    // to String
    string num = "" + to_string(N);
    int ans = 0;
    int j = 0;

    // Iterate the num-string
    // to get the result
    for(j = 0; j < num.length(); j++)
    {

        // Check if digit is even or odd
        if ((num[j] - 48) % 2 == 0)
        {
            int add = 0;
            int i;

            // Iterate until odd sum
            // is obtained by adding
            // consecutive digits
            for(i = j; j < num.length(); j++)
            {
                add += num[j] - 48;

                // Check if sum becomes odd
                if (add % 2 == 1)
                    break;
            }

            if (add == 0)
            {
                ans *= 10;
            }
            else
            {
                int digit = (int)floor(log10(add) + 1);
                ans *= (pow(10, digit));

                // Add the result in ans
                ans += add;
            }

            // Assign the digit index
            // to num string
            i = j;
        }
        else
        {

            // If the number is odd
            int add = 0;
            int i;

            // Iterate until odd sum
            // is obtained by adding
            // consecutive digits
            for(i = j; j < num.length(); j++)
            {
                add += num[j] - 48;

                // Check if sum becomes even
                if (add % 2 == 0)
                {
                    break;
                }
            }

            if (add == 0)
            {
                ans *= 10;
            }
            else
            {
                int digit = (int)floor(
                       log10(add) + 1);
                ans *= (pow(10, digit));

                // Add the result in ans
                ans += add;
            }

            // assign the digit index
            // to main numstring
            i = j;
        }
    }

    // Check if all digits
    // are visited or not
    if (j + 1 >= num.length())
    {
        return ans;
    }
    else
    {
        return ans += num[num.length() - 1] - 48;
    }
}

// Driver code  
int main()
{
    int N = 1667848271;

    cout << key(N);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach

import java.io.*;
import java.util.*;
import java.lang.*;

public class Main {
    // Function to find the key
    // of the given number
    static int key(int N)
    {

        // Convert the integer
        // to String
        String num = "" + N;
        int ans = 0;
        int j = 0;

        // Iterate the num-string
        // to get the result
        for (j = 0; j < num.length(); j++) {

            // Check if digit is even or odd
            if ((num.charAt(j) - 48) % 2 == 0) {
                int add = 0;
                int i;

                // Iterate until odd sum
                // is obtained by adding
                // consecutive digits
                for (i = j; j < num.length(); j++) {
                    add += num.charAt(j) - 48;

                    // Check if sum becomes odd
                    if (add % 2 == 1)
                        break;
                }

                if (add == 0) {
                    ans *= 10;
                }
                else {
                    int digit = (int)Math.floor(
                        Math.log10(add) + 1);
                    ans *= (Math.pow(10, digit));

                    // Add the result in ans
                    ans += add;
                }

                // Assign the digit index
                // to num string
                i = j;
            }
            else {
                // If the number is odd
                int add = 0;
                int i;

                // Iterate until odd sum
                // is obtained by adding
                // consecutive digits
                for (i = j; j < num.length(); j++) {
                    add += num.charAt(j) - 48;

                    // Check if sum becomes even
                    if (add % 2 == 0) {
                        break;
                    }
                }

                if (add == 0) {
                    ans *= 10;
                }
                else {
                    int digit = (int)Math.floor(
                        Math.log10(add) + 1);
                    ans *= (Math.pow(10, digit));

                    // Add the result in ans
                    ans += add;
                }

                // assign the digit index
                // to main numstring
                i = j;
            }
        }

        // Check if all digits
        // are visited or not
        if (j + 1 >= num.length()) {
            return ans;
        }
        else {
            return ans += num.charAt(
                              num.length() - 1)
                          - 48;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 1667848271;
        System.out.print(key(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program of the
# above approach
import math

# Function to find the key
# of the given number
def key(N) :

    # Convert the integer
    # to String
    num = "" + str(N)
    ans = 0
    j = 0

    # Iterate the num-string
    # to get the result
    while j < len(num) :

        # Check if digit is even or odd
        if ((ord(num[j]) - 48) % 2 == 0) :

            add = 0

            # Iterate until odd sum
            # is obtained by adding
            # consecutive digits
            i = j
            while j < len(num) :

                add += ord(num[j]) - 48

                # Check if sum becomes odd
                if (add % 2 == 1) :
                    break

                j += 1

            if (add == 0) :

                ans *= 10

            else :

                digit = int(math.floor(math.log10(add) + 1))
                ans *= (pow(10, digit))

                # Add the result in ans
                ans += add

            # Assign the digit index
            # to num string
            i = j

        else :

            # If the number is odd
            add = 0

            # Iterate until odd sum
            # is obtained by adding
            # consecutive digits
            i = j
            while j < len(num) :

                add += ord(num[j]) - 48

                # Check if sum becomes even
                if (add % 2 == 0) :

                    break

                j += 1

            if (add == 0) :

                ans *= 10

            else :

                digit = int(math.floor(math.log10(add) + 1))
                ans *= (pow(10, digit))

                # Add the result in ans
                ans += add

            # assign the digit index
            # to main numstring
            i = j

        j += 1

    # Check if all digits
    # are visited or not
    if (j + 1) >= len(num) :

        return ans

    else :
        ans += ord(num[len(num) - 1]) - 48
        return ans

N = 1667848271

print(key(N))

# This code is contributed by divyesh072019
```

## C#

```
// C# program of the
// above approach
using System;
class GFG{

// Function to find the key
// of the given number
static int key(int N)
{
  // Convert the integer
  // to String
  String num = "" + N;
  int ans = 0;
  int j = 0;

  // Iterate the num-string
  // to get the result
  for (j = 0; j < num.Length; j++)
  {
    // Check if digit is even or odd
    if ((num[j] - 48) % 2 == 0)
    {
      int add = 0;
      int i;

      // Iterate until odd sum
      // is obtained by adding
      // consecutive digits
      for (i = j; j < num.Length; j++)
      {
        add += num[j] - 48;

        // Check if sum becomes odd
        if (add % 2 == 1)
          break;
      }

      if (add == 0)
      {
        ans *= 10;
      }
      else
      {
        int digit = (int)Math.Floor(
                         Math.Log10(add) + 1);
        ans *= (int)(Math.Pow(10, digit));

        // Add the result in ans
        ans += add;
      }

      // Assign the digit index
      // to num string
      i = j;
    }
    else
    {
      // If the number is odd
      int add = 0;
      int i;

      // Iterate until odd sum
      // is obtained by adding
      // consecutive digits
      for (i = j; j < num.Length; j++)
      {
        add += num[j] - 48;

        // Check if sum becomes even
        if (add % 2 == 0)
        {
          break;
        }
      }

      if (add == 0)
      {
        ans *= 10;
      }
      else {
        int digit = (int)Math.Floor(
                         Math.Log10(add) + 1);
        ans *= (int)(Math.Pow(10, digit));

        // Add the result in ans
        ans += add;
      }

      // assign the digit index
      // to main numstring
      i = j;
    }
  }

  // Check if all digits
  // are visited or not
  if (j + 1 >= num.Length)
  {
    return ans;
  }
  else
  {
    return ans += num[num.Length - 1] - 48;
  }
}

// Driver Code
public static void Main(String[] args)
{
  int N = 1667848271;
  Console.Write(key(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program of the above approach

    // Function to find the key
    // of the given number
    function key(N)
    {

      // Convert the integer
      // to String
      let num = "" + N.toString();
      let ans = 0;
      let j = 0;

      // Iterate the num-string
      // to get the result
      for (j = 0; j < num.length; j++)
      {

        // Check if digit is even or odd
        if ((num[j].charCodeAt() - 48) % 2 == 0)
        {
          let add = 0;
          let i;

          // Iterate until odd sum
          // is obtained by adding
          // consecutive digits
          for (i = j; j < num.length; j++)
          {
            add += num[j].charCodeAt() - 48;

            // Check if sum becomes odd
            if (add % 2 == 1)
              break;
          }

          if (add == 0)
          {
            ans *= 10;
          }
          else
          {
            let digit = Math.floor(Math.log10(add) + 1);
            ans *= parseInt(Math.pow(10, digit), 10);

            // Add the result in ans
            ans += add;
          }

          // Assign the digit index
          // to num string
          i = j;
        }
        else
        {
          // If the number is odd
          let add = 0;
          let i;

          // Iterate until odd sum
          // is obtained by adding
          // consecutive digits
          for (i = j; j < num.length; j++)
          {
            add += num[j].charCodeAt() - 48;

            // Check if sum becomes even
            if (add % 2 == 0)
            {
              break;
            }
          }

          if (add == 0)
          {
            ans *= 10;
          }
          else {
            let digit = Math.floor(Math.log10(add) + 1);
            ans *= parseInt(Math.pow(10, digit), 10);

            // Add the result in ans
            ans += add;
          }

          // assign the digit index
          // to main numstring
          i = j;
        }
      }

      // Check if all digits
      // are visited or not
      if (j + 1 >= num.length)
      {
        return ans;
      }
      else
      {
        return ans += num[num.length - 1].charCodeAt() - 48;
      }
    }

    let N = 1667848271;
      document.write(key(N));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
20291
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)