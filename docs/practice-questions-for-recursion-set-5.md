# 递归练习题|第 5 集

> 原文:[https://www . geesforgeks . org/practice-questions-for-recursion-set-5/](https://www.geeksforgeeks.org/practice-questions-for-recursion-set-5/)

**问题 1**
预测以下程序的输出。下面的 fun()一般做什么？

## C++

```
#include <iostream>
using namespace std;
int fun(int a, int b)
{
    if (b == 0)
        return 0;
    if (b % 2 == 0)
        return fun(a + a, b/2);

    return fun(a + a, b/2) + a;
}

int main()
{
    cout << fun(4, 3) ;
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
#include<stdio.h>

int fun(int a, int b)
{
   if (b == 0)
       return 0;
   if (b % 2 == 0)
       return fun(a+a, b/2);

   return fun(a+a, b/2) + a;
}

int main()
{
  printf("%d", fun(4, 3));
  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    static int fun(int a, int b)
    {
        if (b == 0)
            return 0;
        if (b % 2 == 0)
            return fun(a + a, b/2);

        return fun(a + a, b/2) + a;
    }

    public static void main (String[] args)
    {
        System.out.println(fun(4, 3));
    }
}
// This code is contributed by SHUBHAMSINGH10
```

## 蟒蛇 3

```
def fun(a, b):
    if (b == 0):
        return 0
    if (b % 2 == 0):
        return fun(a + a, b//2)

    return fun(a + a, b//2) + a

# Driver code

print(fun(4, 3))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
using System;

class GFG{

    static int fun(int a, int b)
    {
        if (b == 0)
            return 0;
        if (b % 2 == 0)
            return fun(a + a, b/2);

        return fun(a + a, b/2) + a;
    }

    static public void Main ()
    {
        Console.Write(fun(4, 3));
    }
}

// This code is contributed by SHUBHAMSINGH10
```

## java 描述语言

```
<script>
//Javascript Implementation
function fun(a, b)
{
    if (b == 0)
        return 0;
    if (b % 2 == 0)
        return fun(a + a, Math.floor(b/2));

    return fun(a + a, Math.floor(b/2)) + a;
}
document.write(fun(4, 3));
// This code is contributed by shubhamsingh10
</script>
```

**Output:** 

```
12
```

它计算 a*b (a 乘以 b)。

**问题 2**
在问题 1 中，如果我们用*替换+并用 return 1 替换 return 0，那么改变后的函数会做什么？以下是更改后的功能。

## C++

```
#include <iostream>
using namespace std;

int fun(int a, int b)
{
   if (b == 0)
       return 1;
   if (b % 2 == 0)
       return fun(a*a, b/2);

   return fun(a*a, b/2)*a;
}

int main()
{
  cout << fun(4, 3) ;
  getchar();
  return 0;
}

//This code is contributed by shubhamsingh10
```

## C

```
#include<stdio.h>

int fun(int a, int b)
{
   if (b == 0)
       return 1;
   if (b % 2 == 0)
       return fun(a*a, b/2);

   return fun(a*a, b/2)*a;
}

int main()
{
  printf("%d", fun(4, 3));
  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {
    static int fun(int a, int b)
    {
        if (b == 0)
            return 1;
        if (b % 2 == 0)
            return fun(a*a, b/2);

        return fun(a*a, b/2)*a;
    }

    public static void main (String[] args)
    {
        System.out.println(fun(4, 3));
    }
}
//This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
def fun(a, b):
    if (b == 0):
        return 1
    if (b % 2 == 0):
        return fun(a*a, b//2)

    return fun(a*a, b//2)*a

# Driver code

print(fun(4, 3))

# This code is contributed by shubhamsingh10
```

## C#

```
using System;

public class GFG{

    static int fun(int a, int b)
    {
        if (b == 0)
            return 1;
        if (b % 2 == 0)
            return fun(a*a, b/2);

        return fun(a*a, b/2)*a;
    }

    static public void Main ()
    {
        Console.WriteLine(fun(4, 3));
    }
}
// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
//Javascript Implementation
function fun(a, b)
{
    if (b == 0)
        return 1;
    if (b % 2 == 0)
        return fun(a * a, Math.floor(b/2));

    return fun(a * a, Math.floor(b/2)) * a;
}
document.write(fun(4, 3));
// This code is contributed by shubhamsingh10
</script>
```

**Output:** 

```
64
```

它计算 a^b (a 升到 b 次方)。

**问题 3**
预测以下程序的输出。下面的 fun()一般做什么？

## C++

```
#include <iostream>
using namespace std;

int fun(int n)
{
    if (n > 100)
        return n - 10;
    return fun(fun(n+11));
}

int main()
{
    cout << " " << fun(99) << " ";
    getchar();
    return 0;
}

// This code is contributed by Shubhamsingh10
```

## C

```
#include<stdio.h>

 int fun(int n)
 {
   if (n > 100)
     return n - 10;
   return fun(fun(n+11));
 }

int main()
{
  printf(" %d ", fun(99));
  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {
    static int fun(int n)
    {
        if (n > 100)
            return n - 10;
        return fun(fun(n+11));
    }

    public static void main (String[] args) {
        System.out.println(" " + fun(99) + " ");
    }
}
// This code is contributed by Shubhamsingh10
```

## 蟒蛇 3

```
def fun(n):

    if (n > 100):
        return n - 10

    return fun(fun(n + 11))

# Driver code
print(fun(99))

# This code is contributed by Shubhamsingh10
```

## C#

```
using System;

class GFG{

static int fun(int n)
{
    if (n > 100)
        return n - 10;
    return fun(fun(n + 11));
}

// Driver code   
static public void Main ()
{
    Console.WriteLine(fun(99));
}
}

// This code is contributed by Shubhamsingh10
```

## java 描述语言

```
<script>
function fun(n)
{
    if (n > 100)
        return n - 10

    return fun(fun(n + 11))
}

// Driver code
document.write(fun(99))

// This code is contributed by Bobby Gottumukkala
</script>
```

**Output:** 

```
91
```

```
fun(99) = fun(fun(110)) since 99 ? 100
           = fun(100)    since 110 > 100
           = fun(fun(111)) since 100 ? 100
           = fun(101)    since 111 > 100
           = 91        since 101 > 100
```

fun()的返回值对于所有整数参数 n 101 都是 91。这个函数被称为麦卡锡 91 函数。
如果您发现任何答案/代码不正确，或者您想分享更多关于上述主题的信息/问题，请写评论。