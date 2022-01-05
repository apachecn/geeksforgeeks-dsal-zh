# 带素数的最大数字

> 原文:[https://www.geeksforgeeks.org/largest-number-prime-digits/](https://www.geeksforgeeks.org/largest-number-prime-digits/)

给定一个巨大的整数值 n，求最大整数值 x，使得 x <= n and all the digits of x are prime.
**例:**

```
Input : n = 45
Output : 37
37 is the largest number smaller than
or equal to with all prime digits.

Input : n = 1000
Output : 777

Input : n = 7721
Output : 7577

Input : n = 7221
Output : 5777
```

我们知道素数是 2，3，5 和 7。另外，由于我们必须处理一个非常大的数字的每个数字，如果我们把它作为一个字符串来处理，会更容易。主要思路是先找到第一个非质数位，然后
找到其左边第一个大于 2 的数字。现在我们可以用刚好小于它的质数替换找到的数字。如果数字是 2，我们必须删除它并用 7 替换下一个数字。之后，我们可以用 7 替换它右边的剩余数字。
以下是上述算法的实现:

## C++

```
// CPP program to find largest number smaller than
// equal to n with all prime digits.
#include <bits/stdc++.h>
using namespace std;

// check if character is prime
bool isPrime(char c)
{
    return (c == '2' || c == '3' || c == '5' || c == '7');
}

// replace with previous prime character
void decrease(string& s, int i)
{
    // if 2 erase s[i] and replace next with 7
    if (s[i] <= '2') {
        s.erase(i, 1);
        s[i] = '7';
    }

    else if (s[i] == '3')
        s[i] = '2';
    else if (s[i] <= '5')
        s[i] = '3';
    else if (s[i] <= '7')
        s[i] = '5';
    else
        s[i] = '7';

    return;
}

string primeDigits(string s)
{
    for (int i = 0; i < s.length(); i++) {

        // find first non prime char
        if (!isPrime(s[i])) {

            // find first char greater than 2
            while (s[i] <= '2' && i >= 0)
                i--;

            // like 20
            if (i < 0) {
                i = 0;
                decrease(s, i);
            }

            // like 7721
            else
                decrease(s, i);

            // replace remaining with 7
            for (int j = i + 1; j < s.length(); j++)
                s[j] = '7';           

            break;
        }
    }

    return s;
}

// Driver code
int main()
{
    string s = "45";
    cout << primeDigits(s) << endl;

    s = "1000";
    cout << primeDigits(s) << endl;

    s = "7721";
    cout << primeDigits(s) << endl;

    s = "7221";
    cout << primeDigits(s) << endl;

    s = "74545678912345689748593275897894708927680";
    cout << primeDigits(s) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest number smaller than
// equal to n with all prime digits.
class GFG
{

    // check if character is prime
    public static boolean isPrime(char c)
    {
        return (c == '2' || c == '3' || c == '5' || c == '7');
    }

    // replace with previous prime character
    public static void decrease(StringBuilder s, int i)
    {
        if (s.charAt(i) <= '2')
        {

            // if 2 erase s[i] and replace next with 7
            s.deleteCharAt(i);
            s.setCharAt(i, '7');
        }
        else if (s.charAt(i) == '3')
            s.setCharAt(i, '2');
        else if (s.charAt(i) <= '5')
            s.setCharAt(i, '3');
        else if (s.charAt(i) <= '7')
            s.setCharAt(i, '5');
        else
            s.setCharAt(i, '7');

        return;
    }

    public static String primeDigits(StringBuilder s)
    {
        for (int i = 0; i < s.length(); i++)
        {

            // find first non prime char
            if (!isPrime(s.charAt(i)))
            {

                // find first char greater than 2
                while (i >= 0 && s.charAt(i) <= '2')
                    i--;

                // like 20
                if (i < 0)
                {
                    i = 0;
                    decrease(s, i);
                }

                // like 7721
                else
                    decrease(s, i);

                // replace remaining with 7
                for (int j = i + 1; j < s.length(); j++)
                    s.setCharAt(j, '7');
                break;
            }
        }

        return s.toString();
    }

    // Driver code
    public static void main(String[] args)
    {
        StringBuilder s = new StringBuilder("45");
        System.out.println(primeDigits(s));

        s = new StringBuilder("1000");
        System.out.println(primeDigits(s));

        s = new StringBuilder("7721");
        System.out.println(primeDigits(s));

        s = new StringBuilder("7221");
        System.out.println(primeDigits(s));

        s = new StringBuilder("74545678912345689748593275897894708927680");
        System.out.println(primeDigits(s));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find largest number
# smaller than equal to n with all prime digits.

# check if character is prime
def isPrime(c):
    return (c == '2' or c == '3' or
            c == '5' or c == '7')

# replace with previous prime character
def decrease(s, i):

    # if 2 erase s[i] and replace next with 7
    if (s[i] <= '2'):
        s.pop(i)
        s[i] = '7'
    elif (s[i] == '3'):
        s[i] = '2'
    elif (s[i] <= '5'):
        s[i] = '3'
    elif (s[i] <= '7'):
        s[i] = '5'
    else:
        s[i] = '7'

def primeDigits(s):
    s = [i for i in s]
    i = 0

    while i < len(s):

        # find first non prime char
        if (isPrime(s[i]) == False):

            # find first char greater than 2
            while (s[i] <= '2' and i >= 0):
                i -= 1

            # like 20
            if (i < 0):
                i = 0
                decrease(s, i)

            # like 7721
            else:
                decrease(s, i)

            # replace remaining with 7
            for j in range(i + 1,len(s)):
                s[j] = '7'

            break
        i += 1

    return "".join(s)

# Driver code
s = "45"
print(primeDigits(s))

s = "1000"
print(primeDigits(s))

s = "7721"
print(primeDigits(s))

s = "7221"
print(primeDigits(s))

s = "74545678912345689748593275897894708927680"
print(primeDigits(s))

# This code is contributed by Mohit Kumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest
// number smaller than equal
// to n with all prime digits.

// check if character is prime
function isPrime($c)
{
    return ($c == '2' || $c == '3' ||
            $c == '5' || $c == '7') ?
                                  1 : 0;
}

// replace with previous
// prime character
function decrease($s, $i)
{
    // if 2 erase s[i] and
    // replace next with 7
    if ($s[$i] <= '2')
    {

        $s[$i] = '*';
        $a = str_split($s);
        $s = "";
        for($h = 0; $h < count($a); $h++)
            if($a[$h] != '*')
                $s = $s.$a[$h];

        $s[$i] = '7';
    }

    else if ($s[$i] == '3')
        $s[$i] = '2';
    else if ($s[$i] <= '5')
        $s[$i] = '3';
    else if ($s[$i] <= '7')
        $s[$i] = '5';
    else
        $s[$i] = '7';

    return $s;
}

function primeDigits($s)
{
    for ($i = 0; $i < strlen($s); $i++)
    {

        // find first non prime char
        if (isPrime($s[$i]) == 0)
        {

            // find first char
            // greater than 2
            while ($i >= 0 &&
                   $s[$i] <= '2')
                --$i;

            // like 20
            if ($i < 0)
            {
                $i = 0;
                $s = decrease($s, $i);
            }

            // like 7721
            else
                $s = decrease($s, $i);

            // replace remaining with 7
            for ($j = $i + 1;
                 $j < strlen($s); $j++)
                $s[$j] = '7';    

            break;
        }
    }

    return $s;
}

// Driver code
$s = "45";
echo primeDigits($s) . "\n";

$s = "1000";
echo primeDigits($s) . "\n";

$s = "7721";
echo primeDigits($s) . "\n";

$s = "7221";
echo primeDigits($s) . "\n";

$s = "74545678912345689748593275897894708927680";
echo primeDigits($s);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// Javascript program to find largest number smaller than
// equal to n with all prime digits.

    // check if character is prime
    function isPrime(c)
    {
        return (c == '2' || c == '3' || c == '5' || c == '7');
    }

    // replace with previous prime character
    function decrease(s,i)
    {

        if (s[i] <= '2')
        {

            // if 2 erase s[i] and replace next with 7
            s.splice(i,1)
            s[i]= '7';
        }
        else if (s[i] == '3')
            s[i] = '2';
        else if (s[i] <= '5')
            s[i]= '3';
        else if (s[i] <= '7')
            s[i] = '5';
        else
            s[i] = '7';

        return s;

    }

    function primeDigits(s)
    {
        for (let i = 0; i < s.length; i++)
        {

            // find first non prime char
            if (!isPrime(s[i]))
            {

                // find first char greater than 2
                while (i >= 0 && s[i].charCodeAt(0) <= '2'.charCodeAt(0))
                    i--;

                // like 20
                if (i < 0)
                {
                    i = 0;
                    s=decrease(s.split(""), i);
                }

                // like 7721
                else
                    s=decrease(s.split(""), i);

                // replace remaining with 7
                for (let j = i + 1; j < s.length; j++)
                    s[j] = '7';
                break;
            }
        }

        return s.join("");
    }

    // Driver code
    let s = "45";
    document.write(primeDigits(s)+"<br>");

    s = "1000";
    document.write(primeDigits(s)+"<br>");

    s = "7721";
    document.write(primeDigits(s)+"<br>");

    s = "7221";
    document.write(primeDigits(s)+"<br>");

    s = "74545678912345689748593275897894708927680";
    document.write(primeDigits(s)+"<br>");

// This code is contributed by unknown2108
</script>
```

**输出:**

```
37
777
7577
5777
73777777777777777777777777777777777777777
```

上述程序的时间复杂度为 O(N)，其中 N 是字符串的长度。