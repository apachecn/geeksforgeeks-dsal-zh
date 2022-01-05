# 嘶嘶声实施

> 原文:[https://www.geeksforgeeks.org/fizz-buzz-implementation/](https://www.geeksforgeeks.org/fizz-buzz-implementation/)

在软件开发人员的工作面试中被问到，Fizz Buzz 是一个非常简单的编程任务。

**一轮典型的 Fizz Buzz 可以是:**
写一个程序，打印从 1 到 100 的数字，对于 3 的倍数打印“Fizz”而不是数字，对于 5 的倍数打印“Buzz”。

```
1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, 
Fizz Buzz, 16, 17, Fizz, 19, Buzz, Fizz, 22, 23, Fizz, Buzz, 26, 
Fizz, 28, 29, Fizz Buzz, 31, 32, Fizz, 34, Buzz, Fizz, ...
```

## C++

```
// CPP program to print Fizz Buzz
#include <stdio.h>

int main(void)
{
    int i;
    for (i=1; i<=100; i++)
    {
        // number divisible by 3 and 5 will
        // always be divisible by 15, print
        // 'FizzBuzz' in place of the number
        if (i%15 == 0)       
            printf ("FizzBuzz\t");   

        // number divisible by 3? print 'Fizz'
        // in place of the number
        else if ((i%3) == 0)   
            printf("Fizz\t");                

        // number divisible by 5, print 'Buzz' 
        // in place of the number
        else if ((i%5) == 0)                      
            printf("Buzz\t");                

        else // print the number           
            printf("%d\t", i);                

    }

    return 0;
}
```

## 使用 STL 的 C++语言

```
// CPP program to print Fizz Buzz
#include <iostream>
#include <algorithm>
#include <vector>

int main()
{
    // dynamic array(range) of size 100 of int type
    std :: vector<int> range(100);  

    // 'iota' to fill the vector in increasing manner
    std :: iota(range.begin(), range.end(), 1); 

    // initializing dynamic array of string type
    std :: vector<std::string> values; 

    // resize the vector(values) as that of vector(range)
    values.resize(range.size()); 

    //'auto' to deduce the type of the variable
    auto fizzbuzz = [](int i) -> std::string                
    {
        // number divisible by 15(will also be
        // divisible by both 3 and 5), print 'FizzBuzz'
        if ((i%15) == 0)
            return "FizzBuzz";

        // number divisible by 5, print 'Buzz'
        if ((i%5) == 0)
            return "Buzz";

        // number divisible by 3, print 'Fizz'
        if ((i%3) == 0)
            return "Fizz";

        // to print other numbers
        return std::to_string(i);
    };

    // Operation to each of the elements in the
    // range [begin(), end()) and stores the
    // value returned by each operation in the
    // range that begins at values.begin().
    std :: transform(range.begin(), range.end(),
                    values.begin(), fizzbuzz);   
    for (auto& str: values)                                                  
        std::cout << str << std::endl;

    return 0;                                                                                   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Fizz Buzz
import java.util.*;
class FizzBuzz
{
    public static void main(String args[])
    {
        int n = 100;

        // loop for 100 times
        for (int i=1; i<=n; i++)                                
        {
            //number divisible by 15(divisible by
            // both 3 & 5), print 'FizzBuzz' in
            // place of the number
            if (i%15==0)                                                
                System.out.print("FizzBuzz"+" ");
            // number divisible by 5, print 'Buzz'
            // in place of the number
            else if (i%5==0)    
                System.out.print("Buzz"+" ");

            // number divisible by 3, print 'Fizz'
            // in place of the number
            else if (i%3==0)    
                System.out.print("Fizz"+" ");

            else // print the numbers
                System.out.print(i+" ");                        
        }
    }
}
```

## 计算机编程语言

```
# Python program to print Fizz Buzz

# Loop for 100 times i.e. range
for fizzbuzz in range(1,100):

    # Number divisible by 15,(divisible
    # by both 3 & 5), print 'FizzBuzz'
    # in place of the number
    if fizzbuzz % 15 == 0:
        print("FizzBuzz")                                        
        continue

    # Number divisible by 3, print 'Fizz'
    # in place of the number
    elif fizzbuzz % 3 == 0:    
        print("Fizz")                                        
        continue

    # Number divisible by 5,
    # print 'Buzz' in
    # place of the number
    elif fizzbuzz % 5 == 0:        
        print("Buzz")                                    
        continue

    # Print numbers
    print(fizzbuzz)
```

## C#

```
// C# program to print Fizz Buzz
using System;

class GFG{

// Driver Code
public static void Main()
{
    int n = 100;

    // Loop for 100 times
    for(int i = 1; i <= n; i++)                            
    {

        // Number divisible by 15(
        // divisible by both 3 & 5),
        // print 'FizzBuzz' in place
        // of the number
        if (i % 15 == 0)
            Console.Write("FizzBuzz" + " ");

        // Number divisible by 3,
        // print 'Fizz' in place
        // of the number
        else if (i % 3 == 0)    
            Console.Write("Fizz" + " ");

        // Number divisible by
        // 5, print 'Buzz'
        // in place of the number
        else if (i % 5 == 0)                                            
            Console.Write("Buzz" + " ");

        // Print the numbers
        else
            Console.Write(i + " ");                    
    }
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print Fizz Buzz

$i;
for ($i = 1; $i <= 100; $i++)
{
    // number divisible by 3 and
    // 5 will always be divisible
    // by 15, print 'FizzBuzz' in
    // place of the number
    if ($i % 15 == 0)
        echo "FizzBuzz" . "  ";

    // number divisible by 3? print
    // 'Fizz' in place of the number
    else if (($i % 3) == 0)
        echo "Fizz" . "  ";            

    // number divisible by 5, print
    // 'Buzz' in place of the number
    else if (($i % 5) == 0)                
        echo "Buzz" . "  ";            

    else // print the number        
        echo $i,"  " ;            
}

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// JavaScript program to print Fizz Buzz

    let i;
    for (i=1; i<=100; i++)
    {
        // number divisible by 3 and 5 will
        // always be divisible by 15, print
        // 'FizzBuzz' in place of the number
        if (i%15 == 0)   
            document.write("FizzBuzz" + " ");

        // number divisible by 3? print 'Fizz'
        // in place of the number
        else if ((i%3) == 0)
            document.write("Fizz" + " ");               

        // number divisible by 5, print 'Buzz'
        // in place of the number
        else if ((i%5) == 0)                   
            document.write("Buzz" + " ");               

        else // print the number       
            document.write(i + " ");               
    }

//This code is contributed by Manoj
</script>
```

**输出:**

```
1    2    Fizz    4    Buzz    Fizz    7    8    Fizz    Buzz    11   
Fizz    13    14    FizzBuzz    16    17    Fizz    19    Buzz    
Fizz    22    23    Fizz    Buzz    26    Fizz    28    29    FizzBuzz    
31    32    Fizz    34    Buzz    Fizz    37    38    Fizz    Buzz    41    
Fizz    43    44    FizzBuzz    46    47    Fizz    49    Buzz    Fizz    
52    53    Fizz    Buzz    56    Fizz    58    59    FizzBuzz    61    
62    Fizz    64    Buzz    Fizz    67    68    Fizz    Buzz    71    
Fizz    73    74    FizzBuzz    76    77    Fizz    79    Buzz    Fizz    
82    83    Fizz    Buzz    86    Fizz    88    89    FizzBuzz    91    
92    Fizz    94    Buzz    Fizz    97    98    Fizz    Buzz    
```

**嘶嘶声的变化尝试**

1.  **替换包含数字 3 或 5 的数字:**代替替换包含数字 3 或 5 作为因子的数字，游戏可以通过用“嘶”或“嗡嗡”替换包含数字 3 或 5 的数字来进行。
    例如:1，2，菲茨，4，巴兹，6，7，8，9，10，11，12，菲茨，14，巴兹，16，17，18，19，20，21，22，菲茨，24，巴兹，26，27，28，29，菲茨，菲茨，菲茨，菲茨，菲茨，菲茨，菲茨，40，41，42，菲茨，菲茨
2.  **只替换数字中的数字(3 或 5):**在这个变体中，只替换实际的数字，所以 23 变成“20 嘶”，50 变成“buzzty”。这种变异可以与原始的结合形成一个更具挑战性的序列。
    例如:1、2、菲兹、4、巴兹、菲兹、7、8、菲兹、巴兹、11、菲兹、菲兹、14、菲兹巴兹、16、17、菲兹、19、巴兹、菲兹、22、菲兹、菲兹、菲兹、巴兹、26、菲兹、28、29、菲兹巴兹、菲兹、菲兹、菲兹
3.  **基数变化:**游戏可以在 10 以外的数学基数上进行。例如，在 5 号垒打将按如下方式进行:
    例如:1，2，菲兹，4，巴斯，菲兹，12，13，菲兹，巴兹，21，菲兹，23，24，菲兹巴兹，31，32，菲兹，34，巴兹，菲兹，…
4.  **嘶嘶或嗡嗡声，但不是嘶嘶-嗡嗡声:**更具挑战性的变化在嘶嘶或嗡嗡声上有游戏改变的方向，但在嘶嘶-嗡嗡声上没有。对于某些序列，这会使动作在 2 或 3 名玩家之间反弹，并在爆发时导致失误。例如，3/7 版本的游戏有一个 12 到 18 之间的复杂序列。
5.  **菲茨·巴兹·伍夫:**一个变体已经扩展到拥有自己相关名称的程度。在这种情况下，数字 3 变成菲茨，5 变成巴兹，7 变成汪汪。这个游戏的主要规则是，任何包含该数字或可被该数字整除的数字都被该单词的出现所代替。如果该数字有 2 个实例(即 33 或 55)，并且可被该数字整除，则在本例中该单词被说三次。附加的规则是单词(如果出现不止一个)必须按照标题中给出的顺序来说。
    例如:1、2、菲兹·菲兹(3)、4、巴兹·巴兹(5)、菲兹(6)、汪汪(7)、8、菲兹(9)、巴兹(10)、11、菲兹(12)、菲兹(13)、汪汪(14)、菲兹·巴兹(15)、16、汪汪(17)、菲兹(18)、19、巴兹(20)、菲兹·汪汪(21)、22、菲兹(23)、菲兹(24)、巴兹(18)

**参考资料:**
[https://en . Wikipedia . org/wiki/fiz _ buzz](http://wikipedia%20-%20fizz_buzz/)