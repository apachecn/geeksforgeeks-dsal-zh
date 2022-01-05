# 将 N 拆分成两个整数，A 和 B 的相加使它们相等

> 原文:[https://www . geesforgeks . org/split-n-in-two-integer-and-b 的加法使它们相等/](https://www.geeksforgeeks.org/split-n-into-two-integers-whose-addition-to-a-and-b-makes-them-equal/)

给定三个正整数 **A** 、 **B** 和 **N** ，任务是将 **N** 分成两部分，使其相等，即求两个正整数 **X** 和 **Y** ，使 **X + Y = N** 和 **A + X = B + Y** 。如果不存在这样的配对，打印 **-1** 。

***例:***

> **输入:** A = 1，B = 3，N = 4
> **输出:** 3 1
> **说明:**如果 X = 3，Y = 1，那么 A + X = B + Y，X + Y =4
> 
> **输入:** A = 1，B = 3，N = 1
> **输出:** -1

**天真方法:**
解决这个问题最简单的方法是[用 sum **N**](https://www.geeksforgeeks.org/python-program-to-find-all-possible-pairs-with-given-sum/) 生成所有可能的对，如果 **A + X = B + Y** 则检查每对。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效进场:**
可以观察到，由于 **X + Y = N** 和 **A + X = B + Y** ，那么 X 可以表示为**(N+B–A)/2**。只需检查**(N+B–A)/2**是否为偶数即可。如果是偶数，计算 **X** 和对应的 **Y** 。否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// splitted numbers
void findPair(int A, int B, int N)
{
    int X, Y;

    // Calculate X
    X = N - B + A;

    // If X is odd
    if (X % 2 != 0) {

        // No pair is possible
        cout << "-1";
    }

    // Otherwise
    else {

        // Calculate X
        X = X / 2;

        // Calculate Y
        Y = N - X;
        cout << X << " " << Y;
    }
}

// Driver Code
int main()
{
    int A = 1;
    int B = 3;
    int N = 4;
    findPair(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to calculate the
// splitted numbers
static void findPair(int A, int B, int N)
{
    int X, Y;

    // Calculate X
    X = N - B + A;

    // If X is odd
    if (X % 2 != 0)
    {

        // No pair is possible
        System.out.print("-1");
    }

    // Otherwise
    else
    {

        // Calculate X
        X = X / 2;

        // Calculate Y
        Y = N - X;
        System.out.print(X + " " + Y);
    }
}

//Driver function
public static void main (String[] args)
{
    int A = 1;
    int B = 3;
    int N = 4;

    findPair(A, B, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the
# splitted numbers
def findPair(A, B, N):

    # Calculate X
    X = N - B + A

    # If X is odd
    if (X % 2 != 0):

        # No pair is possible
        print("-1")

    # Otherwise
    else :

        # Calculate X
        X = X // 2

        # Calculate Y
        Y = N - X
        print (X , Y)

# Driver Code
if __name__ == "__main__":

    A = 1
    B = 3
    N = 4

    findPair(A, B, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement 
// the above approach 
using System;

class GFG{

// Function to calculate the 
// splitted numbers 
static void findPair(int A, int B, int N) 
{ 
    int X, Y; 

    // Calculate X 
    X = N - B + A; 

    // If X is odd 
    if (X % 2 != 0) 
    { 

        // No pair is possible 
        Console.Write("-1"); 
    } 

    // Otherwise 
    else
    { 

        // Calculate X 
        X = X / 2; 

        // Calculate Y 
        Y = N - X; 
        Console.Write(X + " " + Y); 
    } 
}

// Driver code
public static void Main(string[] args)
{
    int A = 1; 
    int B = 3; 
    int N = 4; 

    findPair(A, B, N); 
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to calculate the
    // splitted numbers
    function findPair(A , B , N) {
        var X, Y;

        // Calculate X
        X = N - B + A;

        // If X is odd
        if (X % 2 != 0) {

            // No pair is possible
            document.write("-1");
        }

        // Otherwise
        else {

            // Calculate X
            X = X / 2;

            // Calculate Y
            Y = N - X;
            document.write(X + " " + Y);
        }
    }

    // Driver function

        var A = 1;
        var B = 3;
        var N = 4;

        findPair(A, B, N);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
1 3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)