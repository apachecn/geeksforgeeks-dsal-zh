# 从给定的孔中找出数字的程序

> 原文:[https://www . geesforgeks . org/program-to-find-the-number-from-given-holes/](https://www.geeksforgeeks.org/program-to-find-the-number-from-given-holes/)

给定一个代表孔总数的数字 **H** 。任务是找到有这么多孔的最小的数。
T3【注:T5】

1.  0，4，6，9 各有 1 个孔，8 有 2 个孔。
2.  该数字不应包含前导零。

**例:**

> **输入:** H = 1
> **输出:** 0
> **输入:** H = 5
> **输出:** 488
> **说明:**
> 有 5 个孔的数为 488。即(1 + 2 + 2)

**参考:** [数一个整数](https://www.geeksforgeeks.org/count-the-number-of-holes-in-an-integer/)

**进场:**

1.  首先，检查给定的孔数是 0 还是 1，如果是 0 则打印 1，如果是 1 则打印 0。
2.  如果给定的孔数大于 1，则将孔数除以 2，并将余数存储在**‘rem’**变量中。而商在**变量中。**
3.  **现在，如果 rem 变量的值等于 1，那么首先打印 4 次，然后打印 8 次。**
4.  **否则只打印 8 次。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that will find out
// the number
void printNumber(int holes)
{

    // If number of holes
    // equal 0 then return 1
    if (holes == 0)
        cout << "1";

    // If number of holes
    // equal 0 then return 0
    else if (holes == 1)
        cout << "0";

    // If number of holes
    // is more than 0 or 1.
    else {
        int rem = 0, quo = 0;

        rem = holes % 2;
        quo = holes / 2;

        // If number of holes is
        // odd
        if (rem == 1)
            cout << "4";

        for (int i = 0; i < quo; i++)
            cout << "8";
    }
}

// Driver code
int main()
{
    int holes = 3;

    // Calling Function
    printNumber(holes);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

// Function that will find out
// the number
static void printNumber(int holes)
{

    // If number of holes
    // equal 0 then return 1
    if (holes == 0)
        System.out.print("1");

    // If number of holes
    // equal 0 then return 0
    else if (holes == 1)
        System.out.print("0");

    // If number of holes
    // is more than 0 or 1.
    else
    {
        int rem = 0, quo = 0;

        rem = holes % 2;
        quo = holes / 2;

        // If number of holes is
        // odd
        if (rem == 1)
            System.out.print("4");

        for (int i = 0; i < quo; i++)
                System.out.print("8");
    }
}

// Driver code
public static void main (String[] args)
{
    int holes = 3;

    // Calling Function
    printNumber(holes);
}
}

// This code is contributed by Sachin.
```

## **蟒蛇 3**

```
# Python3 implementation of
# the above approach

# Function that will find out
# the number
def printNumber(holes):

    # If number of holes
    # equal 0 then return 1
    if (holes == 0):
        print("1")

    # If number of holes
    # equal 0 then return 0
    elif (holes == 1):
        print("0", end = "")

    # If number of holes
    # is more than 0 or 1.
    else:
        rem = 0
        quo = 0

        rem = holes % 2
        quo = holes // 2

        # If number of holes is
        # odd
        if (rem == 1):
            print("4", end = "")

        for i in range(quo):
            print("8", end = "")

# Driver code
holes = 3

# Calling Function
printNumber(holes)

# This code is contributed by Mohit kumar
```

## **C#**

```
// C# implementation of the above approach
using System;

class GFG
{

// Function that will find out
// the number
static void printNumber(int holes)
{

    // If number of holes
    // equal 0 then return 1
    if (holes == 0)
        Console.Write ("1");

    // If number of holes
    // equal 0 then return 0
    else if (holes == 1)
        Console.Write ("0");

    // If number of holes
    // is more than 0 or 1.
    else
    {
        int rem = 0, quo = 0;

        rem = holes % 2;
        quo = holes / 2;

        // If number of holes is
        // odd
        if (rem == 1)
        Console.Write ("4");

        for (int i = 0; i < quo; i++)
            Console.Write ("8");
    }
}

// Driver code
static public void Main ()
{
    int holes = 3;

    // Calling Function
    printNumber(holes);
}
}

// This code is contributed by jit_t
```

## **java 描述语言**

```
<script>
    // Javascript implementation of the above approach

    // Function that will find out
    // the number
    function printNumber(holes)
    {

        // If number of holes
        // equal 0 then return 1
        if (holes == 0)
            document.write("1");

        // If number of holes
        // equal 0 then return 0
        else if (holes == 1)
            document.write("0");

        // If number of holes
        // is more than 0 or 1.
        else {
            let rem = 0, quo = 0;

            rem = holes % 2;
            quo = parseInt(holes / 2, 10);

            // If number of holes is
            // odd
            if (rem == 1)
                document.write("4");

            for (let i = 0; i < quo; i++)
                document.write("8");
        }
    }

    let holes = 3;

    // Calling Function
    printNumber(holes);

    // This code is contributed by divyeshrabadiya07.
</script>
```

****Output:** 

```
48
```**