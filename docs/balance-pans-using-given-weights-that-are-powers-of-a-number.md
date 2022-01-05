# 使用给定重量的天平盘，该重量是数字的幂

> 原文:[https://www . geeksforgeeks . org/天平盘-使用给定重量的数字幂/](https://www.geeksforgeeks.org/balance-pans-using-given-weights-that-are-powers-of-a-number/)

给定一个带有两个平底锅的简单称重秤，我们得到一个重量 T 和一些其他重量，它们是特定数字 a 的幂，我们的目标是使用给定的重量平衡这些平底锅。更正式地说，我们需要满足这个方程，
T+(a 的某些幂)=(a 的某些其他幂)
记住，我们正好被赋予一个对应于一个幂的权重。
**例:**

```
T = 11    and  a = 4
Then scale can be balanced as,        
11 + 4 + 1 = 16
```

我们可以看到，在这个问题中，我们的第一个目标是用 a 的幂来表示 T，所以当我们用 a 的底写 T 时，如果表示只有 1 和 0，那么我们知道对应于 1 的权重可以使 T，例如

```
If T is 10 and a is 3 then representing 10 on 
base of 3 we get 101 i.e. using 0th power of 3 
and 2nd power of 3 (1 + 9)  we can get 10
```

现在，如果基本表示的所有数字都不是 1 或 0，那么我们就不能平衡标度，除了在基本表示中某个数字是(a–1)的情况，因为在这种情况下，我们可以将相应的幂转移到 T 的一边，并将基本表示中的左数增加 1。例如

```
If T is 7 and a is 3 then representing 7 on base 
3 we get 021.
Now while looping over representation from right 
to left we get 2 (which is 3 - 1), in this case, 
we can transfer corresponding power(3^1) to T’s 
side and increase the left number by 1 i.e.,
T’s side 7 + 3 = 10    and representation 101 (9 + 1)    
which has only 1s and 0s now, so scale can be balanced.
```

所以现在解决这个问题的算法可以表示如下，表示以 a 为基数的 T，如果基数表示的所有数字都是 1 或 0，则标度可以平衡，否则从表示的右侧循环如果任何数字是(a–1)，那么将左侧的数字增加 1，继续这样做，忽略表示中的 1，0，(a–1)和 a 的情况。如果处理完整的基本表示，则比例可以平衡，否则不能平衡。

## C++

```
// C++ code to check whether scale can be balanced or not
#include <bits/stdc++.h>
using namespace std;

// method returns true if balancing of scale is possible
bool isBalancePossible(int T, int a)
{
    // baseForm vector will store T's representation on
    // base a in reverse order
    vector<int> baseForm;

    // convert T to representation on base a
    while (T) {
        baseForm.push_back(T % a);
        T /= a;
    }

    // make first digit of representation as 0
    baseForm.push_back(0);

    // loop over base representation of T
    for (int i = 0; i < baseForm.size(); i++) {

        // if any digit is not 0, 1, (a - 1) or a
        // then balancing is not possible
        if (baseForm[i] != 0 && baseForm[i] != 1 &&
            baseForm[i] != (a - 1) && baseForm[i] != a)
            return false;       

        // if digit is a or (a - 1) then increase left
        // index's count/ (case, when this weight is
        // transferred to T's side)
        if (baseForm[i] == a || baseForm[i] == (a - 1))
            baseForm[i + 1] += 1;       
    }

    // if representation is processed then balancing
    // is possible
    return true;
}

// Driver code to test above methods
int main()
{
    int T = 11;
    int a = 4;

    bool balancePossible = isBalancePossible(T, a);
    if (balancePossible)
        cout << "Balance is possible" << endl;
    else
        cout << "Balance is not possible" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check whether
// scale can be balanced or not
import java.util.*;

class GFG
{

    // method returns true if balancing
    // of scale is possible
    static boolean isBalancePossible(int T, int a)
    {
        // baseForm vector will store T's
        // representation on base a
        // in reverse order
        Vector<Integer> baseForm = new Vector<>();
        int s = 0;

        // convert T to representation on base a
        while (T > 0)
        {
            baseForm.add(T % a);
            T /= a;
            s++;
        }

        // make first digit of representation as 0
        baseForm.add(0);

        // loop over base representation of T
        for (int i = 0; i < s; i++)
        {
            // if any digit is not 0, 1, (a - 1) or a
            // then balancing is not possible
            if (baseForm.get(i) != 0 &&
                baseForm.get(i) != 1 &&
                baseForm.get(i) != (a - 1) &&
                baseForm.get(i) != a)
            {
                return false;
            }

            // if digit is a or (a - 1) then increase left
            // index's count/ (case, when this weight is
            // transferred to T's side)
            if (baseForm.get(i) == a || baseForm.get(i) == (a - 1))
            {
                baseForm.add(i + 1, baseForm.get(i + 1) + 1);
            }
        }

        // if representation is processed 
        // then balancing is possible
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int T = 11;
        int a = 4;

        boolean balancePossible = isBalancePossible(T, a);
        if (balancePossible)
        {
            System.out.println("Balance is possible");
        }
        else
        {
            System.out.println("Balance is not possible");
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## C#

```
// C# code to check whether
// scale can be balanced or not
using System;
using System.Collections.Generic;

class GFG
{

    // method returns true if balancing
    // of scale is possible
    static bool isBalancePossible(int T, int a)
    {
        // baseForm vector will store T's
        // representation on base a
        // in reverse order
        List<int> baseForm = new List<int>();
        int s = 0;

        // convert T to representation on base a
        while (T > 0)
        {
            baseForm.Add(T % a);
            T /= a;
            s++;
        }

        // make first digit of representation as 0
        baseForm.Add(0);

        // loop over base representation of T
        for (int i = 0; i < s; i++)
        {
            // if any digit is not 0, 1, (a - 1) or a
            // then balancing is not possible
            if (baseForm[i] != 0 &&
                baseForm[i] != 1 &&
                baseForm[i] != (a - 1) &&
                baseForm[i] != a)
            {
                return false;
            }

            // if digit is a or (a - 1) then increase left
            // index's count/ (case, when this weight is
            // transferred to T's side)
            if (baseForm[i] == a || baseForm[i] == (a - 1))
            {
                baseForm.Insert(i + 1, baseForm[i+1] + 1);
            }
        }

        // if representation is processed
        // then balancing is possible
        return true;
    }

    // Driver code
    public static void Main()
    {
        int T = 11;
        int a = 4;

        bool balancePossible = isBalancePossible(T, a);
        if (balancePossible)
        {
            Console.WriteLine("Balance is possible");
        }
        else
        {
            Console.WriteLine("Balance is not possible");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check whether scale
// can be balanced or not

// method returns true if balancing
// of scale is possible
function isBalancePossible($T, $a)
{
    // baseForm vector will store T's
    // representation on base a in reverse order
    $baseForm = array();

    // convert T to representation on base a
    while ($T)
    {
        array_push($baseForm, $T % $a);
        $T = (int)($T / $a);
    }

    // make first digit of representation as 0
    array_push($baseForm, 0);

    // loop over base representation of T
    for ($i = 0; $i < count($baseForm); $i++)
    {

        // if any digit is not 0, 1, (a - 1) or a
        // then balancing is not possible
        if ($baseForm[$i] != 0 && $baseForm[$i] != 1 &&
            $baseForm[$i] != ($a - 1) && $baseForm[$i] != $a)
            return false;

        // if digit is a or (a - 1) then increase left
        // index's count/ (case, when this weight is
        // transferred to T's side)
        if ($baseForm[$i] == $a ||
            $baseForm[$i] == ($a - 1))
            $baseForm[$i + 1] += 1;
    }

    // if representation is processed then
    // balancing is possible
    return true;
}

// Driver Code
$T = 11;
$a = 4;

$balancePossible = isBalancePossible($T, $a);
if ($balancePossible)
    echo "Balance is possible\n";
else
    echo "Balance is not possible\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript code to check whether
// scale can be balanced or not

// method returns true if balancing
    // of scale is possible
function isBalancePossible(T,a)
{

    // baseForm vector will store T's
        // representation on base a
        // in reverse order
        let baseForm = [];
        let s = 0;

        // convert T to representation on base a
        while (T > 0)
        {
            baseForm.push(T % a);
            T = Math.floor(T/a);
            s++;
        }

        // make first digit of representation as 0
        baseForm.push(0);

        // loop over base representation of T
        for (let i = 0; i < s; i++)
        {

            // if any digit is not 0, 1, (a - 1) or a
            // then balancing is not possible
            if (baseForm[i] != 0 &&
                baseForm[i] != 1 &&
                baseForm[i] != (a - 1) &&
                baseForm[i] != a)
            {
                return false;
            }

            // if digit is a or (a - 1) then increase left
            // index's count/ (case, when this weight is
            // transferred to T's side)
            if (baseForm[i] == a || baseForm[i] == (a - 1))
            {
                baseForm.splice(i + 1,0, baseForm[i+1] + 1);
            }
        }

        // if representation is processed
        // then balancing is possible
        return true;
}

// Driver code
let T = 11;
let a = 4;

let balancePossible = isBalancePossible(T, a);
if (balancePossible)
{
    document.write("Balance is possible");
}
else
{
    document.write("Balance is not possible");
}

// This code is contributed by rag2127
</script>
```

**输出:**

```
Balance is possible
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。