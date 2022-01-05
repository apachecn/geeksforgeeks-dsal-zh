# 检查一个数是否可以表示为 2 个三角数的和

> 原文:[https://www . geesforgeks . org/check-如果一个数字可以表示为两个三角形数字的和/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-a-sum-of-2-triangular-numbers/)

给定一个整数 **N** ，任务是找出它是否可以写成两个[三角数](https://www.geeksforgeeks.org/triangular-numbers/)的和(可能不同也可能不同)。
**例:**

```
Input: N = 24
Output: YES
24 can be represented as 3+21.

Input: N = 15
Output: NO
```

**方法:**
考虑所有小于 **N** 的三角数，即 sqrt(N)数。让我们将它们添加到一个集合中，对于每个三角形数字 **X** ，我们检查集合中是否存在 **N-X** 。如果任意三角数为真，则答案为是，否则答案为否
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible or not
bool checkTriangularSumRepresentation(int n)
{
    unordered_set<int> tri;
    int i = 1;

    // Store all triangular numbers up to N in a Set
    while (1) {
        int x = i * (i + 1) / 2;
        if (x >= n)
            break;
        tri.insert(x);
        i++;
    }

    // Check if a pair exists
    for (auto tm : tri)
        if (tri.find(n - tm) != tri.end())
            return true;
    return false;
}

// Driver Code
int main()
{
    int n = 24;
    checkTriangularSumRepresentation(n) ? cout << "Yes"
                                        : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to check if it is possible or not
    static boolean checkTriangularSumRepresentation(int n)
    {
        HashSet<Integer> tri = new HashSet<>();
        int i = 1;

        // Store all triangular numbers up to N in a Set
        while (true)
        {
            int x = i * (i + 1) / 2;
            if (x >= n)
            {
                break;
            }
            tri.add(x);
            i++;
        }

        // Check if a pair exists
        for (Integer tm : tri)
        {
            if (tri.contains(n - tm) && (n - tm) !=
                (int) tri.toArray()[tri.size() - 1])
            {
                return true;
            }
        }
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 24;
        if (checkTriangularSumRepresentation(n))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to check if it is possible or not
def checkTriangularSumRepresentation(n) :

    tri = list();
    i = 1;

    # Store all triangular numbers
    # up to N in a Set
    while (1) :
        x = i * (i + 1) // 2;
        if (x >= n) :
            break;

        tri.append(x);
        i += 1;

    # Check if a pair exists
    for tm in tri :
        if n - tm in tri:
            return True;

    return False;

# Driver Code
if __name__ == "__main__" :
    n = 24;

    if checkTriangularSumRepresentation(n) :
        print("Yes")
    else :
        print("No")

# This code is contributed by Ryuga       
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to check if it is possible or not
    static bool checkTriangularSumRepresentation(int n)
    {
        HashSet<int> tri = new HashSet<int>();
        int i = 1;

        // Store all triangular numbers up to N in a Set
        while (true)
        {
            int x = i * (i + 1) / 2;
            if (x >= n)
            {
                break;
            }
            tri.Add(x);
            i++;
        }

        // Check if a pair exists
        foreach (int tm in tri)
        {
            if (tri.Contains(n - tm))
            {
                return true;
            }
        }
        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 24;
        if (checkTriangularSumRepresentation(n))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to check if it is possible or not
function checkTriangularSumRepresentation($n)
{
    $tri = array();
    $i = 1;

    // Store all triangular numbers
    // up to N in a Set
    while (true)
    {
        $x = $i * ($i + 1);
        if ($x >= $n)
            break;

        array_push($tri, $x);
        $i += 1;
    }

    // Check if a pair exists
    foreach($tri as $tm)
        if (in_array($n - $tm, $tri))
            return true;

    return false;
}

// Driver Code
$n = 24;

if (checkTriangularSumRepresentation($n))
    print("Yes");
else
    print("No");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check if it is possible or not
function checkTriangularSumRepresentation(n)
{
    var tri = new Set();
    var i = 1;

    // Store all triangular numbers up to N in a Set
    while (1) {
        var x = i * parseInt((i + 1) / 2);
        if (x >= n)
            break;
        tri.add(x);
        i++;
    }

    var ans = false;
    // Check if a pair exists
    tri.forEach(tm => {
        if (tri.has(n - tm))
            ans = true
    });
    return ans;
}

// Driver Code
var n = 24;
checkTriangularSumRepresentation(n) ? document.write( "Yes")
                                    : document.write( "No");

// This code is contributed by famously.
</script>
```

**Output:** 

```
Yes
```