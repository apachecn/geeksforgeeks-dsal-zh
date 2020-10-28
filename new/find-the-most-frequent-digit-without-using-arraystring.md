# 查找最频繁的数字而不使用数组/字符串

给定一个整数，找到其中出现最多的数字。 如果两个或多个数字出现相同的次数，则返回它们中的最高位。 输入整数作为 int 变量而不是字符串或数组给出。 不允许使用哈希，数组或字符串。

**示例**：

```
Input:  x = 12234
Output: The most frequent digit is 2

Input:  x = 1223377
Output: The most frequent digit is 7

Input:  x = 5
Output: The most frequent digit is 5

Input:  x = 1000
Output: The most frequent digit is 0

```

**我们强烈建议您最小化浏览器，然后自己尝试。**

我们可以创建大小为 10 的映射并存储所有数字的计数，但不允许使用任何数组/字符串。

这个想法很简单，我们编写了一个函数来计算给定整数中给定数字的出现次数。 然后，我们计算给定整数中从 0 到 9 的所有数字。 每当计数大于或等于先前计数时，我们都会不断更新最大计数。 下面是实现。

## C++

```cpp

// Finds maximum occurring digit without using any array/string 
#include <bits/stdc++.h> 
using namespace std; 

// Simple function to count occurrences of digit d in x 
int countOccurrences(long int x, int d) 
{ 
    int count = 0;  // Initialize count of digit d 
    while (x) 
    { 
        // Increment count if current digit is same as d 
        if (x%10 == d) 
           count++; 
        x = x/10; 
    } 
    return count; 
} 

// Returns the max occurring digit in x 
int maxOccurring(long int x) 
{ 
   // Handle negative number 
   if (x < 0) 
      x = -x; 

   int result = 0; // Initialize result which is a digit 
   int max_count = 1; // Initialize count of result 

   // Traverse through all digits 
   for (int d=0; d<=9; d++) 
   { 
      // Count occurrences of current digit 
      int count = countOccurrences(x, d); 

      // Update max_count and result if needed 
      if (count >= max_count) 
      { 
         max_count = count; 
         result = d; 
      } 
   } 
   return result; 
} 

// Driver program 
int main() 
{ 
    long int x = 1223355; 
    cout << "Max occurring digit is " << maxOccurring(x); 
    return 0; 
} 

```

## Java

```java

// Finds maximum occurring digit 
// without using any array/string 
import java.io.*; 

class GFG  
{ 

// Simple function to count  
// occurrences of digit d in x 
static int countOccurrences(int x,  
                            int d) 
{ 
    // Initialize count 
    // of digit d 
    int count = 0;  
    while (x > 0) 
    { 
        // Increment count if 
        // current digit is 
        // same as d 
        if (x % 10 == d) 
        count++; 
        x = x / 10; 
    } 
    return count; 
} 

// Returns the max  
// occurring digit in x 
static int maxOccurring( int x) 
{ 

// Handle negative number 
if (x < 0) 
    x = -x; 

// Initialize result  
// which is a digit 
int result = 0;  

// Initialize count  
// of result 
int max_count = 1;  

// Traverse through 
// all digits 
for (int d = 0; d <= 9; d++) 
{ 
    // Count occurrences 
    // of current digit 
    int count = countOccurrences(x, d); 

    // Update max_count 
    // and result if needed 
    if (count >= max_count) 
    { 
        max_count = count; 
        result = d; 
    } 
} 
return result; 
} 

// Driver Code 
public static void main (String[] args)  
{ 
    int x = 1223355; 
    System.out.println("Max occurring digit is " + 
                                 maxOccurring(x)); 

} 
} 

// This code is contributed 
// by akt_mit 

```

## Python3

```py

# Finds maximum occurring digit  
# without using any array/string  

# Simple function to count  
# occurrences of digit d in x  
def countOccurrences(x, d): 
    count = 0; # Initialize count 
               # of digit d  
    while (x):  

        # Increment count if current 
        # digit is same as d  
        if (x % 10 == d): 
            count += 1;  
        x = int(x / 10);  

    return count;  

# Returns the max occurring 
# digit in x  
def maxOccurring(x): 

    # Handle negative number  
    if (x < 0): 
        x = -x; 

    result = 0; # Initialize result  
                # which is a digit 
    max_count = 1; # Initialize count  
                   # of result  

    # Traverse through all digits 
    for d in range(10): 

        # Count occurrences of current digit 
        count = countOccurrences(x, d); 

        # Update max_count and  
        # result if needed 
        if (count >= max_count): 
            max_count = count; 
            result = d; 

    return result;  

# Driver Code  
x = 1223355;  
print("Max occurring digit is",  
              maxOccurring(x));  

# This code is contributed by mits. 

```

## C#

```cs

// Finds maximum occurring digit 
// without using any array/string 
class GFG  
{ 

// Simple function to count  
// occurrences of digit d in x 
static int countOccurrences(int x, int d) 
{ 
    // Initialize count 
    // of digit d 
    int count = 0;  
    while (x > 0) 
    { 
        // Increment count if 
        // current digit is 
        // same as d 
        if (x % 10 == d) 
        count++; 
        x = x / 10; 
    } 
    return count; 
} 

// Returns the max  
// occurring digit in x 
static int maxOccurring( int x) 
{ 

// Handle negative number 
if (x < 0) 
    x = -x; 

// Initialize result  
// which is a digit 
int result = 0;  

// Initialize count  
// of result 
int max_count = 1;  

// Traverse through 
// all digits 
for (int d = 0; d <= 9; d++) 
{ 
    // Count occurrences 
    // of current digit 
    int count = countOccurrences(x, d); 

    // Update max_count 
    // and result if needed 
    if (count >= max_count) 
    { 
        max_count = count; 
        result = d; 
    } 
} 
return result; 
} 

// Driver Code 
static void Main()  
{ 
    int x = 1223355; 
    System.Console.WriteLine("Max occurring digit is " +  
                                       maxOccurring(x)); 
} 
} 

// This code is contributed by mits 

```

## PHP

```php

<?php 
// Finds maximum occurring digit 
// without using any array/string  

// Simple function to count  
// occurrences of digit d in x  
function countOccurrences($x, $d)  
{  
    // Initialize count of digit d  
    $count = 0;  
    while ($x)  
    {  
        // Increment count if current 
        // digit is same as d  
        if ($x % 10 == $d)  
        $count++;  
        $x = (int)($x / 10);  
    }  
    return $count;  
}  

// Returns the max occurring  
// digit in x  
function maxOccurring($x)  
{  
// Handle negative number  
if ($x < 0)  
    $x = -$x;  

$result = 0; // Initialize result 
             // which is a digit  
$max_count = 1; // Initialize count of result  

// Traverse through all digits  
for ($d = 0; $d <= 9; $d++)  
{  
    // Count occurrences of  
    // current digit  
    $count = countOccurrences($x, $d);  

    // Update max_count and result 
    // if needed  
    if ($count >= $max_count)  
    {  
        $max_count = $count;  
        $result = $d;  
    }  
}  
return $result;  
}  

// Driver Code  
$x = 1223355;  
echo "Max occurring digit is " .  
               maxOccurring($x);  

// This code is contributed by mits 
?> 

```

**Output:**

```
Max occurring digit is 5
```

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

