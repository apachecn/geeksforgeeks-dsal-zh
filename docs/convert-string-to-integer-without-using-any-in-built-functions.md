# 不使用任何内置函数将字符串转换为整数

> 原文:[https://www . geesforgeks . org/convert-string-to-integer-无需使用任何内置函数/](https://www.geeksforgeeks.org/convert-string-to-integer-without-using-any-in-built-functions/)

给定一个字符串 **str** ，任务是在不使用任何内置函数的情况下将给定的字符串转换为数字。

**示例:**

> **输入:** str = "985632"
> **输出:** 985632
> **说明:**
> 给定输入为字符串形式，返回输出为整数形式。
> 
> **输入:** str = "123"
> **输出:** 123
> **说明:**
> 给定输入为字符串形式，返回输出为整数形式。

**方式:**思路是从**48–57**开始使用 **0 到 9** 的数字的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)。
因此，要将数字字符更改为整数，请从字符的 ASCII 值中减去 **48** ，将给出给定字符的相应数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach 
#include <iostream> 
using namespace std; 

// Function to convert string to 
// integer without using functions 
void convert(string s) 
{ 
    // Initialize a variable 
    int num = 0; 
    int n = s.length(); 

    // Iterate till length of the string 
    for (int i = 0; i < n; i++) 

        // Subtract 48 from the current digit 
        num = num * 10 + (int(s[i]) - 48); 

    // Print the answer 
    cout << num; 
} 

// Driver Code 
int main() 
{ 
    // Given string of number 
    char s[] = "123"; 

    // Function Call 
    convert(s); 
    return 0; 
} 
```

## C

```
// C program for the above approach 
#include <stdio.h> 
#include <string.h> 

// Function to convert string to 
// integer without using functions 
void convert(char s[]) 
{ 
    // Initialize a variable 
    int num = 0; 
    int n = strlen(s); 

    // Iterate till length of the string 
    for (int i = 0; i < n; i++) 

        // Subtract 48 from the current digit 
        num = num * 10 + (s[i] - 48); 

    // Print the answer 
    printf("%d", num); 
} 

// Driver Code 
int main() 
{ 
    // Given string of number 
    char s[] = "123"; 

    // Function Call 
    convert(s); 
    return 0; 
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
class GFG{ 

// Function to convert string to 
// integer without using functions 
public static void convert(String s) 
{ 

    // Initialize a variable 
    int num = 0; 
    int n = s.length(); 

    // Iterate till length of the string 
    for(int i = 0; i < n; i++) 

        // Subtract 48 from the current digit 
        num = num * 10 + ((int)s.charAt(i) - 48); 

    // Print the answer 
    System.out.print(num); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // Given string of number 
    String s = "123"; 

    // Function Call 
    convert(s); 
} 
} 

// This code is contributed by divyeshrabadiya07 
```

## 蟒蛇 3

```
# Python3 program for the above approach 

# Function to convert string to 
# integer without using functions 
def convert(s): 

    # Initialize a variable 
    num = 0
    n = len(s) 

    # Iterate till length of the string 
    for i in s: 

        # Subtract 48 from the current digit 
        num = num * 10 + (ord(i) - 48) 

    # Print the answer 
    print(num) 

# Driver code 
if __name__ == '__main__': 

    # Given string of number 
    s = "123"

    # Function Call 
    convert(s) 

# This code is contributed by Shivam Singh 
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function to convert string to 
// integer without using functions 
public static void convert(string s) 
{ 

    // Initialize a variable 
    int num = 0; 
    int n = s.Length; 

    // Iterate till length of the string 
    for(int i = 0; i < n; i++) 

        // Subtract 48 from the current digit 
        num = num * 10 + ((int)s[i] - 48); 

    // Print the answer 
    Console.Write(num); 
} 

// Driver code
public static void Main(string[] args)
{

    // Given string of number 
    string s = "123"; 

    // Function call 
    convert(s); 
}
}

// This code is contributed by rock_cool
```

**Output:**

```
123

```

**时间复杂度:** *O(N)* ，其中 N 为给定字符串的长度。
**辅助空间:** *O(1)*