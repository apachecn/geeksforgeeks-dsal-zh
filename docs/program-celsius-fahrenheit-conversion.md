# 摄氏到华氏转换的程序

> 原文:[https://www . geesforgeks . org/program-摄氏度-华氏度-换算/](https://www.geeksforgeeks.org/program-celsius-fahrenheit-conversion/)

给定以摄氏度为单位的温度，您的任务是将其转换为华氏温度。
示例:

```
Input : 0
Output : 32

Input : -40
Output : -40
```

摄氏刻度转换为华氏刻度的公式

```
 T(°F) = T(°C) × 9/5 + 32
```

## C++

```
// CPP program to convert Celsius
// scale  to Fahrenheit scale
#include <bits/stdc++.h>
using namespace std;

// function to convert Celsius
// scale to Fahrenheit scale
float Cel_To_Fah(float n)
{
    return ((n * 9.0 / 5.0) + 32.0);
}

// driver code
int main()
{
    float n = 20.0;
    cout << Cel_To_Fah(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert Celsius
// scale to Fahrenheit scale
class GFG
{
// function to convert Celsius
// scale to Fahrenheit scale
static float Cel_To_Fah(float n)
{
    return ((n * 9.0f / 5.0f) + 32.0f);
}

// Driver code
public static void main(String[] args) {
    float n = 20.0f;
    System.out.println(Cel_To_Fah(n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python code to convert Celsius scale
# to Fahrenheit scale
def Cel_To_Fah(n):

    # Used the formula
    return (n*1.8)+32

# Driver Code
n = 20
print(int(Cel_To_Fah(n)))

# This code is contributed by Chinmoy Lenka
```

## C#

```
// C# program to convert Celsius
// scale to Fahrenheit scale
using System;

class GFG  {

// function to convert Celsius
// scale to Fahrenheit scale
static float Cel_To_Fah(float n)
{
    return ((n * 9.0f / 5.0f) + 32.0f);
}

// Driver code
public static void Main()
{
    float n = 20.0f;
    Console.Write(Cel_To_Fah(n));
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to convert Celsius
// scale to Fahrenheit scale

// function to convert Celsius
// scale to Fahrenheit scale
function Cel_To_Fah($n)
{
    return (($n * 9.0 / 5.0) + 32.0);
}

    // Driver Code
    $n = 20.0;
    echo Cel_To_Fah($n);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript program to convert Celsius
// scale to Fahrenheit scale

// function to convert Celsius
// scale to Fahrenheit scale
function Cel_To_Fah(n)
{
    return ((n * 9.0 / 5.0) + 32.0);
}

// driver code

    let n = 20.0;
    document.write(Cel_To_Fah(n));

// This code is contributed by Mayank Tyagi

</script>
```

输出:

```
68
```