# 检查两个整数是否彼此为异序词

> 原文：[https://www.geeksforgeeks.org/check-if-two-integer-are-anagrams-of-each-other/](https://www.geeksforgeeks.org/check-if-two-integer-are-anagrams-of-each-other/)

给定两个整数`A`和`B`，任务是检查给定的数字是否彼此为[异序词](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。 就像字符串一样，如果仅通过对数字进行改组就可以使该数字等于其他数字，则该数字被称为其他数字的类似物。

**示例**：

> **输入**：`A = 204, B = 240`
> **输出**：`Yes`
> 
> **输入**：`A = 23, B = 959`
> **输出**：`No`

**方法**：创建两个数组`freqA[]`和`freqB[]`其中`freqA[i]`和`freqB[i]`将分别存储`a`和`b`中数字`i`的频率。 现在遍历频率数组，如果`freqA[i] != freqB[i]`，则对于任何数字`i`，数字均不是彼此的异序词。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

const int TEN = 10; 

// Function to update the frequency array 
// such that freq[i] stores the 
// frequency of digit i in n 
void updateFreq(int n, int freq[]) 
{ 

    // While there are digits 
    // left to process 
    while (n) { 
        int digit = n % TEN; 

        // Update the frequency of 
        // the current digit 
        freq[digit]++; 

        // Remove the last digit 
        n /= TEN; 
    } 
} 

// Function that returns true if a and b 
// are anagarams of each other 
bool areAnagrams(int a, int b) 
{ 

    // To store the frequencies of 
    // the digits in a and b 
    int freqA[TEN] = { 0 }; 
    int freqB[TEN] = { 0 }; 

    // Update the frequency of 
    // the digits in a 
    updateFreq(a, freqA); 

    // Update the frequency of 
    // the digits in b 
    updateFreq(b, freqB); 

    // Match the frequencies of 
    // the common digits 
    for (int i = 0; i < TEN; i++) { 

        // If frequency differs for any digit 
        // then the numbers are not 
        // anagrams of each other 
        if (freqA[i] != freqB[i]) 
            return false; 
    } 

    return true; 
} 

// Driver code 
int main() 
{ 
    int a = 240, b = 204; 

    if (areAnagrams(a, b)) 
        cout << "Yes"; 
    else
        cout << "No"; 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG 
{ 
    static final int TEN = 10; 

    // Function to update the frequency array 
    // such that freq[i] stores the 
    // frequency of digit i in n 
    static void updateFreq(int n, int [] freq) 
    { 

        // While there are digits 
        // left to process 
        while (n > 0) 
        { 
            int digit = n % TEN; 

            // Update the frequency of 
            // the current digit 
            freq[digit]++; 

            // Remove the last digit 
            n /= TEN; 
        } 
    } 

    // Function that returns true if a and b 
    // are anagarams of each other 
    static boolean areAnagrams(int a, int b) 
    { 

        // To store the frequencies of 
        // the digits in a and b 
        int [] freqA = new int[TEN]; 
        int [] freqB = new int[TEN]; 

        // Update the frequency of 
        // the digits in a 
        updateFreq(a, freqA); 

        // Update the frequency of 
        // the digits in b 
        updateFreq(b, freqB); 

        // Match the frequencies of 
        // the common digits 
        for (int i = 0; i < TEN; i++)  
        { 

            // If frequency differs for any digit 
            // then the numbers are not 
            // anagrams of each other 
            if (freqA[i] != freqB[i]) 
                return false; 
        } 
        return true; 
    } 

    // Driver code 
    public static void main (String[] args) 
    { 
        int a = 204, b = 240; 

        if (areAnagrams(a, b)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

// This code is contributed by ihirtik 

```

## Python3

```py

# Python3 implementation of the approach  
TEN = 10

# Function to update the frequency array  
# such that freq[i] stores the  
# frequency of digit i in n  
def updateFreq(n, freq) : 

    # While there are digits  
    # left to process  
    while (n) :  
        digit = n % TEN  

        # Update the frequency of  
        # the current digit  
        freq[digit] += 1

        # Remove the last digit  
        n //= TEN  

# Function that returns true if a and b  
# are anagarams of each other  
def areAnagrams(a, b):  

    # To store the frequencies of  
    # the digits in a and b  
    freqA = [ 0 ] * TEN  
    freqB = [ 0 ] * TEN 

    # Update the frequency of  
    # the digits in a  
    updateFreq(a, freqA)  

    # Update the frequency of  
    # the digits in b  
    updateFreq(b, freqB)  

    # Match the frequencies of  
    # the common digits  
    for i in range(TEN):  

        # If frequency differs for any digit  
        # then the numbers are not  
        # anagrams of each other  
        if (freqA[i] != freqB[i]):  
            return False

    return True

# Driver code  
a = 240
b = 204

if (areAnagrams(a, b)):  
    print("Yes")  
else: 
    print("No")  

# This code is contributed by 
# divyamohan123 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 
    static int TEN = 10; 

    // Function to update the frequency array 
    // such that freq[i] stores the 
    // frequency of digit i in n 
    static void updateFreq(int n, int [] freq) 
    { 

        // While there are digits 
        // left to process 
        while (n > 0) 
        { 
            int digit = n % TEN; 

            // Update the frequency of 
            // the current digit 
            freq[digit]++; 

            // Remove the last digit 
            n /= TEN; 
        } 
    } 

    // Function that returns true if a and b 
    // are anagarams of each other 
    static bool areAnagrams(int a, int b) 
    { 

        // To store the frequencies of 
        // the digits in a and b 
        int [] freqA = new int[TEN]; 
        int [] freqB = new int[TEN];; 

        // Update the frequency of 
        // the digits in a 
        updateFreq(a, freqA); 

        // Update the frequency of 
        // the digits in b 
        updateFreq(b, freqB); 

        // Match the frequencies of 
        // the common digits 
        for (int i = 0; i < TEN; i++)  
        { 

            // If frequency differs for any digit 
            // then the numbers are not 
            // anagrams of each other 
            if (freqA[i] != freqB[i]) 
                return false; 
        } 
        return true; 
    } 

    // Driver code 
    public static void Main () 
    { 
        int a = 204, b = 240; 

        if (areAnagrams(a, b)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed by ihirtik 

```

**Output:**

```
Yes

```



* * *

* * *



