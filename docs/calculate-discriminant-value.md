# 计算判别值

> 原文:[https://www.geeksforgeeks.org/calculate-discriminant-value/](https://www.geeksforgeeks.org/calculate-discriminant-value/)

在代数中， **D** 是一个判别式，帮助我们推导多项式或多项式函数的根的各种性质，甚至不用计算它们。我们来看看这个一般的二次多项式:

```
ax<sup>2 + bx + c</sup>
```

这里，方程的判别式使用公式计算:

```
b<sup>2 – 4ac</sup>
```

现在我们可以推导出以下性质:

*   如果判别式等于零，则多项式具有相等的根，即 a=b。
*   如果判别式是正的，系数是实的，那么多项式有两个实根。

在编程和从判别式中进行推断时，我们必须记住几个条件:

*   如果判别式等于*零*，那么一个解是可能的。
*   如果判别式为*正*，则有两种可能的解。
*   如果判别式为*负*，则不可能有真正的解。

**例:**

```
Input:
a = 20
b = 30
c = 10
Explanation:
(30**2) - (4*20*10) 
Output:
Discriminant is 100 which is positive
Hence Two solutions

Input:
a = 9
b = 7
c = 12
Explanation:
(30**2) - (4*20*10) 
Output:
Discriminant is -383 which is negative
Hence no real solutions
```

## C++

```
// CPP program to calculate Discriminant
#include <bits/stdc++.h>

using namespace std;

void discriminant(int a, int b, int c){

    int discriminant = (b*b) - (4*a*c);
    if(discriminant > 0){
        cout<<"Discriminant is "<<discriminant
            <<" which is Positive"<<endl;

        cout<<"Hence Two Solutions";
    }
    else if(discriminant == 0){
        cout<<"Discriminant is "<<discriminant
            <<" which is Zero"<<endl;

        cout<<"Hence One Solution";
    }
    else if(discriminant < 0){
        cout<<"Discriminant is "<<discriminant
            <<" which is Negative"<<endl;

        cout<<"Hence No Real Solutions";
    }
}

// Driver Code
int main(){
    int a = 20, b = 30, c = 10;

    // function call to print discriminant
    discriminant(a, b, c);
    return 0;
}

// This code is contributed by
// Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate discriminant
public class Discriminant{

    // function to calculate discriminant
    static int disc(int a, int b, int c){
        int dis = (int)Math.pow(b,2) - (4*a*c);
        return dis;
    }

    // Driver Code
    public static void main(String args[]){
        int a=20;
        int b=30;
        int c=10;
        int discriminant = disc(a, b, c);
        if (discriminant > 0){
            System.out.println("Discriminant is " + discriminant
                    + " which is Positive");
            System.out.println("Hence Two Solutions");
        }
        else if (discriminant == 0){
            System.out.println("Discriminant is " + discriminant
                    + " which is Zero");
            System.out.println("Hence One Solution");
        }
        else {
            System.out.println("Discriminant is "+ discriminant
                    + " which is Negative");
            System.out.println("Hence No Real Solutions");
        }
    }
}
```

## 蟒蛇 3

```
# Python program to calculate Discriminant

def discriminant(a, b, c):

    discriminant = (b**2) - (4*a*c)
    if discriminant > 0:

        print('Discriminant is', discriminant,
                "which is Positive")

        print('Hence Two Solutions')

    elif discriminant == 0:

        print('Discriminant is', discriminant,
                "which is Zero")

        print('Hence One Solution')

    elif discriminant < 0:

        print('Discriminant is', discriminant,
                "which is Negative")

        print('Hence No Real Solutions')

# Driver Code
a = 20
b = 30
c = 10
discriminant(a, b, c)
```

## C#

```
// C# program to calculate
// discriminant
using System;

class GFG
{

// function to calculate
// discriminant
static int disc(int a,
                int b, int c)
{
    int dis = (int)Math.Pow(b, 2) -
                    (4 * a * c);
    return dis;
}

// Driver Code
public static void Main()
{
    int a = 20;
    int b = 30;
    int c = 10;
    int discriminant = disc(a, b, c);
    if (discriminant > 0)
    {
        Console.WriteLine("Discriminant is " +
                                discriminant +
                        " which is Positive");
        Console.WriteLine("Hence Two Solutions");
    }

    else if (discriminant == 0)
    {
        Console.WriteLine("Discriminant is " +
                                discriminant +
                            " which is Zero");
        Console.WriteLine("Hence One Solution");
    }

    else
    {
        Console.WriteLine("Discriminant is "+
                            discriminant +
                    " which is Negative");
        Console.WriteLine("Hence No Real Solutions");
    }
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate Discriminant

function discriminant($a, $b, $c)
{

    $discriminant = ($b * $b) - (4 * $a * $c);
    if($discriminant > 0)
    {
        echo "Discriminant is ", $discriminant,
             " which is Positive\n";
        echo "Hence Two Solutions";
    }

    else if($discriminant == 0)
    {
        echo "Discriminant is ", $discriminant,
             " which is Zero\n";
        echo "Hence One Solution";
    }

    else if($discriminant < 0)
    {
        echo "Discriminant is ", $discriminant,
             " which is Negative\n";

        echo "Hence No Real Solutions";
    }
}

// Driver code
$a = 20;
$b = 30;
$c = 10;

// function call to print discriminant
discriminant($a, $b, $c);

// This code is contributed
// by Shashank_Sharma
?>
```

## java 描述语言

```
<script>
// javascript program to calculate discriminant

    // function to calculate discriminant
    function disc(a , b , c) {
        var dis = parseInt( Math.pow(b, 2) - (4 * a * c));
        return dis;
    }

    // Driver Code

        var a = 20;
        var b = 30;
        var c = 10;
        var discriminant = disc(a, b, c);
        if (discriminant > 0) {
            document.write("Discriminant is " + discriminant + " which is Positive<br/>");
            document.write("Hence Two Solutions");
        } else if (discriminant == 0) {
            document.write("Discriminant is " + discriminant + " which is Zero<br/>");
            document.write("Hence One Solution");
        } else {
            document.write("Discriminant is " + discriminant + " which is Negative<br/>");
            document.write("Hence No Real Solutions");
        }

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Discriminant is 100 which is Positive
Hence Two Solutions
```

本文由 [**【钦莫伊蕾恩卡】**](https://www.linkedin.com/in/lenkachinmoy/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。