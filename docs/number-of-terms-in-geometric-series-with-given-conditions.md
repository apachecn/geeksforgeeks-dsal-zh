# 给定条件下几何级数的项数

> 原文:[https://www . geeksforgeeks . org/带有给定条件的几何级数术语数/](https://www.geeksforgeeks.org/number-of-terms-in-geometric-series-with-given-conditions/)

几何级数是整数 b1，b2，b3，…的序列，其中对于每个 i > 1，相应的项满足条件 b <sub>i</sub> = b <sub>i-1</sub> * q，其中 q 称为级数的公比。
给定由两个整数 b1 和 q 以及 m 个“坏”整数 a1、a2 定义的几何级数 b，..，am，和一个整数 l，当满足条件|b <sub>i</sub> | < = l 时，逐一写出所有级数项(包括重复项)(|x|表示 x 的绝对值)。
计算我们的序列中会有多少个数，如果有无限多的整数，则打印“inf”。
**注:**如果某项等于其中一个“坏”整数，则跳过该项，前进到下一项。

**示例:**

```
Input : b1 = 3, q = 2, l = 30,
        m = 4 
        6 14 25 48
Output : 3
The progression will be 3 12 24\. 
6 will also be there but because
it is a bad integer we won't include it

Input : b1 = 123, q = 1, l = 2143435
        m = 4
        123 11 -5453 141245
Output : 0
As value of q is 1, progression will 
always be 123 and would become infinity
but because it is a bad integer we
won't include it and hence our value
will become 0

Input : b1 = 123, q = 1, l = 2143435 
        m = 4
        5234 11 -5453 141245
Output : inf
In this case, value will be infinity 
because series will always be 123 as 
q is 1 and 123 is not a bad integer. 
```

**逼近:**
我们可以把我们的解分成不同的情况:
**情况 1:** 如果一个数列的起始值大于给定的极限，则输出为 0。
**情况 2:** 如果一个数列 q 的起始值为 0，那么还有三种情况:
**情况 2.a:** 如果 0 不是一个坏整数，那么答案就会变成 inf。
**病例 2.b:** If b1！= 0 但 q 是 0，b1 也不是坏整数，答案会是 1。
**情况 2.c:** 如果给定 0 为坏整数，b1 = 0，则答案为 0。
**情况 3:** 如果 q = 1，我们会检查 b1 是否作为坏整数给出。如果是，那么答案就是 0，否则答案就是 inf。
**病例 4:** 如果 q = -1，检查 b1 和-b1 是否存在。如果他们在场，我们的答案将是 0，否则我们的答案将是 inf。
**情况 5:** 如果以上情况都不成立，只需运行一个从 b1 到 l 的循环，计算元素个数。

下面是上述方法的实现:

## C++

```
// CPP program to find number of terms 
// in Geometric Series
#include <bits/stdc++.h>
using namespace std;

// A map to keep track of the bad integers
map<int, bool> mapp;

// Function to calculate No. of elements
// in our series
void progression(int b1, int q, int l,
                 int m, int bad[])
{
    // Updating value of our map
    for (int i = 0; i < m; i++)
        mapp[bad[i]] = 1;   

    // if starting value is greate
    // r than our given limit
    if (abs(b1) > l)
        cout << "0";

    // if q or starting value is 0   
    else if (q == 0 || b1 == 0)
    {  
        // if 0 is not a bad integer,
        // answer becomes inf
        if (mapp[0] != 1)        
            cout << "inf";

        // if q is 0 and b1 is not and b1
        // is not a bad integer, answer becomes 1
        else if (mapp[0] == 1 && mapp[b1] != 1)
            cout << "1";

        else // else if 0 is bad integer and
            // b1 is also a bad integer,
            // answer becomes 0
            cout << "0";
    }
    else if (q == 1) // if q is 1
    {  
        // and b1 is not a bad integer,
        // answer becomes inf
        if (mapp[b1] != 1)
            cout << "inf";

        else // else answer is 0
            cout << "0";
    }
    else if (q == -1) // if q is -1
    {  
        // and either b1 or -b1 is not
        // present answer becomes inf
        if (mapp[b1] != 1 || mapp[-1 * b1] != 1)
            cout << "inf";

        else // else answer becomes 0
            cout << "0";
    }
    else // if none of the above case is true,
         // simpy calculate the number of
        // elements in our series
    {
        int co = 0;
        while (abs(b1) <= l) {
            if (mapp[b1] != 1)
                co++;
            b1 *= 1LL * q;
        }
        cout << co;
    }
}

// driver code
int main()
{  
    // starting value of series,
    // number to be multiplied,
    // limit within which our series,
    // No. of bad integers given
    int b1 = 3, q = 2, l = 30, m = 4;

    // Bad integers
    int bad[4] = { 6, 14, 25, 48 };

    progression(b1, q, l, m, bad);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of terms
// in Geometric Series
import java.util.*;

class GFG
{

    // A map to keep track of the bad integers
    static HashMap<Integer, Boolean> map = new HashMap<>();

    // Function to calculate No. of elements
    // in our series
    static void progression(int b1, int q, int l,
                                int m, int[] bad)
    {

        // Updating value of our map
        for (int i = 0; i < m; i++)
            map.put(bad[i], true);

        // if starting value is greate
        // r than our given limit
        if (Math.abs(b1) > l)
            System.out.print("0");

        // if q or starting value is 0
        else if (q == 0 || b1 == 0)
        {

            // if 0 is not a bad integer,
            // answer becomes inf
            if (!map.containsKey(0))
                System.out.print("inf");

            // if q is 0 and b1 is not and b1
            // is not a bad integer, answer becomes 1
            else if (map.get(0) == true && !map.containsKey(b1))
                System.out.print("1");

            // else if 0 is bad integer and
            // b1 is also a bad integer,
            // answer becomes 0
            else
                System.out.print("0");
        }

        // if q is 1
        else if (q == 1)
        {

            // and b1 is not a bad integer,
            // answer becomes inf
            if (!map.containsKey(b1))
                System.out.print("inf");

            // else answer is 0
            else
                System.out.print("0");

        }

        // if q is -1
        else if (q == -1)
        {

            // and either b1 or -b1 is not
            // present answer becomes inf
            if (!map.containsKey(b1) || !map.containsKey(-1 * b1))
                System.out.print("inf");

            // else answer becomes 0
            else
                System.out.print("0");

        }

        // if none of the above case is true,
        // simpy calculate the number of
        // elements in our series
        else
        {
            int co = 0;
            while (Math.abs(b1) <= l)
            {
                if (!map.containsKey(b1))
                    co++;
                b1 *= q;
            }
            System.out.print(co);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // starting value of series,
        // number to be multiplied,
        // limit within which our series,
        // No. of bad integers given
        int b1 = 3, q = 2, l = 30, m = 4;

        // Bad integers
        int[] bad = { 6, 14, 25, 48 };

        progression(b1, q, l, m, bad);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find number of terms
# in Geometric Series

# A map to keep track of the bad integers
mpp=dict()

# Function to calculate No. of elements
# in our series
def progression(b1, q, l, m, bad):

    # Updating value of our map
    for i in range(m):
        mpp[bad[i]] = 1

    # if starting value is greate
    # r than our given limit
    if (abs(b1) > l):
        print("0",end="")

    # if q or starting value is 0
    elif (q == 0 or b1 == 0) :

        # if 0 is not a bad integer,
        # answer becomes inf
        if (0 not in mpp.keys()):
            print("inf",end="")

        # if q is 0 and b1 is not and b1
        # is not a bad integer, answer becomes 1
        elif (mpp[0] == 1 and b1 not in mpp.keys()) :
            print("1",end="")

        else:
            # b1 is also a bad integer,
            # answer becomes 0
            print("0",end="")
    elif (q == 1): # if q is 1
        # and b1 is not a bad integer,
        # answer becomes inf
        if (b1 not in mpp.keys()) :
            print("inf",end="")
        else: # else answer is 0
            print("0",end="")

    elif (q == -1): # if q is -1
        # and either b1 or -b1 is not
        # present answer becomes inf
        if (b1 not in mpp.keys() or -1 * b1 not in mpp.keys()) :
            print("inf",end="")

        else :# else answer becomes 0
            print("0",end="")
    else :# if none of the above case is true,
        # simpy calculate the number of
        # elements in our series
        co = 0
        while (abs(b1) <= l):
            if (b1 not in mpp.keys()):
                co+=1
            b1 *= q
        print(co,end="")

# Driver code

# starting value of series,
# number to be multiplied,
# limit within which our series,
# No. of bad integers given
b1 = 3
q = 2
l = 30
m = 4

# Bad integers
bad=[6, 14, 25, 48]

progression(b1, q, l, m, bad)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find number of terms
// in Geometric Series
using System;
using System.Collections.Generic;

class GFG
{

    // A map to keep track of the bad integers
    static Dictionary<int,
                      bool> map = new Dictionary<int,
                                                 bool>();

    // Function to calculate No. of elements
    // in our series
    static void progression(int b1, int q, int l,
                            int m, int[] bad)
    {

        // Updating value of our map
        for (int i = 0; i < m; i++)
            if(!map.ContainsKey(bad[i]))
                map.Add(bad[i], true);

        // if starting value is greate
        // r than our given limit
        if (Math.Abs(b1) > l)
            Console.Write("0");

        // if q or starting value is 0
        else if (q == 0 || b1 == 0)
        {

            // if 0 is not a bad integer,
            // answer becomes inf
            if (!map.ContainsKey(0))
                Console.Write("inf");

            // if q is 0 and b1 is not and b1
            // is not a bad integer, answer becomes 1
            else if (map[0] == true &&
                    !map.ContainsKey(b1))
                Console.Write("1");

            // else if 0 is bad integer and
            // b1 is also a bad integer,
            // answer becomes 0
            else
                Console.Write("0");
        }

        // if q is 1
        else if (q == 1)
        {

            // and b1 is not a bad integer,
            // answer becomes inf
            if (!map.ContainsKey(b1))
                Console.Write("inf");

            // else answer is 0
            else
                Console.Write("0");
        }

        // if q is -1
        else if (q == -1)
        {

            // and either b1 or -b1 is not
            // present answer becomes inf
            if (!map.ContainsKey(b1) ||
                !map.ContainsKey(-1 * b1))
                Console.Write("inf");

            // else answer becomes 0
            else
                Console.Write("0");
        }

        // if none of the above case is true,
        // simpy calculate the number of
        // elements in our series
        else
        {
            int co = 0;
            while (Math.Abs(b1) <= l)
            {
                if (!map.ContainsKey(b1))
                    co++;
                b1 *= q;
            }
            Console.Write(co);
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // starting value of series,
        // number to be multiplied,
        // limit within which our series,
        // No. of bad integers given
        int b1 = 3, q = 2, l = 30, m = 4;

        // Bad integers
        int[] bad = { 6, 14, 25, 48 };

        progression(b1, q, l, m, bad);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to find number of terms
    // in Geometric Series

    // A map to keep track of the bad integers
    let map = new Map();

    // Function to calculate No. of elements
    // in our series
    function progression(b1,q,l,m,bad)
    {
        // Updating value of our map
        for (let i = 0; i < m; i++)
            map.set(bad[i], true);

        // if starting value is greate
        // r than our given limit
        if (Math.abs(b1) > l)
            document.write("0");

        // if q or starting value is 0
        else if (q == 0 || b1 == 0)
        {

            // if 0 is not a bad integer,
            // answer becomes inf
            if (!map.has(0))
                document.write("inf");

            // if q is 0 and b1 is not and b1
            // is not a bad integer, answer becomes 1
            else if (map[0] == true && !map.has(b1))
                document.write("1");

            // else if 0 is bad integer and
            // b1 is also a bad integer,
            // answer becomes 0
            else
                document.write("0");
        }

        // if q is 1
        else if (q == 1)
        {

            // and b1 is not a bad integer,
            // answer becomes inf
            if (!map.has(b1))
                document.write("inf");

            // else answer is 0
            else
                document.write("0");

        }

        // if q is -1
        else if (q == -1)
        {

            // and either b1 or -b1 is not
            // present answer becomes inf
            if (!map.has(b1) || !map.has(-1 * b1))
                document.write("inf");

            // else answer becomes 0
            else
                document.write("0");

        }

        // if none of the above case is true,
        // simpy calculate the number of
        // elements in our series
        else
        {
            let co = 0;
            while (Math.abs(b1) <= l)
            {
                if (!map.has(b1))
                    co++;
                b1 *= q;
            }
            document.write(co);
        }
    }

     // Driver Code

    // starting value of series,
    // number to be multiplied,
    // limit within which our series,
    // No. of bad integers given
    let b1 = 3, q = 2, l = 30, m = 4;

    // Bad integers
    let bad = [ 6, 14, 25, 48 ];

    progression(b1, q, l, m, bad);

// This code is contributed by patel2127
</script>
```

**输出:**

```
3
```

本文由 [**萨塔克·科利**](https://auth.geeksforgeeks.org/user/Sarthak%20Kohli/articles) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。