# 如何将给定的数字转换成字符数组

> 原文:[https://www . geesforgeks . org/如何将给定数字转换为字符数组/](https://www.geeksforgeeks.org/how-to-convert-given-number-to-a-character-array/)

给定一个整数 **N，**的任务是将其转换成一个字符数组。

**示例:**

> **输入:** N = 2020
> **输出:** {2，0，2，0}
> **解释:**此处 char arr arr[]= { 2，0，2，0}
> **输入:** N = 12349
> **输出:** {1，2，3，4，9}
> **解释:**此处 char arr arr[]= { 1，2，3

**方法:**这样做的基本方法，是递归查找 N 的所有数字，并将其插入到所需的字符数组中。

1.  计算数字的总位数。
2.  在数字中声明一个字符数组。
3.  将整数分隔成数字，并将其容纳在字符数组中。
4.  在数组的每个元素中，字符“0”的加 ASCII 值为 48。

下面是上述方法的实现:

## C

```
// C program to convert integer
// number into character array

#include <stdio.h>
#include <stdlib.h>

// Function to convert integer to
// character array
char* convertIntegerToChar(int N)
{

    // Count digits in number N
    int m = N;
    int digit = 0;
    while (m) {

        // Increment number of digits
        digit++;

        // Truncate the last
        // digit from the number
        m /= 10;
    }

    // Declare char array for result
    char* arr;

    // Declare duplicate char array
    char arr1[digit];

    // Memory allocation of array
    arr = (char*)malloc(digit);

    // Separating integer into digits and
    // accommodate it to character array
    int index = 0;
    while (N) {

        // Separate last digit from
        // the number and add ASCII
        // value of character '0' is 48
        arr1[++index] = N % 10 + '0';

        // Truncate the last
        // digit from the number
        N /= 10;
    }

    // Reverse the array for result
    int i;
    for (i = 0; i < index; i++) {
        arr[i] = arr1[index - i];
    }

    // Char array truncate by null
    arr[i] = '\0';

    // Return char array
    return (char*)arr;
}

// Driver Code
int main()
{

    // Given number
    int N = 12349;
    int len = 5;

    // Function call
    char* arr = convertIntegerToChar(N);

    // Print char array
    for (int i = 0; i < len; i++)
        printf("%c, ", arr[i]);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert integer
// number into character array
class GFG{

// Function to convert integer to
// character array
static char[] convertIntegerToChar(int N)
{

    // Count digits in number N
    int m = N;
    int digit = 0;

    while (m > 0)
    {

        // Increment number of digits
        digit++;

        // Truncate the last
        // digit from the number
        m /= 10;
    }

    // Declare char array for result
    char[] arr;

    // Declare duplicate char array
    char []arr1 = new char[digit + 1];

    // Memory allocation of array
    arr = new char[digit];

    // Separating integer into digits and
    // accommodate it to character array
    int index = 0;

    while (N > 0)
    {

        // Separate last digit from
        // the number and add ASCII
        // value of character '0' is 48
        arr1[++index] = (char)(N % 10 + '0');

        // Truncate the last
        // digit from the number
        N /= 10;
    }

    // Reverse the array for result
    int i;
    for(i = 0; i < index; i++)
    {
        arr[i] = arr1[index - i];
    }

    // Return char array
    return (char[])arr;
}

// Driver Code
public static void main(String[] args)
{

    // Given number
    int N = 12349;
    int len = 5;

    // Function call
    char[] arr = convertIntegerToChar(N);

    // Print char array
    for(int i = 0; i < len; i++)
        System.out.printf("%c, ", arr[i]);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to convert integer
# number into character array

# Function to convert integer to
# character array
def convertIntegerToChar(N):

    # Count digits in number N
    m = N;
    digit = 0;

    while (m > 0):

        # Increment number of digits
        digit += 1;

        # Truncate the last
        # digit from the number
        m /= 10;   

    # Declare char array for result
    arr = ['0' for i in range(digit)]

    # Declare duplicate char array
    arr1 = ['0' for i in range(digit + 1)];

    # Separating integer
    # into digits and
    # accommodate it
    # to character array
    index = 0;

    while (N > 0):
        index += 1;

        # Separate last digit from
        # the number and add ASCII
        # value of character '0' is 48
        arr1[index] = chr(int(N % 10 + 48));       

        # Truncate the last
        # digit from the number
        N = N // 10;   

    # Reverse the array for result
    for i in range(0, index):
        arr[i] = arr1[index - i];   

    # Return char array
    return arr;

# Driver Code
if __name__ == '__main__':

    # Given number
    N = 12349;
    len = 5;

    # Function call
    arr = convertIntegerToChar(N);

    # Print array
    for i in range(0, len, 1):
        print(arr[i], end = " ");

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to convert integer
// number into character array
using System;

class GFG{

// Function to convert integer to
// character array
static char[] convertintToChar(int N)
{

    // Count digits in number N
    int m = N;
    int digit = 0;

    while (m > 0)
    {

        // Increment number of digits
        digit++;

        // Truncate the last
        // digit from the number
        m /= 10;
    }

    // Declare char array for result
    char[] arr;

    // Declare duplicate char array
    char []arr1 = new char[digit + 1];

    // Memory allocation of array
    arr = new char[digit];

    // Separating integer into digits and
    // accommodate it to character array
    int index = 0;

    while (N > 0)
    {

        // Separate last digit from
        // the number and add ASCII
        // value of character '0' is 48
        arr1[++index] = (char)(N % 10 + '0');

        // Truncate the last
        // digit from the number
        N /= 10;
    }

    // Reverse the array for result
    int i;
    for(i = 0; i < index; i++)
    {
        arr[i] = arr1[index - i];
    }

    // Return char array
    return (char[])arr;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number
    int N = 12349;
    int len = 5;

    // Function call
    char[] arr = convertintToChar(N);

    // Print char array
    for(int i = 0; i < len; i++)
        Console.Write("{0}, ", arr[i]);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript program to convert integer
    // number into character array

    // Function to convert integer to
    // character array
    function convertIntegerToChar(N)
    {

        // Count digits in number N
        let m = N;
        let digit = 0;

        while (m > 0)
        {

            // Increment number of digits
            digit++;

            // Truncate the last
            // digit from the number
            m = parseInt(m / 10, 10);
        }

        // Declare char array for result
        let arr;

        // Declare duplicate char array
        let arr1 = new Array(digit + 1);

        // Memory allocation of array
        arr = new Array(digit);

        // Separating integer into digits and
        // accommodate it to character array
        let index = 0;

        while (N > 0)
        {

            // Separate last digit from
            // the number and add ASCII
            // value of character '0' is 48
            arr1[++index] = String.fromCharCode(N % 10 + '0'.charCodeAt());

            // Truncate the last
            // digit from the number
            N = parseInt(N / 10, 10);
        }

        // Reverse the array for result
        let i;
        for(i = 0; i < index; i++)
        {
            arr[i] = arr1[index - i];
        }

        // Return char array
        return arr;
    }

    // Given number
    let N = 12349;
    let len = 5;

    // Function call
    let arr = convertIntegerToChar(N);

    // Print char array
    for(let i = 0; i < len; i++)
        document.write(arr[i] + ", ");

// This code is contributed by divyeshtsbsdiya07
</script>
```

**Output:** 

```
1, 2, 3, 4, 9,
```