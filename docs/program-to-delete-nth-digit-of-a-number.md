# 删除数字第 n 位的程序

> 原文:[https://www . geeksforgeeks . org/program-to-delete-n 位数/a-number/](https://www.geeksforgeeks.org/program-to-delete-nth-digit-of-a-number/)

给定一个数字 num 和一个数字 n，任务是从开始和结束删除数字 num 的第 n 个数字。
**例:**

> **输入:** num = 1234，n = 3
> **输出:**num _ after _ deleting _ from _ start = 124，num _ after _ deleting _ from _ end = 134
> **输入:** num = 4516312，n = 2
> **输出:**num _ after _ deleting _ from _ start = 416312，num _ after _ deleting _ from _ end = 451632

**进场:**

*   **从起始位置删除第 n 个数字:**
    1.  获取要删除的数字和第 n 位数字。
    2.  [数位数](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)
    3.  通过用变量 I 计数来循环数字次数。
    4.  如果 I 等于(位数–I)，则跳过，否则将第 I 个数字添加为[new _ number =(new _ number * 10)+ith _ digit]。
*   **从结尾删除第 n 个数字:**
    1.  获取要删除的数字和第 n 位数字。
    2.  通过用变量 I 计数来循环数字次数。
    3.  如果 I 等于(n)，则跳过，否则将 ith 数字加为[new _ number =(new _ number * 10)+ith _ digit]。

**执行:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to delete nth digit
// from starting
int deleteFromStart(int num, int n)
{

    // Get the number of digits
    int d = log10(num) + 1;

    // Declare a variable
    // to form the reverse resultant number
    int rev_new_num = 0;

    // Loop with the number
    for (int i = 0; num != 0; i++) {

        int digit = num % 10;
        num = num / 10;

        if (i == (d - n)) {
            continue;
        }
        else {

            rev_new_num = (rev_new_num * 10) + digit;
        }
    }

    // Declare a variable
    // to form the resultant number
    int new_num = 0;

    // Loop with the number
    for (int i = 0; rev_new_num != 0; i++) {

        new_num = (new_num * 10)
                  + (rev_new_num % 10);
        rev_new_num = rev_new_num / 10;
    }

    // Return the resultant number
    return new_num;
}

// Function to delete nth digit
// from ending
int deleteFromEnd(int num, int n)
{

    // Declare a variable
    // to form the reverse resultant number
    int rev_new_num = 0;

    // Loop with the number
    for (int i = 1; num != 0; i++) {

        int digit = num % 10;
        num = num / 10;

        if (i == n) {
            continue;
        }
        else {

            rev_new_num = (rev_new_num * 10) + digit;
        }
    }

    // Declare a variable
    // to form the resultant number
    int new_num = 0;

    // Loop with the number
    for (int i = 0; rev_new_num != 0; i++) {

        new_num = (new_num * 10)
                  + (rev_new_num % 10);
        rev_new_num = rev_new_num / 10;
    }

    // Return the resultant number
    return new_num;
}

// Driver code
int main()
{

    // Get the number
    int num = 1234;
    cout << "Number: " << num << endl;

    // Get the digit number to be deleted
    int n = 3;
    cout << "Digit to be deleted: " << n << endl;

    // Remove the nth digit from starting
    cout << "Number after " << n
         << " digit deleted from starting: "
         << deleteFromStart(num, n) << endl;

    // Remove the nth digit from ending
    cout << "Number after " << n
         << " digit deleted from ending: "
         << deleteFromEnd(num, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG
{
    // Function to delete nth digit
    // from starting
    static int deleteFromStart(int num, int n)
    {

        // Get the number of digits
        int d = (int)Math.log10(num) + 1;

        // Declare a variable
        // to form the reverse resultant number
        int rev_new_num = 0;

        // Loop with the number
        for (int i = 0; num != 0; i++) {

            int digit = num % 10;
            num = num / 10;

            if (i == (d - n)) {
                continue;
            }
            else {

                rev_new_num = (rev_new_num * 10) + digit;
            }
        }

        // Declare a variable
        // to form the resultant number
        int new_num = 0;

        // Loop with the number
        for (int i = 0; rev_new_num != 0; i++) {

            new_num = (new_num * 10)
                    + (rev_new_num % 10);
            rev_new_num = rev_new_num / 10;
        }

        // Return the resultant number
        return new_num;
    }

    // Function to delete nth digit
    // from ending
    static int deleteFromEnd(int num, int n)
    {

        // Declare a variable
        // to form the reverse resultant number
        int rev_new_num = 0;

        // Loop with the number
        for (int i = 1; num != 0; i++) {

            int digit = num % 10;
            num = num / 10;

            if (i == n) {
                continue;
            }
            else {

                rev_new_num = (rev_new_num * 10) + digit;
            }
        }

        // Declare a variable
        // to form the resultant number
        int new_num = 0;

        // Loop with the number
        for (int i = 0; rev_new_num != 0; i++) {

            new_num = (new_num * 10)
                    + (rev_new_num % 10);
            rev_new_num = rev_new_num / 10;
        }

        // Return the resultant number
        return new_num;
    }

    // Driver code
    public static void main(String []args)
    {

        // Get the number
        int num = 1234;
        System.out.println("Number: " + num );

        // Get the digit number to be deleted
        int n = 3;
        System.out.println("Digit to be deleted: " + n );

        // Remove the nth digit from starting
        System.out.println("Number after " + n
            + " digit deleted from starting: "
            + deleteFromStart(num, n));

        // Remove the nth digit from ending
        System.out.println( "Number after " + n
            + " digit deleted from ending: "
            + deleteFromEnd(num, n));

    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to delete nth digit
# from starting
import math;
def deleteFromStart(num, n):

    # Get the number of digits
    d = (math.log10(num) + 1);

    # Declare a variable to form 
    # the reverse resultant number
    rev_new_num = 0;

    # Loop with the number
    i = 0;
    while (num != 0):

        digit = num % 10;
        num = int(num / 10);

        if (i != (int(d) - n)):
            rev_new_num = ((rev_new_num * 10) +
                                        digit);
        i += 1;

    # Declare a variable to form the
    # resultant number
    new_num = 0;

    # Loop with the number
    i = 0;
    while (rev_new_num != 0):

        new_num = ((new_num * 10) + 
                   (rev_new_num % 10));
        rev_new_num = int(rev_new_num / 10);
        i += 1;

    # Return the resultant number
    return new_num;

# Function to delete nth digit
# from ending
def deleteFromEnd(num, n):

    # Declare a variable to form 
    # the reverse resultant number
    rev_new_num = 0;

    # Loop with the number
    i = 1;
    while (num != 0):

        digit = num % 10;
        num = int(num / 10);

        if (i != n):
            rev_new_num = ((rev_new_num * 10) +
                                        digit);
        i += 1;

    # Declare a variable
    # to form the resultant number
    new_num = 0;

    # Loop with the number
    i = 0;
    while (rev_new_num != 0):

        new_num = ((new_num * 10) + 
                   (rev_new_num % 10));
        rev_new_num = int(rev_new_num / 10);
        i += 1;

    # Return the resultant number
    return new_num;

# Driver code
# Get the number
num = 1234;
print("Number:", num);

# Get the digit number to be deleted
n = 3;
print("Digit to be deleted:", n);

# Remove the nth digit from starting
print("Number after", n, 
      "digit deleted from starting:", 
            deleteFromStart(num, n));

# Remove the nth digit from ending
print("Number after", n, 
      "digit deleted from ending:", 
            deleteFromEnd(num, n));

# This code is contributed by chandan_jnu
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{
    // Function to delete nth digit
    // from starting
    static int deleteFromStart(int num, int n)
    {

        // Get the number of digits
        int d = (int)Math.Log10(num) + 1;

        // Declare a variable
        // to form the reverse resultant number
        int rev_new_num = 0;

        // Loop with the number
        for (int i = 0; num != 0; i++) {

            int digit = num % 10;
            num = num / 10;

            if (i == (d - n)) {
                continue;
            }
            else {

                rev_new_num = (rev_new_num * 10) + digit;
            }
        }

        // Declare a variable
        // to form the resultant number
        int new_num = 0;

        // Loop with the number
        for (int i = 0; rev_new_num != 0; i++) {

            new_num = (new_num * 10)
                    + (rev_new_num % 10);
            rev_new_num = rev_new_num / 10;
        }

        // Return the resultant number
        return new_num;
    }

    // Function to delete nth digit
    // from ending
    static int deleteFromEnd(int num, int n)
    {

        // Declare a variable
        // to form the reverse resultant number
        int rev_new_num = 0;

        // Loop with the number
        for (int i = 1; num != 0; i++) {

            int digit = num % 10;
            num = num / 10;

            if (i == n) {
                continue;
            }
            else {

                rev_new_num = (rev_new_num * 10) + digit;
            }
        }

        // Declare a variable
        // to form the resultant number
        int new_num = 0;

        // Loop with the number
        for (int i = 0; rev_new_num != 0; i++) {

            new_num = (new_num * 10)
                    + (rev_new_num % 10);
            rev_new_num = rev_new_num / 10;
        }

        // Return the resultant number
        return new_num;
    }

    // Driver code
    public static void Main()
    {

        // Get the number
        int num = 1234;
        Console.WriteLine("Number: " + num );

        // Get the digit number to be deleted
        int n = 3;
        Console.WriteLine("Digit to be deleted: " + n );

        // Remove the nth digit from starting
        Console.WriteLine("Number after " + n
            + " digit deleted from starting: "
            + deleteFromStart(num, n));

        // Remove the nth digit from ending
        Console.WriteLine( "Number after " + n
            + " digit deleted from ending: "
            + deleteFromEnd(num, n));

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of above approach
// Function to delete nth digit
// from starting

function  deleteFromStart($num, $n)
{

    // Get the number of digits
    $d = (log10($num) + 1);

    // Declare a variable
    // to form the reverse resultant number
    $rev_new_num = 0;

    // Loop with the number
    for ($i = 0; $num != 0; $i++) {

        $digit = $num % 10;
        $num = (int)$num / 10;

        if ($i == ($d - $n)) {
            continue;
        }
        else {

            $rev_new_num = ($rev_new_num * 10) + $digit;
        }
    }

    // Declare a variable
    // to form the resultant number
    $new_num = 0;

    // Loop with the number
    for ($i = 0; $rev_new_num != 0; $i++) {

        $new_num = ($new_num * 10)
                + ($rev_new_num % 10);
        $rev_new_num = (int)$rev_new_num / 10;
    }

    // Return the resultant number
    return $new_num;
}

// Function to delete nth digit
// from ending

function  deleteFromEnd($num, $n)
{

    // Declare a variable
    // to form the reverse resultant number
    $rev_new_num = 0;

    // Loop with the number
    for ($i = 1; $num != 0; $i++) {

        $digit = $num % 10;
        $num = (int)$num / 10;

        if ($i == $n) {
            continue;
        }
        else {

            $rev_new_num = ($rev_new_num * 10) + $digit;
        }
    }

    // Declare a variable
    // to form the resultant number
    $new_num = 0;

    // Loop with the number
    for ($i = 0; $rev_new_num != 0; $i++) {

        $new_num = ($new_num * 10)
                + ($rev_new_num % 10);
        $rev_new_num = (int)$rev_new_num / 10;
    }

    // Return the resultant number
    return $new_num;
}

// Driver code
    // Get the number
    $num = 1234;
    echo "Number: " , $num ,"\n";

    // Get the digit number to be deleted
    $n = 3;
    echo "Digit to be deleted: " ,$n ,"\n";

    // Remove the nth digit from starting
    echo  "Number after " , $n,
        " digit deleted from starting: ",
         deleteFromStart($num, $n),"\n";

    // Remove the nth digit from ending
    echo  "Number after " , $n,
         " digit deleted from ending: ",
        deleteFromEnd($num, $n) ,"\n";

?>
// This code is contributed by jit_t.
```

## java 描述语言

```
<script>

    // Javascript implementation of 
    // the above approach

    // Function to delete nth digit
    // from starting
    function deleteFromStart(num, n)
    {

        // Get the number of digits
        let d = parseInt(Math.log10(num), 10) + 1;

        // Declare a variable
        // to form the reverse resultant number
        let rev_new_num = 0;

        // Loop with the number
        for (let i = 0; num != 0; i++) {

            let digit = num % 10;
            num = parseInt(num / 10, 10);

            if (i == (d - n)) {
                continue;
            }
            else {

                rev_new_num = (rev_new_num * 10) + digit;
            }
        }

        // Declare a variable
        // to form the resultant number
        let new_num = 0;

        // Loop with the number
        for (let i = 0; rev_new_num != 0; i++) {

            new_num = (new_num * 10)
                    + (rev_new_num % 10);
            rev_new_num = parseInt(rev_new_num / 10, 10);
        }

        // Return the resultant number
        return new_num;
    }

    // Function to delete nth digit
    // from ending
    function deleteFromEnd(num, n)
    {

        // Declare a variable
        // to form the reverse resultant number
        let rev_new_num = 0;

        // Loop with the number
        for (let i = 1; num != 0; i++) {

            let digit = num % 10;
            num = parseInt(num / 10, 10);

            if (i == n) {
                continue;
            }
            else {

                rev_new_num = (rev_new_num * 10) + digit;
            }
        }

        // Declare a variable
        // to form the resultant number
        let new_num = 0;

        // Loop with the number
        for (let i = 0; rev_new_num != 0; i++) {

            new_num = (new_num * 10)
                    + (rev_new_num % 10);
            rev_new_num = parseInt(rev_new_num / 10, 10);
        }

        // Return the resultant number
        return new_num;
    }

    // Get the number
    let num = 1234;
    document.write("Number: " + num + "</br>");

    // Get the digit number to be deleted
    let n = 3;
    document.write("Digit to be deleted: " + n  + "</br>");

    // Remove the nth digit from starting
    document.write("Number after " + n
                      + " digit deleted from starting: "
                      + deleteFromStart(num, n) + "</br>");

    // Remove the nth digit from ending
    document.write( "Number after " + n
                      + " digit deleted from ending: "
                      + deleteFromEnd(num, n));

</script>
```

**Output:** 

```
Number: 1234
Digit to be deleted: 3
Number after 3 digit deleted from starting: 124
Number after 3 digit deleted from ending: 134
```

**另一种方法:**(将数字转换为字符串)
**时间复杂度:** O(logN)

## C++

```
// C++ implementation to delete nth digit
// from starting with O(logN) time complexity.
#include<bits/stdc++.h>
using namespace std;

// function to delete nth number from starting
static string fromStart(string inp, int del) 
{
    string inp1 = inp.substr(0, del - 1);
    string inp2 = inp.substr(del, inp.length());
    return inp1 + inp2;
}

// function to delete nth number from ending
static string fromEnd(string inp, int del) 
{
    string inp1 = inp.substr(0, inp.length() - del);
    string inp2 = inp.substr(inp.length() - del + 1, 
                                      inp.length());
    return inp1 + inp2;
}

// Driver Code
int main() 
{
    int in = 1234;

    // type cast input number to string
    stringstream ss;
    ss << in;
    string inp = ss.str();
    int del = 3;
    cout << "num_after_deleting_from_starting " 
         << fromStart(inp, del) << endl;
    cout << "num_after_deleting_from_ending "
         << fromEnd(inp, del) << endl;
    return 0;
}

// This code is contributed by chandan_jnu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to delete nth digit
// from starting with O(logN) time complexity.

public class DeleteN {

    public static void main(String args[]) {

        int in = 1234;
        // type cast input number to string
        String inp = Integer.toString(in);
        int del = 3;
        System.out.println("num_after_deleting_from_starting " + fromStart(inp, del));
        System.out.println("num_after_deleting_from_ending " + fromEnd(inp, del));
    }

    // function to delete nth number from starting
    static String fromStart(String inp, int del) {

        try {
            String inp1 = inp.substring(0, del - 1);
            String inp2 = inp.substring(del, inp.length());
            return inp1 + inp2;
        }

        catch (Exception e) {
            return "Check Input";
        }
    }

    // function to delete nth number from ending
    static String fromEnd(String inp, int del) {

        try {
            String inp1 = inp.substring(0, inp.length() - del);
            String inp2 = inp.substring(inp.length() - del + 1, inp.length());
            return inp1 + inp2;
        }

        catch (Exception e) {
            return "Check Input";
        }
    }

}
```

## 蟒蛇 3

```
# Python3 implementation to delete nth digit
# from starting with O(logN) time complexity.

# function to del1ete nth number 
# from starting
def fromStart(inp, del11): 

    inp1 = inp[0:del1 - 1];
    inp2 = inp[del1:len(inp)];
    return inp1 + inp2;

# function to delete nth number 
# from ending
def fromEnd(inp, del1):
    inp1 = inp[0:len(inp) - del1];
    inp2 = inp[len(inp) - del1 + 1:len(inp)];
    return inp1 + inp2;

# Driver Code
in1 = 1234;

# type cast input number to string
inp = str(in1);
del1 = 3;
print("num_after_deleting_from_starting", 
                   fromStart(inp, del1));
print("num_after_deleting_from_ending", 
                   fromEnd(inp, del1));

# This code is contributed by chandan_jnu
```

## C#

```
// C# implementation to delete nth digit 
// from starting with O(logN) time complexity. 
using System ;

public class DeleteN { 

    public static void Main() { 

        int num = 1234; 

        // type cast input number to string 
        string inp = Convert.ToString(num) ; 
        int del = 3; 
        Console.WriteLine("num_after_deleting_from_starting " 
                            + fromStart(inp, del)); 
        Console.WriteLine("num_after_deleting_from_ending " 
                            + fromEnd(inp, del)); 
    } 

    // function to delete nth number from starting 
    static String fromStart(string inp, int del) { 

        try { 
            string inp1 = inp.Substring(0, del - 1); 
            string inp2 = inp.Substring(del, inp.Length - del); 
            return inp1 + inp2; 
        } 

        catch (Exception ) { 
            return "Check Input"; 
        } 
    } 

    // function to delete nth number from ending 
    static String fromEnd(string inp, int del) { 

        try { 
            string inp1 = inp.Substring(0, inp.Length - del); 
            string inp2 = inp.Substring(inp.Length - del + 1, del - 1); 
            return inp1 + inp2; 
        } 

        catch (Exception e) { 
            Console.WriteLine(e) ;
            return "Check Input"; 
        } 
    } 
} 

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to delete nth digit
// from starting with O(logN) time complexity.

// function to delete nth number from starting
function fromStart($inp, $del) 
{
    $inp1 = substr($inp, 0, $del - 1);
    $inp2 = substr($inp, $del, strlen($inp));
    return $inp1.$inp2;
}

// function to delete nth number from ending
function fromEnd($inp, $del) 
{
    $inp1 = substr($inp, 0, strlen($inp) - $del);
    $inp2 = substr($inp, strlen($inp) - $del + 1, 
                         strlen($inp));
    return $inp1.$inp2;
}

// Driver Code
$in = 1234;

// type cast input number to string
$inp = strval($in);
$del = 3;
print("num_after_deleting_from_starting " .
             fromStart($inp, $del) . "\n");
print("num_after_deleting_from_ending " . 
                    fromEnd($inp, $del));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to delete nth digit
    // from starting with O(logN) time complexity.

    // function to delete nth number from starting
    function fromStart(inp, del) {
      let inp1 = inp.substring(0, del - 1);
      let inp2 = inp.substring(del, inp.length);
      return inp1 + inp2;
    }

    function fromEnd(inp, del) {

      let inp1 = inp.substring(0, inp.length - del);
      let inp2 = inp.substring(inp.length - del + 1, inp.length - del + 1 + inp.length);
      return inp1 + inp2;
    }

    let In = 1234;

      // type cast input number to string
      let inp = In.toString();
    let del = 3;
    document.write("num_after_deleting_from_starting " + fromStart(inp, del) + "</br>");
    document.write("num_after_deleting_from_ending " + fromEnd(inp, del) + "</br>");

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
num_after_deleting_from_starting 124
num_after_deleting_from_ending 134
```