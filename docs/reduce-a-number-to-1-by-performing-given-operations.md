# 通过执行给定的操作

将一个数减少到 1

> 原文:[https://www . geeksforgeeks . org/通过执行给定的操作将数字减少到 1/](https://www.geeksforgeeks.org/reduce-a-number-to-1-by-performing-given-operations/)

给定一个数字 N。任务是在最小步数内将给定的数字 N 减少到 1。您可以在每个步骤中执行以下任何一个操作。

*   **操作 1** :如果数字是偶数，那么你可以将数字除以 2。
*   **操作 2** :如果数字是奇数，那么你可以执行(n+1)或(n-1)。

您需要通过执行上述操作来打印将 N 减少到 1 所需的最小步骤数。

**示例**:

```
Input : n = 15
Output : 5
 15 is odd 15+1=16    
 16 is even 16/2=8     
 8  is even 8/2=4 
 4  is even 4/2=2     
 2  is even 2/2=1     

Input : n = 7
Output : 4
    7->6    
    6->3 
    3->2    
    2->1
```

**方法 1–**
思路是递归计算所需的最小步数。

*   如果这个数是偶数，那么我们只能将这个数除以 2。
*   但是，当数为奇数时，我们可以增加或减少 1。因此，我们将对 n-1 和 n+1 都使用递归，并返回运算次数最少的一个。

下面是上述方法的实现:

## C++

```
// C++ program to count minimum
// steps to reduce a number
#include <cmath>
#include <iostream>

using namespace std;

int countways(int n)
{
    if (n == 1)
        return 0;
    else if (n % 2 == 0)
        return 1 + countways(n / 2);
    else
        return 1 + min(countways(n - 1),
                       countways(n + 1));
}

// Driver code
int main()
{
    int n = 15;

    cout << countways(n) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum
// steps to reduce a number
class Geeks {

    static int countways(int n)
    {
        if (n == 1)
            return 0;
        else if (n % 2 == 0)
            return 1 + countways(n / 2);
        else
            return 1 + Math.min(countways(n - 1), countways(n + 1));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 15;

        System.out.println(countways(n));
    }
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
# Python3 program to count minimum
# steps to reduce a number

def countways(n):
    if (n == 1):
        return 0;
    elif (n % 2 == 0):
        return 1 + countways(n / 2);
    else:
        return 1 + min(countways(n - 1),
                    countways(n + 1));

# Driver code
n = 15;
print(countways(n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to count minimum
// steps to reduce a number
using System;

class GFG {
    static int countways(int n)
    {
        if (n == 1)
            return 0;
        else if (n % 2 == 0)
            return 1 + countways(n / 2);
        else
            return 1 + Math.Min(countways(n - 1), countways(n + 1));
    }

    // Driver code
    static public void Main()
    {
        int n = 15;
        Console.Write(countways(n));
    }
}

// This code is contributed by Raj
```

## java 描述语言

```
<script>

// Javascript program to count minimum
// steps to reduce a number

    function countways(n)
    {
        if (n == 1)
            return 0;
        else if (n % 2 == 0)
            return 1 + countways(n / 2);
        else
            return 1 + Math.min(countways(n - 1),
            countways(n + 1));
    }

    // Driver code
    let n = 15;
    document.write(countways(n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
5
```

上述方法具有 O(2^n).的时间复杂性可以将这种复杂性降低到 0(对数 n)。

**方法 2–(有效解)**
很明显，在奇数上执行 1 的增量或 1 的减量可以产生偶数，其中一个可以被 4 整除。对于一个奇数，唯一可能的运算要么是 1 的增量，要么是 1 的减量，最确定的是一次运算会得到一个可被 4 整除的数，这显然是最优的选择。

```
Algorithm : 
1\. Initialize count = 0
2\. While number is greater than one perform following steps - 
         Perform count++ for each iteration
         if num % 2 == 0, perform division
         else if num % 4 == 3, perform increment
         else perform decrement (as odd % 4 is either 1 or 3)
3\. return count;
```

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

int countSteps(int n)
{
    int count = 0;
    while (n > 1) {
        count++;

        // num even, divide by 2
        if (n % 2 == 0)
            n /= 2;

        // num odd, n%4 == 1
        // or n==3(special edge case),
        // decrement by 1
        else if (n % 4 == 1||n==3)
            n -= 1;

        // num odd, n%4 == 3, increment by 1
        else
            n += 1;
    }

    return count;
}

// driver code

int main()
{
    int n = 15;

    // Function call
    cout << countSteps(n) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

public static int countSteps(int n)
{
    int count = 0;

    while (n > 1)
    {
        count++;

        // num even, divide by 2
        if (n % 2 == 0)
            n /= 2;

        // num odd, n%4 == 1
        // or n==3(special edge case),
        // decrement by 1
        else if (n % 4 == 1||n==3)
            n -= 1;

        // num odd, n%4 == 3, increment by 1
        else
            n += 1;
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int n = 15;

    // Function call
    System.out.print(countSteps(n));
}
}

// This code is contributed by paragpallavsingh
```

## 蟒蛇 3

```
# Python3 program for the above approach
def countSteps(n):

    count = 0
    while (n > 1):
        count += 1

        # num even, divide by 2
        if (n % 2 == 0):
            n //= 2

        # num odd, n%4 == 1
        # or n==3(special edge case),
        # decrement by 1
        elif (n % 4 == 1 or n == 3):
            n -= 1

        # num odd, n%4 == 3, increment by 1
        else:
            n += 1

    return count

# Driver code
if __name__ == "__main__":

    n = 15

    # Function call
    print(countSteps(n))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

public static int countSteps(int n)
{
    int count = 0;

    while (n > 1)
    {
        count++;

        // num even, divide by 2
        if (n % 2 == 0)
            n /= 2;

        // num odd, n%4 == 1
        // or n==3(special edge case),
        // decrement by 1
        else if (n % 4 == 1||n==3)
            n -= 1;

        // num odd, n%4 == 3, increment by 1
        else
            n += 1;
    }
    return count;
}

// Driver code
static public void Main ()
{
    int n = 15;

    // Function call   
    Console.WriteLine(countSteps(n));
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    function countSteps(n)
    {
        let count = 0;

    while (n > 1)
    {
        count++;

        // num even, divide by 2
        if (n % 2 == 0)
            n = Math.floor(n/2);

        // num odd, n%4 == 1
        // or n==3(special edge case),
        // decrement by 1
        else if (n % 4 == 1||n==3)
            n -= 1;

        // num odd, n%4 == 3, increment by 1
        else
            n += 1;
    }
    return count;
    }

    // Driver code
    let  n = 15;
    // Function call
    document.write(countSteps(n));

// This code is contributed by patel2127
</script>
```

**Output**

```
5
```

**时间复杂度:** O(logN)