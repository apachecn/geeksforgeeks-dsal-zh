# 己 acci 编号

> 原文:[https://www.geeksforgeeks.org/hexanacci-numbers/](https://www.geeksforgeeks.org/hexanacci-numbers/)

[**己纳奇数**](https://oeis.org/A001592) 是斐波那契数的推广，其中每个项都是前面六个项的总和。前几个**己二醇数字**如下–**0，0，0，0，0，1，1，2，4，8，16，32，63，125，248，492，976，1936，3840…..**

己 acci 数的第 n 项由下式给出:

> **T(n)= T(n-1)+T(n-2)+T(n-3)+T(n-4)+T(n-5)+T(n-6)**
> 
> 用 **T(0) = T(1) = T(2) = T(3) = T(4) = 0，T(5) = 1**

### 找到己二醇的第 N <sup>个</sup>项

给定一个数字 **N** 。任务是找到**第 n 个**己方账号。

**示例:**

> **输入:**N = 8
> T3】输出: 2
> 
> **输入:**N = 11
> T3】输出: 16

**天真法:**思路是按照递归求数，用[递归](https://www.geeksforgeeks.org/recursion/)求解。

下面是上述方法的实现:

## C++

```
// C++ simple recursive program to print
// Nth Hexanacci numbers.
#include<bits/stdc++.h>
#include<iostream>
using namespace std;

// Function to print the Nth
// Hexanacci number
int printhexaRec(int n)
{
    if (n == 0 || n == 1 ||
        n == 2 || n == 3 ||
        n == 4 || n == 5)
        return 0;

    else if (n == 6)
        return 1;

    else
        return (printhexaRec(n - 1) +
                printhexaRec(n - 2) +
                printhexaRec(n - 3) +
                printhexaRec(n - 4) +
                printhexaRec(n - 5) +
                printhexaRec(n - 6));
}

int printhexa(int n)
{
    cout << printhexaRec(n) << endl;
}

// Driver code
int main()
{
    privatenthexa(n);
}

// This code is contributed by Ritik Bansal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java simple recursive program to print
// Nth Hexanacci numbers.
import java.util.*;
class GFG{

// Function to print the Nth
// Hexanacci number
static int printhexaRec(int n)
{
    if (n == 0 || n == 1 ||
        n == 2 || n == 3 ||
        n == 4 || n == 5)
        return 0;

    else if (n == 6)
        return 1;

    else
        return (printhexaRec(n - 1) +
                printhexaRec(n - 2) +
                printhexaRec(n - 3) +
                printhexaRec(n - 4) +
                printhexaRec(n - 5) +
                printhexaRec(n - 6));
}

static void printhexa(int n)
{
    System.out.print(printhexaRec(n) + "\n");
}

// Driver code
public static void main(String[] args)
{
    int n = 11;
    printhexa(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python simple recursive program to print
# Nth Hexanacci numbers.

# Function to print the Nth
# Hexanacci number
def printhexaRec(n) :
    if (n == 0 or n == 1 or\
        n == 2 or n == 3 or\
        n == 4 or n == 5):
        return 0
    elif (n == 6):
        return 1
    else :
        return (printhexaRec(n - 1) +
                printhexaRec(n - 2) +
                printhexaRec(n - 3)+
                printhexaRec(n - 4)+
                printhexaRec(n - 5)+
                printhexaRec(n - 6))

def printhexa(n) :
    print(printhexaRec(n))

# Driver code
n = 11
printhexa(n)
```

## C#

```
// C# simple recursive program to print
// Nth Hexanacci numbers.
using System;
class GFG{

// Function to print the Nth
// Hexanacci number
static int printhexaRec(int n)
{
    if (n == 0 || n == 1 ||
        n == 2 || n == 3 ||
        n == 4 || n == 5)
        return 0;

    else if (n == 6)
        return 1;

    else
        return (printhexaRec(n - 1) +
                printhexaRec(n - 2) +
                printhexaRec(n - 3) +
                printhexaRec(n - 4) +
                printhexaRec(n - 5) +
                printhexaRec(n - 6));
}

static void printhexa(int n)
{
    Console.Write(printhexaRec(n) + "\n");
}

// Driver code
public static void Main()
{
    int n = 11;
    printhexa(n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript simple recursive program to print
    // Nth Hexanacci numbers.

    // Function to print the Nth
    // Hexanacci number
    function printhexaRec(n)
    {
        if (n == 0 || n == 1 ||
            n == 2 || n == 3 ||
            n == 4 || n == 5)
            return 0;

        else if (n == 6)
            return 1;

        else
            return (printhexaRec(n - 1) +
                    printhexaRec(n - 2) +
                    printhexaRec(n - 3) +
                    printhexaRec(n - 4) +
                    printhexaRec(n - 5) +
                    printhexaRec(n - 6));
    }

    function printhexa(n)
    {
        document.write(printhexaRec(n) + "</br>");
    }

    let n = 11;
    printhexa(n);

</script>
```

**Output:** 

```
16
```

**高效方法:**一个**更好的解决方案**是使用 [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/) 的想法是跟踪的最后六个术语来计算系列的最后一个当前术语。将本系列的最后六个术语初始化为:

```
T(0) = T(1) = T(2) = T(3) = T(4) = 0, T(5) = 1
```

最后，计算该系列第 N <sup>个</sup>项之前的术语:

下面是上述方法的实现:

## C++

```
// C++ implementation to print 
// Nth term of hexanacci numbers. 
#include <bits/stdc++.h>
using namespace std;

// Function to print the Nth
// term of the Hexanacci number
void printhexa(int n)
{
    if (n < 0)
        return;

    // Initialize first five
    // numbers to base cases
    int first = 0;
    int second = 0;
    int third = 0;
    int fourth = 0;
    int fifth = 0;
    int sixth = 1;

    // Declare a current variable
    int curr = 0;

    if (n < 6)
        cout << first << endl;
    else if (n == 6)
        cout << sixth << endl;
    else
    {

        // Loop to add previous five numbers
        // for each number starting from 5
        // and then assign first, second,
        // third, fourth fifth to second,
        // third, fourth, fifth
        // and curr to sixth respectively
        for(int i = 6; i < n; i++) 
        {
            curr = first + second + third +
                   fourth + fifth + sixth;

            first = second;
            second = third;
            third = fourth;
            fourth = fifth;
            fifth = sixth;
            sixth = curr;
        }
    }
    cout << curr << endl;
}

// Driver Code
int main()
{
    int n = 11;

    printhexa(n);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print
// Nth term of hexanacci numbers.
class GFG {

// Function to print the Nth
// term of the Hexanacci number
static void printhexa(int n)
{
    if (n < 0)
        return;

    // Initialize first five
    // numbers to base cases
    int first = 0;
    int second = 0;
    int third = 0;
    int fourth = 0;
    int fifth = 0;
    int sixth = 1;

    // Declare a current variable
    int curr = 0;

    if (n < 6)
        System.out.println(first);
    else if (n == 6)
        System.out.println(sixth);

    else
    {

        // Loop to add previous five numbers
        // for each number starting from 5
        // and then assign first, second,
        // third, fourth fifth to second,
        // third, fourth, fifth
        // and curr to sixth respectively
        for(int i = 6; i < n; i++)
        {
            curr = first + second + third +
                   fourth + fifth + sixth;
            first = second;
            second = third;
            third = fourth;
            fourth = fifth;
            fifth = sixth;
            sixth = curr;
        }
    }
    System.out.println(curr);
}

// Driver code
public static void main(String[] args)
{
    int n = 11;

    printhexa(n);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to print
# Nth term of hexanacci numbers.

# Function to print the Nth
# term of the Hexanacci number  
def printhexa(n) :
    if (n < 0): 
        return 

    # Initialize first five 
    # numbers to base cases 
    first = 0 
    second = 0 
    third = 0 
    fourth = 0
    fifth = 0
    sixth = 1

    # declare a current variable 
    curr = 0 

    if (n <6): 
        print(first)
    elif (n == 6): 
        print(sixth) 

    else:

        # Loop to add previous five numbers 
        # for each number starting from 5 
        # and then assign first, second, 
        # third, fourth fifth to second,
        # third, fourth, fifth 
        # and curr to sixth respectively 
        for i in range(6, n):
            curr = first + second + third +\
                   fourth + fifth + sixth
            first = second 
            second = third 
            third = fourth 
            fourth = fifth
            fifth = sixth
            sixth = curr 

    print(curr)  

# Driver code
n = 11
printhexa(n)
```

## C#

```
// C# implementation to print
// Nth term of hexanacci numbers.
using System;

class GFG{

// Function to print the Nth
// term of the Hexanacci number
static void printhexa(int n)
{
    if (n < 0)
        return;

    // Initialize first five
    // numbers to base cases
    int first = 0;
    int second = 0;
    int third = 0;
    int fourth = 0;
    int fifth = 0;
    int sixth = 1;

    // Declare a current variable
    int curr = 0;

    if (n < 6)
        Console.WriteLine(first);
    else if (n == 6)
        Console.WriteLine(sixth);

    else
    {

        // Loop to add previous five numbers
        // for each number starting from 5
        // and then assign first, second,
        // third, fourth fifth to second,
        // third, fourth, fifth
        // and curr to sixth respectively
        for(int i = 6; i < n; i++)
        {
            curr = first + second + third +
                   fourth + fifth + sixth;
            first = second;
            second = third;
            third = fourth;
            fourth = fifth;
            fifth = sixth;
            sixth = curr;
        }
    }
    Console.WriteLine(curr);
}

// Driver code
public static void Main(String[] args)
{
    int n = 11;

    printhexa(n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript implementation to print 
    // Nth term of hexanacci numbers.

    // Function to print the Nth
    // term of the Hexanacci number
    function printhexa(n)
    {
        if (n < 0)
            return;

        // Initialize first five
        // numbers to base cases
        let first = 0;
        let second = 0;
        let third = 0;
        let fourth = 0;
        let fifth = 0;
        let sixth = 1;

        // Declare a current variable
        let curr = 0;

        if (n < 6)
            document.write(first);
        else if (n == 6)
            document.write(sixth);
        else
        {

            // Loop to add previous five numbers
            // for each number starting from 5
            // and then assign first, second,
            // third, fourth fifth to second,
            // third, fourth, fifth
            // and curr to sixth respectively
            for(let i = 6; i < n; i++) 
            {
                curr = first + second + third +
                       fourth + fifth + sixth;

                first = second;
                second = third;
                third = fourth;
                fourth = fifth;
                fifth = sixth;
                sixth = curr;
            }
        }
        document.write(curr);
    }
    let n = 11;
    printhexa(n);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
16
```

**时间复杂度:** O(N)

**辅助空间:** O(1)