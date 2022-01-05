# 在数组元素的二进制表示中找到给定二进制模式的出现

> 原文:[https://www . geeksforgeeks . org/find-给定二进制数组元素的二进制模式表示出现次数/](https://www.geeksforgeeks.org/find-the-occurrence-of-the-given-binary-pattern-in-the-binary-representation-of-the-array-elements/)

给定一个由正整数 **N** 组成的数组 **arr[]** 和一个由集合 **{0，1}** 中的字符组成的字符串 **patt** ，任务是在给定数组的每个整数的二进制表示中找到 **patt** 的计数出现。
**举例:**

> **输入:** arr[] = {5，106，7，8}，patt = "10"
> **输出:** 1 3 0 1
> 二进制(5) = 101 - >发生(10) = 1
> 二进制(106) = 1101010 - >发生(10) = 3
> 二进制(7) = 111 - >发生(10) = 0
> 二进制(8

**方法:**找到每个数组元素的二进制表示，如[这篇](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)文章中所讨论的。
现在，在先前找到的二进制表示中找到给定模式的出现。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the binary
// representation of n
string decToBinary(int n)
{
    // Array to store binary representation
    int binaryNum[32];

    // Counter for binary array
    int i = 0;
    while (n > 0) {

        // Storing remainder in binary array
        binaryNum[i] = n % 2;
        n = n / 2;
        i++;
    }

    // To store the binary representation
    // as a string
    string binary = "";
    for (int j = i - 1; j >= 0; j--)
        binary += to_string(binaryNum[j]);

    return binary;
}

// Function to return the frequency of
// pat in the given string txt
int countFreq(string& pat, string& txt)
{
    int M = pat.length();
    int N = txt.length();
    int res = 0;

    /* A loop to slide pat[] one by one */
    for (int i = 0; i <= N - M; i++) {
        /* For current index i, check for 
           pattern match */
        int j;
        for (j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;

        // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M) {
            res++;
            j = 0;
        }
    }
    return res;
}

// Function to find the occurrence of
// the given pattern in the binary
// representation of elements of arr[]
void findOccurrence(int arr[], int n, string pattern)
{

    // For every element of the array
    for (int i = 0; i < n; i++) {

        // Find its binary representation
        string binary = decToBinary(arr[i]);

        // Print the occurrence of the given pattern
        // in its binary representation
        cout << countFreq(pattern, binary) << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 106, 7, 8 };
    string pattern = "10";
    int n = sizeof(arr) / sizeof(arr[0]);

    findOccurrence(arr, n, pattern);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the binary
    // representation of n
    static String decToBinary(int n)
    {
        // Array to store binary representation
        int[] binaryNum = new int[32];

        // Counter for binary array
        int i = 0;
        while (n > 0)
        {

            // Storing remainder in binary array
            binaryNum[i] = n % 2;
            n = n / 2;
            i++;
        }

        // To store the binary representation
        // as a string
        String binary = "";
        for (int j = i - 1; j >= 0; j--)
        {
            binary += String.valueOf(binaryNum[j]);
        }
        return binary;
    }

    // Function to return the frequency of
    // pat in the given string txt
    static int countFreq(String pat, String txt)
    {
        int M = pat.length();
        int N = txt.length();
        int res = 0;

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++)
        {
            /* For current index i, check for
            pattern match */
            int j;
            for (j = 0; j < M; j++)
            {
                if (txt.charAt(i + j) != pat.charAt(j))
                {
                    break;
                }
            }

            // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
            if (j == M)
            {
                res++;
                j = 0;
            }
        }
        return res;
    }

    // Function to find the occurrence of
    // the given pattern in the binary
    // representation of elements of arr[]
    static void findOccurrence(int arr[], int n,
                               String pattern)
    {

        // For every element of the array
        for (int i = 0; i < n; i++)
        {

            // Find its binary representation
            String binary = decToBinary(arr[i]);

            // Print the occurrence of the given pattern
            // in its binary representation
            System.out.print(countFreq(pattern,
                                       binary) + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {5, 106, 7, 8};
        String pattern = "10";
        int n = arr.length;
        findOccurrence(arr, n, pattern);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the binary
# representation of n
def decToBinary(n):

    # Array to store binary representation
    binaryNum = [0 for i in range(32)]

    # Counter for binary array
    i = 0
    while (n > 0):

        # Storing remainder in binary array
        binaryNum[i] = n % 2
        n = n // 2
        i += 1

    # To store the binary representation
    # as a string
    binary = ""
    for j in range(i - 1, -1, -1):
        binary += str(binaryNum[j])

    return binary

# Function to return the frequency of
# pat in the given txt
def countFreq(pat, txt):
    M = len(pat)
    N = len(txt)
    res = 0

    # A loop to slide pat[] one by one
    for i in range(N - M + 1):

        # For current index i, check for
        # pattern match
        j = 0
        while(j < M):
            if (txt[i + j] != pat[j]):
                break
            j += 1

        # If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M):
            res += 1
            j = 0

    return res

# Function to find the occurrence of
# the given pattern in the binary
# representation of elements of arr[]
def findOccurrence(arr, n, pattern):

    # For every element of the array
    for i in range(n):

        # Find its binary representation
        binary = decToBinary(arr[i])

        # Print the occurrence of the given pattern
        # in its binary representation
        print(countFreq(pattern, binary), end = " ")

# Driver code
arr = [5, 106, 7, 8]
pattern = "10"
n = len(arr)

findOccurrence(arr, n, pattern)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# code implementation for above approach
using System;

class GFG
{

    // Function to return the binary
    // representation of n
    static String decToBinary(int n)
    {
        // Array to store binary representation
        int[] binaryNum = new int[32];

        // Counter for binary array
        int i = 0;
        while (n > 0)
        {

            // Storing remainder in binary array
            binaryNum[i] = n % 2;
            n = n / 2;
            i++;
        }

        // To store the binary representation
        // as a string
        String binary = "";
        for (int j = i - 1; j >= 0; j--)
        {
            binary += String.Join("", binaryNum[j]);
        }
        return binary;
    }

    // Function to return the frequency of
    // pat in the given string txt
    static int countFreq(String pat, String txt)
    {
        int M = pat.Length;
        int N = txt.Length;
        int res = 0;

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++)
        {
            /* For current index i, check for
            pattern match */
            int j;
            for (j = 0; j < M; j++)
            {
                if (txt[i + j] != pat[j])
                {
                    break;
                }
            }

            // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
            if (j == M)
            {
                res++;
                j = 0;
            }
        }
        return res;
    }

    // Function to find the occurrence of
    // the given pattern in the binary
    // representation of elements of arr[]
    static void findOccurrence(int []arr, int n,
                               String pattern)
    {

        // For every element of the array
        for (int i = 0; i < n; i++)
        {

            // Find its binary representation
            String binary = decToBinary(arr[i]);

            // Print the occurrence of the given pattern
            // in its binary representation
            Console.Write(countFreq(pattern,
                                    binary) + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {5, 106, 7, 8};
        String pattern = "10";
        int n = arr.Length;
        findOccurrence(arr, n, pattern);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the binary
// representation of n
function decToBinary(n)
{
    // Array to store binary representation
    var binaryNum = Array(32);

    // Counter for binary array
    var i = 0;
    while (n > 0) {

        // Storing remainder in binary array
        binaryNum[i] = n % 2;
        n = parseInt(n / 2);
        i++;
    }

    // To store the binary representation
    // as a string
    var binary = "";
    for (var j = i - 1; j >= 0; j--)
        binary += (binaryNum[j].toString());

    return binary;
}

// Function to return the frequency of
// pat in the given string txt
function countFreq(pat, txt)
{
    var M = pat.length;
    var N = txt.length;
    var res = 0;

    /* A loop to slide pat[] one by one */
    for (var i = 0; i <= N - M; i++) {
        /* For current index i, check for 
           pattern match */
        var j;
        for (j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;

        // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M) {
            res++;
            j = 0;
        }
    }
    return res;
}

// Function to find the occurrence of
// the given pattern in the binary
// representation of elements of arr[]
function findOccurrence(arr, n, pattern)
{

    // For every element of the array
    for (var i = 0; i < n; i++) {

        // Find its binary representation
        var binary = decToBinary(arr[i]);

        // Print the occurrence of the given pattern
        // in its binary representation
        document.write( countFreq(pattern, binary) + " ");
    }
}

// Driver code
var arr = [ 5, 106, 7, 8 ];
var pattern = "10";
var n = arr.length;
findOccurrence(arr, n, pattern);

</script>
```

**Output:** 

```
1 3 0 1
```