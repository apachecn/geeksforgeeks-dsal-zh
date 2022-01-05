# 检查在给定方向移动后是否有可能回到起始位置

> 原文:[https://www . geesforgeks . org/check-如果有可能的话-在给定的方向上移动后返回到起始位置/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-return-to-the-starting-position-after-moving-in-the-given-directions/)

给定一个人行进的 N 个方向的弦。任务是检查他/她是否能够回到他/她开始的地方。在第一天(1 <= i <= N), he will travel a positive distance in the following direction:

> 如果字符串的第一个字母是 N
> 则为北，如果字符串的第一个字母是 W
> 则为西，如果字符串的第一个字母是 S
> 则为南，如果字符串的第一个字母是 E，则为东

如果他能在第 n 天后回到他出发的地方，打印“是”，否则打印“否”。
**例:**

> **输入:** str = "NNNWEWESSS"
> **输出:** YES
> 第 1、2、3 天他向北走，第 4 天他向西走，然后最终
> 回到第 5 天第 3 天他站的地方，然后第 6 天他再次向西走
> 。第七天他又回到了第五天他站的地方。在第 10 天，他安全回家。
> **输入:** str = "NW"
> **输出:**否

**方法:**必须有相同数量的 N 和相同数量的 S，也必须有相同数量的 E 和相同数量的 w。所以，计算给出的每种类型的方向，并检查它们是否相等。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of above approach
#include<bits/stdc++.h>
using namespace std;

int main()
    {
        string st = "NNNWEWESSS" ;
        int len = st.length();

        int n = 0 ; // Count of North
        int s = 0 ; // Count of South
        int e = 0 ; // Count of East
        int w = 0 ; // Count of West

        for (int i = 0; i < len ; i++ )
        {
            if(st[i]=='N')
                n += 1;
            if(st[i] == 'S')
                s += 1;
            if(st[i] == 'W')
                w+= 1 ;
            if(st[i] == 'E')
                e+= 1 ;
        }

        if(n == s && w == e)
            cout<<("YES")<<endl;
        else
            cout<<("NO")<<endl;

    }
 // This code is contributed by
 // Sahil_Shelangia
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

public class GFG {

    public static void main(String args[])
    {
                String st = "NNNWEWESSS" ;
                int len = st.length();

                int n = 0 ; // Count of North
                int s = 0 ; // Count of South
                int e = 0 ; // Count of East
                int w = 0 ; // Count of West

                for (int i = 0; i < len ; i++ )
                {
                    if(st.charAt(i)=='N')
                        n+= 1 ;
                    if(st.charAt(i) == 'S')
                        s+= 1 ;
                    if(st.charAt(i) == 'W')
                        w+= 1 ;
                    if(st.charAt(i) == 'E')
                        e+= 1 ;
                }
                if(n == s && w == e)
                    System.out.println("YES");
                else
                    System.out.println("NO") ;

    }
    // This Code is contributed by ANKITRAI1
}
```

## 计算机编程语言

```
# Python implementation of above approach

st = "NNNWEWESSS"
length = len(st)
n = 0 # Count of North
s = 0 # Count of South
e = 0 # Count of East
w = 0 # Count of West
for i in range(length):
    if(st[i]=="N"):
        n+= 1
    if(st[i]=="S"):
        s+= 1
    if(st[i]=="W"):
        w+= 1
    if(st[i]=="E"):
        e+= 1
if(n == s and w == e):
    print("YES")
else:
    print("NO")
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    // Main Method
    public static void Main()
    {

        string st = "NNNWEWESSS" ;
        int len = st.Length;

        int n = 0 ; // Count of North
        int s = 0 ; // Count of South
        int e = 0 ; // Count of East
        int w = 0 ; // Count of West

        for (int i = 0; i < len ; i++ )
        {
            if(st[i]=='N')
                n += 1 ;
            if(st[i] == 'S')
                s += 1 ;
            if(st[i] == 'W')
                w += 1 ;
            if(st[i] == 'E')
                e += 1 ;
        }

        if(n == s && w == e)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO") ;

    }

}

// This code is contributed by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
$st = "NNNWEWESSS";
$len = strlen($st);

$n = 0; // Count of North
$s = 0; // Count of South
$e = 0; // Count of East
$w = 0; // Count of West

for ($i = 0; $i < $len; $i++ )
{
    if($st[$i] == 'N')
        $n += 1;
    if($st[$i] == 'S')
        $s += 1;
    if($st[$i] == 'W')
        $w += 1 ;
    if($st[$i] == 'E')
        $e += 1;
}

if($n == $s && $w == $e)
    echo "YES\n";
else
    echo "NO\n";

// This code is contributed by
// Rajput-Ji
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// driver code

     let st = "NNNWEWESSS" ;
        let len = st.length;

        let n = 0 ; // Count of North
        let s = 0 ; // Count of South
        let e = 0 ; // Count of East
        let w = 0 ; // Count of West

        for (let i = 0; i < len ; i++ )
        {
            if(st[i]=='N')
                n += 1 ;
            if(st[i] == 'S')
                s += 1 ;
            if(st[i] == 'W')
                w += 1 ;
            if(st[i] == 'E')
                e += 1 ;
        }

        if(n == s && w == e)
           document.write("YES");
        else
            document.write("NO") ;

</script>
```

**Output:** 

```
YES
```