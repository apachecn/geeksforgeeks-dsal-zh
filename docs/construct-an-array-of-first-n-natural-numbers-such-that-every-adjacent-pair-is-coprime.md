# 构造一个前 N 个自然数的数组，使得每个相邻的对都是互质的

> 原文:[https://www . geeksforgeeks . org/construct-一个第一个 n 个自然数的数组-这样每个相邻对都是互素/](https://www.geeksforgeeks.org/construct-an-array-of-first-n-natural-numbers-such-that-every-adjacent-pair-is-coprime/)

给定一个正整数 **N** ，任务是构建一个由第一个 **N** 个自然数组成的数组，这样数组中的每一对相邻元素就是一个[同素](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)。如果存在多个解决方案，则打印其中任何一个。

**示例:**

> **输入:** N = 4
> **输出:** 4 1 3 2
> **解释:**
> 数组中所有可能的相邻对都是{ (4，1)，(1，3)，(3，2) }
> 由于数组中所有相邻对都是同素的，所以需要的输出是 4 1 3 2。
> 
> **输入:**N = 7
> T3】输出: 3 4 5 7 6 1 2

**方法:**思路是使用变量 **i** 迭代范围**【1，N】**，打印 **i** 的值。以下是观察结果:

> GCD(i，i + 1) = 1
> 因此，对于 I 的所有可能值，对(I，i + 1)都是互素数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct an arrary with
// adjacent elements as co-prime numbers
void ConstArrayAdjacentCoprime(int N)
{
    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Print i
        cout << i << " ";
    }
}

// Driver Code
int main()
{
    int N = 6;

    ConstArrayAdjacentCoprime(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

    // Function to construct an arrary with
    // adjacent elements as co-prime numbers
    static void ConstArrayAdjacentCoprime(int N)
    {
        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++)
        {

            // Print i
            System.out.print(i + " ");
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
      int N = 6;
      ConstArrayAdjacentCoprime(N);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to construct an arrary with
# adjacent elements as co-prime numbers
def ConstArrayAdjacentCoprime(N):

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Print i
        print(i, end = " ")

# Driver Code
if __name__ == "__main__" :

    N = 6

    ConstArrayAdjacentCoprime(N)

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to construct an arrary with
// adjacent elements as co-prime numbers
static void ConstArrayAdjacentCoprime(int N)
{

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // Print i
        Console.Write(i + " ");
    }
}

// Driver Code
public static void Main ()
{
    int N = 6;

    ConstArrayAdjacentCoprime(N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to construct an arrary with
    // adjacent elements as co-prime numbers
    function ConstArrayAdjacentCoprime(N)
    {

        // Iterate over the range [1, N]
        for (let i = 1; i <= N; i++)
        {

            // Print i
            document.write(i + " ");
        }
    }

// Driver code
    let N = 6;
      ConstArrayAdjacentCoprime(N);

 // This code is contributed by target_2.
</script>
```

**Output:** 

```
1 2 3 4 5 6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)