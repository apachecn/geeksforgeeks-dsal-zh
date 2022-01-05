# 自我描述号

> 原文:[https://www.geeksforgeeks.org/self-descriptive-number/](https://www.geeksforgeeks.org/self-descriptive-number/)

A **自描述数**是一个整数 n 在给定的基数 b 中是 b 位数长，其中 p 位置的每个数字(最高有效数字在 0 位置，最低有效数字在 b–1 位置)计算一个数字 p 在 n 中出现的次数
例如在基数 10 中， **6210001000** 是一个自描述数。

**说明:**
是以 10 为基数的 10 位数。
0 位有 6，6210001000 有 6 个 0。
位置 1 有 2，6210001000 有 2 个 1。
位置 2 有 1，6210001000 有一个 2s。
位置 3 有 0，6210001000 有零 3s。
位置 4 有 0，6210001000 有零个 4。
位置 5 有 0，6210001000 有零 5s。
6 位有 1，6210001000 中有一个 6。
位置 7 有 0，6210001000 有零 7。
位置 8 有 0，6210001000 有零个 8。
9 位有 0，6210001000 有零个 9。
【来源:[维基百科](https://en.wikipedia.org/wiki/Self-descriptive_number)

> 这里有一个程序可以打印所有 100000000 以下的自描述数字。在下面的程序中，我们忽略了一个关于自描述数字的事实，即它应该有与给定基数一样多的位数。

**节目描述:**
**1。**首先从外循环中提取所有数字，并在每次迭代中存储在变量 b 中。
**2。**然后在内部循环中，计算数字 I(这个 I 是外部循环的索引)在字符串中出现的次数。
**3。**最后，将计数器与存储在变量 b 中第 I 个索引处的数字进行比较

## C++

```
// C++ program to print
// all self descriptive
// number below 100000000
#include <iostream>
using namespace std;

bool isSelfDescriptiveNumber(int num)
{
    // converting the integer
    // num to string
    string s = to_string(num);
    for (int i = 0;
             i < s.size(); i++)
    {

        // Extracting each digit
        // one by one from the
        // string
        char temp_char = s.at(i);

        // converting the string
        // (digit) into integer b
        // variable stores the digit
        // present at index 'i'
        int b = temp_char - '0';

        // counting how many
        // times the particular
        // digit occur in the
        // whole number "num"
        int count = 0;
        for (int j = 0;
                 j < s.size(); j++)
        {
            // converting string
            // char to integer
            int temp = s.at(j) - '0';

            // checking whether it is
            // equal to the index 'i'
            // if it is then increment
            // the count .
            if (temp == i)
            {
                count++;
            }
        }

        // If it is not equal
        // it return false .
        if (count != b)
            return false;
    }
    return true;
}

// Driver Code
int main()
{
    for (int i = 0; i < 100000000; i++)
        if (isSelfDescriptiveNumber(i))
            cout << i << endl;
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all self descriptive
// number below 100000000
public class SelfDescriptive {

    public static boolean isSelfDescriptiveNumber(int num)
    {
        // converting the integer num to string
        String s = Integer.toString(num);
        for (int i = 0; i < s.length(); i++) {

            // Extracting each digit one by one from the string
            String temp_char = s.charAt(i) + "";

            // converting the string (digit) into integer
            // b variable stores the digit present at index 'i'
            int b = Integer.parseInt(temp_char);

            // counting how many times the particular digit
            // occur in the whole number "num"
            int count = 0;
            for (int j = 0; j < s.length(); j++) {
                // converting string char to integer
                int temp = Integer.parseInt(s.charAt(j) + "");

                // checking whether it is equal to the index 'i'
                // if it is then increment the count .
                if (temp == i) {
                    count++;
                }
            }

            // If it is not equal
            // it return false .
            if (count != b)
                return false;
        }
        return true;
    }

    public static void main(String[] args)
    {
        for (int i = 0; i < 100000000; i++)
            if (isSelfDescriptiveNumber(i))
                System.out.println(i);       
    }
}
```

## 蟒蛇 3

```
# Python3 program to print
# all self descriptive
# number below 100000000
def isSelfDescriptiveNumber(num):

    # Converting the integer
    # num to string
    s = str(num)

    for i in range(len(s)):

        # Extracting each digit
        # one by one from the
        # string
        temp_char = s[i]

        # Converting the string
        # (digit) into integer b
        # variable stores the digit
        # present at index 'i'
        b = ord(temp_char) - ord('0')

        # Counting how many
        # times the particular
        # digit occur in the
        # whole number "num"
        count = 0

        for j in range(len(s)):

            # Converting string
            # char to integer
            temp = ord(s[j]) - ord('0')

            # Checking whether it is
            # equal to the index 'i'
            # if it is then increment
            # the count .
            if (temp == i):
                count += 1

        # If it is not equal
        # it return false .
        if (count != b):
            return False

    return True

# Driver code
if __name__=="__main__":

    for i in range(100000000):
        if (isSelfDescriptiveNumber(i)):
            print(i)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print
// all self descriptive
// number below 100000000
using System;

class GFG
{
static bool isSelfDescriptiveNumber(int num)
{
    // converting the integer
    // num to string
    string s = num.ToString();
    for (int i = 0;
             i < s.Length; i++)
    {

        // Extracting each digit
        // one by one from the
        // string
        string temp_char = s[i] + "";

        // converting the string
        // (digit) into integer b
        // variable stores the digit
        // present at index 'i'
        int b = int.Parse(temp_char);

        // counting how many
        // times the particular
        // digit occur in the
        // whole number "num"
        int count = 0;
        for (int j = 0;
                 j < s.Length; j++)
        {
            // converting string
            // char to integer
            int temp = int.Parse(s[j] + "");

            // checking whether it is
            // equal to the index 'i'
            // if it is then increment
            // the count .
            if (temp == i)
            {
                count++;
            }
        }

        // If it is not equal
        // it return false .
        if (count != b)
            return false;
    }
    return true;
}

// Driver Code
static void Main()
{
    for (int i = 0; i < 100000000; i++)
        if (isSelfDescriptiveNumber(i))
            Console.WriteLine(i);   
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// all self descriptive
// number below 100000000

// Note:
// 100000000 is a huge no so
// it give sometime TLE error
// because its takes compile
// time above 5 sec
function isSelfDescriptiveNumber($num)
{
    // converting the integer
    // num to string
    $s = strval($num);
    for ($i = 0; $i < strlen($s); $i++)
    {

        // Extracting each digit
        // one by one from the
        // string
        $temp_char = $s[$i];

        // converting the string
        // (digit) into integer b
        // variable stores the digit
        // present at index 'i'
        $b = $temp_char - '0';

        // counting how many
        // times the particular
        // digit occur in the
        // whole number "num"
        $count = 0;
        for ($j = 0; $j < strlen($s); $j++)
        {
            // converting string
            // char to integer
            $temp = $s[$j] - '0';

            // checking whether it is
            // equal to the index 'i'
            // if it is then increment
            // the count .
            if ($temp == $i)
            {
                $count++;
            }
        }

        // If it is not equal
        // it return false .
        if ($count != $b)
            return false;
    }
    return true;
}

// Driver Code
for ($i = 0; $i < 100000000; $i++)
    if (isSelfDescriptiveNumber($i))
        echo $i."\n";

// This code is contributed
// by mits
?>
```

**输出:**

```
1210
2020
21200
3211000

```