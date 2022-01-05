# 所有 K 值的所有可能地板值(N/K)

> 原文:[https://www . geeksforgeeks . org/all-可能的值-of-florn-k-for-all-value-of-k/](https://www.geeksforgeeks.org/all-possible-values-of-floorn-k-for-all-values-of-k/)

给定一个函数**f(K)= floor(N/K)**(**N>0**和 **K > 0** ，任务是为给定的 **N** 找到 **f(K)** 的所有可能值，其中 **K** 取范围**【1，Inf】**内的所有值。
**举例:**

> **输入:** N = 5
> **输出:** 0 1 2 5
> **解释:**
> 5 除 1 = 5
> 5 除 2 = 2
> 5 除 3 = 1
> 5 除 4 = 1
> 5 除 5 = 1
> 5 除 6 = 0
> 5 除 7 = 0
> 所以 f(k)所有可能的不同值都是{0，1，2，5}。
> **输入:** N = 11
> **输出:** 0 1 2 3 5 11
> **解释:**
> 11 除 1 = 11
> 11 除 2 = 5
> 11 除 3 = 3
> 11 除 4 = 2
> 11 除 5 = 2
> 11 除 6 = 1
> 11 除 7 = 1
> …【T39】

**天真方法:**
**最简单的方法**迭代**【1，N+1】**并存储在 [**集合**](https://www.geeksforgeeks.org/set-in-cpp-stl/) 中， **(N/i)** ( 1？我吗？N + 1)以避免重复。
以下是上述方法的实施:

## C++

```
// C++ Program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all
// possible values of
// floor(N/K)
void allQuotients(int N)
{
    set<int> s;

    // loop from 1 to N+1
    for (int k = 1; k <= N + 1; k++) {
        s.insert(N / k);
    }

    for (auto it : s)
        cout << it << " ";
}

int main()
{
    int N = 5;
    allQuotients(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print all
// possible values of
// Math.floor(N/K)
static void allQuotients(int N)
{
    HashSet<Integer> s = new HashSet<Integer>();

    // loop from 1 to N+1
    for(int k = 1; k <= N + 1; k++)
    {
        s.add(N / k);
    }

    for(int it : s)
        System.out.print(it + " ");
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    allQuotients(N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print all possible
# values of floor(N/K)
def allQuotients(N):

    s = set()

    # Iterate from 1 to N+1
    for k in range(1, N + 2):
        s.add(N // k)

    for it in s:
        print(it, end = ' ')

# Driver code
if __name__ == '__main__':

    N = 5

    allQuotients(N)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print all possible
// values of Math.floor(N/K)
static void allQuotients(int N)
{
    SortedSet<int> s = new SortedSet<int>();

    // Loop from 1 to N+1
    for(int k = 1; k <= N + 1; k++)
    {
        s.Add(N / k);
    }

    foreach(int it in s)
    {
        Console.Write(it + " ");
    }
}

// Driver code
static void Main()
{
    int N = 5;

    allQuotients(N);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript Program for the
// above approach

// Function to print all
// possible values of
// floor(N/K)
function allQuotients(N)
{
    var s = new Set();

    // loop from 1 to N+1
    for (var k = 1; k <= N + 1; k++) {
        s.add(parseInt(N / k));
    }

    var ls = Array.from(s).reverse();
    ls.forEach(v => document.write(v+ " "))
}

var N = 5;
allQuotients(N);

</script>
```

**Output:** 

```
0 1 2 5
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*
**高效途径:**
优化的解决方案是迭代**【1，？N]** 并将值 **K** 和 **(N/K)** 插入到集合中。

## C++

```
// C++ Program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all
// possible values of
// floor(N/K)
void allQuotients(int N)
{
    set<int> s;
    s.insert(0);

    for (int k = 1; k <= sqrt(N); k++) {
        s.insert(k);
        s.insert(N / k);
    }

    for (auto it : s)
        cout << it << " ";
}

int main()
{
    int N = 5;
    allQuotients(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to print all
// possible values of
// Math.floor(N/K)
static void allQuotients(int N)
{
    HashSet<Integer> s = new HashSet<Integer>();
    s.add(0);

    // loop from 1 to N+1
    for(int k = 1; k <= Math.sqrt(N); k++)
    {
        s.add(k);
        s.add(N / k);
    }

    for(int it : s)
        System.out.print(it + " ");
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    allQuotients(N);
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import *

# Function to print all possible
# values of floor(N/K)
def allQuotients(N):

    s = set()
    s.add(0)

    for k in range(1, int(sqrt(N)) + 1):
        s.add(k)
        s.add(N // k)

    for it in s:
        print(it, end = ' ')

# Driver code
if __name__ == '__main__':

    N = 5

    allQuotients(N)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print all possible
// values of Math.floor(N/K)
static void allQuotients(int N)
{
    SortedSet<int> s = new SortedSet<int>();
    s.Add(0);

    // loop from 1 to N+1
    for(int k = 1; k <= Math.Sqrt(N); k++)
    {
        s.Add(k);
        s.Add(N / k);
    }

    foreach(int it in s)
    {
        Console.Write(it + " ");
    }
}

// Driver code   
static void Main()
{
    int N = 5;

    allQuotients(N);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript Program for the
// above approach

// Function to print all
// possible values of
// floor(N/K)
function allQuotients(N)
{
    var s = new Set();
    s.add(0);

    for (var k = 1; k <= parseInt(Math.sqrt(N)); k++) {
        s.add(k);
        s.add(parseInt(N / k));
    }
    var tmp = [...s];
    tmp.sort((a,b)=>a-b)

    tmp.forEach(it => {
        document.write( it + " ");
    });
}

var N = 5;
allQuotients(N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
0 1 2 5
```

***时间复杂度:** O(？N)*
***辅助空间:** O(N)*