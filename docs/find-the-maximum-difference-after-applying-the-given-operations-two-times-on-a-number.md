# 对一个数进行两次给定运算后求最大差值

> 原文:[https://www . geeksforgeeks . org/在一个数字上应用两次给定操作后找到最大差异/](https://www.geeksforgeeks.org/find-the-maximum-difference-after-applying-the-given-operations-two-times-on-a-number/)

给定一个整数 **N** ，任务是在给定的整数上应用两次给定的运算后，求最大差。

操作定义如下:

*   从 **N** 中选择任意数字 **(0-9)** ，并用任意其他数字 **(0-9)** 替换同一数字的所有实例。
*   **N** 运算后不能有前导零，也不能等于零。

**示例:**

> **输入:** N = 777
> **输出:** 888
> **说明:**选择数字 7 并用 9 替换其所有出现次数，得到 999。类似地，111 可以通过用 1 替换所有出现的 7 来获得。因此，可能的最大差异是 888。
> 
> **输入:** N = 123456
> **输出:** 820000
> 两次运算后的数字可以是 923456 和 103456。因此，所需的最大差值为 820000。

**说明:**通过对 **N** 的给定运算，减去可得到的最大值和最小值，即可得到最大差值。

*   最大数量可以通过从左边选择 **N** 的第一个数字获得，该数字不等于 **'9'** ，并将该数字的所有实例替换为 **'9'** 。
*   找到最小值有点棘手，因为 **N** 不能有任何前导零，也不能等于零。如果左边的 **N** 的第一个数字是**‘1’**，那么找到左边大于**‘1’**的第一个数字，并用**‘0’**替换该数字的所有实例。
*   否则，如果左边第一个数字 **N** 不等于**‘1’**，则选择该数字并用**‘1’**替换该数字的所有实例。
*   最后，返回最小值和最大值之间的差值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// maximum difference
// after two given operations
// on a number
#include <bits/stdc++.h>
using namespace std;

// Function that returns the
// maximum difference
// after two given operations
// on a number
int minDifference(int num)
{
    // Initialize the strings to make operations
    string maximum = to_string(num);
    string minimum = to_string(num);

    // Store length of the string
    int n = maximum.size();

    // Make the maximum number using
    // the first operation
    for (int i = 0; i < n; i++) {
        // Find the first digit which
        // is not equal to '9'
        if (maximum[i] != '9') {
            // Store the digit for
            // the given operation
            char digit = maximum[i];
            for (int j = i; j < n; j++) {
                // Replace all the selected
                // 'digit' with '9'
                if (maximum[j] == digit)
                    maximum[j] = '9';
            }
            // Break after the operation
            // is completed
            break;
        }
    }
    // Make the minimum number using
    // the second operation

    // Check if first digit is equal to '1'
    if (minimum[0] == '1') {
        for (int i = 1; i < n; i++) {
            // Find the first digit which
            // is greater than '1'
            if (minimum[i] - '0' > 1) {
                // Store the digit for
                // the given operation
                char digit = minimum[i];
                for (int j = i; j < n; j++) {
                    // Replace all the selected
                    // 'digit' with '0'
                    if (digit == minimum[j])
                        minimum[j] = '0';
                }
                // Break after the
                // operation is completed
                break;
            }
        }
    }
    else {
        // Select the first digit for
        // the given operation
        char digit = minimum[0];
        for (int i = 0; i < n; i++) {
            // Replace all the selected
            // 'digit' with '1'
            if (minimum[i] == digit)
                minimum[i] = '1';
        }
    }
    // Return the difference after
    // converting into integers
    return (stoi(maximum)
            - stoi(minimum));
}

// Driver Code
int main()
{
    int N = 1101157;

    cout << minDifference(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// difference after two given operations
// on a number
import java.util.*;

class GFG{

// Function that returns the
// maximum difference
// after two given operations
// on a number
static int minDifference(int num)
{

    // Initialize the strings to make operations
    StringBuilder maximum =
                  new StringBuilder(Integer.toString(num));
    StringBuilder minimum =
                  new StringBuilder(Integer.toString(num));

    // Store length of the string
    int n = maximum.length();

    // Make the maximum number using
    // the first operation
    for(int i = 0; i < n; i++)
    {

       // Find the first digit which
       // is not equal to '9'
       if (maximum.charAt(i) != '9')
       {

           // Store the digit for
           // the given operation
           char digit = maximum.charAt(i);
           for(int j = i; j < n; j++)
           {

              // Replace all the selected
              // 'digit' with '9'
              if (maximum.charAt(j) == digit)
                  maximum.setCharAt(j, '9');
           }

           // Break after the operation
           // is completed
           break;
       }
    }

    // Make the minimum number
    // using the second operation
    // Check if first digit is equal to '1'
    if (minimum.charAt(0) == '1')
    {
        for(int i = 1; i < n; i++)
        {

           // Find the first digit which
           // is greater than '1'
           if (minimum.charAt(i) - '0' > 1)
           {

               // Store the digit for
               // the given operation
               char digit = minimum.charAt(i);
               for(int j = i; j < n; j++)
               {

                  // Replace all the selected
                  // 'digit' with '0'
                  if (digit == minimum.charAt(j))
                      minimum.setCharAt(j, '0');
               }

               // Break after the
               // operation is completed
               break;
           }
        }
    }
    else
    {

        // Select the first digit for
        // the given operation
        char digit = minimum.charAt(0);
        for(int i = 0; i < n; i++)
        {

           // Replace all the selected
           // 'digit' with '1'
           if (minimum.charAt(i) == digit)
               minimum.setCharAt(i, '1');
        }
    }

    // Return the difference after
    // converting into integers
    return (Integer.parseInt(maximum.toString()) -
            Integer.parseInt(minimum.toString()));
}

// Driver code
public static void main(String[] args)
{
    int N = 1101157;

    System.out.println(minDifference(N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the
# maximum difference after
# two given operations
# on a number

# Function that returns the
# maximum difference after 
# two given operations
# on a number
def minDifference(num):

    # Initialize the strings to
    # make operations
    maximum = list(str(num));
    minimum = list(str(num));

    # Store length of the string
    n = len(maximum);

    # Make the maximum number using
    # the first operation
    for i in range(n):

        # Find the first digit which
        # is not equal to '9'
        if (maximum[i] != '9'):

            # Store the digit for
            # the given operation
            digit = maximum[i];

            for j in range(i, n):

                # Replace all the selected
                # 'digit' with '9'
                if (maximum[j] == digit):
                    maximum[j] = '9';

            # Break after the operation
            # is completed
            break;

    # Make the minimum number using
    # the second operation
    # Check if first digit is equal to '1'
    if (minimum[0] == '1'):
        for i in range(1, n):

            # Find the first digit which
            # is greater than '1'
            if (ord(minimum[i]) - ord('0') > 1):

                # Store the digit for
                # the given operation
                digit = minimum[i];
                for j in range(i, n):

                    # Replace all the selected
                    # 'digit' with '0'
                    if (digit == minimum[j]):
                        minimum[j] = '0';

                # Break after the
                # operation is completed
                break;

    else :

        # Select the first digit
        # for the given operation
        digit = minimum[0];
        for i in range(n):

            # Replace all the selected
            # 'digit' with '1'
            if (minimum[i] == digit):
                minimum[i] = '1';

    maximum = "".join(maximum)
    minimum = "".join(minimum)

    # Return the difference after
    # converting into integers
    return (int(maximum) - int(minimum));

# Driver Code
if __name__ == "__main__":

    N = 1101157;

    print(minDifference(N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the maximum
// difference after two given
// operations on a number
using System;
using System.Collections.Generic;

class GFG{

// Function that returns the
// maximum difference after
// two given operations on a
// number
static int minDifference(int num)
{

    // Initialize the strings to make operations
    char[] maximum = (num.ToString()).ToCharArray();
    char[] minimum = (num.ToString()).ToCharArray();

    // Store length of the string
    int n = maximum.Length;

    // Make the maximum number using
    // the first operation
    for(int i = 0; i < n; i++)
    {

        // Find the first digit which
        // is not equal to '9'
        if (maximum[i] != '9')
        {

            // Store the digit for
            // the given operation
            char digit = maximum[i];
            for(int j = i; j < n; j++)
            {

                // Replace all the selected
                // 'digit' with '9'
                if (maximum[j] == digit)
                    maximum[j] = '9';
            }

            // Break after the operation
            // is completed
            break;
        }
    }

    // Make the minimum number using
    // the second operation

    // Check if first digit is equal to '1'
    if (minimum[0] == '1')
    {
        for(int i = 1; i < n; i++)
        {

            // Find the first digit which
            // is greater than '1'
            if (minimum[i] - '0' > 1)
            {

                // Store the digit for
                // the given operation
                char digit = minimum[i];
                for(int j = i; j < n; j++)
                {

                    // Replace all the selected
                    // 'digit' with '0'
                    if (digit == minimum[j])
                        minimum[j] = '0';
                }

                // Break after the
                // operation is completed
                break;
            }
        }
    }
    else
    {

        // Select the first digit for
        // the given operation
        char digit = minimum[0];
        for(int i = 0; i < n; i++)
        {

            // Replace all the selected
            // 'digit' with '1'
            if (minimum[i] == digit)
                minimum[i] = '1';
        }
    }

    // Return the difference after
    // converting into integers
    return Convert.ToInt32(string.Join("", maximum)) -
           Convert.ToInt32(string.Join("", minimum));
}

// Driver Code
static void Main()
{
    int N = 1101157;

    Console.Write(minDifference(N));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// difference after two given
// operations on a number

// Function that returns the
// maximum difference after
// two given operations on a
// number
function minDifference(num)
{

    // Initialize the strings to make operations
    let maximum = (num.toString()).split('');
    let minimum = (num.toString()).split('');

    // Store length of the string
    let n = maximum.length;

    // Make the maximum number using
    // the first operation
    for(let i = 0; i < n; i++)
    {

        // Find the first digit which
        // is not equal to '9'
        if (maximum[i] != '9')
        {

            // Store the digit for
            // the given operation
            let digit = maximum[i];
            for(let j = i; j < n; j++)
            {

                // Replace all the selected
                // 'digit' with '9'
                if (maximum[j] == digit)
                    maximum[j] = '9';
            }

            // Break after the operation
            // is completed
            break;
        }
    }

    // Make the minimum number using
    // the second operation

    // Check if first digit is equal to '1'
    if (minimum[0] == '1')
    {
        for(let i = 1; i < n; i++)
        {

            // Find the first digit which
            // is greater than '1'
            if (minimum[i].charCodeAt() -
                '0'.charCodeAt() > 1)
            {

                // Store the digit for
                // the given operation
                let digit = minimum[i];
                for(let j = i; j < n; j++)
                {

                    // Replace all the selected
                    // 'digit' with '0'
                    if (digit == minimum[j])
                        minimum[j] = '0';
                }

                // Break after the
                // operation is completed
                break;
            }
        }
    }
    else
    {

        // Select the first digit for
        // the given operation
        let digit = minimum[0];
        for(let i = 0; i < n; i++)
        {

            // Replace all the selected
            // 'digit' with '1'
            if (minimum[i] == digit)
                minimum[i] = '1';
        }
    }

    // Return the difference after
    // converting into integers
    return parseInt(maximum.join("")) -
           parseInt(minimum.join(""));
}

// Driver code
let N = 1101157;

document.write(minDifference(N));

// This code is contributed by suresh07

</script>
```

**Output:** 

```
8808850
```