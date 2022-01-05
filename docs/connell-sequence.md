# 康奈尔序列

> 原文:[https://www.geeksforgeeks.org/connell-sequence/](https://www.geeksforgeeks.org/connell-sequence/)

给定一个整数“n”，生成连接序列的前“n”项。
**康奈尔序列**是以第一个奇数即 1 为第一项形成的序列。序列的后续项由前两个偶数组成，即 2 和 4，接下来是三个奇数，即 5、7 和 9，接下来是四个偶数，即 10、12、14 和 16，依此类推。序列继续。
**配方:**

```
a[n] = 2 * n - floor((1 + sqrt(8 * n - 7))/2)   ; n > 1
```

**例:**

```
Input : 6
Output : 1 2 4 5 7 9

Input : 12
Output : 1 2 4 5 7 9 10 12 14 16 17 19
```

这里需要注意的是，将新行中的术语写成，第一行中的第一个术语，下一行中的下两个术语，下一行中的下三个术语等等，给出了一个有趣的模式:
第 1 行:1
第 2 行:2 4
第 3 行:5 7 9
第 4 行:10 12 14 16
第 5 行:17 19 21 23 25
等等……
该模式是特定行的每最后一个数字等于该行号的平方。
例如

1.  在第 2 行，最后一个数字是 4，等于其行号的平方，即 2^2
2.  第 5 行最后一个数字是 25，等于其行号的平方，即 5^2

下面是一个简单的实现，我们通过交替添加奇数和偶数个元素来生成结果。我们使用当前列表的大小来决定下一个要推送的元素数量。

## C++

```
// CPP code to generate first 'n' terms
// of Connell Sequence
#include <bits/stdc++.h>
using namespace std;

// Function to generate a fixed number
// of even or odd terms. The size of r
// decides whether numbers to be generated
// even or odd.
vector<long long int> gen(long long int n,
                  vector<long long int> r)
{
    long long int a = r[r.size() - 1];
    a++;
    for (int i = 1; i <= n; a += 2, i++)
        r.push_back(a);
    return r;
}

// Generating the first 'n' terms of
// Connell Sequence
vector<long long int> conell(long long int n)
{
    vector<long long int> res;
    long long int k = 1;

    // A dummy 0 is inserted at the
    // beginning for consistency
    res.push_back(0);

    while (1)
    {
        // Calling function gen() to generate
        // 'k' number of terms
        res = gen(k, res);
        k++;

        int j = res.size() - 1;
        while (j != n && j + k > n)
            k--;

        // Checking if 'n' terms are
        // already generated
        if (j >= n)
            break;
    }

    // Removing the previously inserted dummy 0
    res.erase(res.begin());

    return res;
}

// Driver Method
int main()
{
    long long int n = 10;

    cout << "The first " << n
         << " terms are" << endl;
    vector<long long int> res = conell(n);
    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to generate
// first 'n' terms
// of Connell Sequence
import java.util.*;

class GFG
{

    // Function to generate a
    // fixed number of even or
    // odd terms. The size of r
    // decides whether numbers
    // to be generated even or odd.

    static Vector<Long> gen(long n, Vector<Long> r)
    {    
        long a = r.get(r.size() - 1);    
        a++;    
        for (int i = 1; i <= n; a += 2, i++)
        {
            r.add(a);
        }    
        return r;    
    }

    // Generating the first
    // 'n' terms of
    // Connell Sequence
    static Vector<Long> conell(long n)
    {    
        Vector<Long> res = new Vector<Long>();    
        long k = 1;

        // A dummy 0 is inserted
        // at the beginning for
        // consistency
        res.add(0L);    

        while (true)
        {
            // Calling function
            // gen() to generate
            // 'k' number of terms
            res = gen(k, res);        
            k++;        

            int j = res.size() - 1;        
            while (j != n && j + k > n)
            {
                k--;
            }

            // Checking if 'n'
            // terms are already
            // generated
            if (j >= n)
            {
                break;
            }        
        }

        // Removing the previously
        // inserted dummy 0
        res.remove(0);    

        return res;    
    }

    // Driver Code
    public static void main(String[] args)
    {
        long n = 10;    

        System.out.println("The first "
                    + n + " terms are");

        Vector<Long> res = conell(n);    
        for (int i = 0; i < res.size(); i++)
        {
            System.out.print(res.get(i) + " ");
        }    
        System.out.println();    
    }
}

// This code has been contributed
// by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to generate first 'n' terms
# of Connell Sequence

# Function to generate a fixed number
# of even or odd terms. The size of r
# decides whether numbers to be generated
# even or odd.
def gen(n, r):
    a = r[-1]
    a += 1
    for i in range(1, n + 1):
        r.append(a)
        a += 2
    return r

# Generating the first 'n' terms of
# Connell Sequence
def conell(n):
    res = []
    k = 1

    # A dummy 0 is inserted at the
    # beginning for consistency
    res.append(0)

    while 1:

        # Calling function gen() to generate
        # 'k' number of terms
        res = gen(k, res)
        k += 1
        j = len(res) - 1
        while j != n and j + k > n:
            k -= 1

        # Checking if 'n' terms are
        # already generated
        if j >= n:
            break

    # Removing the previously inserted dummy 0
    res.remove(res[0])
    return res

# Driver Code
if __name__ == "__main__":
    n = 10
    print("The first %d terms are" % n)
    res = conell(n)
    for i in range(len(res)):
        print(res[i], end = " ")
    print()

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# code to generate
// first 'n' terms
// of Connell Sequence
using System;
using System.Collections.Generic;

class GFG
{
    // Function to generate a
    // fixed number of even or
    // odd terms. The size of r
    // decides whether numbers
    // to be generated even or odd.
    static List<long> gen(long n,
                          List<long> r)
    {
        long a = r[r.Count - 1];
        a++;
        for (int i = 1; i <= n;
                 a += 2, i++)
            r.Add(a);
        return r;
    }

    // Generating the first
    // 'n' terms of
    // Connell Sequence
    static List<long> conell(long n)
    {
        List<long> res = new List<long>();
        long k = 1;

        // A dummy 0 is inserted
        // at the beginning for
        // consistency
        res.Add(0);

        while (true)
        {
            // Calling function
            // gen() to generate
            // 'k' number of terms
            res = gen(k, res);
            k++;

            int j = res.Count - 1;
            while (j != n &&
                   j + k > n)
                k--;

            // Checking if 'n'
            // terms are already
            // generated
            if (j >= n)
                break;
        }

        // Removing the previously
        // inserted dummy 0
        res.RemoveAt(0);

        return res;
    }

    // Driver Code
    static void Main()
    {
        long n = 10;

        Console.WriteLine("The first " +
                      n + " terms are");
        List<long> res = conell(n);
        for (int i = 0; i < res.Count; i++)
            Console.Write(res[i] + " ");
        Console.WriteLine();
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>

// Javascript code to generate first 'n' terms
// of Connell Sequence

// Function to generate a fixed number
// of even or odd terms. The size of r
// decides whether numbers to be generated
// even or odd.
function gen(n, r)
{
    var a = r[r.length - 1];
    a++;
    for (var i = 1; i <= n; a += 2, i++)
        r.push(a);
    return r;
}

// Generating the first 'n' terms of
// Connell Sequence
function conell(n)
{
    var res = [];
    var k = 1;

    // A dummy 0 is inserted at the
    // beginning for consistency
    res.push(0);

    while (1)
    {
        // Calling function gen() to generate
        // 'k' number of terms
        res = gen(k, res);
        k++;

        var j = res.length - 1;
        while (j != n && j + k > n)
            k--;

        // Checking if 'n' terms are
        // already generated
        if (j >= n)
            break;
    }

    // Removing the previously inserted dummy 0
    res.shift();

    return res;
}

// Driver Method
var n = 10;
document.write( "The first " + n
     + " terms are" + "<br>");
var res = conell(n);
for (var i = 0; i < res.length; i++)
    document.write( res[i] + " ");

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
The first 10 terms are
1 2 4 5 7 9 10 12 14 16 
```