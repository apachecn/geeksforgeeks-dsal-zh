# 打印两个给定数字的幂之和的所有整数

> 原文:[https://www . geeksforgeeks . org/print-所有整数都是给定数字的二次幂之和/](https://www.geeksforgeeks.org/print-all-integers-that-are-sum-of-powers-of-two-given-numbers/)

给定三个非负整数 **x** 、 **y** 和**绑定**，任务是打印所有强大的整数**？按排序顺序绑定**。
一个强大的整数的形式是**x<sup>I</sup>+y<sup>j</sup>T14】对于所有的 **i，j？0** 。**

**示例:**

> **输入:** x = 3，y = 5， 限制= 10
> **输出:**2 4 6 8 10
> 3<sup>0</sup>5<sup>0</sup>= 1+1 = 2
> 3<sup>0</sup>5【5】
> 
> **输入:** x = 2，y = 3，边界= 10
> T3】输出: 2 3 4 5 7 9 10

**方法:**初始化 **i = 0** 为外环， **j = 0** 为内环，如果 **x <sup>i</sup> =有界**则脱离外环(因为对其加 y 的任何幂都会使其脱离有界)。如果**x<sup>I</sup>+y<sup>j</sup>>绑定了**然后脱离内环，在内环的每隔一次迭代中，将**x<sup>I</sup>+y<sup>j</sup>T21 保存在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，以保持强大整数的清晰有序列表。最后打印集合的内容。
为避免反复计算 **y** 的功率，可以将 **y** 的所有功率预先计算并存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print powerful integers
void powerfulIntegers(int x, int y, int bound)
{

    // Set is used to store distinct numbers
    // in sorted order
    set<int> s;
    vector<int> powersOfY;
    int i;

    // Store all the powers of y < bound in a vector
    // to avoid calculating them again and again
    powersOfY.push_back(1);
    for (i = y; i < bound && y!= 1; i = i * y)
        powersOfY.push_back(i);

    i = 0;
    while (true) {

        // x^i
        int xPowI = pow(x, i);

        for (auto j = powersOfY.begin(); j != powersOfY.end(); ++j) {
            int num = xPowI + *j;

            // If num is within limits
            // insert it into the set
            if (num <= bound)
                s.insert(num);

            // Break out of the inner loop
            else
                break;
        }

          // Adding any number to it
        // will be out of bounds
        if (xPowI >= bound || x == 1)
            break;

        // Increment i
        i++;
    }

    // Print the contents of the set
    set<int>::iterator itr;
    for (itr = s.begin(); itr != s.end(); itr++) {
        cout << *itr << " ";
    }
}

// Driver code
int main()
{
    int x = 2, y = 3, bound = 10;

    // Print powerful integers
    powerfulIntegers(x, y, bound);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.Math;

class GfG
{

    // Function to print powerful integers
    static void powerfulIntegers(int x,
                        int y, int bound)
    {

        // Set is used to store distinct numbers
        // in sorted order
        Set<Integer> s = new HashSet<>();
        ArrayList<Integer> powersOfY = new ArrayList<>();
        int i;

        // Store all the powers of y < bound in a vector
        // to avoid calculating them again and again
        powersOfY.add(1);
        for (i = y; i < bound && y != 1; i = i * y)
            powersOfY.add(i);

        i = 0;
        while (true)
        {

            // x^i
            int xPowI = (int)Math.pow((double)x, (double)i);

            for (int j = 0; j < powersOfY.size(); ++j)
            {
                int num = xPowI + powersOfY.get(j);

                // If num is within limits
                // insert it into the set
                if (num <= bound)
                    s.add(num);

                // Break out of the inner loop
                else
                    break;
            }

            // Adding any number to it
            // will be out of bounds
            if (xPowI >= bound || x == 1)
                break;

            // Increment i
            i++;
        }

        // Print the contents of the set
        Iterator itr = s.iterator();
        while(itr.hasNext())
        {
            System.out.print(itr.next() + " ");
        }
    }

    // Driver code
    public static void main(String []args)
    {
        int x = 2, y = 1, bound = 10;

        // Print powerful integers
        powerfulIntegers(x, y, bound);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print powerful integers
def powerfulIntegers(x, y, bound) :

    # Set is used to store distinct
    # numbers in sorted order
    s = set()
    powersOfY = []

    # Store all the powers of y < bound
    # in a vector to avoid calculating
    # them again and again
    powersOfY.append(1)
    i = y
    while i < bound and y!=1 :
        powersOfY.append(i)
        i *= y

    i = 0
    while (True) :

        # x^i
        xPowI = pow(x, i)

        for j in powersOfY :
            num = xPowI + j

            # If num is within limits
            # insert it into the set
            if (num <= bound) :
                s.add(num)

            # Break out of the inner loop
            else :
                break

        # Adding any number to it
        # will be out of bounds
        if (xPowI >= bound or x == 1) :
            break

        # Increment i
        i += 1

    # Print the contents of the set
    for itr in s :
        print(itr, end = " ")

# Driver code
if __name__ == "__main__" :

    x = 2
    y = 3
    bound = 10

    # Print powerful integers
    powerfulIntegers(x, y, bound)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System; 
using System.Linq;
using System.Collections.Generic; 
using System.Collections; 

class GFG
{

// Function to print powerful integers
static void powerfulIntegers(int x, int y, int bound)
{

    // Set is used to store distinct numbers
    // in sorted order
    HashSet<int> s = new HashSet<int>(); 
    ArrayList powersOfY = new ArrayList();
    int i;

    // Store all the powers of y < bound in a vector
    // to avoid calculating them again and again
    powersOfY.Add(1);
    for (i = y; i < bound && y != 1; i = i * y)
        powersOfY.Add(i);

    i = 0;
    while (true) 
    {

        // x^i
        int xPowI = (int)Math.Pow(x, i);

        for (int j = 0; j != powersOfY.Count; ++j) 
        {
            int num = xPowI + (int)powersOfY[j];

            // If num is within limits
            // insert it into the set
            if (num <= bound)
                s.Add(num);

            // Break out of the inner loop
            else
                break;
        }

          // Adding any number to it
        // will be out of bounds
        if (xPowI >= bound || x == 1)
            break;

        // Increment i
        i++;
    }

    int[] ar = s.ToArray();
    Array.Sort(ar);
    s.Clear();
    s.UnionWith(ar);

    // Print the contents of the set
    foreach (int t in s)
    {
        Console.Write( t + " ");
    }
}

// Driver code
static void Main()
{
    int x = 2, y = 3, bound = 10;

    // Print powerful integers
    powerfulIntegers(x, y, bound);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print powerful integers
function powerfulIntegers($x, $y, $bound)
{
    // Set is used to store distinct
    // numbers in sorted order
    $s = array();
    $powersOfY = array();

    // Store all the powers of y < bound
    // in a vector to avoid calculating
    // them again and again
    array_push($powersOfY, 1);
    $i = $y;
    while($i < $bound && $y != 1)
    {
        array_push($powersOfY, $i);
        $i *= $y;
    }

    $i = 0;
    while (true)
    {

        // x^i
        $xPowI = pow($x, $i);

        for ($j = 0; $j < count($powersOfY); $j++)
        {
            $num = $xPowI + $powersOfY[$j];

            // If num is within limits
            // insert it into the set
            if ($num <= $bound)
                array_push($s, $num);

            // Break out of the inner loop
            else
                break;
        }

          // Adding any number to it
        // will be out of bounds
        if ($xPowI >= $bound || $x == 1)
            break;

        // Increment i
        $i += 1;
    }

    $s = array_unique($s);
    sort($s);

    // Print the contents of the set
    foreach ($s as &$itr)
        print($itr . " ");
}

// Driver code
$x = 2;
$y = 3;
$bound = 10;

// Print powerful integers
powerfulIntegers($x, $y, $bound);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print powerful integers
function powerfulIntegers(x, y, bound)
{

    // Set is used to store distinct numbers
    // in sorted order
    var s = new Set();
    var powersOfY = [];
    var i;

    // Store all the powers of y < bound in a vector
    // to avoid calculating them again and again
    powersOfY.push(1);
    for(i = y; i < bound && y!= 1; i = i * y)
        powersOfY.push(i);

    i = 0;
    while (true)
    {
        // x^i
        var xPowI = Math.pow(x, i);

        powersOfY.forEach(j => {
            var num = xPowI + j;

            // If num is within limits
            // insert it into the set
            if (num <= bound)
                s.add(num);
        });

        // Adding any number to it
        // will be out of bounds
        if (xPowI >= bound || x == 1)
            break;

        // Increment i
        i++;
    }

    // Print the contents of the set
    [...s].sort((a, b) => a - b).forEach(itr => {
        document.write(itr + " ")
    });
}

// Driver code
var x = 2, y = 3, bound = 10;

// Print powerful integers
powerfulIntegers(x, y, bound);

// This code is contributed by itsok

</script>
```

**Output:** 

```
2 3 4 5 7 9 10
```