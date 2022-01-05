# 十进制数的 9 的补码

> 原文:[https://www.geeksforgeeks.org/9s-complement-decimal-number/](https://www.geeksforgeeks.org/9s-complement-decimal-number/)

十进制数的 9 的补码是它的每一位数字从 9 中减去。和 1 的补码一样，9 的补码是用来用加法减去一个数的。
例如，让我们使用 9 的补码和加法计算“718–123”的值。我们首先找到 718 的 9 的补码，也就是 281。现在我们把 281 加到 123。我们得到 404。9 的补码是 595，等于“718–123”。所以我们可以用加法和 9 的补码找到减法。
如果在最后加一个进位，也称为进位周围的结束，应该加到答案中，去掉进位本身。例如，(83-25)，9 的 25 的补码是 74 和(83+74 = 157)。得到一个进位，现在把它加到数字 57 上，(57+1 = 58)就是答案。
给定一个十进制数 n，求该数的 9 的补码。

```
Input : 25
Output : 9's complement is : 74

Input : 345.45
Output : 9's complement is : 654.54
```

让数字存储为字符串。我们遍历数字的位数，从 9 中减去每个位数。

## C++

```
// C++ program to find 9's complement of a
// number.
#include<iostream>
using namespace std;

void complement(string number)
{
    for (int i=0 ; i < number.length() ; i++ )
        if (number[i] != '.')
            number[i] = '9' - number[i] + '0';

    cout << "9's complement is : " << number;
}

// Driver code
int main()
{
    string number = "345.45";
    complement(number);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 9's complement of a
// number.

class GFG{
static void complement(String number1)
{
    char[] number=number1.toCharArray();
    for (int i=0 ; i < number.length ; i++ )
        if (number[i] != '.')
            number[i] = (char)((int)('9') - (int)(number[i]) + (int)('0'));
    System.out.println( "9's complement is : "+String.valueOf(number));
}

// Driver code
public static void main(String[] args)
{
    String number = "345.45";
    complement(number);
}
}
//This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find 9's
# complement of a number.

def complement(number):

    for i in range(0, len(number)):
        if(number[i] != '.'):
            a = 9 - int(number[i])
            number = (number[:i] +
                     str(a) + number[i + 1:])

    print("9's complement is : ", number)

# Driver code
if __name__=='__main__':
    number = "345.45"
    complement(number)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find 9's complement of a
// number.
using System;

class GFG{
static void complement(string number1)
{
    char[] number=number1.ToCharArray();
    for (int i=0 ; i < number.Length ; i++ )
        if (number[i] != '.')
            number[i] = (char)((int)('9') -
                    (int)(number[i]) + (int)('0'));
    System.Console.WriteLine( "9's complement is : "
                                +new string(number));
}

// Driver code
public static void Main()
{
    String number = "345.45";
    complement(number);
}
}
//This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find 9's complement of a
// number.

function complement( $number)
{
    for ( $i=0 ; $i < strlen($number) ; $i++ )
        if ($number[$i] != '.')
            $number[$i] = '9' - $number[$i] + '0';

    echo "9's complement is : " , $number;
}

// Driver code
    $number = "345.45";
    complement($number);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find 9's complement of a
// number.

function complement(number)
{
    number = number.split('')
    for (let i=0 ; i < number.length; i++ ){       
        if (number[i] != '.'){
            number[i] = String(9 - Number(number[i]) + 0);
         }
    }
    number = number.join("")

    document.write("9's complement is : " + number);
}

// Driver code
    let number = "345.45";
    complement(number);

// This code is contributed by gfgking.

</script>
```

**输出:**

```
9's complement is : 654.54
```

本文由 [**迪本杜·罗伊·乔杜里**](https://auth.geeksforgeeks.org/profile.php?user=Dibyendu Roy Chaudhuri&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。