# 打印 n 项纽曼-康威序列

> 原文:[https://www . geesforgeks . org/print-n-terms-Newman-Conway-sequence/](https://www.geeksforgeeks.org/print-n-terms-newman-conway-sequence/)

[纽曼-康威数](https://www.geeksforgeeks.org/newman-conway-sequence/)是生成以下整数序列的那个。
1 1 2 3 4 4 5 6 7…..并遵循以下递归公式。

```
P(n) = P(P(n - 1)) + P(n - P(n - 1))
```

给定一个数字 n，然后打印 n 个纽曼-康威序列项
示例:

```
Input : 13
Output : 1 1 2 2 3 4 4 4 5 6 7 7 8

Input : 20
Output : 1 1 2 2 3 4 4 4 5 6 7 7 8 8 8 8 9 10 11 12 
```

## C++

```
// C++ Program to print n terms
// of Newman-Conway Sequence
#include <bits/stdc++.h>
using namespace std;

// Function to find
// the n-th element
void sequence(int n)
{
    // Declare array to store sequence
    int f[n + 1];
    f[0] = 0;
    f[1] = 1;
    f[2] = 1;

    cout << f[1] << " " << f[2] << " ";

    for (int i = 3; i <= n; i++) {
        f[i] = f[f[i - 1]] + f[i - f[i - 1]];       
        cout << f[i] << " ";
    }
}

// Driver Program
int main()
{   
    int n = 13;   
    sequence(n);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print n terms
// of Newman-Conway Sequence

class GFG
{
    // Function to find
    // the n-th element
    public static void sequence(int n)
    {
        // Declare array to store sequence
        int f[] = new int[n + 1];

        f[0] = 0;
        f[1] = 1;
        f[2] = 1;

        System.out.print( f[1] + " " + f[2] + " ");
        for (int i = 3; i <= n; i++)
        {
            f[i] = f[f[i - 1]] + f[i - f[i - 1]];    
            System.out.print(f[i] + " ");
        }
    }

    //Driver code
    public static void main(String []args)
    {
        int n = 13 ;
        sequence(n);
    }

}

// This program is contributed
// by upendra singh bartwal
```

## 蟒蛇 3

```
# Python Program to print n terms
# of Newman-Conway Sequence

def sequence(n):

    # Function to find
    # the n-th element
    # Declare array to store sequence
    f = [0, 1, 1]

    print(f[1], end=" "),
    print(f[2], end=" "),
    for i in range(3,n+1):
        f.append( f[f[i - 1]] + f[i - f[i - 1]])
        print(f[i], end=" "),

# driver code
n = 13
sequence(n)

# This code is contributed
# by upendra singh bartwal
```

## C#

```
// C# Program to print n terms
// of Newman-Conway Sequence
using System;
class GFG
{
    // Function to find
    // the n-th element
    public static void sequence(int n)
    {
        // Declare array to store sequence
        int []f = new int[n + 1];

        f[0] = 0;
        f[1] = 1;
        f[2] = 1;

        Console.Write( f[1] + " " + f[2] + " ");
        for (int i = 3; i <= n; i++)
        {
            f[i] = f[f[i - 1]] + f[i - f[i - 1]];
            Console.Write(f[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 13 ;
        sequence(n);
    }

}

// This program is contributed
// by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print n terms
// of Newman-Conway Sequence

// Function to find
// the n-th element
function sequence($n)
{

    // Declare array to
    // store sequence
    $f=array(0);

    $f[0] = 0;
    $f[1] = 1;
    $f[2] = 1;

    echo $f[1] , " " , $f[2] , " ";

    for ($i = 3; $i <= $n; $i++)
    {
        $f[$i] = $f[$f[$i - 1]] +
                 $f[$i - $f[$i - 1]];    
        echo $f[$i], " ";
    }
}

// Driver Code
{
    $n = 13;
    sequence($n);
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to print n terms
// of Newman-Conway Sequence

    // Function to find
    // the n-th element
    function sequence(n)
    {
        // Declare array to store sequence
        let f = [];

        f[0] = 0;
        f[1] = 1;
        f[2] = 1;

        document.write( f[1] + " " + f[2] + " ");
        for (let i = 3; i <= n; i++)
        {
            f[i] = f[f[i - 1]] + f[i - f[i - 1]];    
            document.write(f[i] + " ");
        }
    }

// Driver code

        let n = 13 ;
        sequence(n);

</script>
```

**输出:**

```
1 1 2 2 3 4 4 4 5 6 7 7 8 
```