# 时间复杂度的其他问题

> 原文:[https://www . geesforgeks . org/杂项-时间复杂性问题/](https://www.geeksforgeeks.org/miscellaneous-problems-of-time-complexity/)

**先决条件:** [渐近符号](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)

**时间复杂度:**
时间复杂度是算法所需的时间，表示为问题大小的函数。也可以定义为运行一个程序到完成所需的计算机时间。当我们解决一个时间复杂度的问题时，这个定义帮助最大–
“它是算法相对于输入大小完成任务的操作数。”

以下是一些时间复杂性的杂七杂八的问题，在不同类型的测验中经常被问到。

**1。以下代码的时间复杂度是多少–**

## C

```
void function(int n)
{
    int i = 1, s = 1;
    while (s < n) {
        s = s + i;
        i++;
    }
}
```

**解–**
时间复杂度= O(√n)。

**解释–**
我们可以根据关系 S <sub>i</sub> = S <sub>i-1</sub> + i 来定义‘S’术语，让 *k* 为程序的迭代总次数

<figure class="table">

| **i** | **S** |
| one | one |
| Two | Two |
| three | 2 + 2 |
| four | 2 + 2 + 3 |
| … | … |
| k | 2 + 2 + 3 + 4 + ……+ k |

当 S **> =** n 时，则循环将停止在 k <sup>第</sup>次迭代，
S>= n S = n
2+2+3+4+……+k = n
1+(k *(k+1))/2 = n
k<sup>2</sup>= n
k =√n
因此，时间复杂度为 O(√n)。

**2。以下代码的时间复杂度是多少:**

## C++

```
void fun(int n)
{
    if (n < 5)
        cout << "GeeksforGeeks";
    else {
        for (int i = 0; i < n; i++) {
            cout << i << " ";
        }
    }
}
```

**解–**
时间复杂度=最佳情况下为 O(1)，最差情况下为 O(n)。

**解释–**
这个程序包含 if 和 else 条件。因此，时间复杂性有两种可能性。如果 n 的值小于 5，那么我们只得到 *<u>GeeksforGeeks</u>* 作为输出，其时间复杂度为 O(1)。
但是，如果 n > =5，则 for 循环将执行，时间复杂度变为 O(n)，这被认为是最坏的情况，因为它需要更多的时间。

**3。以下代码的时间复杂度是多少:**

## C++

```
void fun(int a, int b)
{
    while (a != b) {
        if (a > b)
            a = a - b;
        else
            b = b - a;
    }
}
```

**解–**
时间复杂度=最佳情况下 O(1)，最差情况下 O(max(a，b))。

**解释–**
如果 a 和 b 的值相同，则不会执行 while 循环。因此，时间复杂度将为 0(1)。
但是如果一个！=b，则将执行 while 循环。设 a=16，b = 5；

<figure class="table">

| **迭代次数** | **一** | **b** |
| one | Sixteen | five |
| Two | 16-5=11 | five |
| three | 11-5=6 | five |
| four | 6-5=1 | five |
| five | one | 5-1=4 |
| six | one | 4-1=3 |
| seven | one | 3-1=2 |
| eight | one | 2-1=1 |

对于这种情况，while 循环执行了 8 次(a/2 16/2 8)。
如果 a=5，b=16，那么循环也将执行 8 次。所以我们可以说时间复杂度是 O(max(a/2，b/2))**O(max(a，b)) **，因为耗时比较多，所以被认为是最坏的情况。****

****4。以下代码的时间复杂度是多少:****

## **C++**

```
void fun(int n)
{
  for(int i=0;i*i<n;i++)
    cout<<"GeeksforGeeks";
}
```

****解–**
时间复杂度= O(√n)。**

****解释–**
让 **k** 成为循环的迭代次数。**

<figure class="table">

| **i** | **i*i** |
| one | one |
| Two | 2 <sup>2</sup> |
| three | 3 <sup>2</sup> |
| four | 4 <sup>2</sup> |
| … | … |
| k | k <sup>2</sup> |

****当 i * i > =n 即 I * I = n
**I * I = n k<sup>2</sup>= n
**k =√n
时循环停止，因此时间复杂度为 O(√n)。********

********5。以下代码的时间复杂度是多少:********

## ****C++****

```
**void fun(int n, int x)
{
    for (int i = 1; i < n; i = i * x) //or for(int i = n; i >=1; i = i / x)
        cout << "GeeksforGeeks;
}**
```

******解–**
时间复杂度= O(log <sub>x</sub> n)。****

******解释–**
让 **k** 成为循环的迭代次数。****

<figure class="table">

| **itr 数量** | **i=i*x** |
| one | 1*x=x |
| Two | x*x=x <sup>2</sup> |
| three | x <sup>2</sup> *x=x <sup>3</sup> |
| … | … |
| k | x <sup>k-1</sup> *x= x <sup>k</sup> |

</figure>

******当 I>= n x<sup>k</sup>= n
x<sup>k</sup>= n(两边取对数)
k =对数 <sub>x</sub> n
时循环将停止因此，时间复杂度为 O(对数 <sub>x</sub> n)。******

********6。以下代码的时间复杂度是多少:********

## ****C++****

```
**void fun(int n)
{
    for (int i = 0; i < n / 2; i++)
        for (int j = 1; j + n / 2 <= n; j++)
            for (int k = 1; k <= n; k = k * 2)
                cout << "GeeksforGeeks";
}**
```

******解–**
时间复杂度= O(n <sup>2</sup> log <sub>2</sub> n)。****

******解释–**
1<sup>ST</sup>的时间复杂度为 loop = O(n/2)O(n)。
循环的 2 <sup>和</sup>的时间复杂度= 0(n/2)0(n)。
循环= 0 的 3 <sup>rd</sup> 的时间复杂度(log <sub>2</sub> n)。(参考问题编号–5)
因此，函数的时间复杂度将变为 O(n <sup>2</sup> log <sub>2</sub> n)。****

******7。以下代码的时间复杂度是多少:******

## ****C++****

```
**void fun(int n)
{
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j = j + i)
            cout << "GeeksforGeeks";
}**
```

******解–**时间复杂度= O(nlogn)。****

******解释–**
循环 1 的时间复杂度= 0(n)。2 <sup>nd</sup> 循环对 i.
的每个值执行 n/i 次，其时间复杂度为 O(≘<sup>n</sup>T8】I = 1n/I)O(logn)。
因此，函数的时间复杂度= 0(nlogn)。****

******8。以下代码的时间复杂度是多少:******

## ****C++****

```
**void fun(int n)
{
    for (int i = 0; i <= n / 3; i++)
        for (int j = 1; j <= n; j = j + 4)
            cout << "GeeksforGeeks";
}**
```

******解–**时间复杂度= O(n <sup>2</sup> )。****

******解释–**
第一个 for 循环的时间复杂度= O(n/3)O(n)。
第二个 for 循环的时间复杂度= O(n/4)O(n)。
因此，函数的时间复杂度将变为 O(n <sup>2</sup> ) **。******

******9。以下代码的时间复杂度是多少:******

## ****C++****

```
**void fun(int n)
{
    int i = 1;
    while (i < n) {
        int j = n;
        while (j > 0) {
            j = j / 2;
        }
        i = i * 2;
    }
}**
```

******解–**时间复杂度= 0(对数 <sup>2</sup> n)。****

******解释–**
在每次迭代中，我变成两次(T.C=O(logn))，j 变成一半(T.C=O(logn))。所以，时间复杂度会变成 O(log <sup>2</sup> n)。
我们可以把这个 while 循环转换成 for 循环。
为(int I = 1；I<n；i = i * 2)
为(int j = n；j>0；j = j / 2)。****

****以上对于循环的时间复杂度也是 O(log <sup>2</sup> n)。****

******10。考虑下面的 C 代码，** **在循环的执行中进行了多少次比较？******

## ****C++****

```
**void fun(int n)
{
    int j = 1;
    while (j <= n) {
        j = j * 2;
    }
}**
```

******解决方案–**T2】天花板(原木 <sub>2</sub> n)+1。****

******解释–**
让 **k** 成为循环的迭代次数。第 kth 步后，j 的值为 2 <sup>k</sup> 。因此，k=log <sub>2</sub> n，这里我们用 log <sub>2</sub> n 的 *ceil，因为 log <sub>2</sub> n 可能是小数。因为我们要为退出循环再做一次比较。
那么，答案是 ceil(log <sub>2</sub> n)+1。*****

</figure>

</figure>

</figure>