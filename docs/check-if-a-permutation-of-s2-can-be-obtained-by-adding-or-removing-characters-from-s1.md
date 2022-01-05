# 检查是否可以通过添加或删除 S1 的字符来获得 S2 的排列

> 原文:[https://www . geesforgeks . org/check-if-a-置换-S2-可以通过从-s1/](https://www.geeksforgeeks.org/check-if-a-permutation-of-s2-can-be-obtained-by-adding-or-removing-characters-from-s1/) 中添加或删除字符来获得

给定由 **N** 和 **M** 字符组成的两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S1** 和 **S2** ，任务是在从字符串 **S1** 中添加或删除一个字符 a [素数](https://www.geeksforgeeks.org/prime-numbers/)次后，检查字符串 **S1** 是否可以等于 **S2** 的任意排列。如果可能，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**S1 =“gekforgk”，S2 =“geeksforgeeks”
> **输出:**是
> **解释:**
> 如果字符‘e’被加 3(是素数)次，字符‘s’被加 2(是素数)次到 S1，那么它将是“gekforgkeeess”，这是 S2 的一个排列。因此，打印“是”。
> 
> **输入:**S1 =“xyzzyzz”，S2 =“xyy”
> T3】输出:否

**方法:**给定的问题可以通过[计算字符串中的字符频率](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)**【S1】**和 **S2** 来解决，如果任何字符频率的差异不是[质数](https://www.geeksforgeeks.org/tag/prime-number/)，则打印**“否”**。否则，打印**“是”**。按照以下步骤解决问题:

*   初始化频率阵列，说出 **256** 大小的 **freq[]** 。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**【S1】**中的字符，对于每个字符，将**freq【】**中的字符的[频率减少 **1** 。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**【S2】**的字符，对于每个字符，将**freq【】**中的字符频率增加 **1** 。
*   完成以上步骤后，如果**freq【】**中所有元素的绝对值都是质数，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// number is prime or not
bool isPrime(int n)
{

    // If the number is less than 2
    if (n <= 1)
        return false;

    // If the number is 2
    else if (n == 2)
        return true;

    // If N is a multiple of 2
    else if (n % 2 == 0)
        return false;

    // Otherwise, check for the
    // odds values
    for(int i = 3;i <= sqrt(n); i += 2)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to check if S1 can be
// a permutation of S2 by adding
// or removing characters from S1
void checkPermutation(string s1, string s2)
{

    // Initialize a frequency array
    int freq[26] = {0};

    // Decrement the frequency for
    // occurrence in s1
    for(char ch : s1)
    {
        freq[ch - 'a']--;
    }

    // Increment the frequency for
    // occurence in s2
    for(char ch : s2)
    {
        freq[ch - 'a']++;
    }

    bool isAllChangesPrime = true;

    for(int i = 0; i < 26; i++)
    {

        // If frequency of current
        // char is same in s1 and s2
        if (freq[i] == 0)
        {
            continue;
        }

        // Check the frequency for
        // the current char is not
        // prime
        else if (!isPrime(abs(freq[i])))
        {
            isAllChangesPrime = false;
            break;
        }
    }

    // Print the result
    if (isAllChangesPrime)
    {
        cout << "Yes";
    }
    else
    {
        cout << "No";
    }
}

// Driver Code
int main()
{
    string S1 = "gekforgk";
    string S2 = "geeksforgeeks";

    checkPermutation(S1, S2);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

    // Function to check if the given
    // number is prime or not
    private static boolean isPrime(int n)
    {
        // If the number is less than 2
        if (n <= 1)
            return false;

        // If the number is 2
        else if (n == 2)
            return true;

        // If N is a multiple of 2
        else if (n % 2 == 0)
            return false;

        // Otherwise, check for the
        // odds values
        for (int i = 3;
             i <= Math.sqrt(n); i += 2) {
            if (n % i == 0)
                return false;
        }
        return true;
    }

    // Function to check if S1 can be
    // a permutation of S2 by adding
    // or removing characters from S1
    private static void checkPermutation(
        String s1, String s2)
    {
        // Initialize a frequency array
        int freq[] = new int[26];

        // Decrement the frequency for
        // occurrence in s1
        for (char ch : s1.toCharArray()) {
            freq[ch - 'a']--;
        }

        // Increment the frequency for
        // occurence in s2
        for (char ch : s2.toCharArray()) {
            freq[ch - 'a']++;
        }

        boolean isAllChangesPrime = true;

        for (int i = 0; i < 26; i++) {

            // If frequency of current
            // char is same in s1 and s2
            if (freq[i] == 0) {
                continue;
            }

            // Check the frequency for
            // the current char is not
            // prime
            else if (!isPrime(
                         Math.abs(freq[i]))) {
                isAllChangesPrime = false;
                break;
            }
        }

        // Print the result
        if (isAllChangesPrime) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }

    // Driver Code
    public static void main(
        String[] args)
    {

        String S1 = "gekforgk";
        String S2 = "geeksforgeeks";
        checkPermutation(S1, S2);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

from math import sqrt
# Function to check if the given
# number is prime or not
def isPrime(n):
    # If the number is less than 2
    if (n <= 1):
        return False

    # If the number is 2
    elif(n == 2):
        return True

    # If N is a multiple of 2
    elif(n % 2 == 0):
        return False

    # Otherwise, check for the
    # odds values
    for i in range(3,int(sqrt(n))+1,2):
        if (n % i == 0):
            return False
    return True

# Function to check if S1 can be
# a permutation of S2 by adding
# or removing characters from S1
def checkPermutation(s1, s2):
    # Initialize a frequency array
    freq = [0 for i in range(26)]

    # Decrement the frequency for
    # occurrence in s1
    for ch in s1:
        if ord(ch) - 97 in freq:
            freq[ord(ch) - 97] -= 1
        else:
            freq[ord(ch) - 97] = 1

    # Increment the frequency for
    # occurence in s2
    for ch in s2:
        if ord(ch) - 97 in freq:
            freq[ord(ch) - 97] += 1
        else:
            freq[ord(ch) - 97] = 1

    isAllChangesPrime = True

    for i in range(26):
        # If frequency of current
        # char is same in s1 and s2
        if (freq[i] == 0):
            continue

        # Check the frequency for
        # the current char is not
        # prime
        elif(isPrime(abs(freq[i]))==False):
            isAllChangesPrime = False
            break

    # Print the result
    if (isAllChangesPrime==False):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    S1 = "gekforgk"
    S2 = "geeksforgeeks"

    checkPermutation(S1, S2)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the given
// number is prime or not
private static bool isPrime(int n)
{

    // If the number is less than 2
    if (n <= 1)
        return false;

    // If the number is 2
    else if (n == 2)
        return true;

    // If N is a multiple of 2
    else if (n % 2 == 0)
        return false;

    // Otherwise, check for the
    // odds values
    for(int i = 3; i <= Math.Sqrt(n); i += 2)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to check if S1 can be
// a permutation of S2 by adding
// or removing characters from S1
private static void checkPermutation(
    string s1, string s2)
{

    // Initialize a frequency array
    int[] freq = new int[26];

    // Decrement the frequency for
    // occurrence in s1
    foreach (char ch in s1.ToCharArray())
    {
        freq[ch - 'a']--;
    }

    // Increment the frequency for
    // occurence in s2
    foreach (char ch in s2.ToCharArray())
    {
        freq[ch - 'a']++;
    }

    bool isAllChangesPrime = true;

    for(int i = 0; i < 26; i++)
    {

        // If frequency of current
        // char is same in s1 and s2
        if (freq[i] == 0)
        {
            continue;
        }

        // Check the frequency for
        // the current char is not
        // prime
        else if (!isPrime(Math.Abs(freq[i])))
        {
            isAllChangesPrime = false;
            break;
        }
    }

    // Print the result
    if (isAllChangesPrime != false)
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}

// Driver Code
public static void Main(String[] args)
{
    string S1 = "gekforgk";
    string S2 = "geeksforgeeks";

    checkPermutation(S1, S2);
}
}

// This code is contributed by target_2
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if the given
    // number is prime or not
function isPrime(n)
{
    // If the number is less than 2
        if (n <= 1)
            return false;

        // If the number is 2
        else if (n == 2)
            return true;

        // If N is a multiple of 2
        else if (n % 2 == 0)
            return false;

        // Otherwise, check for the
        // odds values
        for (let i = 3;
             i <= Math.floor(Math.sqrt(n)); i += 2) {
            if (n % i == 0)
                return false;
        }
        return true;
}

// Function to check if S1 can be
    // a permutation of S2 by adding
    // or removing characters from S1
function checkPermutation(s1, s2)
{

    // Initialize a frequency array
        let freq = new Array(26);
        for(let i = 0; i < 26; i++)
            freq[i] = 0;

        // Decrement the frequency for
        // occurrence in s1
        for (let ch = 0; ch < s1.length; ch++) {
            freq[s1[ch].charCodeAt(0) - 'a'.charCodeAt(0)]--;
        }

        // Increment the frequency for
        // occurence in s2
        for (let ch = 0; ch < s2.length; ch++) {
            freq[s2[ch].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        let isAllChangesPrime = true;

        for (let i = 0; i < 26; i++)
        {

            // If frequency of current
            // char is same in s1 and s2
            if (freq[i] == 0) {
                continue;
            }

            // Check the frequency for
            // the current char is not
            // prime
            else if (!isPrime(
                         Math.abs(freq[i]))) {
                isAllChangesPrime = false;
                break;
            }
        }

        // Print the result
        if (isAllChangesPrime) {
            document.write("Yes");
        }
        else {
            document.write("No");
        }
}

// Driver Code
let S1 = "gekforgk";
let S2 = "geeksforgeeks";
checkPermutation(S1, S2);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(max(N，M))*
***辅助空间:** O(1)*