# 大数的商和余数程序

> 原文:[https://www . geesforgeks . org/program-商-余数-大数/](https://www.geeksforgeeks.org/program-quotient-remainder-big-number/)

给定一串数字并给定另一个数字(比如 m)[0<= m <= 10^18]. The task is to calculate the modulus of the given number.
**]示例:**

```
Input : num = "214"
         m = 5
Output : Remainder = 4
         Quotient = 42         

Input : num = "214755974562154868"
        m = 17
Output : Remainder = 15
         Quotient = 12632704386009109

Input : num = "6466868439215689498894"
        m = 277
Output : Remainder = 213  
         Quotient = 23346095448432092053         
```

为了找到商，我们可以在算法中打印商，或者将这些数字存储在数组中，稍后打印。

```
Initialize mod = 0
First take first digit (from right) and find 
mod using formula:
mod = (mod * 10 + digit) % m
quo[i] = mod / m
where i denotes the position of quotient number

Let's take an example.
num = 12345
m = 9
Initialize mod = 0
quo[i] = (mod * 10 + num[i]) / m
mod = (mod * 10 + num[i]) % m
Where i denotes the position of the i-th digit

1) quo[1] = (0 * 10 + 1) / 9 = 0
   mod = (0 * 10 + 1) % 9 = 1
2) quo[2] = (1 * 10 + 2) / 9 = 12 / 9 = 1 
   mod = (1 * 10 + 2) % 9 = 12 % 9 = 3
3) quo[3] = (3 * 10 + 3) / 9 = 33 / 9 = 3
   mod = (3 * 10 + 3) % 9 = 33 % 9 = 6
4) quo[4] = (6 * 10 + 4) / 9 = 64 / 9 = 7
   mod = (6 * 10 + 4) % 9 = 64 % 9 = 1
5) quo[5] = (1 * 10 + 5) / 9 = 15 / 9 = 1
   mod = (1 * 10 + 5) % 9 = 15 % 9 = 6

Concatenating all values of quotient together
(from 1 to n) where n is the number of digits. 
Thus, modulus is 6 and quotient is 01371.
```

我们也可以用这个技巧来求大数的商和余数。
以下是上述方法的实施:

## C++

```
// CPP program to find quotient and remainder
// when a number is divided by large number
// represented as string.
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

// Function to calculate the modulus
void modBigNumber(string num, ll m)
{
    // Store the modulus of big number
    vector<int> vec;
    ll mod = 0;

    // Do step by step division
    for (int i = 0; i < num.size(); i++) {

        int digit = num[i] - '0';

        // Update modulo by concatenating
        // current digit.
        mod = mod * 10 + digit;

        // Update quotient
        int quo = mod / m;
        vec.push_back(quo);

        // Update mod for next iteration.
        mod = mod % m;       
    }

    cout << "\nRemainder : " << mod << "\n";

    cout << "Quotient : ";

    // Flag used to remove starting zeros
    bool zeroflag = 0;
    for (int i = 0; i < vec.size(); i++) {
        if (vec[i] == 0 && zeroflag == 0)
            continue;
        zeroflag = 1;
        cout << vec[i];
    }

    return;
}

// Driver Code
int main()
{
    string num = "14598499948265358486";
    ll m = 487;
    modBigNumber(num, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find quotient and remainder
// when a number is divided by large number
// represented as String.
import java.util.Vector;

class GFG {

// Function to calculate the modulus
    static void modBigNumber(String num, long m) {
        // Store the modulus of big number
        Vector<Integer> vec = new Vector<>();
        long mod = 0;

        // Do step by step division
        for (int i = 0; i < num.length(); i++) {

            int digit = num.charAt(i) - '0';

            // Update modulo by concatenating
            // current digit.
            mod = mod * 10 + digit;

            // Update quotient
            int quo = (int) (mod / m);
            vec.add(vec.size(), quo);

            // Update mod for next iteration.
            mod = mod % m;
        }

        System.out.print("\nRemainder : " + mod + "\n");

        System.out.print("Quotient : ");

        // Flag used to remove starting zeros
        boolean zeroflag = false;
        for (int i = 0; i < vec.size(); i++) {
            if (vec.get(i) == 0 && zeroflag == false) {
                continue;
            }
            zeroflag = true;
            System.out.print(vec.get(i));
        }

        return;
    }

// Driver Code
    public static void main(String[] args) {

        String num = "14598499948265358486";
        long m = 487;
        modBigNumber(num, m);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find quotient and remainder
# when a number is divided by large number
# represented as string.

# Function to calculate the modulus
def modBigNumber(num, m):
    # Store the modulus of big number
    vec = []
    mod = 0

    # Do step by step division
    for i in range(0,len(num),1):
        digit = ord(num[i]) - ord('0')

        # Update modulo by concatenating
        # current digit.
        mod = mod * 10 + digit

        # Update quotient
        quo = int(mod / m)
        vec.append(quo)

        # Update mod for next iteration.
        mod = mod % m    

    #print("\n")
    print("Remainder :",mod)

    print("Quotient :",end = " ")

    # Flag used to remove starting zeros
    zeroflag = 0;
    for i in range(0,len(vec),1):
        if (vec[i] == 0 and zeroflag == 0):
            continue
        zeroflag = 1
        print(vec[i],end="")

    return

# Driver Code
if __name__ == '__main__':
    num = "14598499948265358486"
    m = 487
    modBigNumber(num, m)

# This code is contributed by
# Surendra_Gangwar

```

