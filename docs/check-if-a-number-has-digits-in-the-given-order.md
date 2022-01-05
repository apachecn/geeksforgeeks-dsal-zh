# 检查给定订单中的数字是否有数字

> 原文:[https://www . geeksforgeeks . org/check-如果给定订单中有数字/](https://www.geeksforgeeks.org/check-if-a-number-has-digits-in-the-given-order/)

给定一个数字 n。任务是检查该数字的数字是否遵循以下任何顺序:

*   数字是严格递增的。
*   或者，数字是严格递减的。
*   或者，数字先严格按照递增顺序，然后严格按照递减顺序。

如果数字遵循上述任何顺序，则打印是，否则打印否
**示例** :

```
Input : N = 415
Output : NO

Input : N = 123454321
Output : YES
```

通过逐个提取每个数字，从右向左遍历数字。保留一个指针，告诉当前序列是降序还是升序，-1 表示严格升序，1 表示严格降序。首先，当我们从右向左走时，顺序应该严格地增加。当我们遇到一个小于前一个数字的数字时，将标志更改为递减(即-1)，当我们按递增顺序得到等于前一个数字的任何数字时，我们直接打印编号
以下是上述方法的实现:

## C++

```
// CPP program to check if the digits are in
// the given order
#include<bits/stdc++.h>
using namespace std;

// Check if the digits follow the correct order
bool isCorrectOrder(int n)
{
    bool flag = true;

    // to store the previous digit
    int prev = -1;

    // pointer to tell what type of sequence
    // are we dealing with
    int type = -1;

    while(n != 0)
    {
        if(type ==-1)
        {
            if(prev ==-1)
            {
                prev = n % 10;
                n = n/10;
                continue;
            }
            // check if we have same digit
            // as the previous digit
            if(prev == n % 10)
            {  
                flag = false;
                break;
            }
            // checking the peak point of the number
            if(prev > n % 10)
            { 
                type = 1;
                prev = n % 10;
                n = n/10;
                continue;
            }

            prev = n % 10;
            n = n / 10;
        }
        else
        {  
            // check if we have same digit
            // as the previous digit
            if(prev == n % 10)
            {  
                flag = false;
                break;
            }
            // check if the digit is greater than
            // the previous one
            // If true, then break from the loop as
            // we are in descending order part
            if(prev < n % 10)
            {          
                flag = false;
                break;
            }

            prev = n % 10;
            n = n / 10;
        }
    }

    return flag;
}

// Driver code
int main()
{
    int n = 123454321;

    if(isCorrectOrder(n))
        cout<<"YES";
    else
        cout<<"NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the digits are in
// the given order
import java.io.*;

class GFG {

// Check if the digits follow the correct order
static boolean isCorrectOrder(int n)
{
    boolean flag = true;

    // to store the previous digit
    int prev = -1;

    // pointer to tell what type of sequence
    // are we dealing with
    int type = -1;

    while(n != 0)
    {
        if(type ==-1)
        {
            if(prev ==-1)
            {
                prev = n % 10;
                n = n/10;
                continue;
            }
            // check if we have same digit
            // as the previous digit
            if(prev == n % 10)
            {
                flag = false;
                break;
            }
            // checking the peak point of the number
            if(prev > n % 10)
            {
                type = 1;
                prev = n % 10;
                n = n/10;
                continue;
            }

            prev = n % 10;
            n = n / 10;
        }
        else
        {
            // check if we have same digit
            // as the previous digit
            if(prev == n % 10)
            {
                flag = false;
                break;
            }
            // check if the digit is greater than
            // the previous one
            // If true, then break from the loop as
            // we are in descending order part
            if(prev < n % 10)
            {        
                flag = false;
                break;
            }

            prev = n % 10;
            n = n / 10;
        }
    }

    return flag;
}

// Driver code

    public static void main (String[] args) {
        int n = 123454321;

    if(isCorrectOrder(n))
        System.out.println("YES");
    else
        System.out.println("NO");
    }
}

 // This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 program to check if the
# digits are in the given order

# Check if the digits follow
# the correct order
def isCorrectOrder(n):

    flag = True;

    # to store the previous digit
    prev = -1;

    # pointer to tell what type of
    # sequence are we dealing with
    type = -1;

    while(n != 0):
        if(type ==-1):
            if(prev ==-1):
                prev = n % 10;
                n = int(n / 10);
                continue;

            # check if we have same digit
            # as the previous digit
            if(prev == n % 10):
                flag = False;
                break;

            # checking the peak point
            # of the number
            if(prev > n % 10):
                type = 1;
                prev = n % 10;
                n = int(n / 10);
                continue;

            prev = n % 10;
            n = int(n / 10);
        else:

            # check if we have same digit
            # as the previous digit
            if(prev == n % 10):
                flag = False;
                break;

            # check if the digit is greater
            # than the previous one
            # If true, then break from the
            # loop as we are in descending
            # order part
            if(prev < n % 10):
                flag = False;
                break;

            prev = n % 10;
            n = int(n / 10);

    return flag;

# Driver code
n = 123454321;

if(isCorrectOrder(n)):
    print("YES");
else:
    print("NO");

# This Code is contributed by mits
```

## C#

```
// C# program to check if the
// digits are in the given order
using System;

class GFG
{

// Check if the digits follow
// the correct order
static bool isCorrectOrder(int n)
{
    bool flag = true;

    // to store the previous digit
    int prev = -1;

    // pointer to tell what type of
    // sequence are we dealing with
    int type = -1;

    while(n != 0)
    {
        if(type == -1)
        {
            if(prev == -1)
            {
                prev = n % 10;
                n = n / 10;
                continue;
            }

            // check if we have same digit
            // as the previous digit
            if(prev == n % 10)
            {
                flag = false;
                break;
            }

            // checking the peak point
            // of the number
            if(prev > n % 10)
            {
                type = 1;
                prev = n % 10;
                n = n / 10;
                continue;
            }

            prev = n % 10;
            n = n / 10;
        }
        else
        {
            // check if we have same digit
            // as the previous digit
            if(prev == n % 10)
            {
                flag = false;
                break;
            }

            // check if the digit is greater
            // than the previous one
            // If true, then break from the
            // loop as we are in descending
            // order part
            if(prev < n % 10)
            {    
                flag = false;
                break;
            }

            prev = n % 10;
            n = n / 10;
        }
    }

    return flag;
}

// Driver code
public static void Main ()
{
    int n = 123454321;

    if(isCorrectOrder(n))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if the
// digits are in the given order

// Check if the digits follow
// the correct order
function isCorrectOrder($n)
{
    $flag = true;

    // to store the previous digit
    $prev = -1;

    // pointer to tell what type of
    // sequence are we dealing with
    $type = -1;

    while($n != 0)
    {
        if($type ==-1)
        {
            if($prev ==-1)
            {
                $prev = $n % 10;
                $n = (int)$n / 10;
                continue;
            }

            // check if we have same digit
            // as the previous digit
            if($prev == $n % 10)
            {
                $flag = false;
                break;
            }

            // checking the peak point
            // of the number
            if($prev > $n % 10)
            {
                $type = 1;
                $prev = $n % 10;
                $n = (int)$n / 10;
                continue;
            }

            $prev = $n % 10;
            $n = (int)$n / 10;
        }
        else
        {
            // check if we have same digit
            // as the previous digit
            if($prev == $n % 10)
            {
                $flag = false;
                break;
            }

            // check if the digit is greater
            // than the previous one
            // If true, then break from the
            // loop as we are in descending
            // order part
            if($prev < $n % 10)
            {    
                $flag = false;
                break;
            }

            $prev = $n % 10;
            $n = (int) $n / 10;
        }
    }

    return $flag;
}

// Driver code
$n = 123454321;

if(isCorrectOrder($n))
    echo "YES";
else
    echo "NO";

// This Code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if the digits are in
// the given order

// Check if the digits follow the correct order
function isCorrectOrder(n)
{
    let flag = true;

    // to store the previous digit
    let prev = -1; 

    // pointer to tell what type of sequence 
    // are we dealing with
    let type = -1; 

    while(n != 0)
    {
        if(type ===-1)
        {
            if(prev ===-1)
            {
                prev = n % 10;
                n = Math.floor(n/10);
                continue;
            }
            // check if we have same digit 
            // as the previous digit
            if(prev == n % 10) 
            {   
                flag = false;
                break;
            }
            // checking the peak point of the number
            if(prev > n % 10) 
            {  
                type = 1;
                prev = n % 10;
                n = Math.floor(n/10);
                continue;
            }

            prev = n % 10;
            n = Math.floor(n / 10);
        }
        else
        {   
            // check if we have same digit
            // as the previous digit
            if(prev == n % 10) 
            {   
                flag = false;
                break;
            }
            // check if the digit is greater than 
            // the previous one 
            // If true, then break from the loop as 
            // we are in descending order part
            if(prev < n % 10) 
            {           
                flag = false;
                break;
            }

            prev = n % 10;
            n = Math.floor(n / 10);
        }
    }

    return flag;
}

// Driver code

    let n = 123454321;

    if(isCorrectOrder(n))
        document.write("YES");
    else
        document.write("NO");

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
YES
```

**时间复杂度:**O(logN)
T3】辅助空间: O(1)