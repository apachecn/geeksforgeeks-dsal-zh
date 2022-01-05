# 从 N 的值中找出 N！

> 原文:[https://www.geeksforgeeks.org/find-n-from-the-value-of-n/](https://www.geeksforgeeks.org/find-n-from-the-value-of-n/)

给定一个数字 **K** ，代表一个数字 **N** 的阶乘，任务是找到 **N** 的值。
**注:**K<10<sup>18</sup>
**例:**

> **输入:**K = 120
> T3】输出:5
> T6】说明:T8】5！= 1 * 2 * 3 * 4 * 5 = 120
> **输入:** K = 6
> **输出:** 3
> **解释:**
> 3！= 1 * 2 * 3 = 6

**进场:**给出 N 的值！还不到 10 <sup>18</sup> 。通过观察我们可以看出，这仅适用于 **N < = 18** 。因此，我们可以预先计算从 1 到 18 的阶乘值，并将其存储在哈希表或映射中。预计算后，对于 N 的每一个值！，则在常数时间内返回相应的 N。
以下是上述方法的实现:

## C++

```
// C++ program to find a number such that
// the factorial of that number is given

#include "bits/stdc++.h"
#define ll long long int
using namespace std;

// Map to precompute and store the
// factorials of the numbers
map<ll, ll> m;

// Function to precompute factorial
int precompute()
{

    ll fact = 1;
    for (ll i = 1; i <= 18; i++) {

        // Calculating the factorial for
        // each i and storing in a map
        fact = fact * i;
        m[fact] = i;
    }
}

// Driver code
int main()
{
    // Precomputing the factorials
    precompute();

    int K = 120;
    cout << m[K] << endl;

    K = 6;
    cout << m[K] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a number such that
// the factorial of that number is given
import java.util.*;

class GFG{

// Map to precompute and store the
// factorials of the numbers
static Map<Integer, Integer> m = new HashMap<Integer, Integer>();

// Function to precompute factorial
static void precompute()
{

    int fact = 1;
    for (int i = 1; i <= 18; i++) {

        // Calculating the factorial for
        // each i and storing in a map
        fact = fact * i;
        m.put(fact, i);
    }
}

// Driver code
public static void main(String[] args)
{
    // Precomputing the factorials
    precompute();

    int K = 120;
    System.out.print(m.get(K) +"\n");

    K = 6;
    System.out.print(m.get(K) +"\n");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find a number such that
# the factorial of that number is given

# Map to precompute and store the
# factorials of the numbers
m = {};

# Function to precompute factorial
def precompute() :

    fact = 1;
    for i in range(1, 19) :

        # Calculating the factorial for
        # each i and storing in a map
        fact = fact * i;
        m[fact] = i;

# Driver code
if __name__ == "__main__" :

    # Precomputing the factorials
    precompute();

    K = 120;
    print(m[K]);

    K = 6;
    print(m[K]) ;

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find a number such that
// the factorial of that number is given
using System;
using System.Collections.Generic;

class GFG{

// Map to precompute and store the
// factorials of the numbers
static Dictionary<int, int> m = new Dictionary<int, int>();

// Function to precompute factorial
static void precompute()
{

    int fact = 1;
    for (int i = 1; i <= 18; i++) {

        // Calculating the factorial for
        // each i and storing in a map
        fact = fact * i;
        m.Add(fact, i);
    }
}

// Driver code
public static void Main(String[] args)
{
    // Precomputing the factorials
    precompute();

    int K = 120;
    Console.Write(m[K] +"\n");

    K = 6;
    Console.Write(m[K] +"\n"); 
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Map to precompute and store the
// factorials of the numbers
var m = {};

// Function to precompute factorial
function precompute()
{

    var fact = 1;
    for (var i = 1; i <= 18; i++) {

        // Calculating the factorial for
        // each i and storing in a map
        fact = fact * i;
        m[fact] = i;
    }
}

// Driver code
precompute();
var K = 120;
document.write(m[K] + "<br>");

K = 6;
document.write(m[K]);

// This code is contributed by Shivanisingh
</script>
```

**Output:** 

```
5
3
```