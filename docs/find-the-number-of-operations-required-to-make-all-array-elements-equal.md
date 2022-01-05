# 求所有数组元素相等所需的运算次数

> 原文:[https://www . geeksforgeeks . org/find-使所有数组元素相等所需的操作数/](https://www.geeksforgeeks.org/find-the-number-of-operations-required-to-make-all-array-elements-equal/)

给定一个由 **N** 个整数组成的数组，任务是找出使数组中所有元素相等所需的运算次数。在一个操作中，我们可以将相等的权重从最大元素分配给数组的其余元素。如果在执行上述操作后无法使数组元素相等，则打印-1。

**示例**:

> **输入** : arr = [1，6，1，1，1]；
> **输出** : 4
> **说明**:从 max 元素分配后 arr 变为**【2，2，2，2，2】**。
> **输入** : arr = [2，2，3]；
> **输出** : -1
> **说明**:此处 arr 分配后变为[3，3，1]。

**算法**:

*   声明临时变量来存储执行操作的次数。
*   找到给定数组的最大元素并存储其索引值。
*   检查 n 次减法后所有元素是否等于最大元素。
*   再次检查每个元素是否等于其他元素，并返回 n。

下面是上述方法的实现:

## C++

```
// C++ program to find the number
//of operations required to make
//all array elements Equal
#include<bits/stdc++.h>
using namespace std;

//Function to find maximum
//element of the given array
int find_n(int a[],int n)
{
        int j = 0, k = 0, s = 0;

        int x = *max_element(a, a + n);
        int y = *min_element(a, a + n);
        for (int i = 0; i < n; i++)
        {
            if (a[i] == x)
            {
                s = i;
                break;
            }

        }
        for (int i =0;i<n;i++)
        {
            if (a[i] != x && a[i] <= y && a[i] != 0)
            {
                a[j] += 1;
                a[s] -= 1;
                x -= 1;
                k += 1;
                j += 1;
            }
            else if (a[i] != 0)
            {
                j += 1;
            }
        }

        for (int i = 0; i < n; i++)
        {
            if (a[i] != x)
            {
                k = -1;
                break;
            }
        }
        return k;
    }

// Driver Code
int main()
{

    int a[] = {1, 6, 1, 1, 1};
    int n = sizeof(a)/sizeof(a[0]);
    cout << (find_n(a, n));

    return 0;
}

// This code contributed by princiraj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
//of operations required to make
//all array elements Equal

import java.util.Arrays;

class GFG {

//Function to find maximum
//element of the given array
    static int find_n(int[] a) {
        int j = 0, k = 0, s = 0;

        int x = Arrays.stream(a).max().getAsInt();
        int y = Arrays.stream(a).min().getAsInt();
        for (int i : a) {
            if (a[i] == x) {
                s = i;
                break;
            }

        }
        for (int i : a) {
            if (i != x && i <= y && i != 0) {
                a[j] += 1;
                a[s] -= 1;
                x -= 1;
                k += 1;
                j += 1;
            } else if (i != 0) {
                j += 1;
            }
        }

        for (int i : a) {
            if (a[i] != x) {
                k = -1;
                break;
            }
        }
        return k;
    }
//Driver Code

    public static void main(String[] args) {

        int[] a = {1, 6, 1, 1, 1};
        System.out.println(find_n(a));
    }

}
```

## 蟒蛇 3

```
# Python program to find the number
# of operations required to make
# all array elements Equal

# Function to find maximum
# element of the given array
def find_n(a):
    j, k = 0, 0

    x = max(a)
    for i in range(len(a)):
        if(a[i] == x):
            s = i
            break

    for i in a:
        if(i != x and i <= min(a) and i !='\0'):
            a[j] += 1
            a[s] -= 1
            x -= 1
            k += 1
            j += 1
        elif(i != '\0'):
            j += 1

    for i in range(len(a)):    
        if(a[i] != x):
            k = -1
        break

    return k

# Driver Code
a = [1, 6, 1, 1, 1]
print (find_n(a))
```

## C#

```
// C# program to find the number
// of operations required to make
// all array elements Equal
using System;
using System.Linq;

class GFG
{

// Function to find maximum
// element of the given array
static int find_n(int []a)
{
    int j = 0, k = 0, s = 0;

    int x = a.Max();
    int y = a.Min();
    foreach(int i in a)
    {
        if (a[i] == x)
        {
            s = i;
            break;
        }

    }

    foreach (int i in a)
    {
        if (i != x && i <= y && i != 0)
        {
            a[j] += 1;
            a[s] -= 1;
            x -= 1;
            k += 1;
            j += 1;
        }

        else if (i != 0)
        {
            j += 1;
        }
    }

    foreach (int i in a)
    {
        if (a[i] != x)
        {
            k = -1;
            break;
        }
    }
    return k;
}

// Driver Code
public static void Main()
{
    int[] a = {1, 6, 1, 1, 1};
    Console.Write(find_n(a));
}
}

// This code contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of
// operations required to make all
// array elements Equal

// Function to find maximum element of
// the given array
function find_n(&$a)
{
    $j = 0;
    $k = 0;

    $x = max($a);
    for ($i = 0; $i < sizeof($a); $i++)
    {
        if($a[$i] == $x)
        {
            $s = $i;
            break;
        }
    }

    for($i = 0; $i < sizeof($a); $i++)
    {
        if($a[$i] != $x and $a[$i] <= min($a) and
                            $a[$i] !=0)
        {
            $a[$j] += 1;
            $a[$s] -= 1;
            $x -= 1;
            $k += 1;
            $j += 1;
        }
        else if($a[$i] != 0)
            $j += 1;
    }   

    for($i = 0; $i < sizeof($a); $i++)
    {
        if($a[$i] != $x)
        {
            $k = -1;
            break;
        }
    }
    return $k;
}

// Driver Code
$a = array(1, 6, 1, 1, 1);
echo(find_n($a));

// This code is contributed by
// Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// javascript program to find the number
//of operations required to make
//all array elements Equal

//Function to find maximum
//element of the given array
function find_n(a) {
    var j = 0, k = 0, s = 0;

    var x = Math.max.apply(Math, a);
    var y = Math.min.apply(Math, a);
    for (var i = 0; i < n; i++)
        {
            if (a[i] == x)
            {
                s = i;
                break;
            }

        }
        for (var i =0;i<n;i++)
        {
            if (a[i] != x && a[i] <= y && a[i] != 0)
            {
                a[j] += 1;
                a[s] -= 1;
                x -= 1;
                k += 1;
                j += 1;
            }
            else if (a[i] != 0)
            {
                j += 1;
            }
        }

        for (var i = 0; i < n; i++)
        {
            if (a[i] != x)
            {
                k = -1;
                break;
            }
        }
        return k;
}
//Driver Code
var a = [1, 6, 1, 1, 1];
var n = a.length;
document.write(find_n(a,n));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
4
```

**时间复杂度** : O(n)