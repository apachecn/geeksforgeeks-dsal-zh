# 将 1 到 3999 之间的十进制数转换为罗马数字

> 原文:[https://www . geesforgeks . org/converting-十进制数字-介于-1 到-3999 之间的数字-罗马数字/](https://www.geeksforgeeks.org/converting-decimal-number-lying-between-1-to-3999-to-roman-numerals/)

给定一个数字，找到它对应的罗马数字。
**例:**

```
Input : 9
Output : IX

Input : 40
Output : XL

Input :  1904
Output : MCMIV
```

下面是罗马符号的列表，其中也包括减号:

```
SYMBOL       VALUE
I             1
IV            4
V             5
IX            9
X             10
XL            40
L             50
XC            90
C             100
CD            400
D             500
CM            900 
M             1000       
```

想法是分别转换给定数字的单位、十、百和千位。如果数字是 0，那么就没有对应的罗马数字符号。数字 4 和 9 的转换与其他数字略有不同，因为这些数字遵循[减法符号](https://en.wikipedia.org/wiki/Roman_numerals)。

**将十进制数转换为罗马数字的算法**
将给定的数字与 1000、900、500、400、100、90、50、40、10、9、5、4、1 的基值进行比较。刚好小于或等于给定数字的基础值将是初始基础值(最大基础值)。将该数除以其最大的基值，相应的基符号将重复商次，余数将成为未来除法和重复的数。该过程将重复进行，直到数字变为零。

**演示上述算法的示例:**

```
Convert 3549 to its Roman Numerals
```

**输出:**

```
MMMDXLIX
```

**说明:**

**说明:**

**第一步**

*   最初数字= 3549
*   自 3549 > = 1000；最大基础值最初为 1000。
*   除以 3549/1000。商= 3，余数=549。对应的符号 **M** 将重复三次。
*   我们将结果值附加到第二个列表中。
*   现在余数不等于 0，所以我们再次调用函数。

**第二步**

*   现在，数字= 549
*   1000 > 549 >= 500 ;最大基础值将是 500。
*   除以 549/500。商= 1，余数=49。一旦&停止循环，相应的符号 **D** 将重复出现。
*   我们将结果值附加到第二个列表中。
*   现在余数不等于 0，所以我们再次调用函数。

**第三步**

*   现在，数字= 49
*   50 > 49 >= 40 ;最大的基础值是 40。
*   平分 49/40。商= 1，余数= 9。一旦&停止循环，相应的符号 **XL** 将重复出现。
*   我们将结果值附加到第二个列表中。
*   现在余数不等于 0，所以我们再次调用函数。

**第四步**

*   现在，数字= 9
*   数字 9 出现在列表 ls 中，因此我们直接从字典字典中获取值，并将余数设置为 0 并停止循环。
*   余数= 0。对应的符号 **IX** 会重复一次，现在余数为 0，所以我们不再调用该函数。

**第五步**

*   最后，我们加入第二个列表值。
*   获得的输出 **MMMDXLIX。**

以下是上述算法的实现:

## C++

```
// C++ Program to convert decimal number to
// roman numerals
#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal to Roman Numerals
int printRoman(int number)
{
    int num[] = {1,4,5,9,10,40,50,90,100,400,500,900,1000};
    string sym[] = {"I","IV","V","IX","X","XL","L","XC","C","CD","D","CM","M"};
    int i=12;    
    while(number>0)
    {
      int div = number/num[i];
      number = number%num[i];
      while(div--)
      {
        cout<<sym[i];
      }
      i--;
    }
}

//Driver program
int main()
{
    int number = 3549;

    printRoman(number);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to convert decimal number to
// roman numerals
class GFG {

// To add corresponding base symbols in the array
// to handle cases that follow subtractive notation.
// Base symbols are added index 'i'.
    static int sub_digit(char num1, char num2, int i, char[] c) {
        c[i++] = num1;
        c[i++] = num2;
        return i;
    }

// To add symbol 'ch' n times after index i in c[]
    static int digit(char ch, int n, int i, char[] c) {
        for (int j = 0; j < n; j++) {
            c[i++] = ch;
        }
        return i;
    }

// Function to convert decimal to Roman Numerals
    static void printRoman(int number) {
        char c[] = new char[10001];
        int i = 0;

        // If number entered is not valid
        if (number <= 0) {
            System.out.printf("Invalid number");
            return;
        }

        // TO convert decimal number to roman numerals
        while (number != 0) {
            // If base value of number is greater than 1000
            if (number >= 1000) {
                // Add 'M' number/1000 times after index i
                i = digit('M', number / 1000, i, c);
                number = number % 1000;
            } // If base value of number is greater than or
            // equal to 500
            else if (number >= 500) {
                // To add base symbol to the character array
                if (number < 900) {
                    // Add 'D' number/1000 times after index i
                    i = digit('D', number / 500, i, c);
                    number = number % 500;
                } // To handle subtractive notation in case of number
                // having digit as 9 and adding corresponding base
                // symbol
                else {
                    // Add C and M after index i/.
                    i = sub_digit('C', 'M', i, c);
                    number = number % 100;
                }
            } // If base value of number is greater than or equal to 100
            else if (number >= 100) {
                // To add base symbol to the character array
                if (number < 400) {
                    i = digit('C', number / 100, i, c);
                    number = number % 100;
                } // To handle subtractive notation in case of number
                // having digit as 4 and adding corresponding base
                // symbol
                else {
                    i = sub_digit('C', 'D', i, c);
                    number = number % 100;
                }
            } // If base value of number is greater than or equal to 50
            else if (number >= 50) {
                // To add base symbol to the character array
                if (number < 90) {
                    i = digit('L', number / 50, i, c);
                    number = number % 50;
                } // To handle subtractive notation in case of number
                // having digit as 9 and adding corresponding base
                // symbol
                else {
                    i = sub_digit('X', 'C', i, c);
                    number = number % 10;
                }
            } // If base value of number is greater than or equal to 10
            else if (number >= 10) {
                // To add base symbol to the character array
                if (number < 40) {
                    i = digit('X', number / 10, i, c);
                    number = number % 10;
                } // To handle subtractive notation in case of
                // number having digit as 4 and adding
                // corresponding base symbol
                else {
                    i = sub_digit('X', 'L', i, c);
                    number = number % 10;
                }
            } // If base value of number is greater than or equal to 5
            else if (number >= 5) {
                if (number < 9) {
                    i = digit('V', number / 5, i, c);
                    number = number % 5;
                } // To handle subtractive notation in case of number
                // having digit as 9 and adding corresponding base
                // symbol
                else {
                    i = sub_digit('I', 'X', i, c);
                    number = 0;
                }
            } // If base value of number is greater than or equal to 1
            else if (number >= 1) {
                if (number < 4) {
                    i = digit('I', number, i, c);
                    number = 0;
                } // To handle subtractive notation in case of
                // number having digit as 4 and adding corresponding
                // base symbol
                else {
                    i = sub_digit('I', 'V', i, c);
                    number = 0;
                }
            }
        }

        // Printing equivalent Roman Numeral
        System.out.printf("Roman numeral is: ");
        for (int j = 0; j < i; j++) {
            System.out.printf("%c", c[j]);
        }
    }

//Driver program
    public static void main(String[] args) {
        int number = 3549;

        printRoman(number);
    }
}
// This code is contributed by PrinciRaj1992 
```

## 蟒蛇 3

```
# Python3 program to convert
# decimal number to roman numerals

ls=[1000,900,500,400,100,90,50,40,10,9,5,4,1]
dict={1:"I",4:"IV",5:"V",9:"IX",10:"X",40:"XL",50:"L",90:"XC",100:"C",400:"CD",500:"D",900:"CM",1000:"M"}
ls2=[]

# Function to convert decimal to Roman Numerals
def func(no,res):
    for i in range(0,len(ls)):
        if no in ls:
            res=dict[no]
            rem=0
            break
        if ls[i]<no:
            quo=no//ls[i]
            rem=no%ls[i]
            res=res+dict[ls[i]]*quo
            break
    ls2.append(res)
    if rem==0:
        pass
    else:
        func(rem,"")

# Driver code
if __name__ == "__main__":
    func(3549, "")
    print("".join(ls2))

# This code is contributed by
# VIKAS CHOUDHARY(vikaschoudhary344)
```

## C#

```
// C# Program to convert decimal number 
// to roman numerals 
using System;
class GFG 
{ 

// To add corresponding base symbols in the 
// array to handle cases which follow subtractive 
// notation. Base symbols are added index 'i'. 
static int sub_digit(char num1, char num2, 
                         int i, char[] c) 
{ 
    c[i++] = num1; 
    c[i++] = num2; 
    return i; 
} 

// To add symbol 'ch' n times after index i in c[] 
static int digit(char ch, int n, int i, char[] c) 
{ 
    for (int j = 0; j < n; j++)
    { 
        c[i++] = ch; 
    } 
    return i; 
} 

// Function to convert decimal to Roman Numerals 
static void printRoman(int number)
{ 
    char[] c = new char[10001]; 
    int i = 0; 

    // If number entered is not valid 
    if (number <= 0) 
    { 
        Console.WriteLine("Invalid number"); 
        return; 
    } 

    // TO convert decimal number to 
    // roman numerals 
    while (number != 0) 
    { 
        // If base value of number is 
        // greater than 1000 
        if (number >= 1000)
        { 
            // Add 'M' number/1000 times after index i 
            i = digit('M', number / 1000, i, c); 
            number = number % 1000; 
        }

        // If base value of number is greater 
        // than or equal to 500 
        else if (number >= 500) 
        { 
            // To add base symbol to the character array 
            if (number < 900) 
            { 

                // Add 'D' number/1000 times after index i 
                i = digit('D', number / 500, i, c); 
                number = number % 500; 
            } 

            // To handle subtractive notation in case 
            // of number having digit as 9 and adding 
            // corresponding base symbol 
            else 
            { 

                // Add C and M after index i/. 
                i = sub_digit('C', 'M', i, c); 
                number = number % 100; 
            } 
        }

        // If base value of number is greater 
        // than or equal to 100 
        else if (number >= 100) 
        { 
            // To add base symbol to the character array 
            if (number < 400) 
            { 
                i = digit('C', number / 100, i, c); 
                number = number % 100; 
            } 

            // To handle subtractive notation in case 
            // of number having digit as 4 and adding 
            // corresponding base symbol 
            else 
            { 
                i = sub_digit('C', 'D', i, c); 
                number = number % 100; 
            } 
        } 

        // If base value of number is greater
        // than or equal to 50 
        else if (number >= 50) 
        { 

            // To add base symbol to the character array 
            if (number < 90)
            { 
                i = digit('L', number / 50, i, c); 
                number = number % 50; 
            }

            // To handle subtractive notation in case
            // of number having digit as 9 and adding 
            // corresponding base symbol 
            else 
            { 
                i = sub_digit('X', 'C', i, c); 
                number = number % 10; 
            } 
        } 

        // If base value of number is greater 
        // than or equal to 10 
        else if (number >= 10) 
        { 

            // To add base symbol to the character array 
            if (number < 40) 
            { 
                i = digit('X', number / 10, i, c); 
                number = number % 10; 
            } 

            // To handle subtractive notation in case of 
            // number having digit as 4 and adding 
            // corresponding base symbol 
            else 
            { 
                i = sub_digit('X', 'L', i, c); 
                number = number % 10; 
            } 
        } 

        // If base value of number is greater
        // than or equal to 5 
        else if (number >= 5) 
        { 
            if (number < 9)
            { 
                i = digit('V', number / 5, i, c); 
                number = number % 5; 
            }

            // To handle subtractive notation in case 
            // of number having digit as 9 and adding 
            // corresponding base symbol 
            else
            { 
                i = sub_digit('I', 'X', i, c); 
                number = 0; 
            } 
        } 

        // If base value of number is greater 
        // than or equal to 1 
        else if (number >= 1) 
        { 
            if (number < 4) 
            { 
                i = digit('I', number, i, c); 
                number = 0; 
            }

            // To handle subtractive notation in 
            // case of number having digit as 4 
            // and adding corresponding base symbol 
            else 
            { 
                i = sub_digit('I', 'V', i, c); 
                number = 0; 
            } 
        } 
    } 

    // Printing equivalent Roman Numeral 
    Console.WriteLine("Roman numeral is: "); 
    for (int j = 0; j < i; j++)
    { 
        Console.Write("{0}", c[j]); 
    } 
} 

// Driver Code
public static void Main() 
{ 
    int number = 3549; 

    printRoman(number); 
} 
} 

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript Program to convert decimal number to
// roman numerals

// Function to convert decimal to Roman Numerals
function printRoman(number)
{
    let num = [1,4,5,9,10,40,50,90,100,400,500,900,1000];
    let sym = ["I","IV","V","IX","X","XL","L","XC","C","CD","D","CM","M"];
    let i=12;
    while(number>0)
    {
    let div = Math.floor(number/num[i]);
    number = number%num[i];
    while(div--)
    {
        document.write(sym[i]);
    }
    i--;
    }
}

//Driver program

    let number = 3549;

    printRoman(number);

//This code is contributed by Manoj
</script>
```

**Output**

```
MMMDXLIX
```

参考文献:[http://blog . function fun . net/2009/01/project-Euler-89-converting-to-and-from . html](http://blog.functionalfun.net/2009/01/project-euler-89-converting-to-and-from.html)

**另一种方法 1:** :
在这种方法中我们首先要观察问题。问题陈述中给出的数字最多可为 4 位。解决这个问题的思路是:

1.  把给定的数字在不同的地方分成数字，如一、二、百或千。
2.  从千位开始打印相应的罗马值。例如，如果千位的数字是 3，那么打印罗马数字 3000。
3.  重复第二步，直到我们到达某人的位置。

**例** :
假设输入的数字是 3549。所以，从千之地开始，我们将开始印刷罗马版。在这种情况下，我们将按照下面给出的顺序打印:
**第一个**:相当于 3000
**第二个**:相当于 500
**第三个**:相当于 40
**第四个**:相当于 9
的罗马，因此，输出将是: **MMMDXLIX**

以下是上述想法的实现。

## C++

```
// C++ Program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate roman equivalent
string intToRoman(int num)
{
    // storing roman values of digits from 0-9
    // when placed at different places
    string m[] = { "", "M", "MM", "MMM" };
    string c[] = { "",  "C",  "CC",  "CCC",  "CD",
                   "D", "DC", "DCC", "DCCC", "CM" };
    string x[] = { "",  "X",  "XX",  "XXX",  "XL",
                   "L", "LX", "LXX", "LXXX", "XC" };
    string i[] = { "",  "I",  "II",  "III",  "IV",
                   "V", "VI", "VII", "VIII", "IX" };

    // Converting to roman
    string thousands = m[num / 1000];
    string hundreds = c[(num % 1000) / 100];
    string tens = x[(num % 100) / 10];
    string ones = i[num % 10];

    string ans = thousands + hundreds + tens + ones;

    return ans;
}

// Driver program to test above function
int main()
{
    int number = 3549;
    cout << intToRoman(number);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach

class GFG {
    // Function to calculate roman equivalent
    static String intToRoman(int num)
    {
        // storing roman values of digits from 0-9
        // when placed at different places
        String m[] = { "", "M", "MM", "MMM" };
        String c[] = { "",  "C",  "CC",  "CCC",  "CD",
                       "D", "DC", "DCC", "DCCC", "CM" };
        String x[] = { "",  "X",  "XX",  "XXX",  "XL",
                       "L", "LX", "LXX", "LXXX", "XC" };
        String i[] = { "",  "I",  "II",  "III",  "IV",
                       "V", "VI", "VII", "VIII", "IX" };

        // Converting to roman
        String thousands = m[num / 1000];
        String hundreds = c[(num % 1000) / 100];
        String tens = x[(num % 100) / 10];
        String ones = i[num % 10];

        String ans = thousands + hundreds + tens + ones;

        return ans;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int number = 3549;
        System.out.println(intToRoman(number));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to calculate roman equivalent

def intToRoman(num):

    # Storing roman values of digits from 0-9
    # when placed at different places
    m = ["", "M", "MM", "MMM"]
    c = ["", "C", "CC", "CCC", "CD", "D",
         "DC", "DCC", "DCCC", "CM "]
    x = ["", "X", "XX", "XXX", "XL", "L",
         "LX", "LXX", "LXXX", "XC"]
    i = ["", "I", "II", "III", "IV", "V",
         "VI", "VII", "VIII", "IX"]

    # Converting to roman
    thousands = m[num // 1000]
    hundreds = c[(num % 1000) // 100]
    tens = x[(num % 100) // 10]
    ones = i[num % 10]

    ans = (thousands + hundreds +
           tens + ones)

    return ans

# Driver code
if __name__ == "__main__":

    number = 3549

    print(intToRoman(number))

# This code is contributed by rutvik_56
```

## C#

```
// C# Program for above approach

using System;
class GFG {
    // Function to calculate roman equivalent
    static String intToRoman(int num)
    {
        // storing roman values of digits from 0-9
        // when placed at different places
        String[] m = { "", "M", "MM", "MMM" };
        String[] c = { "",  "C",  "CC",  "CCC",  "CD",
                       "D", "DC", "DCC", "DCCC", "CM" };
        String[] x = { "",  "X",  "XX",  "XXX",  "XL",
                       "L", "LX", "LXX", "LXXX", "XC" };
        String[] i = { "",  "I",  "II",  "III",  "IV",
                       "V", "VI", "VII", "VIII", "IX" };

        // Converting to roman
        String thousands = m[num / 1000];
        String hundreds = c[(num % 1000) / 100];
        String tens = x[(num % 100) / 10];
        String ones = i[num % 10];

        String ans = thousands + hundreds + tens + ones;

        return ans;
    }

    // Driver program to test above function
    public static void Main()
    {
        int number = 3549;
        Console.WriteLine(intToRoman(number));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program for above approach

// Function to calculate roman equivalent
function intToRoman($num) 
{ 
    // storing roman values of digits from 0-9 
    // when placed at different places
    $m = array("", "M", "MM", "MMM");
    $c = array("", "C", "CC", "CCC", "CD", "D", 
                   "DC", "DCC", "DCCC", "CM");
    $x = array("", "X", "XX", "XXX", "XL", "L", 
                   "LX", "LXX", "LXXX", "XC");
    $i = array("", "I", "II", "III", "IV", "V", 
                   "VI", "VII", "VIII", "IX");

    // Converting to roman
    $thousands = $m[$num / 1000];
    $hundreds = $c[($num % 1000) / 100];
    $tens = $x[($num % 100) / 10];
    $ones = $i[$num % 10];

    $ans = $thousands . $hundreds . $tens . $ones;

    return $ans;
}

// Driver Code
$number = 3549;
echo intToRoman($number);

// This code is contributed by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript Program for above approach

// Function to calculate roman equivalent
function intToRoman(num)
{
    // storing roman values of digits from 0-9
    // when placed at different places
    let m = ["", "M", "MM", "MMM"];
    let c = ["", "C", "CC", "CCC", "CD", "D",
                        "DC", "DCC", "DCCC", "CM"];
    let x = ["", "X", "XX", "XXX", "XL", "L",
                        "LX", "LXX", "LXXX", "XC"];
    let i = ["", "I", "II", "III", "IV", "V",
                        "VI", "VII", "VIII", "IX"];

    // Converting to roman
    let thousands = m[Math.floor(num/1000)];
    let hundreds = c[Math.floor((num%1000)/100)];
    let tens = x[Math.floor((num%100)/10)];
    let ones = i[num%10];

    let ans = thousands + hundreds + tens + ones;

    return ans;
}

// Driver program to test above function

    let number = 3549;
    document.write(intToRoman(number));

//This code is contributed by Mayank Tyagi
</script>
```

**Output**

```
MMMDXLIX
```

感谢**沙斯沃特·贾恩**提供上述解决方案。

**另一种方法 2:** :
在这种方法中，我们考虑数字中的主要有效数字。例:在 1234 中，主要有效数字是 1。同样，在 345 中，它是 3。
为了提取主有效数字，我们需要保持一个除数(让我们称之为 div)，比如 1000 代表 1234(因为 1234 / 1000 = 1)，100 代表 345 (345 / 100 = 3)。
另外，让我们维护一个名为 romannumber = { 1:“I”，5:“V”，10:“X”，50:“L”，100:“C”，500:“D”，1000:“M”}

**算法如下:**

**如果主有效数字< = 3**

*   罗马数字[div] * mainSignificantDigit

**如果主有效数字== 4**

*   罗马数字[div] +罗马数字[div * 5]

**if 5 < =主有效数字< =8**

*   罗马数字[div * 5] +(罗马数字[div] *(主数字-5))

**如果主有效数字==3**

*   罗马数字[div] +罗马数字[div*10]

**例** :
假设输入的数字是 3649。

ITER 1

*   最初数字= 3649
*   主要有效数字是 3。Div = 1000。
*   所以，罗马数字[1000] * 3
*   给出:嗯

**Iter 2**

*   现在，数字= 649
*   主要有效数字是 6。Div = 100。
*   所以罗马数字[100*5] +(罗马数字[div] * ( 6-5))
*   给出:DC

**Iter 3**

*   现在，数字= 49
*   主要有效数字是 4。Div = 10。
*   所以罗马数字[10] +罗马数字[10 * 5]
*   给出:XL

**Iter 4**

*   现在，数字= 9
*   主要有效数字是 9。Div = 1。
*   所以罗马数字[1] *罗马数字[1*10]
*   给出:IX

最终结果通过杵所有以上:MMMDCXLIX

下面是上面想法的 Python 实现。

## 计算机编程语言

```
# Python 3 program to convert Decimal
# number to Roman numbers.
import math

def integerToRoman(A):
    romansDict = \
        {
            1: "I",
            5: "V",
            10: "X",
            50: "L",
            100: "C",
            500: "D",
            1000: "M",
            5000: "G",
            10000: "H"
        }

    div = 1
    while A >= div:
        div *= 10

    div /= 10

    res = ""

    while A:

        # main significant digit extracted
        # into lastNum 
        lastNum = int(A / div)

        if lastNum <= 3:
            res += (romansDict[div] * lastNum)
        elif lastNum == 4:
            res += (romansDict[div] + 
                          romansDict[div * 5])
        elif 5 <= lastNum <= 8:
            res += (romansDict[div * 5] + 
            (romansDict[div] * (lastNum - 5)))
        elif lastNum == 9:
            res += (romansDict[div] +
                         romansDict[div * 10])

        A = math.floor(A % div)
        div /= 10

    return res

# Driver code
print("Roman Numeral of Integer is:" 
                   + str(integerToRoman(3549)))
```

**Output**

```
Roman Numeral of Integer is:MMMDXLIX

```

感谢 **Sriharsha Sammeta** 提供上述解决方案。
本文由**拉胡尔·阿格拉瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。