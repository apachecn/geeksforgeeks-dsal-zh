# 计算给定范围内可被‘M’整除的数字

> 原文:[https://www . geesforgeks . org/count-numbers-除尽-m-给定-range/](https://www.geeksforgeeks.org/count-numbers-divisible-m-given-range/)

A 和 B 是定义范围的两个数字，其中 A <= B. Find the total numbers in the given range [A … B] divisible by ‘M’
示例:

```
Input  : A = 25, B = 100, M = 30
Output : 3
Explanation : In the given range [25 - 100], 
30, 60 and 90 are divisible by 30

Input : A = 6, B = 15, M = 3
Output : 4
Explanation : In the given range [6 - 15],
6, 9, 12 and 15 are divisible by 3
```

**方法 1:【蛮力】**
运行一个从 A 到 b 的循环，如果找到一个可被‘M’整除的数，递增计数器。
以下是上述方法的实施:

## C++

```
// Program to count the numbers divisible by
// M in a given range
#include <bits/stdc++.h>
using namespace std;

int countDivisibles(int A, int B, int M)
{
    // Variable to store the counter
    int counter = 0;

    // Running a loop from A to B and check
    // if a number is divisible by M.
    for (int i = A; i <= B; i++)
        if (i % M == 0)
            counter++;

    return counter;
}

// Driver code
int main()
{
    // A and B define the range, M is the dividend
    int A = 30, B = 100, M = 30;

    // Printing the result
    cout << countDivisibles(A, B, M) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the numbers divisible by
// M in a given range
import java.io.*;

class GFG {
    // Function to count the numbers divisible by
    // M in a given range
    static int countDivisibles(int A, int B, int M)
    {
        // Variable to store the counter
        int counter = 0;

        // Running a loop from A to B and check
        // if a number is divisible by M.
        for (int i = A; i <= B; i++)
            if (i % M == 0)
                counter++;

        return counter;
    }

    // driver program
    public static void main(String[] args)
    {
        // A and B define the range, M is the dividend
        int A = 30, B = 100, M = 30;

        // Printing the result
        System.out.println(countDivisibles(A, B, M));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Program to count the numbers
# divisible by M in a given range

def countDivisibles(A, B, M):

    # Variable to store the counter
    counter = 0;

    # Running a loop from A to B
    # and check if a number is
    # divisible by M.
    for i in range(A, B):
        if (i % M == 0):
            counter = counter + 1

    return counter

# Driver code
# A and B define the range,
# M is the dividend
A = 30
B = 100
M = 30

# Printing the result
print(countDivisibles(A, B, M))

# This code is contributed by Sam007.
```

## C#

```
// C# program to count the numbers
// divisible by M in a given range
using System;

public class GFG {

    // Function to count the numbers divisible by
    // M in a given range
    static int countDivisibles(int A, int B, int M)
    {
        // Variable to store the counter
        int counter = 0;

        // Running a loop from A to B and check
        // if a number is divisible by M.
        for (int i = A; i <= B; i++)
            if (i % M == 0)
                counter++;

        return counter;
    }

    // driver program
    public static void Main()
    {
        // A and B define the range, M is the dividend
        int A = 30, B = 100, M = 30;

        // Printing the result
        Console.WriteLine(countDivisibles(A, B, M));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count the
// numbers divisible by
// M in a given range

function countDivisibles($A, $B, $M)
{

    // Variable to store the counter
    $counter = 0;

    // Running a loop from
    // A to B and check
    // if a number is
    // divisible by M.
    for ($i = $A; $i <= $B; $i++)
        if ($i % $M == 0)
            $counter++;

    return $counter;
}

    // Driver Code
    // A and B define the range,
    // M is the dividend
    $A = 30;
    $B = 100;
    $M = 30;

    // Printing the result
    echo countDivisibles($A, $B, $M), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript Program to count the
// numbers divisible by
// M in a given range

function countDivisibles(A, B, M)
{

    // Variable to store the counter
    let counter = 0;

    // Running a loop from
    // A to B and check
    // if a number is
    // divisible by M.
    for (let i = A; i <= B; i++)
        if (i % M == 0)
            counter++;

    return counter;
}

    // Driver Code
    // A and B define the range,
    // M is the dividend
    let A = 30;
    let B = 100;
    let M = 30;

    // Printing the result
    document.write(countDivisibles(A, B, M));

// This code is contributed by gfgking.
</script>
```

输出:

```
3
```

**方法 2:【更好】**
在找到第一个可除数后，可以通过增加迭代器‘M’次来修改循环。还有，如果‘A’小于‘M’，可以改成‘M’，因为小于‘M’的数不能被它除。
**方法 3:【高效】**

```
Let B = b * M and
    A = a * M
The count of numbers divisible by
'M' between A and B will be equal
to b - a.

Example:
A = 25, B = 70, M = 10.
Now, a = 2, b = 7.
Count = 7 - 2 = 5.
```

可以观察到，如果 A 能被 M 整除，“b–A”将排除 A 的计数，因此计数将小于 1。因此，在这种情况下，我们显式添加 1。
**A 被 M 整除的例子:**

```
A = 30, B = 70, M = 10.
Now, a = 3, b = 7.
Count = 7 - 3 = 4.
But, Count should be 5\. Thus, we will
add 1 explicitly.
```

下面是上述方法的实现:

## C++

```
// C++ program to count the numbers divisible by
// M in a given range
#include <bits/stdc++.h>
using namespace std;

// Function to count the numbers divisible by
// M in a given range
int countDivisibles(int A, int B, int M)
{

    // Add 1 explicitly as A is divisible by M
    if (A % M == 0)
        return (B / M) - (A / M) + 1;

    // A is not divisible by M
    return (B / M) - (A / M);
}

// driver program
int main()
{

    // A and B define the range, M is the dividend
    int A = 30, B = 100, M = 30;

    // Printing the result
    cout << (countDivisibles(A, B, M));
}

// This code is contributed by subham348.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the numbers divisible by
// M in a given range
import java.io.*;

class GFG {
    // Function to count the numbers divisible by
    // M in a given range
    static int countDivisibles(int A, int B, int M)
    {
        // Add 1 explicitly as A is divisible by M
        if (A % M == 0)
            return (B / M) - (A / M) + 1;

        // A is not divisible by M
        return (B / M) - (A / M);
    }

    // driver program
    public static void main(String[] args)
    {
        // A and B define the range, M is the dividend
        int A = 30, B = 100, M = 30;

        // Printing the result
        System.out.println(countDivisibles(A, B, M));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Program to count the numbers divisible
# by M in a given range

# Returns count of numbers in [A B] that
# are divisible by M.
def countDivisibles(A, B, M):

    # Add 1 explicitly as A is divisible by M
    if (A % M == 0):
        return ((B / M) - (A / M)) + 1

    # A is not divisible by M
    return ((B / M) - (A / M))

# Driver Code
# A and B define the range, M
# is the divident
A = 30
B = 70
M = 10

# Printing the result
print(countDivisibles(A, B, M))

# This code is contributed by Sam007
```

## C#

```
// C# program to count the numbers
// divisible by M in a given range
using System;

public class GFG {

    // Function to count the numbers divisible by
    // M in a given range
    static int countDivisibles(int A, int B, int M)
    {
        // Add 1 explicitly as A is divisible by M
        if (A % M == 0)
            return (B / M) - (A / M) + 1;

        // A is not divisible by M
        return (B / M) - (A / M);
    }

    // driver program
    public static void Main()
    {
        // A and B define the range, M is the dividend
        int A = 30, B = 100, M = 30;

        // Printing the result
        Console.WriteLine(countDivisibles(A, B, M));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count the numbers
// divisible by M in a given range

// Returns count of numbers in
// [A B] that are divisible by M.
function countDivisibles($A, $B, $M)
{

    // Add 1 explicitly as A
    // is divisible by M
    if ($A % $M == 0)
        return ($B / $M) -
               ($A / $M) + 1;

    // A is not divisible by M
    return ($B / $M) -
           ($A / $M);
}

    // Driver Code
    // A and B define the range,
    // M is the divident
    $A = 30;
    $B = 70;
    $M = 10;

    // Printing the result
    echo countDivisibles($A, $B, $M) ;
    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
// Javascript Program to count the numbers
// divisible by M in a given range

// Returns count of numbers in
// [A B] that are divisible by M.
function countDivisibles(A, B, M)
{

    // Add 1 explicitly as A
    // is divisible by M
    if (A % M == 0)
        return (B / M) -
            (A / M) + 1;

    // A is not divisible by M
    return (B / M) -
        (A / M);
}

    // Driver Code
    // A and B define the range,
    // M is the divident
    let A = 30;
    let B = 70;
    let M = 10;

    // Printing the result
    document.write(countDivisibles(A, B, M));

// This code is contributed by gfgking
```

**Output**

```
3
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。