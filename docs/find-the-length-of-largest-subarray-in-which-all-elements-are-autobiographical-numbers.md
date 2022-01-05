# 求所有元素都是自传体数的最大子阵的长度

> 原文:[https://www . geeksforgeeks . org/find-最大长度子阵列-其中所有元素都是自传体数字/](https://www.geeksforgeeks.org/find-the-length-of-largest-subarray-in-which-all-elements-are-autobiographical-numbers/)

给定整数的**数组 arr[]** ，我们的任务是找到最大子数组的长度，使得子数组的所有元素都是 [**自传体数。**](https://www.geeksforgeeks.org/self-descriptive-number/)

> [**自传体数字**](https://www.geeksforgeeks.org/self-descriptive-number/) 是这样一个数字，它的第一个数字计算其中有多少个 0，第二个数字计算其中有多少个 1，以此类推。
> 比如 21200 有 2 个零，1 个一，2 个二和 0 个三和 0 个四。

**例:**

> **输入:** arr[]={21200，1，1303，1210，2020}
> **输出:** 2
> **解释:**
> 以所有数字为自传号的子阵最大长度为{1210，2020}。
> **输入:** arr[]={100，200，300，400，1200，500}
> **输出:** 0
> **说明:**
> 无一为自传号。

**方法:**
要解决上面提到的问题，我们必须遵循下面给出的步骤:

*   从索引 0 开始遍历数组，并用 0 初始化一个*最大长度*和*当前长度*变量。
*   如果当前元素是自传数字，则递增 *current_length* 变量并继续，否则将 current_length 设置为 0。
*   在每一步，将最大长度指定为**最大长度=最大(当前长度，最大长度)。**max _ length 的最终值将存储所需的结果。

以下是上述方法的实现:

## C++

```
// C++ program to find the length of the
// largest subarray whose every element is an
// Autobiographical Number

#include <bits/stdc++.h>
using namespace std;

// function to check number is autobiographical
bool isAutoBiographyNum(int number)
{

    int count = 0, position, size, digit;
    string NUM;

    // Convert integer to string
    NUM = to_string(number);
    size = NUM.length();

    // Iterate for every digit to check
    // for their total count
    for (int i = 0; i < size; i++) {
        position = NUM[i] - '0';
        count = 0;

        // Check occurrence of every number
        // and count them
        for (int j = 0; j < size; j++) {
            digit = NUM[j] - '0';
            if (digit == i)
                count++;
        }

        // Check if any position mismatches with
        // total count them return with false
        // else continue with loop
        if (position != count)
            return false;
    }

    return true;
}

// Function to return the length of the
// largest subarray whose every
// element is a Autobiographical number
int checkArray(int arr[], int n)
{

    int current_length = 0;
    int max_length = 0;

    // Utility function which checks every element
    // of array for Autobiographical number
    for (int i = 0; i < n; i++) {

        // Check if element arr[i] is an
        // Autobiographical number
        if (isAutoBiographyNum(arr[i]))
            // Increment the current length
            current_length++;

        else
            current_length = 0;

        // Update max_length value
        max_length = max(max_length, current_length);
    }

    // Return the final result
    return max_length;
}

// Driver code
int main()
{
    int arr[] = { 21200, 1, 1303, 1210, 2020 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << checkArray(arr, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of the
// largest subarray whose every element is 
// an autobiographical number
class GFG {

// Function to check number is autobiographical
static boolean isAutoBiographyNum(int number)
{

    int count = 0, position, size, digit;
    String NUM;

    // Convert integer to string
    NUM = Integer.toString(number);
    size = NUM.length();

    // Iterate for every digit to check
    // for their total count
    for(int i = 0; i < size; i++)
    {
       position = NUM.charAt(i) - '0';
       count = 0;

       // Check occurrence of every number
       // and count them
       for(int j = 0; j < size; j++)
       {
          digit = NUM.charAt(j) - '0';
          if (digit == i)
              count++;
       }

       // Check if any position mismatches with
       // total count them return with false
       // else continue with loop
       if (position != count)
           return false;
    }

    return true;
}

// Function to return the length of the
// largest subarray whose every
// element is a Autobiographical number
static int checkArray(int arr[], int n)
{
    int current_length = 0;
    int max_length = 0;

    // Utility function which checks every element
    // of array for autobiographical number
    for(int i = 0; i < n; i++)
    {

       // Check if element arr[i] is an
       // autobiographical number
       if (isAutoBiographyNum(arr[i]) == true)
       {

           // Increment the current length
           current_length++;
       }
       else
       {
           current_length = 0;
       }

       // Update max_length value
       max_length = Math.max(max_length, current_length);
    }

    // Return the final result
    return max_length;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 21200, 1, 1303, 1210, 2020 };
    int n = arr.length;

    System.out.println(checkArray(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the length of the
# largest subarray whose every element is an
# autobiographical number

# Function to check number is autobiographical
def isAutoBiographyNum(number):

    count = 0;

    # Convert integer to string
    NUM = str(number);
    size = len(NUM);

    # Iterate for every digit to check
    # for their total count
    for i in range(size):
        position = ord(NUM[i]) - ord('0');
        count = 0;

        # Check occurrence of every number
        # and count them
        for j in range(size):

            digit = ord(NUM[j]) - ord('0');
            if (digit == i):
                count += 1;

        # Check if any position mismatches with
        # total count them return with false
        # else continue with loop
        if (position != count):
            return False;

    return True;

# Function to return the length of the
# largest subarray whose every
# element is a autobiographical number
def checkArray(arr, n):

    current_length = 0;
    max_length = 0;

    # Utility function which checks every element
    # of array for autobiographical number
    for i in range(n):

        # Check if element arr[i] is an
        # autobiographical number
        if (isAutoBiographyNum(arr[i])):

            # Increment the current length
            current_length += 1;
        else:
            current_length = 0;

        # Update max_length value
        max_length = max(max_length,
                         current_length);

    # Return the final result
    return max_length;

# Driver code
if __name__ == "__main__":

    arr = [ 21200, 1, 1303, 1210, 2020 ];
    n = len(arr);

    print(checkArray(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the length of the
// largest subarray whose every element 
// is an autobiographical number
using System;

class GFG {

// Function to check number is autobiographical
static bool isAutoBiographyNum(int number)
{
    int count = 0, position, size, digit;
    string NUM;

    // Convert integer to string
    NUM = number.ToString();
    size = NUM.Length;

    // Iterate for every digit to check
    // for their total count
    for(int i = 0; i < size; i++)
    {
       position = NUM[i] - '0';
       count = 0;

       // Check occurrence of every number
       // and count them
       for(int j = 0; j < size; j++)
       {
          digit = NUM[j] - '0';
          if (digit == i)
              count++;
       }

       // Check if any position mismatches 
       // with total count them return with 
       // false else continue with loop
       if (position != count)
           return false;
    }
    return true;
}

// Function to return the length of the
// largest subarray whose every element
// is a autobiographical number
static int checkArray(int []arr, int n)
{
    int current_length = 0;
    int max_length = 0;

    // Utility function which checks every element
    // of array for autobiographical number
    for(int i = 0; i < n; i++)
    {

       // Check if element arr[i] is an
       // autobiographical number
       if (isAutoBiographyNum(arr[i]) == true)
       {

           // Increment the current length
           current_length++;
       }
       else
       {
           current_length = 0;
       }

       // Update max_length value
       max_length = Math.Max(max_length,
                             current_length);
    }

    // Return the final result
    return max_length;
}

// Driver code
public static void Main (string[] args)
{
    int []arr = { 21200, 1, 1303, 1210, 2020 };
    int n = arr.Length;

    Console.WriteLine(checkArray(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // Javascript program to find the length of the
    // largest subarray whose every element is an
    // Autobiographical Number

    // function to check number is autobiographical
    function isAutoBiographyNum(number)
    {

        let count = 0, position, size, digit;
        let NUM;

        // Convert integer to string
        NUM = number.toString();
        size = NUM.length;

        // Iterate for every digit to check 
        // for their total count
        for (let i = 0; i < size; i++) {
            position = NUM[i].charCodeAt() - '0'.charCodeAt();
            count = 0;

            // Check occurrence of every number 
            // and count them
            for (let j = 0; j < size; j++) {
                digit = NUM[j].charCodeAt() - '0'.charCodeAt();
                if (digit == i)
                    count++;
            }

            // Check if any position mismatches with 
            // total count them return with false 
            // else continue with loop
            if (position != count)
                return false;
        }

        return true;
    }

    // Function to return the length of the
    // largest subarray whose every
    // element is a Autobiographical number
    function checkArray(arr, n)
    {

        let current_length = 0;
        let max_length = 0;

        // Utility function which checks every element 
        // of array for Autobiographical number
        for (let i = 0; i < n; i++) {

            // Check if element arr[i] is an 
            // Autobiographical number
            if (isAutoBiographyNum(arr[i]))
                // Increment the current length
                current_length++;

            else
                current_length = 0;

            // Update max_length value
            max_length = Math.max(max_length, current_length);
        }

        // Return the final result
        return max_length;
    }

    let arr = [ 21200, 1, 1303, 1210, 2020 ];

    let n = arr.length;

    document.write(checkArray(arr, n));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n * log n)