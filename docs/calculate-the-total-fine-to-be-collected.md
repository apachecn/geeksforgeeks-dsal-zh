# 计算待收罚款总额

> 原文:[https://www . geeksforgeeks . org/计算待收罚款总额/](https://www.geeksforgeeks.org/calculate-the-total-fine-to-be-collected/)

给定一个日期和包含在该日期行驶的汽车数量的整数数组(一个整数)，任务是根据以下规则计算罚款总额:

*   奇数编号的汽车只能在奇数日期行驶。
*   偶数日期的偶数车。
*   否则一辆车将被罚款 250 卢比。

**例:**

```
Input: car_num[] = {3, 4, 1, 2}, date = 15
Output: 500
Car with numbers '4' and '2' will be fined
250 each.

Input: car_num[] = {1, 2, 3} , date = 16
Output: 500
Car with numbers '1' and '3' will be fined
250 each.
```

**进场:**

1.  开始遍历给定的数组。
2.  检查当前车号和日期是否不匹配，即一个是偶数，另一个是奇数，反之亦然。
3.  如果不匹配，就对那个车号罚款。否则不行。
4.  打印罚款总额。

以下是上述方法的实现:

## C++

```
// C++ implementation to calculate
// the total fine collected
#include <bits/stdc++.h>
using namespace std;

// function to calculate the total fine collected
int totFine(int car_num[], int n, int date, int fine)
{
    int tot_fine = 0;

    // traverse the array elements
    for (int i = 0; i < n; i++)

        // if both car no and date are odd or
        // both are even, then statement
        // evaluates to true
        if (((car_num[i] ^ date) & 1) == 1)
            tot_fine += fine;

    // required total fine
    return tot_fine;
}

// Driver program to test above
int main()
{
    int car_num[] = { 3, 4, 1, 2 };
    int n = sizeof(car_num) / sizeof(car_num[0]);
    int date = 15, fine = 250;

    cout << totFine(car_num, n, date, fine);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to calculate
// the total fine collected
class GFG
{

// function to calculate
// the total fine collected
static int totFine(int car_num[], int n,
                   int date, int fine)
{
int tot_fine = 0;

// traverse the array elements
for (int i = 0; i < n; i++)

    // if both car no and date
    // are odd or both are even,
    // then statement evaluates to true
    if (((car_num[i] ^ date) & 1) == 1)
        tot_fine += fine;

// required total fine
return tot_fine;
}

// Driver Code
public static void main(String[] args)
{
    int car_num[] = { 3, 4, 1, 2 };
    int n = car_num.length;
    int date = 15, fine = 250;

    System.out.println(totFine(car_num, n,
                               date, fine));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to calculate
# the total fine collected

# function to calculate the total fine collected
def totFine(car_num, n, date, fine) :

    tot_fine = 0

    # traverse the array elements
    for i in range(n) :

        # if both car no and date are odd or
        # both are even, then statement
        # evaluates to true
        if (((car_num[i] ^ date) & 1) == 1 ):
            tot_fine += fine

    # required total fine
    return tot_fine

# Driver Program
if __name__ == "__main__" :

    car_num = [ 3, 4, 1, 2 ]
    n = len(car_num)
    date, fine = 15, 250

    # function calling
    print(totFine(car_num, n, date, fine))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation to calculate
// the total fine collected
using System;

class GFG
{

// function to calculate the
// total fine collected
static int totFine(int[] car_num, int n,
                   int date, int fine)
{
int tot_fine = 0;

// traverse the array elements
for (int i = 0; i < n; i++)

    // if both car no and date
    // are odd or both are even,
    // then statement evaluates to true
    if (((car_num[i] ^ date) & 1) == 1)
        tot_fine += fine;

// required total fine
return tot_fine;
}

// Driver Code
public static void Main()
{
    int[] car_num = { 3, 4, 1, 2 };
    int n = car_num.Length;
    int date = 15, fine = 250;

    Console.Write(totFine(car_num, n,
                          date, fine));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to calculate
// the total fine collected

// function to calculate the
// total fine collected
function totFine(&$car_num, $n,
                  $date, $fine)
{
    $tot_fine = 0;

    // traverse the array elements
    for ($i = 0; $i < $n; $i++)

        // if both car no and date
        // are odd or both are even,
        // then statement evaluates
        // to true
        if ((($car_num[$i] ^
              $date) & 1) == 1)
            $tot_fine += $fine;

    // required total fine
    return $tot_fine;
}

// Driver Code
$car_num = array(3, 4, 1, 2 );
$n = sizeof($car_num);
$date = 15;
$fine = 250;

echo totFine($car_num, $n,
             $date, $fine);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation to calculate
// the total fine collected

// function to calculate the total fine collected
function totFine(car_num, n, date, fine)
{
    let tot_fine = 0;

    // traverse the array elements
    for (let i = 0; i < n; i++)

        // if both car no and date are odd or
        // both are even, then statement
        // evaluates to true
        if (((car_num[i] ^ date) & 1) == 1)
            tot_fine += fine;

    // required total fine
    return tot_fine;
}

// Driver program to test above

    let car_num = [ 3, 4, 1, 2 ];
    let n = car_num.length;
    let date = 15, fine = 250;

    document.write(totFine(car_num, n, date, fine));

//This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
500
```

**来源:**[https://www . geeksforgeeks . org/Microsoft-面试-实习经验/](https://www.geeksforgeeks.org/microsoft-interview-experience-for-internship/)