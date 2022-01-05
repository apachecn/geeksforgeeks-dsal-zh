# 递归练习题|第 6 集

> 原文:[https://www . geesforgeks . org/practice-questions-for-recursion-set-6/](https://www.geeksforgeeks.org/practice-questions-for-recursion-set-6/)

**问题 1**
考虑以下递归 C 函数。让 *len* 为字符串 s 的长度， *num* 为屏幕上打印的字符数。给出*号*和*号*之间的关系，其中*号*总是大于 0。

## C++

```
void abc(char *s)
{
    if(s[0] == '\0')
        return;

    abc(s + 1);
    abc(s + 1);
    cout << s[0];   
}

// This code is contributed by shubhamsingh10
```

## C

```
void abc(char *s)
{
    if(s[0] == '\0')
        return;

    abc(s + 1);
    abc(s + 1);
    printf("%c", s[0]);   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static void abc(char *s)
{
    if(s[0] == '\0')
        return;

    abc(s + 1);
    abc(s + 1);
    System.out.print(s[0]);   
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
def abc(s):
    if(len(s) == 0):
        return

    abc(s[1:])
    abc(s[1:])
    print(s[0])

# This code is contributed by shubhamsingh10
```

## C#

```
static void abc(char *s)
{
    if(s[0] == '\0')
        return;

    abc(s + 1);
    abc(s + 1);
    Console.Write(s[0]);
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
//Javascript Implementation
function abc(s)
{
    if(s.length == 0)
        return;

    abc(s.substring(1));
    abc(s.substring(1));
    document.write(s[0]);   
}

// This code is contributed by shubhamsingh10
</script>
```

以下是 *num* 和 *len* 的关系。

```
 num = 2^len-1
```

```
s[0] is 1 time printed
s[1] is 2 times printed
s[2] is 4 times printed
s[i] is printed 2^i times
s[strlen(s)-1] is printed 2^(strlen(s)-1) times
total = 1+2+....+2^(strlen(s)-1)
      = (2^strlen(s)) - 1
```

例如，以下程序打印 7 个字符。

## C++

```
#include <bits/stdc++.h>
using namespace std;

void abc(char s[])
{
    if(s[0] == '\0')
        return;

    abc(s + 1);
    abc(s + 1);
    cout << s[0];
}

int main()
{
    abc("xyz");
    return 0;
}
//This code is contributed by shubhamsingh10
```

## C

```
#include<stdio.h>

void abc(char *s)
{
    if(s[0] == '\0')
        return;

    abc(s + 1);
    abc(s + 1);
    printf("%c", s[0]);
}

int main()
{
    abc("xyz");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class GFG
{
    static void abc(String s)
    {
        if(s.length() == 0)
            return;

        abc(s.substring(1));
        abc(s.substring(1));
        System.out.print(s.charAt(0));
    }

    public static void main(String[] args) {
        abc("xyz");
    }
}

// This code is contributed by divyeh072019
```

## 蟒蛇 3

```
def abc(s):
    if(len(s) == 0):
        return

    abc(s[1:])
    abc(s[1:])
    print(s[0],end="")

# Driver code

abc("xyz")

# This code is contributed by shubhamsingh10
```

## C#

```
using System;
class GFG {

    static void abc(string s)
    {
        if(s.Length == 0)
            return;

        abc(s.Substring(1));
        abc(s.Substring(1));
        Console.Write(s[0]);
    }

  // Driver code
  static void Main() {
    abc("xyz");
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation

function abc(s)
{
    if(s.length == 0)
        return;

    abc(s.substring(1));
    abc(s.substring(1));
    document.write(s[0]);
}

abc("xyz");

//This code is contributed by shubhamsingh10
</script>
```

感谢巴拉特·纳格提出这个解决方案。

**问题 2**

## C++

```
#include <iostream>
using namespace std;

int fun(int count)
{
    cout << count << endl;
    if(count < 3)
    {
        fun(fun(fun(++count)));
    }
    return count;
}

int main()
{
    fun(1);
    return 0;
}

// This code is contributed by Shubhamsingh10
```

## C

```
#include<stdio.h>
int fun(int count)
{
    printf("%d\n", count);
    if(count < 3)
    {
      fun(fun(fun(++count)));
    }
    return count;
}

int main()
{
    fun(1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{
static int fun(int count)
{
    System.out.println(count);
    if(count < 3)
    {
        fun(fun(fun(++count)));
    }
    return count;
}

public static void main(String[] args)
{
    fun(1);
}
}

// This code is contributed by Shubhamsingh10
```

## 蟒蛇 3

```
def fun(count):
    print(count)
    if(count < 3):
        count+=1
        fun(fun(fun(count)))

    return count

if __name__=="__main__": 

    fun(1)

# This code is contributed by Shubhamsingh10
```

## C#

```
using System;

class GFG{

    static int fun(int count) 
    { 
        Console.Write(count+"\n"); 
        if(count < 3) 
        { 
            fun(fun(fun(++count))); 
        } 
        return count; 
    } 

    static public void Main ()
    { 
        fun(1);  
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

    function fun(count)
    {
        document.write(count + "</br>");
        if(count < 3)
        {
            fun(fun(fun(++count)));
        }
        return count;
    }

    fun(1);

</script>
```

**输出:**

```
 1
 2
 3
 3
 3
 3
 3
```

main()函数调用 fun(1)。fun(1)打印“1”并调用 fun(fun(2))。fun(2)打印“2”并调用 fun(fun(3))。所以函数调用序列变得有趣(有趣(fun)(fun(fun(3))))。fun(3)打印“3”并返回 3(请注意，计数不会增加，也不会调用更多的函数，就好像计数 3 的条件不成立一样)。所以函数调用序列简化为 fun(fun(fun(3)))。fun(3)再次打印“3”并返回 3。所以函数调用再次减少为乐趣(fun(fun(3))，它再次打印“3”并将其减少为乐趣(fun(3))。这样继续下去，我们在屏幕上打印了 5 次“3”。

如果您发现任何答案/代码不正确，或者您想分享关于上述主题的更多信息/问题，请写评论。