# 从给定数量的最低有效位开始翻转连续的设置位

> 原文:[https://www . geeksforgeeks . org/flip-连续设置位-从给定数字的 lsb 开始/](https://www.geeksforgeeks.org/flip-consecutive-set-bits-starting-from-lsb-of-a-given-number/)

给定一个正整数 **N** ，任务是从 **N** 的二进制表示中的 LSB 开始，通过翻转连续的**设定位**来找到可以得到的数。

**示例:**

> **输入:** N = 39
> **输出:** 32
> **解释:**
> 二进制表示(39)<sub>10</sub>=(100111)<sub>2</sub>
> 从 LSB 开始翻转所有连续的置位后，得到的数为(100000)
> 二进制表示(32) <sub>10</sub> 为(100006)
> 
> **输入:** N = 4
> **输出:** 4
> **解释:**
> 二进制表示(4)<sub>10</sub>=(100)<sub>2</sub>
> 由于没有设置 LSB，所以数字保持不变。

**天真方法:**最简单的方法是[通过用 **1** 对 **N** 执行](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/) [**逻辑 AND( & )**](https://www.geeksforgeeks.org/what-are-the-differences-between-bitwise-and-logical-and-operators-in-cc/) 直到 **N & 1** 不是 **0** 并对**设定位的数量进行计数然后，简单地将 **N** 左移**设定位**的计数。打印获得的号码作为所需答案。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number after
// converting 1s from end to 0s
int findNumber(int N)
{
    // Count of 1s
    int count = 0;

    // AND operation of N and 1
    while ((N & 1) == 1) {
        N = N >> 1;
        count++;
    }

    // Left shift N by count
    return N << count;
}

// Driver Code
int main()
{
    int N = 39;

    // Function Call
    cout << findNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the number after
// converting 1s from end to 0s
static int findNumber(int N)
{

    // Count of 1s
    int count = 0;

    // AND operation of N and 1
    while ((N & 1) == 1)
    {
        N = N >> 1;
        count++;
    }

    // Left shift N by count
    return N << count;
}

// Driver Code
public static void main (String[] args)
{
    int N = 39;

    // Function Call
    System.out.println(findNumber(N));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number after
# converting 1s from end to 0s
def findNumber(N):

    # Count of 1s
    count = 0

    # AND operation of N and 1
    while ((N & 1) == 1):
        N = N >> 1
        count += 1

    # Left shift N by count
    return N << count

# Driver Code
if __name__ == "__main__":

    N = 39

    # Function Call
    print(findNumber(N))

# This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the number after
// converting 1s from end to 0s
static int findNumber(int N)
{

    // Count of 1s
    int count = 0;

    // AND operation of N and 1
    while ((N & 1) == 1)
    {
        N = N >> 1;
        count++;
    }

    // Left shift N by count
    return N << count;
}

// Driver Code
public static void Main()
{
    int N = 39;

    // Function Call
    Console.WriteLine(findNumber(N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the number after
// converting 1s from end to 0s
function findNumber(N)
{

    // Count of 1s
    let count = 0;

    // AND operation of N and 1
    while ((N & 1) == 1)
    {
        N = N >> 1;
        count++;
    }

    // Left shift N by count
    return N << count;
}

// Driver Code

      let N = 39;

    // Function Call
    document.write(findNumber(N));

</script>
```

**Output:** 

```
32
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，找到 **N** 和 **(N + 1)** 的 [**逻辑与(& )**](https://www.geeksforgeeks.org/what-are-the-differences-between-bitwise-and-logical-and-operators-in-cc/) 。关键的观察是将 **1** 加到一个数字上，使得从 LSB 开始的每一个连续的**设定位**变成 **0** 。因此 **N & (N + 1)** 给出了需要的数字。

插图:

```
N = 39, therefore (N+1)=40
⇒   N = 39 = (100111)
⇒ N+1 = 40 = (101000)
Performing Logical AND(&) operation:
  1 0 0 1 1 1 
& 1 0 1 0 0 0
----------------
  1 0 0 0 0 0  ⇒ 32
----------------

Will this always work? Add 1 to N:
 1 0 0 1 1 1
 +         1
 ------------- 
 1 0 1 0 0 0    
 --------------     
It can be clearly seen that the continuous set bits from the LSB becomnes unset.
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number after
// converting 1s from end to 0s
int findNumber(int N)
{
    // Return the logical AND
    // of N and (N + 1)
    return N & (N + 1);
}

// Driver Code
int main()
{
    int N = 39;

    // Function Call
    cout << findNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the number after
// converting 1s from end to 0s
static int findNumber(int N)
{

    // Return the logical AND
    // of N and (N + 1)
    return N & (N + 1);
}

// Driver Code
public static void main(String[] args)
{
    int N = 39;

    // Function Call
    System.out.print(findNumber(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number after
# converting 1s from end to 0s
def findNumber(N):

    # Return the logical AND
    # of N and (N + 1)
    return N & (N + 1)

# Driver Code
if __name__ == '__main__':
    N = 39

    # Function Call
    print(findNumber(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find the number after
// converting 1s from end to 0s
static int findNumber(int N)
{

    // Return the logical AND
    // of N and (N + 1)
    return N & (N + 1);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 39;

    // Function Call
    Console.Write(findNumber(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program of the above approach

// Function to find the number after
// converting 1s from end to 0s
function findNumber(N)
{

    // Return the logical AND
    // of N and (N + 1)
    return N & (N + 1);
}

    // Driver Code

    let N = 39;

    // Function Call
     document.write(findNumber(N));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
32
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*