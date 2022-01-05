# 古尔德序列

> 原文:[https://www.geeksforgeeks.org/goulds-sequence/](https://www.geeksforgeeks.org/goulds-sequence/)

给定一个正整数 n，任务是打印高达第 n 项的古尔德序列。
在数学中，[古尔德序列](https://en.wikipedia.org/wiki/Gould%27s_sequence)是一个整数序列，其第 n <sup>个</sup>项表示帕斯卡三角形第 n-1 <sup>个</sup>行中奇数的计数。这个序列仅由 2 的幂组成。
**举例** :

```
Row Number                Pascal's triangle                 count of odd numbers in i<sup>th row</sup>
0th row                             1                                         1    
1st row                           1   1                                       2    
2nd row                         1   2   1                                     2    
3rd row                       1   3   3   1                                   4    
4th row                     1   4   6   4   1                                 2   
5th row                   1   5   10  10  5   1                               4   
6th row                 1   6   15  20  15  6   1                             4   
7th row               1   7   21  35  35  21  7   1                           8 
8th row             1  8   28   56  70   56  28  8  1                         2 
9th row           1   9  36  84  126  126  84  36  9  1                       4  
10th row        1  10  45  120 210  256  210 120 45 10  1                     4 
```

古尔德序列的前几项是-

> 1，2，2，4，2，4，4，8，2，4，4，8，4，8，8，16，2，4，4，8，4，8，8，8，8，16，4，8，8，16，8，16，16，32

生成古尔德序列的一个**简单解法**是从第 0 行到第 n 行生成帕斯卡三角形的每一行，并对每行出现的奇数进行计数。
通过计算二项式系数 C(n，I)，可以很容易地计算出第 n 行的元素。
关于这种方法的更多细节，请参考–[帕斯卡三角形](https://www.geeksforgeeks.org/pascal-triangle/)。
以下是上述思路的实现

## C++

```
// CPP program to generate
// Gould's Sequence

#include <bits/stdc++.h>
using namespace std;

// Function to generate gould's Sequence
void gouldSequence(int n)
{
    // loop to generate each row
    // of pascal's Triangle up to nth row
    for (int row_num = 1; row_num <= n; row_num++) {

        int count = 1;
        int c = 1;

        // Loop to generate each element of ith row
        for (int i = 1; i <= row_num; i++) {

            c = c * (row_num - i) / i;

            // if c is odd
            // increment count
            if (c % 2 == 1)
                count++;
        }

        // print count of odd elements
        cout << count << " ";
    }
}

// Driver code
int main()
{

    // Get n
    int n = 16;

    // Function call
    gouldSequence(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to generate
// Gould's Sequence

class GFG {

    // Function to generate gould's Sequence
    static void gouldSequence(int n)
    {
        // loop to generate each row
        // of pascal's Triangle up to nth row
        for (int row_num = 1; row_num <= n; row_num++) {

            int count = 1;
            int c = 1;

            // Loop to generate each element of ith row
            for (int i = 1; i <= row_num; i++) {

                c = c * (row_num - i) / i;

                // if c is odd
                // increment count
                if (c % 2 == 1)
                    count++;
            }

            // print count of odd elements
            System.out.print(count + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // Get n
        int n = 16;

        // Function call
        gouldSequence(n);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to generate
# Gould's Sequence

# Function to generate gould's Sequence
def gouldSequence(n):

    # loop to generate each row
    # of pascal's Triangle up to nth row
    for row_num in range (1, n):

        count = 1
        c = 1

        # Loop to generate each
        # element of ith row
        for i in range (1, row_num):
            c = c * (row_num - i) / i

            # if c is odd
            # increment count
            if (c % 2 == 1):
                count += 1

        # print count of odd elements
        print(count, end = " ")

# Driver code

# Get n
n = 16;

# Function call
gouldSequence(n)

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to generate
// Gould's Sequence

using System;
class GFG {

    // Function to generate gould's Sequence
    static void gouldSequence(int n)
    {
        // loop to generate each row
        // of pascal's Triangle up to nth row
        for (int row_num = 1; row_num <= n; row_num++) {

            int count = 1;
            int c = 1;

            // Loop to generate each element of ith row
            for (int i = 1; i <= row_num; i++) {

                c = c * (row_num - i) / i;

                // if c is odd
                // increment count
                if (c % 2 == 1)
                    count++;
            }

            // print count of odd elements
            Console.Write(count + " ");
        }
    }

    // Driver code
    public static void Main()
    {

        // Get n
        int n = 16;

        // Function call
        gouldSequence(n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate
// Gould's Sequence
// Function to generate gould's Sequence
function  gouldSequence($n)
{
    // loop to generate each row
    // of pascal's Triangle up to nth row
    for ($row_num = 1; $row_num <= $n; $row_num++) {

        $count = 1;
        $c = 1;

        // Loop to generate each element of ith row
        for ($i = 1; $i <= $row_num; $i++) {

            $c = $c * ($row_num - $i) / $i;

            // if c is odd
            // increment count
            if ($c % 2 == 1)
                $count++;
        }

        // print count of odd elements
    echo  $count , " ";
    }
}

// Driver code
    // Get n
    $n = 16;
    // Function call
    gouldSequence($n);

?>
```

## java 描述语言

```
<script>

// Javascript program to generate
// Gould's Sequence

// Function to generate gould's Sequence
function gouldSequence(n)
{
    // loop to generate each row
    // of pascal's Triangle up to nth row
    for (var row_num = 1; row_num <= n; row_num++) {

        var count = 1;
        var c = 1;

        // Loop to generate each element of ith row
        for (var i = 1; i <= row_num; i++) {

            c = c * (row_num - i) / i;

            // if c is odd
            // increment count
            if (c % 2 == 1)
                count++;
        }

        // print count of odd elements
        document.write( count + " ");
    }
}

// Driver code
// Get n
var n = 16;
// Function call
gouldSequence(n);

</script>
```

**Output** 

```
1 2 2 4 2 4 4 8 2 4 4 8 4 8 8 16 
```

一个**有效的解决方案**是基于这样一个事实，即在二进制表示中，帕斯卡三角形的第一行中奇数的计数是 2，而 1 的计数是 1，例如

```
for row=5
5 in binary = 101
count of 1's =2
2<sup>2</sup>= 4

So, 5th row of pascal triangle will have 4 odd number
```

**通过将每一个行号的二进制表示中的 1 计数到 n，我们可以生成高达 n 的古尔德序列。
下面是上述思想的实现-** 

## **C++**

```
// CPP program to generate
// Gould's Sequence

#include <bits/stdc++.h>
using namespace std;

// Utility function to count odd numbers
// in ith row of Pascals's triangle
int countOddNumber(int row_num)
{

    // Count set bits in row_num

    // Initialize count as zero
    unsigned int count = 0;
    while (row_num) {
        count += row_num & 1;
        row_num >>= 1;
    }

    // Return 2^count
    return (1 << count);
}

// Function to generate gould's Sequence
void gouldSequence(int n)
{
    // loop to generate gould's Sequence up to n
    for (int row_num = 0; row_num < n; row_num++) {

        cout << countOddNumber(row_num) << " ";
    }
}

// Driver code
int main()
{

    // Get n
    int n = 16;

    // Function call
    gouldSequence(n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// JAVA program to generate
// Gould's Sequence

class GFG {

    // Utility function to count odd numbers
    // in ith row of Pascals's triangle
    static int countOddNumber(int row_num)
    {

        // Count set bits in row_num

        // Initialize count as zero
        int count = 0;
        while (row_num > 0) {
            count += row_num & 1;
            row_num >>= 1;
        }

        // Return 2^count
        return (1 << count);
    }

    // Function to generate gould's Sequence
    static void gouldSequence(int n)
    {
        // loop to generate gould's Sequence up to n
        for (int row_num = 0; row_num < n; row_num++) {

            System.out.print(countOddNumber(row_num) + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // Get n
        int n = 16;

        // Function call
        gouldSequence(n);
    }
}
```

## **蟒蛇 3**

```
# Python3 program to generate
# Gould's Sequence

# Utility function to count odd numbers
# in ith row of Pascals's triangle
def countOddNumber(row_num):

    # Count set bits in row_num
    # Initialize count as zero
    count = 0
    while row_num != 0:
        count += row_num & 1
        row_num >>= 1

    # Return 2^count
    return (1 << count)

# Function to generate gould's Sequence
def gouldSequence(n):

    # loop to generate gould's
    # Sequence up to n
    for row_num in range(0, n):
        print(countOddNumber(row_num), end = " ")

# Driver code
if __name__ == "__main__":

    # Get n
    n = 16

    # Function call
    gouldSequence(n)

# This code is contributed
# by Rituraj Jain
```

## **C#**

```
// C# program to generate
// Gould's Sequence

using System;
class GFG {

    // Utility function to count odd numbers
    // in ith row of Pascals's triangle
    static int countOddNumber(int row_num)
    {

        // Count set bits in row_num

        // Initialize count as zero
        int count = 0;
        while (row_num > 0) {
            count += row_num & 1;
            row_num >>= 1;
        }

        // Return 2^count
        return (1 << count);
    }

    // Function to generate gould's Sequence
    static void gouldSequence(int n)
    {
        // loop to generate gould's Sequence up to n
        for (int row_num = 0; row_num < n; row_num++) {

            Console.Write(countOddNumber(row_num) + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        // Get n
        int n = 16;

        // Function call
        gouldSequence(n);
    }
}
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to generate
// Gould's Sequence

// Utility function to count odd numbers
// in ith row of Pascals's triangle
function countOddNumber($row_num)
{

    // Count set bits in row_num

    // Initialize count as zero
    $count = 0;
    while ($row_num)
    {
        $count += $row_num & 1;
        $row_num >>= 1;
    }

    // Return 2^count
    return (1 << $count);
}

// Function to generate gould's Sequence
function gouldSequence($n)
{
    // loop to generate gould's Sequence up to n
    for ($row_num = 0;
         $row_num < $n; $row_num++)
    {

        echo countOddNumber($row_num), " ";
    }
}

// Driver code

// Get n
$n = 16;

// Function call
gouldSequence($n);

// This code is contributed
// by Sach_Code
?>
```

## **java 描述语言**

```
<script>
// javascript program to generate
// Gould's Sequence
   // Utility function to count odd numbers
    // in ith row of Pascals's triangle
    function countOddNumber(row_num)
    {

        // Count set bits in row_num

        // Initialize count as zero
        var count = 0;
        while (row_num > 0) {
            count += row_num & 1;
            row_num >>= 1;
        }

        // Return 2^count
        return (1 << count);
    }

    // Function to generate gould's Sequence
    function gouldSequence(n)
    {
        // loop to generate gould's Sequence up to n
        for (var row_num = 0; row_num < n; row_num++) {

            document.write(countOddNumber(row_num) + " ");
        }
    }

    // Driver code

        // Get n
        var n = 16;

        // Function call
        gouldSequence(n);

// This code is contributed by gauravrajput1
</script>
```

****Output** 

```
1 2 2 4 2 4 4 8 2 4 4 8 4 8 8 16 
```** 

**一个**更好的解决方案(使用动态规划)**是基于这样的观察，即在前面两项的每一次幂都翻倍之后。
**例如**** 

```
first term of the sequence is - 1
Now After every power of 2 we will double the value of previous terms

Terms up to 2<sup>1</sup>  1 **2**
Terms up to 2<sup>2</sup>  1 2 **2 4**
Terms up to 2<sup>3</sup>  1 2 2 4 **2 4 4 8**
Terms up to 2<sup>4</sup>  1 2 2 4 2 4 4 8 **2 4 4 8 4 8 8 16**
```

**因此，我们可以在 2 <sup>i</sup> 之后，通过将先前项
的值加倍来计算古尔德的序列项。以下是上述方法的实现-** 

## **C++**

```
// CPP program to generate
// Gould's Sequence

#include <bits/stdc++.h>
using namespace std;

// 32768 = 2^15
#define MAX 32768

// Array to store Sequence up to
// 2^16 = 65536
int arr[2 * MAX];

// Utility function to pre-compute odd numbers
// in ith row of Pascals's triangle
int gouldSequence()
{

    // First term of the Sequence is 1
    arr[0] = 1;

    // Initialize i to 1
    int i = 1;

    // Initialize p to 1 (i.e 2^i)
    // in each iteration
    // i will be pth power of 2
    int p = 1;

    // loop to generate gould's Sequence
    while (i <= MAX) {

        // i is pth power of 2
        // traverse the array
        // from j=0 to i i.e (2^p)

        int j = 0;

        while (j < i) {

            // double the value of arr[j]
            // and store to arr[i+j]
            arr[i + j] = 2 * arr[j];
            j++;
        }

        // update i to next power of 2
        i = (1 << p);

        // increment p
        p++;
    }
}

// Function to print gould's Sequence
void printSequence(int n)
{
    // loop to generate gould's Sequence up to n

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Driver code
int main()
{

    gouldSequence();

    // Get n
    int n = 16;

    // Function call
    printSequence(n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// JAVA program to generate
// Gould's Sequence

class GFG {

    // 32768 = 2^15
    static final int MAX = 32768;

    // Array to store Sequence up to
    // 2^16 = 65536
    static int[] arr = new int[2 * MAX];

    // Utility function to pre-compute odd numbers
    // in ith row of Pascals's triangle
    static void gouldSequence()
    {

        // First term of the Sequence is 1
        arr[0] = 1;

        // Initialize i to 1
        int i = 1;

        // Initialize p to 1 (i.e 2^i)
        // in each iteration
        // i will be pth power of 2
        int p = 1;

        // loop to generate gould's Sequence
        while (i <= MAX) {

            // i is pth power of 2
            // traverse the array
            // from j=0 to i i.e (2^p)

            int j = 0;

            while (j < i) {
                // double the value of arr[j]
                // and store to arr[i+j]
                arr[i + j] = 2 * arr[j];
                j++;
            }

            // update i to next power of 2
            i = (1 << p);

            // increment p
            p++;
        }
    }

    // Function to print gould's Sequence
    static void printSequence(int n)
    {
        // loop to generate gould's Sequence up to n

        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        gouldSequence();

        // Get n
        int n = 16;

        // Function call
        printSequence(n);
    }
}
```

## **蟒蛇 3**

```
# Python3 program to generate
# Gould's Sequence

# 32768 = 2^15
MAX = 32768

# Array to store Sequence up to
# 2^16 = 65536
arr = [None] * (2 * MAX)

# Utility function to pre-compute
# odd numbers in ith row of Pascals's
# triangle
def gouldSequence():

    # First term of the Sequence is 1
    arr[0] = 1

    # Initialize i to 1
    i = 1

    # Initialize p to 1 (i.e 2^i)
    # in each iteration
    # i will be pth power of 2
    p = 1

    # loop to generate gould's Sequence
    while i <= MAX:

        # i is pth power of 2
        # traverse the array
        # from j=0 to i i.e (2^p)
        j = 0

        while j < i:

            # double the value of arr[j]
            # and store to arr[i+j]
            arr[i + j] = 2 * arr[j]
            j += 1

        # update i to next power of 2
        i = (1 << p)

        # increment p
        p += 1

# Function to print gould's Sequence
def printSequence(n):

    # loop to generate gould's Sequence
    # up to n
    for i in range(0, n):
        print(arr[i], end = " ")

# Driver code
if __name__ == "__main__":

    gouldSequence()

    # Get n
    n = 16

    # Function call
    printSequence(n)

# This code is contributed
# by Rituraj Jain
```

## **C#**

```
// C# program to generate
// Gould's Sequence

using System;
class GFG {

    // 32768 = 2^15
    static int MAX = 32768;

    // Array to store Sequence up to
    // 2^16 = 65536
    static int[] arr = new int[2 * MAX];

    // Utility function to pre-compute odd numbers
    // in ith row of Pascals's triangle
    static void gouldSequence()
    {

        // First term of the Sequence is 1
        arr[0] = 1;

        // Initialize i to 1
        int i = 1;

        // Initialize p to 1 (i.e 2^i)
        // in each iteration
        // i will be pth power of 2
        int p = 1;

        // loop to generate gould's Sequence
        while (i <= MAX) {

            // i is pth power of 2
            // traverse the array
            // from j=0 to i i.e (2^p)

            int j = 0;

            while (j < i) {
                // double the value of arr[j]
                // and store to arr[i+j]
                arr[i + j] = 2 * arr[j];
                j++;
            }

            // update i to next power of 2
            i = (1 << p);

            // increment p
            p++;
        }
    }

    // Function to print gould's Sequence
    static void printSequence(int n)
    {
        // loop to generate gould's Sequence up to n

        for (int i = 0; i < n; i++) {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {

        gouldSequence();

        // Get n
        int n = 16;

        // Function call
        printSequence(n);
    }
}
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to generate
// Gould's Sequence

// 32768 = 2^15
$MAX = 32768;

// Array to store Sequence up to
// 2^16 = 65536
$arr = array_fill(0, 2 * $MAX, 0);

// Utility function to pre-compute
// odd numbers in ith row of
// Pascals's triangle
function gouldSequence()
{
    global $MAX, $arr;

    // First term of the Sequence is 1
    $arr[0] = 1;

    // Initialize i to 1
    $i = 1;

    // Initialize p to 1 (i.e 2^i)
    // in each iteration
    // i will be pth power of 2
    $p = 1;

    // loop to generate gould's Sequence
    while ($i <= $MAX)
    {

        // i is pth power of 2
        // traverse the array
        // from j=0 to i i.e (2^p)
        $j = 0;

        while ($j < $i)
        {

            // double the value of arr[j]
            // and store to arr[i+j]
            $arr[$i + $j] = 2 * $arr[$j];
            $j++;
        }

        // update i to next power of 2
        $i = (1 << $p);

        // increment p
        $p++;
    }
}

// Function to print gould's Sequence
function printSequence($n)
{
    global $MAX, $arr;

    // loop to generate gould's
    // Sequence up to n

    for ($i = 0; $i < $n; $i++)
    {
        echo $arr[$i]." ";
    }
}

// Driver code
gouldSequence();

// Get n
$n = 16;

// Function call
printSequence($n);

// This code is contributed by mits
?>
```

## **java 描述语言**

```
<script>

// Javascript program to generate
// Gould's Sequence

// 32768 = 2^15
var MAX = 32768;

// Array to store Sequence up to
// 2^16 = 65536
var arr = Array(2 * MAX);

// Utility function to pre-compute odd numbers
// in ith row of Pascals's triangle
function gouldSequence()
{

    // First term of the Sequence is 1
    arr[0] = 1;

    // Initialize i to 1
    var i = 1;

    // Initialize p to 1 (i.e 2^i)
    // in each iteration
    // i will be pth power of 2
    var p = 1;

    // loop to generate gould's Sequence
    while (i <= MAX) {

        // i is pth power of 2
        // traverse the array
        // from j=0 to i i.e (2^p)

        var j = 0;

        while (j < i) {

            // double the value of arr[j]
            // and store to arr[i+j]
            arr[i + j] = 2 * arr[j];
            j++;
        }

        // update i to next power of 2
        i = (1 << p);

        // increment p
        p++;
    }
}

// Function to print gould's Sequence
function printSequence(n)
{
    // loop to generate gould's Sequence up to n

    for (var i = 0; i < n; i++) {
        document.write( arr[i] + " ");
    }
}

// Driver code
gouldSequence();
// Get n
var n = 16;
// Function call
printSequence(n);

</script>
```

****Output** 

```
1 2 2 4 2 4 4 8 2 4 4 8 4 8 8 16 
```**