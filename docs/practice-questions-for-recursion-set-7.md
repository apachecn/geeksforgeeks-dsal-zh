# 递归练习题|第 7 集

> 原文:[https://www . geesforgeks . org/practice-questions-for-recursion-set-7/](https://www.geeksforgeeks.org/practice-questions-for-recursion-set-7/)

**问题 1** 预测以下程序的输出。下面的 fun()一般做什么？

## C++

```
#include <iostream>
using namespace std;

int fun(int n, int* fp)
{
    int t, f;

    if (n <= 2) {
        *fp = 1;
        return 1;
    }
    t = fun(n - 1, fp);
    f = t + *fp;
    *fp = t;
    return f;
}

int main()
{
    int x = 15;
    cout << fun(5, &x) << endl;

    return 0;
}
```

## C

```
#include <stdio.h>

int fun ( int n, int *fp )
{
    int t, f;

    if ( n <= 2 )
    {
        *fp = 1;
        return 1;
    }
    t = fun ( n-1, fp );
    f = t + *fp;
    *fp = t;
    return f;
}

int main()
{
    int x = 15;
    printf("%d\n",fun(5, &x));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {
    static int fp = 15;
    static int fun ( int n)
    {
        int t, f;

        if ( n <= 2 )
        {
            fp = 1;
            return 1;
        }
        t = fun ( n - 1);
        f = t + fp;
        fp = t;
        return f;
    }
     public static void main (String[] args)
    {
        System.out.println(fun(5));
    }
}
// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
fp = 15
def fun ( n ):
    global fp
    if ( n <= 2 ):
        fp = 1
        return 1

    t = fun ( n - 1 )
    f = t + fp
    fp = t
    return f

# Driver code

print(fun(5))

# This code is contributed by shubhamsingh10
```

## C#

```
using System;

class GFG{
    static int fp = 15;
    static int fun ( int n)
    {
        int t, f;

        if ( n <= 2 )
        {
            fp = 1;
            return 1;
        }
        t = fun ( n - 1 );
        f = t + fp;
        fp = t;
        return f;
    }

    static public void Main ()
    {
        Console.Write(fun(5));
    }
}
// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
//Javascript Implementation
var fp = 15;
function fun( n )
{
    var t, f;

    if ( n <= 2 )
    {
        fp = 1;
        return 1;
    }
    t = fun ( n - 1 );
    f = t + fp;
    fp = t;
    return f;
}

// Driver Code

document.write(fun(5));

// This code is contributed by shubhamsingh10

</script>
```

**Output**

```
5

```

程序计算第 n 个斐波那契数。语句 t = fun ( n-1，fp)给出第(n-1)个斐波那契数，*fp 用于存储第(n-2)个斐波那契数。*fp 的初始值(在上面的程序中是 15)无关紧要。下面的递归树显示了从 1 到 10 的所有步骤，用于 fun(5，&x)的执行。

```
                              (1) fun(5, fp)
                              /           \
                         (2) fun(4, fp)  (10) t = 5, f = 8, *fp = 5
                         /          \
                   (3) fun(3, fp)  (9) t = 3, f = 5, *fp = 3
                  /            \
           (4) fun(2, fp)      (8) t = 2, f = 3, *fp = 2
          /          \
   (5) fun(1, fp)   (7) t = 1, f = 2, *fp = 1
   /
(6) *fp = 1
```

**问题 2:** 预测以下程序的输出。

## C++

```
#include <iostream>
using namespace std;
void fun(int n)
{
    if(n > 0)
    {
        fun(n - 1);
        cout << n <<" ";
        fun(n - 1);
    }
}

int main()
{
    fun(4);
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
#include <stdio.h>

void fun(int n)
{
    if(n > 0)
    {
        fun(n-1);
        printf("%d ", n);
        fun(n-1);
    }
}

int main()
{
    fun(4);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{
static void fun(int n)
{
    if(n > 0)
    {
        fun(n - 1);
        System.out.print(n+" ");
        fun(n - 1);
    }
}

public static void main(String[] args)
{
    fun(4);
}
}
// This code is contributed by Shubhamsingh10
```

## 蟒蛇 3

```
def fun(n):

    if(n > 0):
        fun(n - 1)
        print(n,end=" ")
        fun(n - 1)

# driver code

fun(4)

# This code is contributed by shubhamsingh10
```

## C#

```
using System;

class GFG{
    static void fun(int n)
    {
        if(n > 0)
        {
            fun(n - 1);
            Console.Write(n+" ");
            fun(n - 1);
        }
    }

    static public void Main ()
    { 
        fun(4);  
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
function fun(n)
{
    if(n > 0)
        fun(n - 1);
        document.write(n+" ")
        fun(n - 1);
}

// driver code
fun(4)

// This code is contributed by bobby.
</script>
```

**Output**

```
1 2 1 3 1 2 1 4 1 2 1 3 1 2 1 
```

```
                     fun(4)
                   /
                fun(3), print(4), fun(3) [fun(3) prints 1 2 1 3 1 2 1]
               /
           fun(2), print(3), fun(2) [fun(2) prints 1 2 1]
           /
       fun(1), print(2), fun(1) [fun(1) prints 1]
       /
    fun(0), print(1), fun(0) [fun(0) does nothing]
```

如果您发现任何答案/代码不正确，或者您想分享关于上述主题的更多信息/问题，请写评论。