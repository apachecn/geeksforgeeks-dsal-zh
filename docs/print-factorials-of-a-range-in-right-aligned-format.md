# 以右对齐格式打印一个范围的阶乘

> 原文:[https://www . geesforgeks . org/print-factories-of-a-range-in-right-aligned-format/](https://www.geeksforgeeks.org/print-factorials-of-a-range-in-right-aligned-format/)

给定两个数字 m 和 n，任务是找出包括 m 和 n 在内的所有数字的阶乘，然后以下面的格式打印。
**例:**

```
Input : 6 10
Output :
     720
    5040
   40320
  362880
 3628800

Input : 10 20
Output :
             3628800
            39916800
           479001600
          6227020800
         87178291200
       1307674368000
      20922789888000
     355687428096000
    6402373705728000
  121645100408832000
 2432902008176640000
```

我们使用 boost 多精度库存储大数的阶乘，并使用 setw()函数打印阶乘。
**setw(int)->**setw(int)是一个用于结果中意图的函数。

## C++

```
// CPP Program to print format of factorial
#include <boost/multiprecision/cpp_int.hpp>
#include <iostream>
#include <vector>
using namespace std;
using boost::multiprecision::cpp_int;

vector<cpp_int> find_factorial(int num1, int num2)
{
    // vector for store the result
    vector<cpp_int> vec;

    // variable for store the
    // each number factorial
    cpp_int fac = 1;

    // copy of first number
    int temp = num1;

    // found first number factorial
    while (1) {
        if (temp == 1)
            break;
        fac *= temp;
        temp--;
    }

    // push the first number in result vector
    vec.push_back(fac);

    // incerement the first number
    num1++;

    // found the all reaming number
    // factorial loop is working until
    // all required number factorial founded
    while (num1 <= num2) {
        fac *= num1;

        // store the result of factorial
        vec.push_back(fac);

        // incerement the first number
        num1++;
    }

    // return the result
    return (vec);
}

// function for print the result
void print_format(vector<cpp_int>& result)
{
    // setw() is used for fill the blank
    // right is used for right justification of data
    int digits = result.back().str().size();

    for (int i = 0; i < result.size(); i++) {
         cout <<  setw(digits + 1) << 
                    right << result[i] <<  endl;
    }
}

// Driver function
int main()
{

    // number which found the factorial
    // of between range
    int m = 10, n = 20;

    // store the result of factorial
    vector<cpp_int> result_fac;

    // function for found factorial
    result_fac = find_factorial(m, n);

    // function for print format
    print_format(result_fac);

    return 0;
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP Program to print
// format of factorial

function find_factorial($num1,
                        $num2)
{
    // vector for store
    // the result
    $vec;
    $t = 0;

    // variable for store the
    // each number factorial
    $fac = 1;

    // copy of first number
    $temp = $num1;

    // found first
    // number factorial
    while (1)
    {
        if ($temp == 1)
            break;
        $fac *= $temp;
        $temp--;
    }

    // push the first number
    // in result vector
    $vec[$t++] = $fac;

    // incerement the
    // first number
    $num1++;

    // found the all reaming
    // number factorial loop
    // is working until all
    // required number
    // factorial founded
    while ($num1 <= $num2)
    {
        $fac *= $num1;

        // store the result
        // of factorial
        $vec[$t++] = $fac;

        // incerement
        // the first number
        $num1++;
    }

    // return the result
    return ($vec);
}

// function for
// print the result
function print_format($result)
{
    // setw() is used for fill
    // the blank right is used
    // for right justification
    // of data
    $x = count($result);
    $digits = strlen((string)$result[$x - 1]);

    for ($i = 0; $i < $x; $i++)
    {
        echo str_pad($result[$i], ($digits + 1),
                      " ", STR_PAD_LEFT) . "\n";
    }
}

// Driver Code

// number which found
// the factorial
// of between range
$m = 10;
$n = 20;

// store the result
// of factorial
$result_fac;

// function for
// found factorial
$result_fac = find_factorial($m, $n);

// function for
// print format
print_format($result_fac);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to print
// format of factorial

function find_factorial(num1, num2)
{
    // vector for store
    // the result
    let vec = [];
    let t = 0;

    // variable for store the
    // each number factorial
    let fac = 1;

    // copy of first number
    let temp = num1;

    // found first
    // number factorial
    while (1)
    {
        if (temp == 1)
            break;
        fac *= temp;
        temp--;
    }

    // push the first number
    // in result vector
    vec[t++] = fac;

    // incerement the
    // first number
    num1++;

    // found the all reaming
    // number factorial loop
    // is working until all
    // required number
    // factorial founded
    while (num1 <= num2)
    {
        fac *= num1;

        // store the result
        // of factorial
        vec[t++] = fac;

        // incerement
        // the first number
        num1++;
    }

    // return the result
    return (vec);
}

// function for
// print the result
function print_format(result)
{
    // setw() is used for fill
    // the blank right is used
    // for right justification
    // of data
    let x = result.length;
    let digits = String(result[x - 1]).length;

    for (let i = 0; i < x; i++)
    {
    result[i] = new Array(x - i).fill(" ").join(" ") +
    result[i];
      document.write(String(result[i]) + "<br>");
    }
}

// Driver Code

// number which found
// the factorial
// of between range
let m = 10;
let n = 20;

// store the result
// of factorial
let result_fac;

// function for
// found factorial
result_fac = find_factorial(m, n);

// function for
// print format
print_format(result_fac);

// This code is contributed
// by gfgking

</script>
```

**输出:**

```
             3628800
            39916800
           479001600
          6227020800
         87178291200
       1307674368000
      20922789888000
     355687428096000
    6402373705728000
  121645100408832000
 2432902008176640000
```