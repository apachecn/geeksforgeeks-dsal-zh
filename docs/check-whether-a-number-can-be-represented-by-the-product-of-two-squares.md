# 检查一个数字是否可以用两个正方形的乘积来表示

> 原文:[https://www . geesforgeks . org/check-一个数字是否可以用两个正方形的乘积来表示/](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-by-the-product-of-two-squares/)

给定一个**整数 n** ，我们的任务是检查数字 n 是否可以用两个正方形的乘积来表示。如果可能，则打印“是”，否则打印“否”。
**例:**

> **输入:** n = 144
> **输出:**是
> **说明:**
> 给定的数字 144 可以表示为 2 <sup>2</sup> * 6 <sup>2</sup> = 144。
> 
> **输入:** n = 25
> **输出:**否
> **说明:**
> 给定的数字 25 不能表示为两个平方数的乘积。

**天真法:**
解决上述问题的天真法是使用**蛮力法**。使用 2 进行循环迭代，直到 n，每次我们将检查两个数的平方的乘积是否等于 n。如果我们找到这样的组合，我们将打印“是”，否则打印“否”

下面是上述方法的实现:

## C++

```
// C++ implementation to Check whether a number can
// be represented by the product of two squares
#include <bits/stdc++.h>
using namespace std;

// Function to check if there exist two
// numbers product of whose squares is n.
bool prodSquare(int n)
{
    for (long i = 2; i * i <= n; i++)

        for (long j = 2; j <= n; j++)

            // check whether the product of the square
            // of both numbers is equal to N
            if (i * i * j * j == n)
                return true;

    return false;
}

// Driver code
int main()
{
    int n = 25;
    if (prodSquare(n))
        cout << "Yes";

    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether a number can
// be represented by the product of two squares
class GFG{

// Function to check if there exist two
// numbers product of whose squares is n.
static boolean prodSquare(int n)
{
    for (long i = 2; i * i <= n; i++)

        for (long j = 2; j <= n; j++)

            // Check whether the product of the square
            // of both numbers is equal to N
            if (i * i * j * j == n)
                return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    int n = 25;
    if (prodSquare(n))
        System.out.print("Yes");

    else
        System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to check whether
# a number can be represented by the
# product of two squares

# Function to check if there exist two
# numbers product of whose squares is n.
def prodSquare(n):

    for i in range(2, (n) + 1):
        if(i * i < (n + 1)):
            for j in range(2, n + 1):

                # Check whether the product
                # of the square of both
                # numbers is equal to N
                if ((i * i * j * j) == n):
                    return True;
    return False;

# Driver code
if __name__ == '__main__':

    n = 25;

    if (prodSquare(n)):
        print("Yes");
    else:
        print("No");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to check whether
// a number can be represented by
// the product of two squares
using System;

class GFG{

// Function to check if there
// exist two numbers product
// of whose squares is n.
static bool prodSquare(int n)
{
    for(long i = 2; i * i <= n; i++)

       for(long j = 2; j <= n; j++)

          // Check whether the product
          // of the square of both
          // numbers is equal to N
          if (i * i * j * j == n)
              return true;

    return false;
}

// Driver code
public static void Main(String[] args)
{
    int n = 25;

    if (prodSquare(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// javascript implementation to check whether a number can
// be represented by the product of two squares

// Function to check if there exist two
// numbers product of whose squares is n.
    function prodSquare(n) {
        for (i = 2; i * i <= n; i++)

            for (j = 2; j <= n; j++)

                // Check whether the product of the square
                // of both numbers is equal to N
                if (i * i * j * j == n)
                    return true;

        return false;
    }

    // Driver code

        var n = 25;
        if (prodSquare(n))
            document.write("Yes");

        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
No
```

**时间复杂度:** O(n)

**辅助空间:** O(1)

**高效方法:**
要优化上述方法，使用 **hashmap** ，我们将存储数字的平方直到 sqrt(n)，并且每次我们将在 hashmap 中搜索(n / sqrt(i))，如果它存在，则返回 Yes，否则返回 No

## C++

```
// C++ implementation to Check whether a number can
// be represented by the product of two squares
#include <bits/stdc++.h>
using namespace std;

// Function to check if there exist two
// numbers product of whose squares is n
bool prodSquare(int n)
{
    // Initialize map
    unordered_map<float, float> s;

    for (int i = 2; i * i <= n; ++i) {

        // Store square value in hashmap
        s[i * i] = 1;

        if (s.find(n / (i * i)) != s.end())
            return true;
    }
    return false;
}

// Driver code
int main()
{
    int n = 25;

    if (prodSquare(n))
        cout << "Yes";

    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether
// a number can be represented by the
// product of two squares
import java.util.*;

class GFG{

// Function to check if there exist two
// numbers product of whose squares is n
static boolean prodSquare(int n)
{

    // Initialize map
    HashMap<Float, Float> s = new HashMap<Float, Float>();

    for(int i = 2; i * i <= n; ++i)
    {

       // Store square value in hashmap
       s.put((float)(i * i), (float) 1);

       if (s.containsKey((float) n / (i * i)))
           return true;
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    int n = 25;

    if (prodSquare(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to check whether
# a number can be represented by the
# product of two squares

# Function to check if there exist two
# numbers product of whose squares is n
def prodSquare(n):

    # Initialize dict/map
    s = dict()

    i = 2
    while (i * i <= n):

        # Store square value in hashmap
        s[i * i] = 1

        if ((n // (i * i)) in s):
            return True

        i += 1

    return False

# Driver Code
if __name__ == '__main__':

    n = 25

    if (prodSquare(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by himanshu77
```

## C#

```
// C# implementation to check whether
// a number can be represented by the
// product of two squares
using System;
using System.Collections.Generic;

class GFG{

// Function to check if there exist two
// numbers product of whose squares is n
static bool prodSquare(int n)
{

    // Initialize map
    Dictionary<float,
               float> s = new Dictionary<float,
                                         float>();
    for(int i = 2; i * i <= n; ++i)
    {

       // Store square value in hashmap
       s.Add((float)(i * i), (float) 1);

       if (s.ContainsKey((float) n / (i * i)))
           return true;
    }
    return false;
}

// Driver code
public static void Main(String[] args)
{
    int n = 25;

    if (prodSquare(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
//Javascript implementation to check whether
// K times of a element is present in
// the array

// Function to check if there exist two
// numbers product of whose squares is n
function prodSquare(n)
{
    // Initialize map
    var s = new Map();

    for (var i = 2; i * i <= n; ++i) {

        // Store square value in hashmap
        s.set(i * i,1);

        if (s.has(n / (i * i)))
            return true;
    }
    return false;
}

// Driver program to test above
var n = 25;
if (prodSquare(n))
    document.write("Yes");
else
    document.write("No");
// This code is contributed by shivani.
</script>
```

**Output:** 

```
No
```

**时间复杂度:** O(sqrt n)

**辅助空间:** O(sqrt n)