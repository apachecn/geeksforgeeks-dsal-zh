# 通过翻转字符来修改二进制字符串，使得由 1 组成的任何一对索引既不是同素的，也不能被彼此整除

> 原文:[https://www . geeksforgeeks . org/modify-a-binary-string-by-flips-这样任何一对由-1 组成的索引都不是同素的，也不能被彼此整除/](https://www.geeksforgeeks.org/modify-a-binary-string-by-flips-such-that-any-pair-of-indices-consisting-of-1s-are-neither-co-prime-nor-divisible-by-each-other/)

给定一个整数 **N** 和一个由 **4*N** 个**0**组成的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)，最初的任务是翻转字符，使得由 **1** s 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/)的任意两对索引既不是[同素](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)也不是可以被彼此整除的索引对。
***注:**考虑基于 **1 的**索引。*

**示例:**

> **输入:** N = 3，S =**“**000000000000”
> **输出:** 000000010101
> **说明:**在修改后的字符串“000000010101”中，1 的索引为{8，10，12}。在上述一组指数中，不存在任何一对同素且可被彼此整除的指数。
> 
> **输入:** N = 2，S =**【00000000】
> **输出:** 00000101**

****方法:**给定的问题可以基于这样的观察来解决:如果字符在位置 **4*N，4 * N–2，4 * N–4、…** 直到 **N 项**处翻转，则不存在任何一对可被彼此整除且具有 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 作为 **1** 的索引。**

**下面是上述方法的实现:**

## **C++**

```
#include <iostream>
using namespace std;

// Function to modify a string such
// that there doesn't exist any pair
// of indices consisting of 1s, whose
// GCD is 1 and are divisible by each other
void findString(char S[], int N)
{
  int strLen = 4 * N;

  // Flips characters at indices
  // 4N, 4N - 2, 4N - 4 .... upto N terms
  for (int i = 1; i <= N; i++) {

    S[strLen - 1] = '1';
    strLen -= 2;
  }

  // Print the string
  for (int i = 0; i < 4 * N; i++) {
    cout << S[i];
  }
}

// Driver code
int main()
{

  int N = 2;

  char S[4 * N];

  // Initialize the string S
  for (int i = 0; i < 4 * N; i++)
    S[i] = '0';
  // function call
  findString(S, N);
  return 0;
}

// This code is contributed by aditya7409.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to modify a string such
    // that there doesn't exist any pair
    // of indices consisting of 1s, whose
    // GCD is 1 and are divisible by each other
    public static void findString(char S[], int N)
    {
        int strLen = 4 * N;

        // Flips characters at indices
        // 4N, 4N - 2, 4N - 4 .... upto N terms
        for (int i = 1; i <= N; i++) {

            S[strLen - 1] = '1';
            strLen -= 2;
        }

        // Print the string
        System.out.println(S);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2;

        char S[] = new char[4 * N];

        // Initialize the string S
        for (int i = 0; i < 4 * N; i++)
            S[i] = '0';

        findString(S, N);
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to modify a string such
# that there doesn't exist any pair
# of indices consisting of 1s, whose
# GCD is 1 and are divisible by each other
def findString(S, N) :
  strLen = 4 * N

  # Flips characters at indices
  # 4N, 4N - 2, 4N - 4 .... upto N terms
  for i in range(1, N + 1):
    S[strLen - 1] = '1'
    strLen -= 2

  # Print the string
  for i in range(4 * N):
    print(S[i], end = "")

# Driver code

N = 2
S = [0] * (4 * N)

# Initialize the string S
for i in range(4 * N):
    S[i] = '0'

# function call
findString(S, N)

# This code is contributed by sanjoy_62.
```

## **C#**

```
// C# program to implement
// the above approach
using System;

public class GFG
{

    // Function to modify a string such
    // that there doesn't exist any pair
    // of indices consisting of 1s, whose
    // GCD is 1 and are divisible by each other
    public static void findString(char[] S, int N)
    {
        int strLen = 4 * N;

        // Flips characters at indices
        // 4N, 4N - 2, 4N - 4 .... upto N terms
        for (int i = 1; i <= N; i++) {

            S[strLen - 1] = '1';
            strLen -= 2;
        }

        // Print the string
        Console.WriteLine(S);
    }

// Driver Code
public static void Main(String[] args)
{
    int N = 2;
    char[] S = new char[4 * N];

    // Initialize the string S
    for (int i = 0; i < 4 * N; i++)
        S[i] = '0';

    findString(S, N);
}
}

// This code is contributed by souravghosh0416.
```

## **java 描述语言**

```
<script>
      // Function to modify a string such
      // that there doesn't exist any pair
      // of indices consisting of 1s, whose
      // GCD is 1 and are divisible by each other
      function findString(S, N) {
        var strLen = 4 * N;

        // Flips characters at indices
        // 4N, 4N - 2, 4N - 4 .... upto N terms
        for (var i = 1; i <= N; i++)
        {
          S[strLen - 1] = "1";
          strLen -= 2;
        }

        // Print the string
        for (var i = 0; i < 4 * N; i++)
        {
          document.write(S[i]);
        }
      }

      // Driver code
      var N = 2;
      var S = [...Array(4 * N)];

      // Initialize the string S
      for (var i = 0; i < 4 * N; i++) S[i] = "0";

      // function call
      findString(S, N);

      // This code is contributed by rdtank.
    </script>
```

****Output:** 

```
00000101
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**