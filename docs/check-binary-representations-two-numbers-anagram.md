# 检查两个数字的二进制表示是否是字谜

> 原文:[https://www . geeksforgeeks . org/check-binary-表象-二进制-数字-字谜/](https://www.geeksforgeeks.org/check-binary-representations-two-numbers-anagram/)

给定两个数字，你需要检查它们在二进制表示中是否是彼此的字谜。
**例:**

```
Input : a = 8, b = 4 
Output : Yes
Binary representations of both
numbers have same 0s and 1s.

Input : a = 4, b = 5
Output : No
```

**简单方法:**

1.  使用简单的十进制到二进制表示技术找到“a”和“b”的二进制表示。
2.  检查两个二进制表示是否是字谜

## C++

```
// A simple C++ program to check if binary
// representations of two numbers are anagram.
#include <bits/stdc++.h>
#define ull unsigned long long int
using namespace std;

const int SIZE = 8 * sizeof(ull);

bool bit_anagram_check(ull a, ull b)
{
    // Find reverse binary representation of a
    // and store it in binary_a[]
    int i = 0, binary_a[SIZE] = { 0 };
    while (a > 0) {
        binary_a[i] = a % 2;
        a /= 2;
        i++;
    }

    // Find reverse binary representation of b
    // and store it in binary_a[]
    int j = 0, binary_b[SIZE] = { 0 };
    while (b > 0) {
        binary_b[j] = b % 2;
        b /= 2;
        j++;
    }

    // Sort two binary representations
    sort(binary_a, binary_a + SIZE);
    sort(binary_b, binary_b + SIZE);

    // Compare two sorted binary representations
    for (int i = 0; i < SIZE; i++)
        if (binary_a[i] != binary_b[i])
            return false;

    return true;
}

// Driver code
int main()
{
    ull a = 8, b = 4;
    cout << bit_anagram_check(a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to check if binary
// representations of two numbers are anagram
import java.io.*;
import java.util.*;

class GFG
{
    public static int SIZE = 8;

    // Function to check if binary representation
    // of two numbers are anagram
    static int bit_anagram_check(long a, long b)
    {
        // Find reverse binary representation of a
        // and store it in binary_a[]
        int i = 0;
        long[] binary_a = new long[SIZE];
        Arrays.fill(binary_a, 0);
        while (a > 0)
        {
            binary_a[i] = a%2;
            a /= 2;
            i++;
        }

        // Find reverse binary representation of b
        // and store it in binary_a[]
        int j = 0;
        long[] binary_b = new long[SIZE];
        Arrays.fill(binary_b, 0);
        while (b > 0)
        {
            binary_b[j] = b%2;
            b /= 2;
            j++;
        }

        // Sort two binary representations
        Arrays.sort(binary_a);
        Arrays.sort(binary_b);

        // Compare two sorted binary representations
        for (i = 0; i < SIZE; i++)
            if (binary_a[i] != binary_b[i])
                return 0;

        return 1;
    }

    // driver program
    public static void main (String[] args)
    {
        long a = 8, b = 4;
        System.out.println(bit_anagram_check(a, b));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# A simple C++ program to check if binary
# representations of two numbers are anagram.
SIZE = 8
def bit_anagram_check(a, b):

    # Find reverse binary representation of a
    # and store it in binary_a[]
    global size

    i = 0
    binary_a = [0] * SIZE
    while (a > 0):
        binary_a[i] = a % 2
        a //= 2
        i += 1

    # Find reverse binary representation of b
    # and store it in binary_a[]
    j = 0
    binary_b = [0] * SIZE
    while (b > 0):
        binary_b[j] = b % 2
        b //= 2
        j += 1

    # Sort two binary representations
    binary_a.sort()
    binary_b.sort()

    # Compare two sorted binary representations
    for i in range(SIZE):
        if (binary_a[i] != binary_b[i]):
            return 0
    return 1

# Driver code
if __name__ == "__main__":

    a = 8
    b = 4
    print(bit_anagram_check(a, b))

    # This code is contributed by ukasp.
```

## C#

```
// A simple C# program to check if
// binary representations of two
// numbers are anagram
using System;

class GFG
{
public static int SIZE = 8;

// Function to check if binary
// representation of two numbers
// are anagram
public static int bit_anagram_check(long a,
                                    long b)
{
    // Find reverse binary representation
    // of a and store it in binary_a[]
    int i = 0;
    long[] binary_a = new long[SIZE];
    Arrays.Fill(binary_a, 0);
    while (a > 0)
    {
        binary_a[i] = a % 2;
        a /= 2;
        i++;
    }

    // Find reverse binary representation 
    // of b and store it in binary_a[]
    int j = 0;
    long[] binary_b = new long[SIZE];
    Arrays.Fill(binary_b, 0);
    while (b > 0)
    {
        binary_b[j] = b % 2;
        b /= 2;
        j++;
    }

    // Sort two binary representations
    Array.Sort(binary_a);
    Array.Sort(binary_b);

    // Compare two sorted binary
    // representations
    for (i = 0; i < SIZE; i++)
    {
        if (binary_a[i] != binary_b[i])
        {
            return 0;
        }
    }

    return 1;
}

public static class Arrays
{
public static T[] CopyOf<T>(T[] original,
                            int newLength)
{
    T[] dest = new T[newLength];
    System.Array.Copy(original, dest, newLength);
    return dest;
}

public static T[] CopyOfRange<T>(T[] original,
                                 int fromIndex,
                                 int toIndex)
{
    int length = toIndex - fromIndex;
    T[] dest = new T[length];
    System.Array.Copy(original, fromIndex,
                         dest, 0, length);
    return dest;
}

public static void Fill<T>(T[] array, T value)
{
    for (int i = 0; i < array.Length; i++)
    {
        array[i] = value;
    }
}

public static void Fill<T>(T[] array, int fromIndex,
                           int toIndex, T value)
{
    for (int i = fromIndex; i < toIndex; i++)
    {
        array[i] = value;
    }
}
}

// Driver Code
public static void Main(string[] args)
{
    long a = 8, b = 4;
    Console.WriteLine(bit_anagram_check(a, b));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// A simple Javascript program to check if binary
// representations of two numbers are anagram

    let SIZE = 8;

    // Function to check if binary representation
    // of two numbers are anagram
    function bit_anagram_check(a,b)
    {
        // Find reverse binary representation of a
        // and store it in binary_a[]
        let i = 0;
        let binary_a = new Array(SIZE);
        for(let i=0;i<SIZE;i++)
        {
            binary_a[i]=0;
        }
        while (a > 0)
        {
            binary_a[i] = a%2;
            a = Math.floor(a/2);
            i++;
        }

        // Find reverse binary representation of b
        // and store it in binary_a[]
        let j = 0;
        let binary_b = new Array(SIZE);
        for(let i=0;i<SIZE;i++)
        {
            binary_b[i]=0;
        }
        while (b > 0)
        {
            binary_b[j] = b%2;
            b = Math.floor(b/2);
            j++;
        }

        // Sort two binary representations
        binary_a.sort(function(a,b){return a-b;});
        binary_b.sort(function(a,b){return a-b;});

        // Compare two sorted binary representations
        for (i = 0; i < SIZE; i++)
            if (binary_a[i] != binary_b[i])
                return 0;

        return 1;
    }

    // driver program
    let a = 8, b = 4;
    document.write(bit_anagram_check(a, b));

    //This code is contributed by rag2127

</script>
```

**输出:**

```
1
```

请注意，上面的代码使用了 GCC 特定的函数。如果我们希望为其他编译器编写代码，我们可以使用[计数整数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)中的设置位。
**时间复杂度:** O (1)
**辅助空间:** O (1)没有多余的空间被使用。
本文由 [**阿迪蒂亚·古普塔**](https://www.linkedin.com/in/aditya-gupta-437504a7?trk=hp-identity-name) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。