# 写大数幂函数

> 原文:[https://www . geesforgeks . org/writing-power-function-for-大数/](https://www.geeksforgeeks.org/writing-power-function-for-large-numbers/)

我们给出了两个数字 x 和 n，它们分别是基数和指数。写一个计算 x^n 的函数，其中 1<= x, n <= 10000 and overflow may happen
t1【例:T3】

```
Input : x = 5, n = 20
Output : 95367431640625

Input : x = 2, n = 100
Output : 1267650600228229401496703205376
```

在上面的例子中，2^100 有 31 位数字，即使我们使用 long long int 也不可能存储这些数字，long int 最多可以存储 18 位数字。背后的想法是将 x，n 乘以并将结果存储在 res[]数组中。
这里是求一个数的幂的算法。
**力量(n)**
1。创建一个最大大小的数组 res[]并将 x 存储在 res[]数组中，并将 res_size 初始化为 x 中的位数。
2。对从 i=2 到 n 的所有数字执行以下操作
…..将 x 乘以 res[]并更新 res[]和 res_size 以存储乘法结果。
**乘(res[]，x)**
1。将进位初始化为 0。
2。对 i=0 到 res_size-1
执行以下操作……a .找到 prod = RES[I]* x+进位。
….b .将产品的最后一位数字存储在 res[i]中，其余数字存储在 carry 中。
3。将进位的所有数字存储在 res[]中，并将 res_size 增加位数。

## C++

```
// C++ program to compute
// factorial of big numbers
#include <iostream>
using namespace std;

// Maximum number of digits in
// output
#define MAX 100000

// This function multiplies x
// with the number represented by res[].
// res_size is size of res[] or
// number of digits in the number
// represented by res[]. This function
// uses simple school mathematics
// for multiplication.
// This function may value of res_size
// and returns the new value of res_size
int multiply(int x, int res[], int res_size) {

// Initialize carry
int carry = 0;

// One by one multiply n with
// individual digits of res[]
for (int i = 0; i < res_size; i++) {
    int prod = res[i] * x + carry;

    // Store last digit of
    // 'prod' in res[]
    res[i] = prod % 10;

    // Put rest in carry
    carry = prod / 10;
}

// Put carry in res and
// increase result size
while (carry) {
    res[res_size] = carry % 10;
    carry = carry / 10;
    res_size++;
}
return res_size;
}

// This function finds
// power of a number x
void power(int x, int n)
{

//printing value "1" for power = 0
if(n == 0 ){
    cout<<"1";
    return;
}

int res[MAX];
int res_size = 0;
int temp = x;

// Initialize result
while (temp != 0) {
    res[res_size++] = temp % 10;
    temp = temp / 10;
}

// Multiply x n times
// (x^n = x*x*x....n times)
for (int i = 2; i <= n; i++)
    res_size = multiply(x, res, res_size);

cout << x << "^" << n << " = ";
for (int i = res_size - 1; i >= 0; i--)
    cout << res[i];
}

// Driver program
int main() {
int exponent = 100;
int base = 20;
power(base, exponent);
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute
// factorial of big numbers
class GFG {
// Maximum number of digits in
// output
static final int MAX = 100000;

// This function multiplies x
// with the number represented by res[].
// res_size is size of res[] or
// number of digits in the number
// represented by res[]. This function
// uses simple school mathematics
// for multiplication.
// This function may value of res_size
// and returns the new value of res_size
static int multiply(int x, int res[], int res_size) {

    // Initialize carry
    int carry = 0;

    // One by one multiply n with
    // individual digits of res[]
    for (int i = 0; i < res_size; i++) {
    int prod = res[i] * x + carry;

    // Store last digit of
    // 'prod' in res[]
    res[i] = prod % 10;

    // Put rest in carry
    carry = prod / 10;
    }

    // Put carry in res and
    // increase result size
    while (carry > 0) {
    res[res_size] = carry % 10;
    carry = carry / 10;
    res_size++;
    }
    return res_size;
}

// This function finds
// power of a number x
static void power(int x, int n) {

    //printing value "1" for power = 0
    if(n == 0 ){
    System.out.print("1");
    return;
}
    int res[] = new int[MAX];
    int res_size = 0;
    int temp = x;

    // Initialize result
    while (temp != 0) {
    res[res_size++] = temp % 10;
    temp = temp / 10;
    }

    // Multiply x n times
    // (x^n = x*x*x....n times)
    for (int i = 2; i <= n; i++)
    res_size = multiply(x, res, res_size);

    System.out.print(x + "^" + n + " = ");
    for (int i = res_size - 1; i >= 0; i--)
    System.out.print(res[i]);
}
// Driver code
public static void main(String[] args) {
    int exponent = 100;
    int base = 2;
    power(base, exponent);
}
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to compute
# factorial of big numbers

# Maximum number of digits in
# output
MAX=100000

# This function multiplies x
# with the number represented by res[].
# res_size is size of res[] or
# number of digits in the number
# represented by res[]. This function
# uses simple school mathematics
# for multiplication.
# This function may value of res_size
# and returns the new value of res_size
def multiply(x, res, res_size):

    # Initialize carry
    carry = 0

    # One by one multiply n with
    # individual digits of res[]
    for i in range(res_size):
        prod = res[i] * x + carry

        # Store last digit of
        # 'prod' in res[]
        res[i] = prod % 10

        # Put rest in carry
        carry = prod // 10

    # Put carry in res and
    # increase result size
    while (carry):
        res[res_size] = carry % 10
        carry = carry // 10
        res_size+=1

    return res_size

# This function finds
# power of a number x
def power(x,n):

    # printing value "1" for power = 0
     if (n == 0) :
        print("1")
        return

    res=[0 for i in range(MAX)]
    res_size = 0
    temp = x

    # Initialize result
    while (temp != 0):
        res[res_size] = temp % 10;
        res_size+=1
        temp = temp // 10

    # Multiply x n times
    # (x^n = x*x*x....n times)
    for i in range(2, n + 1):
        res_size = multiply(x, res, res_size)

    print(x , "^" , n , " = ",end="")
    for i in range(res_size - 1, -1, -1):
        print(res[i], end="")

# Driver program

exponent = 100
base = 2
power(base, exponent)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to compute
// factorial of big numbers
using System;

class GFG {

    // Maximum number of digits in
    // output
    static int MAX = 100000;

    // This function multiplies x
    // with the number represented by res[].
    // res_size is size of res[] or
    // number of digits in the number
    // represented by res[]. This function
    // uses simple school mathematics
    // for multiplication.
    // This function may value of res_size
    // and returns the new value of res_size
    static int multiply(int x, int []res,
                            int res_size)
    {

        // Initialize carry
        int carry = 0;

        // One by one multiply n with
        // individual digits of res[]
        for (int i = 0; i < res_size; i++)
        {
            int prod = res[i] * x + carry;

            // Store last digit of
            // 'prod' in res[]
            res[i] = prod % 10;

            // Put rest in carry
            carry = prod / 10;
        }

        // Put carry in res and
        // increase result size
        while (carry > 0)
        {
            res[res_size] = carry % 10;
            carry = carry / 10;
            res_size++;
        }

        return res_size;
    }

    // This function finds
    // power of a number x
    static void power(int x, int n)
    {
        //printing value "1" for power = 0
    if(n == 0 ){
    Console.Write("1");
    return;
    }
        int []res = new int[MAX];
        int res_size = 0;
        int temp = x;

        // Initialize result
        while (temp != 0) {
            res[res_size++] = temp % 10;
            temp = temp / 10;
        }

        // Multiply x n times
        // (x^n = x*x*x....n times)
        for (int i = 2; i <= n; i++)
            res_size = multiply(x, res, res_size);

        Console.Write(x + "^" + n + " = ");

        for (int i = res_size - 1; i >= 0; i--)
            Console.Write(res[i]);
    }

    // Driver code
    public static void Main()
    {
        int exponent = 100;
        int b_ase = 2;
        power(b_ase, exponent);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute
// factorial of big numbers

// Maximum number of
// digits in output

// This function multiplies
// x with the number represented
// by res[]. res_size is size of
// res[] or number of digits in
// the number represented by res[].
// This function uses simple school
// mathematics for multiplication.
// This function may value of
// res_size and returns the new
// value of res_size
function multiply($x, $res)
{

// Initialize carry
$carry = 0;
$res_size = count($res);

// One by one multiply
// n with individual
// digits of res[]
for ($i = 0;
    $i < $res_size; $i++)
{
    $prod = $res[$i] *
            $x + $carry;

    // Store last digit of
    // 'prod' in res[]
    $res[$i] = $prod % 10;

    // Put rest in carry
    $carry = (int)($prod / 10);
}

// Put carry in res and
// increase result size
while ($carry)
{
    if($carry % 10)
    $res[$res_size++] = $carry % 10;
    $carry = (int)($carry / 10);
}
return $res;
}

// This function finds
// power of a number x
function power($x, $n)
{
     //printing value "1" for power = 0
    if($n == 0 ){
    echo "1";
    return;
    }
$res_size = 0;
$res = array();
$temp = $x;

// Initialize result
while ($temp != 0)
{
    $res[$res_size++] = $temp % 10;
    $temp = $temp / 10;
}

// Multiply x n times
// (x^n = x*x*x....n times)
for ($i = 2; $i <= $n; $i++)
    $res = multiply($x, $res);

echo $x . "^" .
    $n . " = ";
$O = 0;
for ($i = count($res) - 1;
    $i >= 0; $i--, $O++)
if($res[$i])
break;
for ($i = count($res) - $O - 1;
            $i >= 0; $i--)
    echo $res[$i];
}

// Driver Code
$exponent = 100;
$base = 2;
power($base, $exponent);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to compute
// factorial of big numbers

// Maximum number of digits in
// output
let MAX = 100000

// This function multiplies x
// with the number represented by res[].
// res_size is size of res[] or
// number of digits in the number
// represented by res[]. This function
// uses simple school mathematics
// for multiplication.
// This function may value of res_size
// and returns the new value of res_size
function multiply( x,  res, res_size) {

// Initialize carry
let carry = 0;

// One by one multiply n with
// individual digits of res[]
for (let i = 0; i < res_size; i++) {
    let prod = res[i] * x + carry;

    // Store last digit of
    // 'prod' in res[]
    res[i] = prod % 10;

    // Put rest in carry
    carry = Math.floor(prod / 10);
}

// Put carry in res and
// increase result size
while (carry) {
    res[res_size] = carry % 10;
    carry =  Math.floor(carry / 10);
    res_size++;
}
return res_size;
}

// This function finds
// power of a number x
function power( x, n)
{

//printing value "1" for power = 0
if(n == 0 ){
    document.write("1");
    return;
}

let res = new Array(MAX);
let res_size = 0;
let temp = x;

// Initialize result
while (temp != 0) {
    res[res_size++] = temp % 10;
    temp =  Math.floor(temp / 10);
}

// Multiply x n times
// (x^n = x*x*x....n times)
for (let i = 2; i <= n; i++)
    res_size = multiply(x, res, res_size);

document.write( x + "^" + n + " = ");
for (let i = res_size - 1; i >= 0; i--)
    document.write(res[i]);
}

// Driver Code

let exponent = 100;
let base = 2;
power(base, exponent);

</script>
```

**输出:**

```
2^100 = 1267650600228229401496703205376
```