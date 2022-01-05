# 递归练习题|第 3 集

> 原文:[https://www . geesforgeks . org/practice-questions-for-recursion-set-3/](https://www.geeksforgeeks.org/practice-questions-for-recursion-set-3/)

解释下面递归函数的功能。

**问题 1**

## C++

```
void fun1(int n)
{
   int i = 0;  
   if (n > 1)
     fun1(n - 1);
   for (i = 0; i < n; i++)
     cout << " * ";
}

// This code is contributed by shubhamsingh10
```

## C

```
void fun1(int n)
{
   int i = 0; 
   if (n > 1)
     fun1(n-1);
   for (i = 0; i < n; i++)
     printf(" * ");
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static void fun1(int n)
{
   int i = 0;  
   if (n > 1)
     fun1(n - 1);
   for (i = 0; i < n; i++)
     System.out.print(" * ");
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
def  fun1(n):
    i = 0
    if (n > 1):
        fun1(n - 1)
    for i in range(n):
        print(" * ",end="")

# This code is contributed by shubhamsingh10
```

## C#

```
static void fun1(int n)
{
    int i = 0;
    if (n > 1)
        fun1(n-1);
    for (i = 0; i < n; i++)
        Console.Write(" * ");
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

function fun1(n)
{
    let i = 0;  

    if (n > 1)
        fun1(n - 1);

    for(i = 0; i < n; i++)
        document.write(" * ");
}

// This code is contributed by gottumukkalabobby

</script>
```

答:打印的星星总数等于 1 + 2 + …。(n-2) + (n-1) + n，即 n(n+1)/2。

**问题 2**

## C++

```
#define LIMIT 1000
void fun2(int n)
{
  if (n <= 0)
     return;
  if (n > LIMIT)
    return;
  cout << n <<" ";
  fun2(2*n);
  cout << n <<" ";
}

// This code is contributed by shubhamsingh10
```

## C

```
#define LIMIT 1000
void fun2(int n)
{
  if (n <= 0)
     return;
  if (n > LIMIT)
    return;
  printf("%d ", n);
  fun2(2*n);
  printf("%d ", n);
}  
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
int LIMIT = 1000;
void fun2(int n)
{
    if (n <= 0) return;
    if (n > LIMIT) return;

    System.out.print(String.format("%d ", n));
    fun2(2 * n);
    System.out.print(String.format("%d ", n));
}
```

## 蟒蛇 3

```
LIMIT = 1000
def fun2(n):
    if (n <= 0):
        return
    if (n > LIMIT):
        return
    print(n, end=" ")
    fun2(2 * n)
    print(n, end=" ")

# This code is contributed by shubhamsingh10
```

## C#

```
int LIMIT = 1000
void fun2(int n)
{
    if (n <= 0)
        return;
    if (n > LIMIT)
        return;
    Console.Write(n+" ");
    fun2(2*n);
    Console.Write(n+" ");
}

// This code is contributed by Shubhamsingh10
```

## java 描述语言

```
<script>

let LIMIT = 1000;
function fun2(n)
{
    if (n <= 0)
        return;
    if (n > LIMIT)
        return;

    document.write(n + " "));
    fun2(2 * n);
    document.write(n + " "));
}

// This code is contributed by gottumukkalabobby

</script>
```

答:对于正 n，fun2(n)打印 n，2n，4n，8n …的值，而该值小于 LIMIT。以递增顺序打印数值后，它会以相反的顺序再次打印相同的数字。例如，fun2(100)打印 100，200，400，800，800，400，200，100。
如果 n 为负，则立即返回函数。
如果您发现任何答案/代码不正确，或者您想分享更多关于上述主题的信息，请写评论。