# 检查一个数是否可以表示为两个正方形的差

> 原文:[https://www . geesforgeks . org/check-一个数字是否可以表示为两个平方的差/](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-as-difference-of-two-squares/)

给定一个数字 **N** ，任务是检查这个数字是否可以表示为两个完美正方形的差。

**示例:**

> **输入:** N = 3
> **输出:**是
> **解释:**
> 2<sup>2</sup>–1<sup>1</sup>= 3
> 
> **输入:**N = 10
> T3】输出:否

**方法:**思想是所有的数都可以表示为两个平方的差，除了当除以 4 时产生 2 的余数的数。

让我们通过几个例子来想象一下:

```
N = 4 => 22 - 02
N = 6 => Can't be expressed as 6 % 4 = 2
N = 8 => 32 - 12
N = 10 => Can't be expressed as 10 % 4 = 2
N = 11 => 62 - 52
N = 12 => 42 - 22
and so on...
```

因此，其思想是当给定的数除以 4 时，简单地检查余数是否为 2。

下面是上述方法的实现:

## C++

```
// C++ program to check whether a number
// can be represented by the difference
// of two squares

#include <bits/stdc++.h>
using namespace std;

// Function to check whether a number
// can be represented by the difference
// of two squares
bool difSquare(int n)
{
    // Checking if n % 4 = 2 or not
    if (n % 4 != 2) {
        return true;
    }

    return false;
}

// Driver code
int main()
{

    int n = 45;
    if (difSquare(n)) {
        cout << "Yes\n";
    }
    else {
        cout << "No\n";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a number
// can be represented by the difference
// of two squares
import java.util.*;

class GFG{

// Function to check whether a number
// can be represented by the difference
// of two squares
static boolean difSquare(int n)
{

    // Checking if n % 4 = 2 or not
    if (n % 4 != 2)
    {
        return true;
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    int n = 45;

    if (difSquare(n))
    {
        System.out.print("Yes\n");
    }
    else
    {
        System.out.print("No\n");
    }
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to check whether a number
# can be represented by the difference
# of two squares

# Function to check whether a number
# can be represented by the difference
# of two squares
def difSquare(n):

    # Checking if n % 4 = 2 or not
    if (n % 4 != 2):
        return True
    return False

# Driver code
if __name__ == '__main__':

    n = 45

    if (difSquare(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to check whether a number
// can be represented by the difference
// of two squares
using System;
class GFG{

// Function to check whether a number
// can be represented by the difference
// of two squares
static bool difSquare(int n)
{

    // Checking if n % 4 = 2 or not
    if (n % 4 != 2)
    {
        return true;
    }
    return false;
}

// Driver code
public static void Main()
{
    int n = 45;

    if (difSquare(n))
    {
        Console.Write("Yes\n");
    }
    else
    {
        Console.Write("No\n");
    }
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// Javascript program to check whether a number
// can be represented by the difference
// of two squares

// Function to check whether a number
// can be represented by the difference
// of two squares
function difSquare(n)
{

    // Checking if n % 4 = 2 or not
    if (n % 4 != 2)
    {
        return true;
    }
    return false;
}

// Driver code
var n = 45;

if (difSquare(n))
{
    document.write("Yes\n");
}
else
{
    document.write("No\n");
}

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```