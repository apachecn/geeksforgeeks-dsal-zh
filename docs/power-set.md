# 电源设置

> 原文:[https://www.geeksforgeeks.org/power-set/](https://www.geeksforgeeks.org/power-set/)

**幂集**集合 S 的幂集 P(S)是 S 的所有子集的集合，例如 S = {a，b，c}那么 P(s) = {{}，{a}，{b}，{c}，{a，b}，{a，c}，{b，c}，{a，b，c}，{a，b，c}}。
如果 s 包含 n 个元素，那么 P(s)将包含 2^n 元素

**算法:**

```
Input: Set[], set_size
1\. Get the size of power set
    powet_set_size = pow(2, set_size)
2  Loop for counter from 0 to pow_set_size
     (a) Loop for i = 0 to set_size
          (i) If ith bit in counter is set
               Print ith element from set for this subset
     (b) Print separator for subsets i.e., newline
```

**例:**

```
Set  = [a,b,c]
power_set_size = pow(2, 3) = 8
Run for binary counter = 000 to 111

Value of Counter            Subset
    000                    -> Empty set
    001                    -> a
    010                    -> b
    011                    -> ab
    100                    -> c
    101                    -> ac
    110                    -> bc
    111                    -> abc
```

**方法 1:**

## C++

```
// C++ Program of above approach
#include <iostream>
#include <math.h>
using namespace std;

class gfg
{

public:
void printPowerSet(char *set, int set_size)
{
    /*set_size of power set of a set with set_size
    n is (2**n -1)*/
    unsigned int pow_set_size = pow(2, set_size);
    int counter, j;

    /*Run from counter 000..0 to 111..1*/
    for(counter = 0; counter < pow_set_size; counter++)
    {
    for(j = 0; j < set_size; j++)
    {
        /* Check if jth bit in the counter is set
            If set then print jth element from set */
        if(counter & (1 << j))
            cout << set[j];
    }
    cout << endl;
    }
}
};

/*Driver code*/
int main()
{
    gfg g;
    char set[] = {'a','b','c'};
    g.printPowerSet(set, 3);
    return 0;
}

// This code is contributed by SoM15242
```

## C

```
#include <stdio.h>
#include <math.h>

void printPowerSet(char *set, int set_size)
{
    /*set_size of power set of a set with set_size
      n is (2**n -1)*/
    unsigned int pow_set_size = pow(2, set_size);
    int counter, j;

    /*Run from counter 000..0 to 111..1*/
    for(counter = 0; counter < pow_set_size; counter++)
    {
      for(j = 0; j < set_size; j++)
       {
          /* Check if jth bit in the counter is set
             If set then print jth element from set */
          if(counter & (1<<j))
            printf("%c", set[j]);
       }
       printf("\n");
    }
}

/*Driver program to test printPowerSet*/
int main()
{
    char set[] = {'a','b','c'};
    printPowerSet(set, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for power set
import java .io.*;

public class GFG {

    static void printPowerSet(char []set,
                            int set_size)
    {

        /*set_size of power set of a set
        with set_size n is (2**n -1)*/
        long pow_set_size =
            (long)Math.pow(2, set_size);
        int counter, j;

        /*Run from counter 000..0 to
        111..1*/
        for(counter = 0; counter <
                pow_set_size; counter++)
        {
            for(j = 0; j < set_size; j++)
            {
                /* Check if jth bit in the
                counter is set If set then
                print jth element from set */
                if((counter & (1 << j)) > 0)
                    System.out.print(set[j]);
            }

            System.out.println();
        }
    }

    // Driver program to test printPowerSet
    public static void main (String[] args)
    {
        char []set = {'a', 'b', 'c'};
        printPowerSet(set, 3);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# python3 program for power set

import math;

def printPowerSet(set,set_size):

    # set_size of power set of a set
    # with set_size n is (2**n -1)
    pow_set_size = (int) (math.pow(2, set_size));
    counter = 0;
    j = 0;

    # Run from counter 000..0 to 111..1
    for counter in range(0, pow_set_size):
        for j in range(0, set_size):

            # Check if jth bit in the
            # counter is set If set then
            # print jth element from set
            if((counter & (1 << j)) > 0):
                print(set[j], end = "");
        print("");

# Driver program to test printPowerSet
set = ['a', 'b', 'c'];
printPowerSet(set, 3);

# This code is contributed by mits.
```

## C#

```
// C# program for power set
using System;

class GFG {

    static void printPowerSet(char []set,
                            int set_size)
    {
        /*set_size of power set of a set
        with set_size n is (2**n -1)*/
        uint pow_set_size =
              (uint)Math.Pow(2, set_size);
        int counter, j;

        /*Run from counter 000..0 to
        111..1*/
        for(counter = 0; counter <
                   pow_set_size; counter++)
        {
            for(j = 0; j < set_size; j++)
            {
                /* Check if jth bit in the
                counter is set If set then
                print jth element from set */
                if((counter & (1 << j)) > 0)
                    Console.Write(set[j]);
            }

            Console.WriteLine();
        }
    }

    // Driver program to test printPowerSet
    public static void Main ()
    {
        char []set = {'a', 'b', 'c'};
        printPowerSet(set, 3);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for power set

function printPowerSet($set, $set_size)
{

    // set_size of power set of
    // a set with set_size
    // n is (2**n -1)
    $pow_set_size = pow(2, $set_size);
    $counter; $j;

    // Run from counter 000..0 to
    // 111..1
    for($counter = 0; $counter < $pow_set_size;
                                    $counter++)
    {
        for($j = 0; $j < $set_size; $j++)
        {

            /* Check if jth bit in
               the counter is set
               If set then print
               jth element from set */
            if($counter & (1 << $j))
                echo $set[$j];
        }

    echo "\n";
    }
}

    // Driver Code
    $set = array('a','b','c');
    printPowerSet($set, 3);

// This code is contributed by Vishal Tripathi
?>
```

## java 描述语言

```
<script>
// javascript program for power setpublic

    function printPowerSet(set, set_size)
    {

        /*
         * set_size of power set of a set with set_size n is (2**n -1)
         */
        var pow_set_size = parseInt(Math.pow(2, set_size));
        var counter, j;

        /*
         * Run from counter 000..0 to 111..1
         */
        for (counter = 0; counter < pow_set_size; counter++)
        {
            for (j = 0; j < set_size; j++)
            {

                /*
                 * Check if jth bit in the counter is set If set then print jth element from set
                 */
                if ((counter & (1 << j)) > 0)
                    document.write(set[j]);
            }
            document.write("<br/>");
        }
    }

    // Driver program to test printPowerSet
        let set = [ 'a', 'b', 'c' ];
        printPowerSet(set, 3);

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
a
b
ab
c
ac
bc
abc
```

**时间复杂度:** O(n2^n)

**辅助空间:** O(1)
**方法 2:**
这个方法是 python 编程语言特有的。我们可以迭代一个 0 到集合长度的循环，以获得并生成该字符串与可迭代长度的所有可能组合。下面的程序将给出上述思想的实现。

## 蟒蛇 3

```
#Python program to find powerset
from itertools import combinations
def print_powerset(string):
    for i in range(0,len(string)+1):
        for element in combinations(string,i):
            print(''.join(element))
string=['a','b','c']
print_powerset(string)
```

**Output:** 

```
a
b
c
ab
ac
bc
abc
```

[**递归程序生成动力集**](https://www.geeksforgeeks.org/recursive-program-to-generate-power-set/)
Java 中的[动力集](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/)参考 Java 中的实现以及更多打印动力集的方法。
**参考文献:**
[http://en.wikipedia.org/wiki/Power_set](http://en.wikipedia.org/wiki/Power_set)

If you like GeeksforGeeks and would like to contribute, you can also write an article using [write.geeksforgeeks.org](https://write.geeksforgeeks.org/) or mail your article to review-team@geeksforgeeks.org. See your article appearing on the GeeksforGeeks main page and help other Geeks.Please write comments if you find anything incorrect, or you want to share more information about the topic discussed above.