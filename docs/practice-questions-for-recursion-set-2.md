# 递归练习题|第 2 集

> 原文:[https://www . geesforgeks . org/practice-questions-for-recursion-set-2/](https://www.geeksforgeeks.org/practice-questions-for-recursion-set-2/)

解释以下功能的功能。

**问题 1**

## C

```
/* Assume that n is greater than or equal to 1 */
int fun1(int n)
{
    if (n == 1)
        return 0;
    else
        return 1 + fun1(n / 2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Assume that n is greater than or equal to 1 */
static int fun1(int n)
{
    if (n == 1)
        return 0;
    else
        return 1 + fun1(n / 2);
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Assume that n is greater than or equal to 1 */
def fun1(n):
    if(n == 1):
        return 0
    else:
        return 1 + fun1(n//2)

# This code is contributed by shubhamsingh10
```

## C#

```
/* Assume that n is greater than or equal to 1 */
static int fun1(int n)
{
    if (n == 1)
        return 0;
    else
        return 1 + fun1(n / 2);
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

/* Assume that n is greater than or equal to 1 */
function fun1(n)
{
    if (n == 1)
        return 0
    else
        return 1 + fun1(n / 2)
}

// This code is contributed by gottumukkalabobby

</script>
```

## C++

```
/* Assume that n is greater than or equal to 1 */
int fun1(int n)
{
    if (n == 1)
        return 0;
    else
        return 1 + fun1(n / 2);
}

// This code is contributed by shubhamsingh10
// Improved by Adwitiya Mourya
```

回答:函数计算并返回

![log2floor](img/df370890d8deebcf04c7ecac155b8f85.png)

。例如，如果 n 在 8 和 15 之间，那么 fun1()返回 3。如果 n 在 16 到 31 之间，则 fun1()返回 4。
**问题 2**

## C++

```
/* Assume that n is greater than or equal to 0 */
void fun2(int n)
{
if(n == 0)
    return;

fun2(n/2);
cout << n%2 << endl;
}

//This code is contributed by shubhamsingh10
```

## C

```
/* Assume that n is greater than or equal to 0 */
void fun2(int n)
{
  if(n == 0)
    return;

  fun2(n/2);
  printf("%d", n%2);
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Assume that n is greater than or equal to 1 */
static void fun2(int n)
{
if(n == 0)
    return;

fun2(n/2);
System.out.println(n%2);
}

// This code is contributed by Shubhamsingh10
```

## 蟒蛇 3

```
# Assume that n is greater than or equal to 0 */
def fun2(n):
    if(n == 0):
        return

    fun2(n / 2)
    print(n % 2, end="")

# This code is contributed by shubhamsingh10
```

## C#

```
void fun2(int n)
{
if(n == 0)
    return;

fun2(n/2);
Console.Write(n%2);
}
// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// Assume that n is greater than or equal to 1
function fun2(n)
{
    if (n == 0)
        return;

    fun2(n / 2);
    document.write(n % 2 + " ")
}

// This code is contributed by gottumukkalabobby

</script>
```

回答:fun2()函数打印 n 的二进制等价物。例如，如果 n 是 21，那么 fun2()打印 10101。
注意，上面的函数只是用来练习递归的，它们并不是它们提供的功能的理想实现。
如发现任何答案/代码不正确，请写评论。