# 没有可被 3 整除的元素的三元组和 N

> 原文:[https://www . geesforgeks . org/无元素可被 3 整除的三元组 n/](https://www.geeksforgeeks.org/triplet-with-no-element-divisible-by-3-and-sum-n/)

给定一个大于 2 的整数 N，任务是打印 a、b 和 c 的任意组合，使得:

> *   a+b+ c = N

**示例:**

```
Input: N = 233
Output: 77 77 79

Input: N = 3
Output: 1 1 1
```

一种简单的方法是使用三个循环并检查给定的条件。

下面是上述方法的实现:

## C++

```
// C++ program to print a, b and c
// such that a+b+c=N
#include <bits/stdc++.h>
using namespace std;

// Function to print a, b and c
void printCombination(int n)
{

    // first loop
    for (int i = 1; i < n; i++) {

        // check for 1st number
        if (i % 3 != 0) {

            // second loop
            for (int j = 1; j < n; j++) {

                // check for 2nd number
                if (j % 3 != 0) {

                    // third loop
                    for (int k = 1; k < n; k++) {

                        // Check for 3rd number
                        if (k % 3 != 0 && (i + j + k) == n) {
                            cout << i << " " << j << " " << k;
                            return;
                        }
                    }
                }
            }
        }
    }
}

// Driver Code
int main()
{
    int n = 233;

    printCombination(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print a,
// b and c such that a+b+c=N
import java.io.*;

class GFG
{

// Function to print a, b and c
static void printCombination(int n)
{
    // first loop
    for (int i = 1; i < n; i++)
    {

        // check for 1st number
        if (i % 3 != 0)
        {

            // second loop
            for (int j = 1; j < n; j++)
            {

                // check for 2nd number
                if (j % 3 != 0)
                {

                    // third loop
                    for (int k = 1; k < n; k++)
                    {

                        // Check for 3rd number
                        if (k % 3 != 0 && (i + j + k) == n)
                        {
                            System.out.println( i + " " +
                                                j + " " + k);
                            return;
                        }
                    }
                }
            }
        }
    }
}

// Driver Code
public static void main (String[] args)
{
    int n = 233;

    printCombination(n);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to print a, b
# and c such that a+b+c=N

# Function to print a, b and c
def printCombination(n):

    # first loop
    for i in range(1, n):

        # check for 1st number
        if (i % 3 != 0):

            # second loop
            for j in range(1, n):

                # check for 2nd number
                if (j % 3 != 0):

                    # third loop
                    for k in range(1, n):

                        # Check for 3rd number
                        if (k % 3 != 0 and
                           (i + j + k) == n):
                            print(i, j, k);
                            return;

# Driver Code
n = 233;

printCombination(n);

# This code is contributed
# by mits
```

## C#

```
// C# program to print a,
// b and c such that a+b+c=N
class GFG
{

// Function to print a, b and c
static void printCombination(int n)
{
    // first loop
    for (int i = 1; i < n; i++)
    {

        // check for 1st number
        if (i % 3 != 0)
        {

            // second loop
            for (int j = 1; j < n; j++)
            {

                // check for 2nd number
                if (j % 3 != 0)
                {

                    // third loop
                    for (int k = 1; k < n; k++)
                    {

                        // Check for 3rd number
                        if (k % 3 != 0 && (i + j + k) == n)
                        {
                            System.Console.WriteLine(i + " " +
                                                     j + " " + k);
                            return;
                        }
                    }
                }
            }
        }
    }
}

// Driver Code
static void Main ()
{
    int n = 233;

    printCombination(n);
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print a, b and c
// such that a+b+c=N

// Function to print a, b and c
function printCombination($n)
{

    // first loop
    for ($i = 1; $i < $n; $i++)
    {

        // check for 1st number
        if ($i % 3 != 0)
        {

            // second loop
            for ($j = 1; $j < $n; $j++)
            {

                // check for 2nd number
                if ($j % 3 != 0)
                {

                    // third loop
                    for ($k = 1; $k < $n; $k++)
                    {

                        // Check for 3rd number
                        if ($k % 3 != 0 &&
                           ($i + $j + $k) == $n)
                        {
                            echo $i , " " , $j , " " , $k;
                            return;
                        }
                    }
                }
            }
        }
    }
}

// Driver Code
$n = 233;

printCombination($n);

// This code is contributed
// inder_verma
?>
```

## java 描述语言

```
<script>
// Javascript program to print a, b and c
// such that a+b+c=N

// Function to print a, b and c
function printCombination(n)
{

    // first loop
    for (let i = 1; i < n; i++) {

        // check for 1st number
        if (i % 3 != 0) {

            // second loop
            for (let j = 1; j < n; j++) {

                // check for 2nd number
                if (j % 3 != 0) {

                    // third loop
                    for (let k = 1; k < n; k++) {

                        // Check for 3rd number
                        if (k % 3 != 0 && (i + j + k) == n) {
                            document.write(i + " " + j + " " + k);
                            return;
                        }
                    }
                }
            }
        }
    }
}

// Driver Code
let n = 233;
printCombination(n);

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
1 2 230
```

**时间复杂度:** O(n <sup>3</sup>

**高效方法:**

1.  将 1 视为三个数字之一。
2.  另外两个数字是:
    *   **(2，n-3)** 如果 n-2 可被 3 整除。
    *   否则 **(1，n-2)** 如果 n-2 不能被 3 整除。

下面是上述方法的实现:

## C++

```
// C++ program to print a, b and c
// such that a+b+c=N
#include <bits/stdc++.h>
using namespace std;

// Function to print a, b and c
void printCombination(int n)
{
    cout << 1 << " ";

    // check if n-2 is divisible
    // by 3 or not
    if ((n - 2) % 3 == 0)
        cout << 2 << " " << n - 3;
    else
        cout << 1 << " " << n - 2;
}

// Driver Code
int main()
{
    int n = 233;

    printCombination(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print a, b
// and c such that a+b+c=N
class GFG
{
// Function to print a, b and c
static void printCombination(int n)
{
    System.out.print(1 + " ");

    // check if n-2 is divisible
    // by 3 or not
    if ((n - 2) % 3 == 0)
        System.out.print(2 + " " + (n - 3));
    else
        System.out.print(1 + " " + (n - 2));
}

// Driver Code
public static void main(String[] args)
{
    int n = 233;

    printCombination(n);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to print a, b and c
# such that a+b+c=N

# Function to print a, b and c
def printCombination(n):
    print("1 ",end="");

    # check if n-2 is divisible
    # by 3 or not
    if ((n - 2) % 3 == 0):
        print("2",n - 3,end="");
    else:
        print("1",(n - 2),end="");

# Driver code
if __name__=='__main__':
    n = 233;

    printCombination(n);

# This code is contributed by mits
```

## C#

```
// C# program to print a, b
// and c such that a+b+c=N

class GFG
{
// Function to print a, b and c
static void printCombination(int n)
{
    System.Console.Write(1 + " ");

    // check if n-2 is divisible
    // by 3 or not
    if ((n - 2) % 3 == 0)
        System.Console.Write(2 + " " + (n - 3));
    else
        System.Console.Write(1 + " " + (n - 2));
}

// Driver Code
static void Main()
{
    int n = 233;

    printCombination(n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print a, b and c
// such that a+b+c=N

// Function to print a, b and c
function printCombination($n)
{
    echo "1 ";

    // check if n-2 is divisible
    // by 3 or not
    if (($n - 2) % 3 == 0)
        echo "2 " . ($n - 3);
    else
        echo "1 " . ($n - 2);
}

// Driver code
$n = 233;

printCombination($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print a, b and c
// such that a+b+c=N

// Function to print a, b and c
function printCombination(n)
{
    document.write(1 + " ");

    // Check if n-2 is divisible
    // by 3 or not
    if ((n - 2) % 3 == 0)
        document.write(2 + " " + (n - 3));
    else
        document.write(1 + " " + (n - 2));
}

// Driver Code
let n = 233;

printCombination(n);

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
1 2 230
```

**时间复杂度:** O(1)