# 实施火焰游戏的程序

> 原文:[https://www . geesforgeks . org/program-to-implement-fires-game/](https://www.geeksforgeeks.org/program-to-implement-flames-game/)

**FLAMES** 是一款以首字母缩略词命名的热门游戏:朋友、恋人、深情、婚姻、敌人、兄弟姐妹。这个游戏不能准确预测一个人是否适合你，但是和你的朋友一起玩这个游戏会很有趣。
这个游戏有两个步骤:

*   取这两个名字。
*   删除常见字符及其各自的常见事件。
*   获取剩余字符的计数。
*   将火焰字母作为[“F”、“L”、“A”、“M”、“E”、“S”]
*   用我们得到的计数开始移除字母。
*   最后一个过程就是结果的字母。

**例:**

```
Input: Player1 = AJAY, Player2 = PRIYA
Output: Friends
```

**解释:**在上面给定的两个名字中，A 和 Y 是在两个名字中出现一次的共同字母(共同计数)，所以我们从两个名字中删除这些字母。现在数一下剩下的字母总数，是 5 个。现在开始用我们得到的计数一个接一个地从火焰中移除字母，持续这个过程的字母就是结果。
以逆时针循环的方式进行计数。

> 火焰
> 从 F 开始计数， E 在第 5 次计数，因此我们移除 E 并再次开始计数，但这次从 S 开始
> FLAMS
> M 在第 5 次计数，因此我们移除 M 并从 S 开始计数
> FLAS
> S 在第 5 次计数，因此我们移除 S 并从 f 开始计数
> FLA
> L 在第 5 次计数，因此我们移除 L 并从 A 开始计数
> FA
> A 在第 5 次计数，因此我们移除 A。现在我们只剩下一个字母，因此这是最终答案。
> F
> 所以，关系是 F 即朋友。

**进场:**需要三个计数器，两个初始化为零的名称，一个初始化为 5 的火焰。使用了三个字符串，两个用于名称，一个已经存储了 FILES。在这里，程序首先计算第一个名字中的字母数量，然后计算第二个名字中的字母数量，然后在使用 strlen 将它们存储到整数变量中之后，对每个名字运行一个 for 循环来计算公共字母。然后通过使用嵌套的 if-else，从每个名称中取消字母，用一个字符串表示。再次重复 for 循环以继续该过程。因此，计数器旋转，火焰中的每个字母都被指向。随着字母被取消，循环再次运行。然后对于每个字母，使用 If else 语句，打印对应于最后一个字母的结果。
下面是实现:

## C++

```
// C++ program to implement FLAMES game
#include <bits/stdc++.h>
using namespace std;

// Function to find out the flames result
void flame(char* a, char* b)
{
    int i, j, k, l = 1, n, m, sc = 0, tc, rc = 0, fc = 5;
    char q[25], w[25], c;
    char f[] = "flames";

    strcpy(q, a);
    strcpy(w, b);
    n = strlen(a);
    m = strlen(b);
    tc = n + m;

    for (i = 0; i < n; i++)
    {
        c = a[i];
        for (j = 0; j < m; j++)
        {
            if (c == b[j])
            {
                a[i] = -1;
                b[j] = -1;
                sc = sc + 2;
                break;
            }
        }
    }

    rc = tc - sc;

    for (i = 0;; i++)
    {
        if (l == (rc))
        {
            for (k = i; f[k] != '\0'; k++)
            {
                f[k] = f[k + 1];
            }
            f[k + 1] = '\0';
            fc = fc - 1;
            i = i - 1;
            l = 0;
        }
        if (i == fc)
        {
            i = -1;
        }
        if (fc == 0)
        {
            break;
        }
        l++;
    }

    // Print the results
    if (f[0] == 'e')
        cout << q <<" is ENEMY to " << w;
    else if (f[0] == 'f')
        cout << q <<" is FRIEND to "<<w;
    else if (f[0] == 'm')
        cout << q <<" is going to MARRY "<<w;
    else if (f[0] == 'l')
        cout << q <<" is in LOVE with "<<w;
    else if (f[0] == 'a')
        cout << q <<" has more AFFECTION on "<<w;
    else
        cout << q << " and "<< w <<" are SISTERS/BROTHERS ";
}

// Driver code
int main()
{
    char a[] = "AJAY";
    char b[] = "PRIYA";

    flame(a, b);
}

// This code is contributed by SHUBHMASINGH10
```

## C

```
// C program to implement FLAMES game

#include <stdio.h>
#include <string.h>

// Function to find out the flames result
void flame(char* a, char* b)
{
    int i, j, k, l = 1, n, m, sc = 0, tc, rc = 0, fc = 5;
    char q[25], w[25], c;
    char f[] = "flames";

    strcpy(q, a);
    strcpy(w, b);
    n = strlen(a);
    m = strlen(b);
    tc = n + m;

    for (i = 0; i < n; i++) {
        c = a[i];
        for (j = 0; j < m; j++) {
            if (c == b[j]) {
                a[i] = -1;
                b[j] = -1;
                sc = sc + 2;
                break;
            }
        }
    }

    rc = tc - sc;

    for (i = 0;; i++) {
        if (l == (rc)) {
            for (k = i; f[k] != '\0'; k++) {
                f[k] = f[k + 1];
            }
            f[k + 1] = '\0';
            fc = fc - 1;
            i = i - 1;
            l = 0;
        }
        if (i == fc) {
            i = -1;
        }
        if (fc == 0) {
            break;
        }
        l++;
    }

    // Print the results
    if (f[0] == 'e')
        printf("%s is ENEMY to %s ", q, w);
    else if (f[0] == 'f')
        printf("%s is FRIEND to %s ", q, w);
    else if (f[0] == 'm')
        printf("%s is going to MARRY %s", q, w);
    else if (f[0] == 'l')
        printf("%s is in LOVE with %s ", q, w);
    else if (f[0] == 'a')
        printf("%s has more AFFECTION on %s ", q, w);
    else
        printf("%s and %s are SISTERS/BROTHERS ", q, w);
}

// Driver code
int main()
{

    char a[] = "AJAY";
    char b[] = "PRIYA";

    flame(a, b);
}
```

## 蟒蛇 3

```
# Python3 program to implement FLAMES game

# Function to find out the flames result
def flame(a, b):
    l, sc = 1, 0
    rc, fc = 0, 5
    f = "flames"
    f = [i for i in f]
    q = "".join(a)
    w = "".join(b)

    # print(q, w)
    n = len(a)
    m = len(b)
    tc = n + m
    for i in range(n):
        c = a[i]
        for j in range(m):
            if (c == b[j]):
                a[i] = -1
                b[j] = -1
                sc = sc + 2
                break

    rc = tc - sc
    i = 0

    while (i):
        if (l == (rc)):
            for k in range(i,len(f)):
                f[k] = f[k + 1]
            f[k + 1] = '\0'
            fc = fc - 1
            i = i - 1
            l = 0
        if (i == fc):
            i = -1
        if (fc == 0):
            break
        l += 1
        i += 1

    # Print the results
    if (f[0] == 'e'):
        print(q, "is ENEMY to", w)
    elif (f[0] == 'f'):
        print(q, "is FRIEND to", w)
    elif (f[0] == 'm'):
        print(q, "is going to MARRY", w)
    elif (f[0] == 'l'):
        print(q, "is in LOVE with", w)
    elif (f[0] == 'a'):
        print(q, "has more AFFECTION on", w)
    else:
        print(q, "and", w, "are SISTERS/BROTHERS ")

# Driver code
a = "AJAY"
b = "PRIYA"
a = [i for i in a]
b = [j for j in b]

# print(a,b)
flame(a, b)

# This code is contributed by Mohit Kumar
```

## java 描述语言

```
<script>
// Javascript program to implement FLAMES game

// Function to find out the flames result
function flame(a,b)
{
    let i, j, k, l = 1, n, m, sc = 0, tc, rc = 0, fc = 5;
    let c;
    let f = "flames";

    let q = a.join("")
    let w = b.join("")
    n = a.length;
    m = b.length;
    tc = n + m;

    for (i = 0; i < n; i++)
    {
        c = a[i];
        for (j = 0; j < m; j++)
        {
            if (c == b[j])
            {
                a[i] = -1;
                b[j] = -1;
                sc = sc + 2;
                break;
            }
        }
    }

    rc = tc - sc;

    for (i = 0;; i++)
    {
        if (l == (rc))
        {
            for (k = i; k<f.length; k++)
            {
                f[k] = f[k + 1];
            }
            f[k + 1] = '\0';
            fc = fc - 1;
            i = i - 1;
            l = 0;
        }
        if (i == fc)
        {
            i = -1;
        }
        if (fc == 0)
        {
            break;
        }
        l++;
    }

    // Print the results
    if (f[0] == 'e')
        document.write(q+" is ENEMY to "+w);

    else if (f[0] == 'f')
        document.write(q+" is FRIEND to "+w);

    else if (f[0] == 'm')
        document.write(q+" is going to MARRY "+w);

    else if (f[0] == 'l')
        document.write(q+" is in LOVE with "+w);

    else if (f[0] == 'a')
        document.write(q+" has more AFFECTION on "+w);

    else
        document.write(q+" and "<+w+" are SISTERS/BROTHERS ");

}

// Driver code
let a="AJAY".split("");
let b= "PRIYA".split("");
flame(a, b);

// This code is contributed by unknown2108.
</script>
```

**Output:** 

```
AJAY is FRIEND to PRIYA
```