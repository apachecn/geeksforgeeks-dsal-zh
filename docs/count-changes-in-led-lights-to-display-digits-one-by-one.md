# 对 Led 灯的变化进行计数，以逐个显示数字

> 原文:[https://www . geesforgeks . org/count-in-changes-in-led-lights-to-display-digits-逐一/](https://www.geeksforgeeks.org/count-changes-in-led-lights-to-display-digits-one-by-one/)

给定一个数字 n。当显示一个又一个给定的数字时，计算发光二极管灯的变化次数。(最初所有指示灯都熄灭)。数字以字符串的形式输入。
参见[本](https://www.electronics-tutorials.ws/articles/segment3.gif?x98918)图像的七段显示以便更好的理解。
**示例:**

```
Input : n = "082"
Output : 9
We need 6 LED lights to display 0 in seven segment display. We need 7 lights for 8 and 5 lights for 2\. So total on/off is 6 + 1 + 2 = 9.

Input : n = "12345"
Output : 7
```

来源:[摩根士丹利采访集 20](https://www.geeksforgeeks.org/morgan-stanley-interview-set-20-on-campus/)

这个想法是预先计算显示给定数字所需的 led 灯。现在迭代这个数字，并继续添加更改。对于实现，使用了字符串哈希的基本概念。
下面是上面问题的实现。

## C++

```
// CPP program to count number of on offs to
// display digits of a number.
#include<bits/stdc++.h>
using namespace std;

int countOnOff(string n)
{
    // store the led lights required to display
    // a particular number.
    int Led[] = { 6, 2, 5, 5, 4, 5, 6, 3, 7, 5 };

    int len = n.length();

    // compute the change in led and keep
    // on adding the change
    int sum = Led[n[0] - '0'];
    for (int i = 1; i < len; i++) {
        sum = sum + abs(Led[n[i] - '0'] -
              Led[n[i - 1] - '0']);
    }

    return sum;
}

// Driver code
int main()
{
    string n = "082";
    cout << countOnOff(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of on offs to
// display digits of a number.
import java.io.*;

class GFG
{
static int countOnOff(String n)
{
    // store the led lights required to display
    // a particular number.
    int Led[] = { 6, 2, 5, 5, 4, 5, 6, 3, 7, 5 };

    int len = n.length();

    // compute the change in led and keep
    // on adding the change
    int sum = Led[n.charAt(0) - '0'];
    for (int i = 1; i < len; i++) {
        sum = sum + Math.abs(Led[n.charAt(i) - '0'] -
            Led[n.charAt(i - 1) - '0']);
    }

    return sum;
}

// Driver code
public static void main(String args[])
{
    String n = "082";
    System.out.println( countOnOff(n) );
}
}
```

## 蟒蛇 3

```
# Python3 program to count number of on offs to
# display digits of a number.

def countOnOff(n):

    # store the led lights required to display
    # a particular number.
    Led = [ 6, 2, 5, 5, 4, 5, 6, 3, 7, 5 ]

    leng = len(n)

    # compute the change in led and keep
    # on adding the change
    sum = Led[int(n[0]) - int('0')]
    for i in range(1,leng):
        sum = (sum + abs(Led[int(n[i]) - int('0')]
                - Led[int(n[i - 1]) - int('0')]))

    return sum

#Driver code
if __name__=='__main__':
    n = "082"
    print(countOnOff(n))

# this code is contributed by
# ash264
```

## C#

```
// C# program to count number of on
// offs to display digits of a number.
using System;

class GFG
{
public static int countOnOff(string n)
{
    // store the led lights required
    // to display a particular number.
    int[] Led = new int[] {6, 2, 5, 5, 4,
                           5, 6, 3, 7, 5};

    int len = n.Length;

    // compute the change in led and
    // keep on adding the change
    int sum = Led[n[0] - '0'];
    for (int i = 1; i < len; i++)
    {
        sum = sum + Math.Abs(Led[n[i] - '0'] -
                             Led[n[i - 1] - '0']);
    }

    return sum;
}

// Driver code
public static void Main(string[] args)
{
    string n = "082";
    Console.WriteLine(countOnOff(n));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of on offs to display digits
// of a number.

function countOnOff($n)
{
    // store the led lights required
    // to display a particular number.
    $Led = array(6, 2, 5, 5, 4,
                 5, 6, 3, 7, 5 );

    $len = strlen($n);

    // compute the change in led
    // and keep on adding the change
    $sum = $Led[$n[0] - '0'];
    for ($i = 1; $i < $len; $i++)
    {
        $sum = $sum + abs($Led[$n[$i] - '0'] -
                          $Led[$n[$i - 1] - '0']);
    }

    return $sum;
}

// Driver code
$n = "082";
echo countOnOff($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// javascript program to count number of on offs to
// display digits of a number.
function countOnOff( n)
{
    // store the led lights required to display
    // a particular number.
    var Led = [ 6, 2, 5, 5, 4, 5, 6, 3, 7, 5 ];

    var len = n.length;

    // compute the change in led and keep
    // on adding the change
    var sum = Led[n.charAt(0) - '0'];
    for (i = 1; i < len; i++) {
        sum = sum + Math.abs(Led[n.charAt(i) - '0'] -
            Led[n.charAt(i - 1) - '0']);
    }

    return sum;
}

// Driver code

n = "082";
document.write( countOnOff(n) );

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
9
```