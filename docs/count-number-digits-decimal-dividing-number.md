# 数除一个数字后的小数位数

> 原文:[https://www . geesforgeks . org/count-number-digits-decimal-number/](https://www.geeksforgeeks.org/count-number-digits-decimal-dividing-number/)

给我们两个数字 A 和 b，我们需要计算小数点后的位数。如果数字是无理数，那么打印“INF”。
**例:**

```
Input  : x = 5, y = 3
Output : INF
5/3 = 1.666....

Input :  x = 3, y = 6
Output : 1
3/6 = 0.5 
```

这个想法很简单，我们按照学校的划分，一个一个地划分，同时记录剩余部分。如果余数为 0，我们返回小数点后的位数。如果余数重复，我们返回 INF。

## C++

```
// CPP program to count digits after dot when a
// number is divided by another.
#include <bits/stdc++.h>
using namespace std;

int count(int x, int y)
{
    int ans = 0;  // Initialize result

    unordered_map<int, int> m;

    // calculating remainder
    while (x % y != 0) {

        x = x % y;

        ans++;

        // if this remainder appeared before then
        // the numbers are irrational and would not
        // converge to a solution the digits after
        // decimal will be infinite
        if (m.find(x) != m.end())
            return -1;

        m[x] = 1;
        x = x * 10;
    }
    return ans;
}

// Driver code
int main()
{
    int res = count(1, 2);
    (res == -1)? cout << "INF" : cout << res;

    cout << endl;
    res = count(5, 3);
    (res == -1)? cout << "INF" : cout << res;

    cout << endl;
    res = count(3, 5);
    (res == -1)? cout << "INF" : cout << res;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count digits after dot when a
// number is divided by another.
import java.util.*;

class GFG
{

static int count(int x, int y)
{
    int ans = 0; // Initialize result

    Map<Integer,Integer> m = new HashMap<>();

    // calculating remainder
    while (x % y != 0)
    {

        x = x % y;

        ans++;

        // if this remainder appeared before then
        // the numbers are irrational and would not
        // converge to a solution the digits after
        // decimal will be infinite
        if (m.containsKey(x))
            return -1;

        m.put(x, 1);
        x = x * 10;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int res = count(1, 2);
    if((res == -1))
        System.out.println("INF");
    else
        System.out.println(res);

    res = count(5, 3);
    if((res == -1))
        System.out.println("INF");
    else
        System.out.println(res);

    res = count(3, 5);
    if((res == -1))
        System.out.println("INF");
    else
        System.out.println(res);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count digits after dot
# when a number is divided by another.
def count(x, y):
    ans = 0 # Initialize result

    m = dict()

    # calculating remainder
    while x % y != 0:
        x %= y

        ans += 1

        # if this remainder appeared before then
        # the numbers are irrational and would not
        # converge to a solution the digits after
        # decimal will be infinite
        if x in m:
            return -1

        m[x] = 1
        x *= 10

    return ans

# Driver Code
if __name__ == "__main__":
    res = count(1, 2)

    print("INF") if res == -1 else print(res)

    res = count(5, 3)
    print("INF") if res == -1 else print(res)

    res = count(3, 5)
    print("INF") if res == -1 else print(res)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to count digits after dot when a
// number is divided by another.
using System;
using System.Collections.Generic;

class GFG
{

static int count(int x, int y)
{
    int ans = 0; // Initialize result

    Dictionary<int,int> m = new Dictionary<int,int>();

    // calculating remainder
    while (x % y != 0)
    {

        x = x % y;

        ans++;

        // if this remainder appeared before then
        // the numbers are irrational and would not
        // converge to a solution the digits after
        // decimal will be infinite
        if (m.ContainsKey(x))
            return -1;

        m.Add(x, 1);
        x = x * 10;
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int res = count(1, 2);
    if((res == -1))
        Console.WriteLine("INF");
    else
        Console.WriteLine(res);

    res = count(5, 3);
    if((res == -1))
        Console.WriteLine("INF");
    else
        Console.WriteLine(res);

    res = count(3, 5);
    if((res == -1))
        Console.WriteLine("INF");
    else
        Console.WriteLine(res);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to count digits after dot when a
// number is divided by another.

function count(x,y)
{
    let ans = 0; // Initialize result
    let m = new Map();
    // calculating remainder
    while (x % y != 0)
    {

        x = x % y;

        ans++;

        // if this remainder appeared before then
        // the numbers are irrational and would not
        // converge to a solution the digits after
        // decimal will be infinite
        if (m.has(x))
            return -1;

        m.set(x, 1);
        x = x * 10;
    }
    return ans;
}

// Driver code
let res = count(1, 2);
    if((res == -1))
        document.write("INF"+"<br>");
    else
        document.write(res+"<br>");

    res = count(5, 3);
    if((res == -1))
        document.write("INF"+"<br>");
    else
        document.write(res+"<br>");

    res = count(3, 5);
    if((res == -1))
        document.write("INF"+"<br>");
    else
        document.write(res+"<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
1
INF
1
```

**时间复杂度:** O(N * log(N))

**辅助空间:** O(N)

本文由 [**拉胡尔·查瓦拉**](https://www.linkedin.com/in/rahulchawla1995/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。