## C#

```
// C# program to find quotient and remainder
// when a number is divided by large number
// represented as String.
using System;
using System.Collections.Generic;

class GFG {

// Function to calculate the modulus
    static void modBigNumber(string num, long m) {
        // Store the modulus of big number
        List<int> vec = new List<int>();
        long mod = 0;

        // Do step by step division
        for (int i = 0; i < num.Length; i++) {

            int digit = num[i] - '0';

            // Update modulo by concatenating
            // current digit.
            mod = mod * 10 + digit;

            // Update quotient
            int quo = (int) (mod / m);
            vec.Add(quo);

            // Update mod for next iteration.
            mod = mod % m;
        }

        Console.Write("Remainder : " + mod + "\n");

        Console.Write("Quotient : ");

        // Flag used to remove starting zeros
        bool zeroflag = false;
        for (int i = 0; i < vec.Count; i++) {
            if (vec[i] == 0 && zeroflag == false) {
                continue;
            }
            zeroflag = true;
            Console.Write(vec[i]);
        }

        return;
    }

// Driver Code
    public static void Main() {

        string num = "14598499948265358486";
        long m = 487;
        modBigNumber(num, m);
    }
}
// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find quotient
// and remainder when a number
// is divided by large number
// represented as string.

// Function to calculate
// the modulus
function modBigNumber($num, $m)
{
    // Store the modulus
    // of big number
    $vec;
    $x = 0;
    $mod = 0;

    // Do step by
    // step division
    for ($i = 0;
         $i < strlen($num); $i++)
    {
        $digit = $num[$i] - '0';

        // Update modulo
        // by concatenating
        // current digit.
        $mod = $mod * 10 + $digit;

        // Update quotient
        $quo = (int)($mod / $m);
        $vec[$x++] = $quo;

        // Update mod for
        // next iteration.
        $mod = $mod % $m;
    }

    echo "Remainder : " .
             $mod . "\n";

    echo "Quotient : ";

    // Flag used to
    // remove starting zeros
    $zeroflag = 0;
    for ($i = 0; $i < $x; $i++)
    {
        if ($vec[$i] == 0 &&
            $zeroflag == 0)
            continue;
        $zeroflag = 1;
        echo $vec[$i];
    }

    return;
}

// Driver Code
$num = "14598499948265358486";
$m = 487;
modBigNumber($num, $m);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find quotient
// and remainder when a number
// is divided by large number
// represented as string.

// Function to calculate
// the modulus
function modBigNumber(num, m)
{
    // Store the modulus
    // of big number
    let vec = [];
    let x = 0;
    let mod = 0;

    // Do step by
    // step division
    for (let i = 0;
         i < num.length; i++)
    {
        digit = num[i] - '0';

        // Update modulo
        // by concatenating
        // current digit.
        mod = mod * 10 + digit;

        // Update quotient
        quo = parseInt(mod / m);
        vec[x++] = quo;

        // Update mod for
        // next iteration.
        mod = mod % m;
    }

    document.write( "Remainder : " + mod + "<br>");

    document.write("Quotient : ");

    // Flag used to
    // remove starting zeros
    let zeroflag = 0;
    for (let i = 0; i < x; i++)
    {
        if (vec[i] == 0 &&
            zeroflag == 0)
            continue;
        zeroflag = 1;
        document.write(vec[i]);
    }

    return;
}

// Driver Code

let num = "14598499948265358486";
let m = 487;
modBigNumber(num, m);

// This code is contributed
// by gfgking

</script>
```

**输出:**

```
Remainder = 430
Quotient = 29976385930729688
```

本文由 [**沙钦·毕斯特**](https://www.linkedin.com/in/sachin-bisht-984b5013a/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。