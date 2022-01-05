# 位数重复的数字的平方|集合 1 (3，6 和 9)

> 原文:[https://www . geeksforgeeks . org/重复一位数的数字方块/](https://www.geeksforgeeks.org/squares-of-numbers-with-repeated-single-digits/)

给定一个由个位数组成的数，求它的平方。可以假设个位数是 3、6 和 9。数字可能非常大，即可能超过 long long int。
示例:

```
Input : 33 66 99
Output : 
Square of 33 is : 1089
Square of 66 is : 4356
Square of 99 is : 9801

Input : 333 666 999 
Output : 
Square of 333 is : 110889
Square of 666 is : 443556
Square of 999 is : 998001
```

**方法 1(写成 1111…1 的倍数)**
一个有趣的事实是，每个这样的数都可以表示成 1111…1 的倍数。例如，33333 = 3 * 11111。11，111，1111，11111 …的平方分别是 121，12321，1234321，123454321，…。所以一个简单的解决方法是找到 111 的平方…11，然后将结果乘以 3 或 6 或 9(我们可以使用[乘以大数](https://www.geeksforgeeks.org/multiply-large-numbers-represented-as-strings/))。
**方法 2(使用数字模式)**
**对于 333…333**统计数字个数，按以下方式打印:
假设数字个数为 n，然后写 n-1 乘以 1，再写一次 0，然后写 n-1 乘以 8，最后写 9。
示例:
{ 3333 } = 11108889
**对于 666…666**计算位数并按以下方式打印:
假设位数为 n，然后写 n-1 乘以 4，然后写一次 3，然后写 n-1 乘以 5，最后写 6。
例:
{ 6666 } = 44435556
**对于 999…999**计算位数并按以下方式打印:
假设位数为 n，然后写 n-1 乘以 9，然后写一次 8，然后写 n-1 乘以 0，最后写 1。
示例:
{ 9999 } = 99980001
以下是上述方法的实现:

## C++

```
// C++ program to find square of
// these large numbers
#include <iostream>
using namespace std;

// Function to find the square of
// 333...333, 666...666 and 999...999
string find_Square_369(string num)
{
    char a, b, c, d;

    // if the number is 333...333
    if (num[0] == '3')
        a = '1', b = '0', c = '8', d = '9';

    // if the number is 666...666
    else if (num[0] == '6')
        a = '4', b = '3', c = '5', d = '6';

    // if the number is 999...999
    else
        a = '9', b = '8', c = '0', d = '1';

    // variable for hold result
    string result = "";

    // find the no of digit
    int size = num.size();

    // add size-1 time a in result
    for (int i = 1; i < num.size(); i++)
        result += a;

    // add one time b in result
    result += b;

    // add size-1 time c in result
    for (int i = 1; i < num.size(); i++)
        result += c;

    // add one time d in result
    result += d;

    // return result
    return result;
}

// Drivers code
int main()
{

    string num_3, num_6, num_9;
    num_3 = "3333";
    num_6 = "6666";
    num_9 = "9999";

    string result = "";

    // find square of 33..33
    result = find_Square_369(num_3);
    cout << "Square of " << num_3 << " is : " << result << endl;

    // find square of 66..66
    result = find_Square_369(num_6);
    cout << "Square of " << num_6 << " is : " << result << endl;

    // find square of 66..66
    result = find_Square_369(num_9);
    cout << "Square of " << num_9 << " is : " << result << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find square of
// these large numbers
class GFG {

    // Function to find the square of
    // 333...333, 666...666 and 999...999
    static String find_Square_369(String num)
    {
        char a, b, c, d;

        // if the number is 333...333
        if (num.charAt(0) == '3')
            {a = '1'; b = '0'; c = '8'; d = '9';}

        // if the number is 666...666
        else if (num.charAt(0) == '6')
            {a = '4'; b = '3'; c = '5'; d = '6';}

        // if the number is 999...999
        else
            {a = '9'; b = '8'; c = '0'; d = '1';}

        // variable for hold result
        String result = "";

        // find the no of digit
        int size = num.length();

        // add size-1 time a in result
        for (int i = 1; i < size; i++)
            result += a;

        // add one time b in result
        result += b;

        // add size-1 time c in result
        for (int i = 1; i < size; i++)
            result += c;

        // add one time d in result
        result += d;

        // return result
        return result;
    }

    // Drivers code
    public static void main(String[] args)
    {

        String num_3, num_6, num_9;
        num_3 = "3333";
        num_6 = "6666";
        num_9 = "9999";

        String result = "";

        // find square of 33..33
        result = find_Square_369(num_3);
        System.out.println("Square of " + num_3
                            + " is : " + result);

        // find square of 66..66
        result = find_Square_369(num_6);
        System.out.println("Square of " + num_9
                            + " is : " + result);

        // find square of 66..66
        result = find_Square_369(num_9);
        System.out.println("Square of " + num_9
                            + " is : " + result);

    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Pyhton 3 program to find square of
# these large numbers

# Function to find the square of
# 333...333, 666...666 and 999...999
def find_Square_369(num):

    # if the number is 333...333
    if (num[0] == '3'):
        a = '1'
        b = '0'
        c = '8'
        d = '9'

    # if the number is 666...666
    elif (num[0] == '6'):
        a = '4'
        b = '3'
        c = '5'
        d = '6'

    # if the number is 999...999
    else:
        a = '9'
        b = '8'
        c = '0'
        d = '1'

    # variable for hold result
    result = ""

    # find the no of digit
    size = len(num)

    # add size-1 time a in result
    for i in range(1, size):
        result += a

    # add one time b in result
    result += b

    # add size-1 time c in result
    for i in range(1, size):
        result += c

    # add one time d in result
    result += d

    # return result
    return result

# Drivers code
# Your Python 3 Code

num_3 = "3333"
num_6 = "6666"
num_9 = "9999"

result = ""

# find square of 33..33
result = find_Square_369(num_3)
print("Square of " + num_3 + " is : "
                            + result);

# find square of 66..66
result = find_Square_369(num_6)
print("Square of " + num_6 + " is : "
                            + result);

# find square of 66..66
result = find_Square_369(num_9)
print("Square of " + num_9 + " is : "
                           + result);

# This code is contributed by Smitha
```

## C#

```
// C# program to find square of
// these large numbers
using System;

class GFG {

    // Function to find the square of
    // 333...333, 666...666 and 999...999
    static string find_Square_369(string num)
    {
        char a, b, c, d;

        // if the number is 333...333
        if (num[0] == '3')
            {a = '1'; b = '0'; c = '8'; d = '9';}

        // if the number is 666...666
        else if (num[0] == '6')
            {a = '4'; b = '3'; c = '5'; d = '6';}

        // if the number is 999...999
        else
            {a = '9'; b = '8'; c = '0'; d = '1';}

        // variable for hold result
        string result = "";

        // find the no of digit
        int size = num.Length;

        // add size-1 time a in result
        for (int i = 1; i < size; i++)
            result += a;

        // add one time b in result
        result += b;

        // add size-1 time c in result
        for (int i = 1; i < size; i++)
            result += c;

        // add one time d in result
        result += d;

        // return result
        return result;
    }

    // Drivers code
    public static void Main()
    {
        string num_3, num_6, num_9;
        num_3 = "3333";
        num_6 = "6666";
        num_9 = "9999";

        string result = "";

        // find square of 33..33
        result = find_Square_369(num_3);
        Console.Write("Square of " + num_3
                + " is : " + result + "\n");

        // find square of 66..66
        result = find_Square_369(num_6);
        Console.Write("Square of " + num_9
                + " is : " + result + "\n");

        // find square of 66..66
        result = find_Square_369(num_9);
        Console.Write("Square of " + num_9
                + " is : " + result + "\n");
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find square of
// these large numbers

// Function to find the square of
// 333...333, 666...666 and 999...999
function find_Square_369($num)
{

    // if the number is 333...333
    if ($num[0] == '3')
    {
        $a = '1';
        $b = '0';
        $c = '8';
        $d = '9';
    }

    // if the number is 666...666
    else if ($num[0] == '6')
    {
        $a = '4';
        $b = '3';
        $c = '5';
        $d = '6';
    }

    // if the number is 999...999
    else
    {
        $a = '9';
        $b = '8';
        $c = '0';
        $d = '1';
    }

    // variable for hold result
    $result = "";

    // find the no of digit
    $size = strlen($num);

    // add size-1 time a in result
    for ($i = 1; $i < $size; $i++)
        $result = $result.$a;

    // add one time b in result
    $result = $result.$b;

    // add size-1 time c in result
    for ($i = 1; $i < $size; $i++)
        $result = $result.$c;

    // add one time d in result
    $result = $result.$d;

    // return result
    return $result;
}

// Drivers code

$num_3 = "3333";
$num_6 = "6666";
$num_9 = "9999";

$result = "";

// find square of 33..33
$result = find_Square_369($num_3);
echo "Square of " . $num_3 . " is : " . $result ."\n" ;

// find square of 66..66
$result = find_Square_369($num_6);
echo "Square of " . $num_6 . " is : " .$result ."\n";

// find square of 66..66
$result = find_Square_369($num_9);
echo "Square of " . $num_9 . " is : ".$result ."\n";

return 0;
?>
```

## java 描述语言

```
<script>
// Javascript program to find square of
// these large numbers

    // Function to find the square of
    // 333...333, 666...666 and 999...999
    function find_Square_369(num)
    {
        let a, b, c, d;

        // if the number is 333...333
        if (num[0] == '3')
            {a = '1'; b = '0'; c = '8'; d = '9';}

        // if the number is 666...666
        else if (num[0] == '6')
            {a = '4'; b = '3'; c = '5'; d = '6';}

        // if the number is 999...999
        else
            {a = '9'; b = '8'; c = '0'; d = '1';}

        // variable for hold result
        let result = "";

        // find the no of digit
        let size = num.length;

        // add size-1 time a in result
        for (let i = 1; i < size; i++)
            result += a;

        // add one time b in result
        result += b;

        // add size-1 time c in result
        for (let i = 1; i < size; i++)
            result += c;

        // add one time d in result
        result += d;

        // return result
        return result;
    }

    // Drivers code
    let num_3, num_6, num_9;

    num_3 = "3333";
    num_6 = "6666";
    num_9 = "9999";

    let result = "";

    // find square of 33..33
    result = find_Square_369(num_3);
    document.write("Square of " + num_3
                            + " is : " + result+"<br>");

    // find square of 66..66
    result = find_Square_369(num_6);
    document.write("Square of " + num_9
                            + " is : " + result+"<br>");

    // find square of 66..66
    result = find_Square_369(num_9);
    document.write("Square of " + num_9
                            + " is : " + result+"<br>");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Square of 3333 is : 11108889
Square of 6666 is : 44435556
Square of 9999 is : 99980001
```