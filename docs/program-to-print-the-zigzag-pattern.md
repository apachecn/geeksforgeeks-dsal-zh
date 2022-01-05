# 打印锯齿形图案的程序

> 原文:[https://www . geesforgeks . org/program-to-print-the-zigzag-pattern/](https://www.geeksforgeeks.org/program-to-print-the-zigzag-pattern/)

给定表示行数的数字 N。任务是打印 N 行的锯齿形图案，如下例所示。
**例** :

```
Input : N = 3 
Output : 1 
         3*2 
         4*5*6

Input : N = 5
Output : 1 
         3*2 
         4*5*6 
         10*9*8*7 
         11*12*13*14*15
```

**接近** :

1.  使用 for 循环打印行数。
2.  奇数行和偶数行分别使用两个变量 var 和 var1。
3.  行号为奇数时，计算行的起点，然后同时打印并递增变量。
4.  行号为偶数时，计算对应的起点，同时打印并递减变量。

以下是上述方法的实现:

## C++

```
// CPP program to print the given
// zigzag pattern

#include<iostream>
using namespace std;

// Function to print the zigzag pattern
void printPattern(int n)
{  
    int var1, var = 1;

    for(int i = 1; i <= n; i++)
    {  
        // for odd rows
        if(i%2!=0)
        {  
            // calculate starting value
            var = var + i - 1;
            for(int j=1; j<=i; j++)
            {
                if(j==1)
                {
                    cout<<var;
                }
                else
                   cout<<"*"<<var;

               var++;   
            }
        }
        else // for even rows
        {        
            var1 = var + i -1; // calculate starting value
            for(int j=1; j<=i; j++)
            {
                if(j==1)
                {
                    // print without star
                    cout<<var1;
                }
                else
                {
                    // print with star
                    cout<<"*"<<var1;
                }
                var1--;
            }
        }
        cout<<endl;
    }

}

// Driver code
int main()
{
    int n = 5;

    printPattern(n);

    return 0;
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the given
// zigzag pattern
class GFG
{
// Function to print the
// zigzag pattern
static void printPattern(int n)
{
    int var1, var = 1;

    for(int i = 1; i <= n; i++)
    {
        // for odd rows
        if(i % 2 != 0)
        {
            // calculate starting value
            var = var + i - 1;
            for(int j = 1; j <= i; j++)
            {
                if(j == 1)
                {
                    System.out.print(var);
                }
                else
                System.out.print("*" + var);

            var++;
            }
        }
        else // for even rows
        {    
            var1 = var + i -1; // calculate starting value
            for(int j = 1; j <= i; j++)
            {
                if(j == 1)
                {
                    // print without star
                    System.out.print(var1);
                }
                else
                {
                    // print with star
                    System.out.print("*" + var1);
                }
                var1--;
            }
        }
        System.out.print("\n");
    }

}

// Driver code
public static void main(String [] arg)
{
    int n = 5;

    printPattern(n);
}
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python3 program to print the given
# zigzag pattern

# Function to print the zigzag pattern
def printPattern(n):

    var = 0
    var = 1

    for i in range(1, n + 1):

        # for odd rows
        if(i % 2 != 0):

            # calculate starting value
            var = var + i - 1
            for j in range(1, i + 1):

                if(j == 1):

                    print(var, end = "")
                else:
                    print("*", end = "")
                    print(var, end = "")

                var += 1

        else: # for even rows

            var1 = var + i -1 # calculate starting value
            for j in range(1, i + 1):

                if(j == 1):

                    # prwithout star
                    print(var1, end = "")

                else:

                    # prwith star
                    print("*", end = "")
                    print(var1, end = "")

                var1 -= 1

        print()

# Driver code
n = 5

printPattern(n)

# This code is contributed by Mohit kumar
```

## C#

```
// C# program to print the given
// zigzag pattern
using System;
class GFG
{
// Function to print the
// zigzag pattern
static void printPattern(int n)
{
    int var1, var = 1;

    for(int i = 1; i <= n; i++)
    {
        // for odd rows
        if(i % 2 != 0)
        {
            // calculate starting value
            var = var + i - 1;
            for(int j = 1; j <= i; j++)
            {
                if(j == 1)
                {
                    Console.Write(var);
                }
                else
                    Console.Write("*" + var);

            var++;
            }
        }
        else // for even rows
        {    
            var1 = var + i -1; // calculate starting value
            for(int j = 1; j <= i; j++)
            {
                if(j == 1)
                {
                    // print without star
                    Console.Write(var1);
                }
                else
                {
                    // print with star
                    Console.Write("*" + var1);
                }
                var1--;
            }
        }
        Console.Write("\n");
    }

}

// Driver code
public static void Main()
{
    int n = 5;

    printPattern(n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the given
// zigzag pattern

// Function to print the zigzag pattern
function printPattern($n)
{
    $var1; $var = 1;

    for($i = 1; $i <= $n; $i++)
    {
        // for odd rows
        if($i % 2 != 0)
        {
            // calculate starting value
            $var = $var + $i - 1;
            for($j = 1; $j <= $i; $j++)
            {
                if($j == 1)
                {
                    echo $var;
                }
                else
                    echo "*" . $var;

                $var++;
            }
        }
        else // for even rows
        {    
            // calculate starting value
            $var1 = $var + $i - 1;
            for($j = 1; $j <= $i; $j++)
            {
                if($j == 1)
                {
                    // print without star
                    echo $var1;
                }
                else
                {
                    // print with star
                    echo "*" . $var1;
                }
                $var1--;
            }
        }
        echo "\n";
    }

}

// Driver code
$n = 5;

printPattern($n);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>
      // JavaScript program to print the given
      // zigzag pattern

      // Function to print the zigzag pattern
      function printPattern(n)
      {
        var var1,
          var2 = 1;

        for (var i = 1; i <= n; i++)
        {

          // for odd rows
          if (i % 2 != 0)
          {

            // calculate starting value
            var2 = var2 + i - 1;
            for (var j = 1; j <= i; j++)
            {
              if (j == 1)
              {
                document.write(var2);
              }
              else document.write("*" + var2);

              var2++;
            }
          }

          // for even rows
          else
          {
            var1 = var2 + i - 1; // calculate starting value
            for (var j = 1; j <= i; j++) {
              if (j == 1)
              {

                // print without star
                document.write(var1);
              }
              else
              {

                // print with star
                document.write("*" + var1);
              }
              var1--;
            }
          }
          document.write("<br>");
        }
      }

      // Driver code
      var n = 5;
      printPattern(n);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
1
3*2
4*5*6
10*9*8*7
11*12*13*14*15
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(1)