# 将所有同质数从 1 到 N 分组

> 原文:[https://www . geesforgeks . org/group-all-co-prime-numbers-from-1-n/](https://www.geeksforgeeks.org/group-all-co-prime-numbers-from-1-to-n/)

给定一个整数 **N** ，任务是对数字进行分组，使得每个组都是相互共质数，并且总分组最小。

**示例:**

> **输入:** N = 8
> **输出:**
> 1 2 3
> 4 5
> 6 7
> 8
> 
> **输入:** N = 5
> **输出:**
> 1 2 3
> 4 5

**方法:**这个问题的关键观察是两个连续的数总是同素的。也就是 GCD(a，a+1) = 1。另一个重要的观察是偶数不能列在一组中。因为它们会导致最大公约数为 2。因此，每一个连续的偶数和奇数可以组成一个组，1 可以在任何组中，因为 1 的数字的最大公约数总是 1。

下面是上述方法的实现:

## C++

```
// C++ implementation to group
// mutually coprime numbers into
// one group with minimum group possible
#include<bits/stdc++.h>
using namespace std;

// Function to group the mutually
// co-prime numbers into one group
void mutually_coprime(int n)
{
    if (n <= 3)
    {

        // Loop for the numbers less
        // than the 4
        for(int j = 1; j <= n; j++)
        {
            cout << j << " ";
        }
        cout << "\n";
    }
    else
    {

        // Integers 1, 2 and 3 can be
        // grouped into one group
        cout << "1 2 3\n";

        for(int j = 4; j < n; j += 2)
        {

            // Consecutive even and
            // odd numbers
            cout << j << " " << j + 1 << "\n";
        }
        if(n % 2 == 0)
            cout << n << "\n";
    }
}

// Driver Code        
int main()
{
    int n = 9;

    // Function call
    mutually_coprime(n);
}

// This code is contributed by yatinagg
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to group
// mutually coprime numbers into
// one group with minimum group possible
class GFG{

// Function to group the mutually
// co-prime numbers into one group
static void mutually_coprime(int n)
{
    if (n <= 3)
    {

        // Loop for the numbers less
        // than the 4
        for(int j = 1; j < n + 1; j++)
           System.out.print(j + " ");
        System.out.println();
    }
    else
    {

        // Integers 1, 2 and 3 can be
        // grouped into one group
        System.out.println("1 2 3");
        for(int j = 4; j < n; j += 2)
        {

           // Consecutive even and
           // odd numbers
           System.out.println(j + " " + (j + 1));
           if (n % 2 == 0)
           System.out.println(n);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 9;

    // Function Call
    mutually_coprime(n);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to group
# mutually coprime numbers into
# one group with minimum group possible

# Function to group the mutually
# co-prime numbers into one group
def mutually_coprime (n):   
    if ( n <= 3):
        # Loop for the numbers less
        # than the 4
        for j in range (1, n + 1):
            print (j, end =" ")
        print ()
    else:
        # Integers 1, 2 and 3 can be
        # grouped into one group
        print (1, 2, 3)
        for j in range ( 4, n, 2 ):

            # Consecutive even and
            # odd numbers
            print (j, ( j + 1 ))
        if(n % 2 == 0):        
            print (n)

# Driver Code           
if __name__ == "__main__":
    n = 9

    # Function Call
    mutually_coprime (n)
```

## C#

```
// C# implementation to group
// mutually coprime numbers into
// one group with minimum group possible
using System;

class GFG{

// Function to group the mutually
// co-prime numbers into one group
static void mutually_coprime(int n)
{
    if (n <= 3)
    {

        // Loop for the numbers less
        // than the 4
        for(int j = 1; j < n + 1; j++)
           Console.Write(j + " ");

        Console.WriteLine();
    }
    else
    {

        // ints 1, 2 and 3 can be
        // grouped into one group
        Console.WriteLine("1 2 3");
        for(int j = 4; j < n; j += 2)
        {
           // Consecutive even and
           // odd numbers
           Console.WriteLine(j + " " + (j + 1));

           if (n % 2 == 0)
               Console.WriteLine(n);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int n = 9;

    // Function Call
    mutually_coprime(n);
}
}
// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to group
// mutually coprime numbers into
// one group with minimum group possible

// Function to group the mutually
// co-prime numbers into one group
function mutually_coprime(n)
{
    if (n <= 3)
    {

        // Loop for the numbers less
        // than the 4
        for(let j = 1; j < n + 1; j++)
           document.write(j + " " + "<br/>");
        document.write("<br/>");
    }
    else
    {

        // Integers 1, 2 and 3 can be
        // grouped into one group
        document.write("1 2 3" + "<br/>");
        for(let j = 4; j < n; j += 2)
        {

           // Consecutive even and
           // odd numbers
           document.write(j + " " + (j + 1) + "<br/>");
           if (n % 2 == 0)
           document.write(n + "<br/>");
        }
    }
}

// Driver Code

    let n = 9;

    // Function Call
    mutually_coprime(n);

</script>
```

**Output:** 

```
1 2 3
4 5
6 7
8 9         
```

时间复杂度:0(n)

辅助空间:0(1)