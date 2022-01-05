# 检查数字 N 的所有数字的频率的异或是否为零

> 原文:[https://www . geeksforgeeks . org/检查数字 n 的所有数字的频率的异或是否为零/](https://www.geeksforgeeks.org/check-if-the-xor-of-the-frequency-of-all-digits-of-a-number-n-is-zero-or-not/)

给定一个数字 N，任务是检查数字频率的异或值是否为零。
**例:**

```
Input: N = 122233
Output: Yes
Frequencies of 1, 2 and 3 are 1, 3, 2 respectively.
And Xor of 1, 3 and 2 is 0.

Input: N = 123
Output: No
```

**方法:**统计所有数字的频率，然后对所有频率进行迭代，如果答案为零，则进行异或运算，然后打印“是”否则打印“否”
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

bool check(int s)
{

// creating a frequency array
    int freq[10] = {0},r;
    while(s != 0)
    {

    // Finding the last digit of the number
        r = s % 10;

        // Dividing the number by 10 to
        // eliminate last digit
        s = int(s / 10);

        // counting frequency of each digit
        freq[r] += 1;
    }

    int xor__ = 0;

    // checking if the xor of all frequency is zero or not
    for (int i=0;i<10;i++)
    {
    xor__ = xor__ ^ freq[i];
    if(xor__ == 0)
        return true;
    else
        return false;
    }

}

// Driver function
int main()
{

int s = 122233;
if(check(s))
cout<<"Yes"<<endl;
else
    cout<<"No"<<endl;
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
static boolean check(int s)
{

// creating a frequency array
    int[] freq = new int[10];

    int r,i;
    for(i=0;i<10;i++)
    {
        freq[i]= 0;
    }
    while(s != 0)
    {

    // Finding the last digit of the number
        r = s % 10;

        // Dividing the number by 10 to
        // eliminate last digit
        s = (int)(s / 10);

        // counting frequency of each digit
        freq[r] += 1;
    }

    int xor__ = 0;

    // checking if the xor of all frequency is zero or not
    for ( i=0;i<10;i++)
    {
    xor__ = xor__ ^ freq[i];
    if(xor__ == 0)
        return true;
    else
        return false;
    }
    return true;

}

// Driver function
    public static void main(String[] args) {
        int s = 122233;
        if(check(s))
            System.out.println("Yes\n");
        else
            System.out.println("No\n");
}

// This code is contributed by
// Rajput-Ji
}
```

## 蟒蛇 3

```
# Python implementation of the above approach
def check(s):

    # creating a frequency array
    freq =[0]*10
    while(s != 0):

        # Finding the last digit of the number
        r = s % 10

        # Dividing the number by 10 to
        # eliminate last digit
        s = s//10

        # counting frequency of each digit
        freq[r]+= 1

    xor = 0

    # checking if the xor of all frequency is zero or not
    for i in range(10):
        xor = xor ^ freq[i]
    if(xor == 0):
        return True
    else:
        return False

s = 122233
if(check(s)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

static bool check(int s)
{

    // creating a frequency array
    int[] freq = new int[10];

    int r, i;
    for(i = 0; i < 10; i++)
    {
        freq[i]= 0;
    }
    while(s != 0)
    {

    // Finding the last digit of the number
        r = s % 10;

        // Dividing the number by 10 to
        // eliminate last digit
        s = (int)(s / 10);

        // counting frequency of each digit
        freq[r] += 1;
    }

    int xor__ = 0;

    // checking if the xor of all frequency is zero or not
    for ( i = 0; i < 10; i++)
    {
    xor__ = xor__ ^ freq[i];
    if(xor__ == 0)
        return true;
    else
        return false;
    }
    return true;

}

    // Driver code
    public static void Main()
    {
        int s = 122233;
        if(check(s))
            Console.Write("Yes\n");
        else
            Console.Write("No\n");
    }
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
function check($s)
{
    // creating a frequency array
    $freq =array_fill(0,10,0);
    while($s != 0)
    {
        // Finding the last digit of the number
        $r = $s % 10;

        // Dividing the number by 10 to
        // eliminate last digit
        $s = (int)($s/10);

        // counting frequency of each digit
        $freq[$r]+= 1;
    }
    $xor = 0;

    // checking if the xor of all frequency is zero or not
    for($i=0;$i<10;$i++)
        $xor = $xor ^ $freq[$i];
    if($xor == 0)
        return true;
    else
        return false;
}

// Main Drive
$s = 122233;
if(check($s))
    print("Yes");
else
    print("No");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

function check(s)
{

// creating a frequency array
    let freq = new Array(10).fill(0), r;
    while(s != 0)
    {

    // Finding the last digit of the number
        r = s % 10;

        // Dividing the number by 10 to
        // eliminate last digit
        s = parseInt(s / 10);

        // counting frequency of each digit
        freq[r] += 1;
    }

    let xor__ = 0;

    // checking if the xor of all
    // frequency is zero or not
    for (let i=0;i<10;i++)
    {
    xor__ = xor__ ^ freq[i];
    if(xor__ == 0)
        return true;
    else
        return false;
    }

}

// Driver function

let s = 122233;
if(check(s))
document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```