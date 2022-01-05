# 找到最小数量的纸币和金额总和

> 原文:[https://www . geesforgeks . org/find-number-currency-notes-sum-up-给定金额/](https://www.geeksforgeeks.org/find-number-currency-notes-sum-upto-given-amount/)

给定一个金额，找出不同面额的纸币的最小数量，这些纸币的总和就是给定的金额。从最高面额的纸币开始，尽量容纳给定数量的纸币。
我们可以假设我们有无限量的价值纸币供应{2000、500、200、100、50、20、10、5、1}
**示例:**

```
Input : 800
Output : Currency  Count 
         500 : 1
         200 : 1
         100 : 1

Input : 2456
Output : Currency  Count
         2000 : 1
         200 : 2
         50 : 1
         5 : 1
         1 : 1
```

这个问题是[换币问题](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)的简单变异。这里贪婪方法的工作原理是给定的系统是规范的(详情请参考[这个](https://arxiv.org/abs/0809.0400)和[这个](https://arxiv.org/pdf/0809.0400.pdf))
下面是寻找音符数量的程序实现:

## C++

```
// C++ program to accept an amount
// and count number of notes
#include <bits/stdc++.h>
using namespace std;

// function to count and
// print currency notes
void countCurrency(int amount)
{
    int notes[9] = { 2000, 500, 200, 100,
                     50, 20, 10, 5, 1 };
    int noteCounter[9] = { 0 };

    // count notes using Greedy approach
    for (int i = 0; i < 9; i++) {
        if (amount >= notes[i]) {
            noteCounter[i] = amount / notes[i];
            amount = amount - noteCounter[i] * notes[i];
        }
    }

    // Print notes
    cout << "Currency Count ->" << endl;
    for (int i = 0; i < 9; i++) {
        if (noteCounter[i] != 0) {
            cout << notes[i] << " : "
                << noteCounter[i] << endl;
        }
    }
}

// Driver function
int main()
{
    int amount = 868;
    countCurrency(amount);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to accept an amount
# and count number of notes

# Function to count and print
# currency notes
def countCurrency(amount):

    notes = [2000, 500, 200, 100,
               50, 20, 10, 5, 1]

    noteCounter = [0, 0, 0, 0, 0,
                     0, 0, 0, 0]

    print ("Currency Count -> ")

    for i, j in zip(notes, noteCounter):
        if amount >= i:
            j = amount // i
            amount = amount - j * i
            print (i ," : ", j)

# Driver code
amount = 868
countCurrency(amount)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to accept an amount
// and count number of notes
import java.util.*;
import java.lang.*;

public class GfG{

    // function to count and
    // print currency notes
    public static void countCurrency(int amount)
    {
        int[] notes = new int[]{ 2000, 500, 200, 100, 50, 20, 10, 5, 1 };
        int[] noteCounter = new int[9];

        // count notes using Greedy approach
        for (int i = 0; i < 9; i++) {
            if (amount >= notes[i]) {
                noteCounter[i] = amount / notes[i];
                amount = amount - noteCounter[i] * notes[i];
            }
        }

        // Print notes
        System.out.println("Currency Count ->");
        for (int i = 0; i < 9; i++) {
            if (noteCounter[i] != 0) {
                System.out.println(notes[i] + " : "
                    + noteCounter[i]);
            }
        }
    }

    // driver function
    public static void main(String argc[]){
        int amount = 868;
        countCurrency(amount);
    }

    /* This code is contributed by Sagar Shukla */
}
```

## C#

```
// C# program to accept an amount
// and count number of notes
using System;

public class GfG{

    // function to count and
    // print currency notes
    public static void countCurrency(int amount)
    {
        int[] notes = new int[]{ 2000, 500, 200, 100, 50, 20, 10, 5, 1 };
        int[] noteCounter = new int[9];

        // count notes using Greedy approach
        for (int i = 0; i < 9; i++) {
            if (amount >= notes[i]) {
                noteCounter[i] = amount / notes[i];
                amount = amount - noteCounter[i] * notes[i];
            }
        }

        // Print notes
        Console.WriteLine("Currency Count ->");
        for (int i = 0; i < 9; i++) {
            if (noteCounter[i] != 0) {
                Console.WriteLine(notes[i] + " : "
                    + noteCounter[i]);
            }
        }
    }

    // Driver function
    public static void Main(){
        int amount = 868;
        countCurrency(amount);
    }

}

/* This code is contributed by vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to accept an amount
// and count number of notes

// function to count and
// prcurrency notes
function countCurrency($amount)
{
    $notes = array(2000, 500, 200, 100,
                   50, 20, 10, 5, 1);
    $noteCounter = array(0, 0, 0, 0, 0,
                         0, 0, 0, 0, 0);

    // count notes using
    // Greedy approach
    for ($i = 0; $i < 9; $i++)
    {
        if ($amount >= $notes[$i])
        {
            $noteCounter[$i] = intval($amount /
                                      $notes[$i]);
            $amount = $amount -
                      $noteCounter[$i] *
                      $notes[$i];
        }
    }    
    // Print notes
    echo ("Currency Count ->"."\n");
    for ($i = 0; $i < 9; $i++)
    {
        if ($noteCounter[$i] != 0)
        {
            echo ($notes[$i] . " : " .
                  $noteCounter[$i] . "\n");
        }
    }
}

// Driver Code
$amount = 868;
countCurrency($amount);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to accept an amount
// and count number of notes

    // function to count and
    // print currency notes
    function countCurrency(amount)
    {
        let notes = [ 2000, 500, 200, 100, 50, 20, 10, 5, 1 ];
        let noteCounter = Array(9).fill(0);

        // count notes using Greedy approach
        for (let i = 0; i < 9; i++) {
            if (amount >= notes[i]) {
                noteCounter[i] = Math.floor(amount / notes[i]);
                amount = amount - noteCounter[i] * notes[i];
            }
        }

        // Print notes
       document.write("Currency Count ->" + "<br/>");
        for (let i = 0; i < 9; i++) {
            if (noteCounter[i] != 0) {
                document.write(notes[i] + " : "
                    + noteCounter[i] + "<br/>");
            }
        }
    }

// driver code

    let amount = 868;
    countCurrency(amount);

</script>
```

**输出:**

```
Currency  Count ->
500 : 1
200 : 1
100 : 1
50 : 1
10 : 1
5 : 1
1 : 3
```