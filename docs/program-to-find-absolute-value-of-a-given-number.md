# 程序求给定数的绝对值

> 原文:[https://www . geesforgeks . org/program-to-find-绝对值给定数字/](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)

给定一个整数 **N** ，任务是求给定整数的绝对值。
**例:**

> **输入:** N = -6
> **输出:** 6
> **输入:** N = 12
> **输出:** 12

**方法 1–天真方法:**因为任何数字的绝对值总是正的。对于任何正数，绝对值是数字本身，对于任何负数，绝对值是 **(-1)** 乘以负数。

## C++

```
// C++ program for Method 1
#include <bits/stdc++.h>
using namespace std;

// Function to find the absolute value
void findAbsolute(int N)
{

    // If the number is less than
    // zero, then multiply by (-1)
    if (N < 0)
    {
        N = (-1) * N;
    }

    // Print the absolute value
    cout << " " << N;
}

// Driver Code
int main()
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program for Method 1
#include <stdio.h>

// Function to find the absolute value
void findAbsolute(int N)
{

    // If the number is less than
    // zero, then multiply by (-1)
    if (N < 0) {
        N = (-1) * N;
    }

    // Print the absolute value
    printf("%d ", N);
}

// Driver Code
int main()
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Method 1
class GFG{

// Function to find the absolute value
static void findAbsolute(int N)
{

    // If the number is less than
    // zero, then multiply by (-1)
    if (N < 0)
    {
        N = (-1) * N;
    }

    // Print the absolute value
    System.out.printf("%d ", N);
}

// Driver Code
public static void main(String[] args)
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for Method 1

# Function to find the absolute value
def findAbsolute(N):

    # If the number is less than
    # zero, then multiply by (-1)
    if (N < 0):
        N = (-1) * N;

    # Print the absolute value
    print(N);

# Driver code
if __name__ == '__main__':

    # Given integer
    N = -12;

    # Function call
    findAbsolute(N);

# This is code contributed by amal kumar choubey
```

## C#

```
// C# program for Method 1
using System;
using System.Collections.Generic;

class GFG{

// Function to find the absolute value
static void findAbsolute(int N)
{

    // If the number is less than
    // zero, then multiply by (-1)
    if (N < 0)
    {
        N = (-1) * N;
    }

    // Print the absolute value
    Console.Write("{0} ", N);
}

// Driver Code
public static void Main(String[] args)
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
    // Javascript program for Method 1

    // Function to find the absolute value
    function findAbsolute(N)
    {

        // If the number is less than
        // zero, then multiply by (-1)
        if (N < 0) 
        {
            N = (-1) * N;
        }

        // Print the absolute value
        document.write(" " + N);
    }

    // Given integer
    let N = -12;

    // Function call
    findAbsolute(N);

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
12
```

**方法 2–使用位屏蔽:**由于负数存储在 [2s 补码形式](https://www.geeksforgeeks.org/1s-2s-complement-binary-number/)中，为了获得绝对值，我们必须切换数字的位，并将 1 添加到结果中。以下是步骤:

1.  将掩码设置为整数右移 31(假设使用 32 位存储整数)。

```
mask = n >> 31
```

2.  对于负数，上述步骤将掩码设置为 1 1 1 1 1 1 1 1，对于正数设置为 0 0 0 0 0 0 0。给定的数字加上掩码。

```
mask + n
```

2.  掩码+n 和掩码的异或给出绝对值。

```
(mask + n)^mask 
```

## C++

```
// C++ program for Method 2
#include <bits/stdc++.h>
using namespace std;
#define CHAR_BIT 8

// Function to find the absolute
// value
void findAbsolute(int N)
{

    // Find mask
    int mask = N >> (sizeof(int) * CHAR_BIT - 1);

    // Print the absolute value
    // by (mask + N)^mask
    cout << ((mask + N) ^ mask);
}

// Driver Code
int main()
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
    return 0;
}

// This code is contributed by Code_Mech
```

## C

```
// C program for Method 2
#include <stdio.h>
#define CHAR_BIT 8

// Function to find the absolute
// value
void findAbsolute(int N)
{

    // Find mask
    int mask
        = N
          >> (sizeof(int) * CHAR_BIT - 1);

    // Print the absolute value
    // by (mask + N)^mask
    printf("%d ", (mask + N) ^ mask);
}

// Driver Code
int main()
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Method 2
class GFG{

static final int CHAR_BIT = 8;

// Function to find the absolute value
static void findAbsolute(int N)
{

    // Find mask
    int mask = N >> (Integer.SIZE / 8 *
                         CHAR_BIT - 1);

    // Print the absolute value
    // by (mask + N)^mask
    System.out.printf("%d ", (mask + N) ^ mask);
}

// Driver Code
public static void main(String[] args)
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for Method 2
import sys

CHAR_BIT = 8;

# Function to find the absolute value
def findAbsolute(N):

    # Find mask
    mask = N >> (sys.getsizeof(int()) // 8 *
                              CHAR_BIT - 1);

    # Print the absolute value
    # by (mask + N)^mask
    print((mask + N) ^ mask);

# Driver Code
if __name__ == '__main__':

    # Given integer
    N = -12;

    # Function call
    findAbsolute(N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for Method 2
using System;

class GFG{

static readonly int CHAR_BIT = 8;

// Function to find the absolute value
static void findAbsolute(int N)
{

    // Find mask
    int mask = N >> (sizeof(int) / 8 *
                        CHAR_BIT - 1);

    // Print the absolute value
    // by (mask + N)^mask
    Console.Write((mask + N) ^ mask);
}

// Driver Code
public static void Main(String[] args)
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for Method 2

    let CHAR_BIT = 8;

    // Function to find the absolute value
    function findAbsolute(N)
    {

        // Find mask
        let mask = N >> (4 / 8 * CHAR_BIT - 1);

        // Print the absolute value
        // by (mask + N)^mask
        document.write((mask + N) ^ mask);
    }

    // Given integer
    let N = -12;

    // Function call
    findAbsolute(N);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
12
```

**方法 3–使用内置 abs()函数:**内置函数 [**abs()**](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/) 在 [stdlib.h](https://www.geeksforgeeks.org/whats-difference-between-and/) 库中查找任意数字的绝对值。
以下是上述方法的实施:

## C++

```
// C++ program for Method 3
# include<bits/stdc++.h>
using namespace std;

// Function to find the absolute
// value
void findAbsolute(int N)
{

    // Find absolute
    int X = abs(N);

    // Print the absolute value
    cout << X;
}

// Driver Code
int main()
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
    return 0;
}

// This code is contributed by Nidhi_biet
```

## C

```
// C program for Method 3

#include <stdio.h>
#include <stdlib.h>

// Function to find the absolute
// value
void findAbsolute(int N)
{

    // Find absolute
    int X = abs(N);

    // Print the absolute value
    printf("%d ", X);
}

// Driver Code
int main()
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Method 3
class GFG{

// Function to find the absolute
// value
static void findAbsolute(int N)
{

    // Find absolute
    int X = Math.abs(N);

    // Print the absolute value
    System.out.printf("%d", X);
}

// Driver Code
public static void main(String[] args)
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for Method 3
import math

# Function to find the absolute
# value
def findAbsolute(N):

    # Find absolute
    X = abs(N);

    # Print the absolute value
    print(X);

# Driver Code

# Given integer
N = -12;

# Function call
findAbsolute(N);

# This code is contributed by Nidhi_biet
```

## C#

```
// C# program for Method 3
using System;

class GFG{

// Function to find the absolute
// value
static void findAbsolute(int N)
{

    // Find absolute
    int X = Math.Abs(N);

    // Print the absolute value
    Console.Write("{0}", X);
}

// Driver Code
public static void Main(String[] args)
{

    // Given integer
    int N = -12;

    // Function call
    findAbsolute(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for Method 3

    // Function to find the absolute
    // value
    function findAbsolute(N)
    {

        // Find absolute
        let X = Math.abs(N);

        // Print the absolute value
        document.write(X);
    }

    // Given integer
    let N = -12;

    // Function call
    findAbsolute(N);

</script>
```

**Output:** 

```
12
```