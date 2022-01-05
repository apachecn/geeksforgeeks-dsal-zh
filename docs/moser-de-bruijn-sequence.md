# 莫塞-德布鲁因序列

> 原文:[https://www.geeksforgeeks.org/moser-de-bruijn-sequence/](https://www.geeksforgeeks.org/moser-de-bruijn-sequence/)

给定一个整数“n”，打印 Moser-de Bruijn 序列的前“n”项。

**莫瑟-德布鲁因序列**是将数字 4(例如 1、4、16、64 等)的不同幂相加得到的序列。

**示例:**

```
Input : 5
Output : 0 1 4 5 16

Input : 10
Output : 0 1 4 5 16 17 20 21 64 65
```

观察到序列的项遵循递归关系:

```
1) S(2 * n) = 4 * S(n)
2) S(2 * n + 1) = 4 * S(n) + 1
with S(0) = 0 and S(1) = 1
```

这里要注意的是，任何 4 的非相异幂之和的数都不是序列的一部分。例如，8 不是序列的一部分，因为它是 4 的非相异幂的和，即 4 和 4。
因此，任何不是 4 的幂并且出现在序列中的数必须是 4 的不同幂的和。
例如，21 是序列的一部分，即使它不是 4 的幂，因为它是 4 的不同幂的和，即 1、4 和 16。

使用上面讨论的递归关系来有效地生成序列。

## C++

```
// CPP code to generate first 'n' terms
// of the Moser-de Bruijn Sequence
#include <bits/stdc++.h>
using namespace std;

// Function to generate nth term
// of Moser-de Bruijn Sequence
int gen(int n)
{
    // S(0) = 0
    if (n == 0)
        return 0;

    // S(1) = 1
    else if (n == 1)
        return 1;

    // S(2 * n) = 4 * S(n)
    else if (n % 2 == 0)
        return 4 * gen(n / 2);

    // S(2 * n + 1) = 4 * S(n) + 1
    else if (n % 2 == 1)
        return 4 * gen(n / 2) + 1;
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
void moserDeBruijn(int n)
{
    for (int i = 0; i < n; i++)
        cout << gen(i) << " ";
    cout << "\n";
}

// Driver Code
int main()
{
    int n = 15;
    cout << "First " << n << " terms of "
         << "Moser-de Bruijn Sequence : \n";
    moserDeBruijn(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to generate first 'n' terms
// of the Moser-de Bruijn Sequence

class GFG
{

// Function to generate nth term
// of Moser-de Bruijn Sequence
public static int gen(int n)
{

    // S(0) = 0
    if (n == 0)
        return 0;

    // S(1) = 1
    else if (n == 1)
        return 1;

    // S(2 * n) = 4 * S(n)
    else if (n % 2 == 0)
        return 4 * gen(n / 2);

    // S(2 * n + 1) = 4 * S(n) + 1
    else if (n % 2 == 1)
        return 4 * gen(n / 2) + 1;
    return 0;
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
public static void moserDeBruijn(int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(gen(i) + " ");
    System.out.println();
}

// Driver Code
public static void main(String args[])
{
    int n = 15;
    System.out.println("First " + n +
                       " terms of " +
      "Moser-de Bruijn Sequence : ");
    moserDeBruijn(n);
}
}

// This code is contributed by JaideepPyne.
```

## 蟒蛇 3

```
# Python code to generate first
# 'n' terms of the Moser-de
# Bruijn Sequence

# Function to generate nth term
# of Moser-de Bruijn Sequence
def gen(n):

    # S(0) = 0
    if n == 0:
        return 0

    # S(1) = 1
    elif n ==1:
        return 1

    # S(2 * n) = 4 * S(n)
    elif n % 2 ==0:
        return 4 * gen(n // 2)

    # S(2 * n + 1) = 4 * S(n) + 1
    elif n % 2 == 1:
        return 4 * gen(n // 2) +1

# Generating the first 'n' terms
# of Moser-de Bruijn Sequence
def moserDeBruijn(n):
    for i in range(n):
        print(gen(i), end = " ")

# Driver Program
n = 15
print("First", n, "terms of ",
       "Moser-de Bruijn Sequence:")
moserDeBruijn(n)

# This code is contributed by Shrikant13
```

## C#

```
// C# code to generate first 'n' terms
// of the Moser-de Bruijn Sequence
using System;

class GFG {

// Function to generate nth term
// of Moser-de Bruijn Sequence
public static int gen(int n)
{

    // S(0) = 0
    if (n == 0)
        return 0;

    // S(1) = 1
    else if (n == 1)
        return 1;

    // S(2 * n) = 4 * S(n)
    else if (n % 2 == 0)
        return 4 * gen(n / 2);

    // S(2 * n + 1) = 4 * S(n) + 1
    else if (n % 2 == 1)
        return 4 * gen(n / 2) + 1;
    return 0;
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
public static void moserDeBruijn(int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(gen(i) + " ");
        Console.WriteLine();
}

// Driver Code
public static void Main()
{
    int n = 15;
    Console.WriteLine("First " + n +
                    " terms of " +
    "Moser-de Bruijn Sequence : ");
    moserDeBruijn(n);
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to generate first 'n' terms
// of the Moser-de Bruijn Sequence

// Function to generate nth term
// of Moser-de Bruijn Sequence
function gen($n)
{

    // S(0) = 0
    if ($n == 0)
        return 0;

    // S(1) = 1
    else if ($n == 1)
        return 1;

    // S(2 * n) = 4 * S(n)
    else if ($n % 2 == 0)
        return 4 * gen($n / 2);

    // S(2 * n + 1) = 4 * S(n) + 1
    else if ($n % 2 == 1)
        return 4 * gen($n / 2) + 1;
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
function moserDeBruijn($n)
{
    for ($i = 0; $i < $n; $i++)
        echo(gen($i) . " ");
    echo("\n");
}

// Driver Code
$n = 15;
echo("First " . $n . " terms of " .
  "Moser-de Bruijn Sequence : \n");
echo(moserDeBruijn($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript code to generate first 'n' terms
// of the Moser-de Bruijn Sequence

// Function to generate nth term
// of Moser-de Bruijn Sequence
function gen(n)
{

    // S(0) = 0
    if (n == 0)
        return 0;

    // S(1) = 1
    else if (n == 1)
        return 1;

    // S(2 * n) = 4 * S(n)
    else if (n % 2 == 0)
        return 4 * gen(parseInt(n / 2, 10));

    // S(2 * n + 1) = 4 * S(n) + 1
    else if (n % 2 == 1)
        return 4 * gen(parseInt(n / 2, 10)) + 1;

    return 0;
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
function moserDeBruijn(n)
{
    for(let i = 0; i < n; i++)
        document.write(gen(i) + " ");

    document.write("</br>");
}

// Driver code
let n = 15;
document.write("First " + n + " terms of " +
               "Moser-de Bruijn Sequence : " + "</br>");
moserDeBruijn(n);

// This code is contributed by decode2207

</script>
```

**输出:**

```
First 15 terms of Moser-de Bruijn Sequence : 
0 1 4 5 16 17 20 21 64 65 68 69 80 81 84
```

**动态编程实现:**

## C++

```
// CPP code to generate first 'n' terms
// of the Moser-de Bruijn Sequence
#include <bits/stdc++.h>
using namespace std;

// Function to generate nth term
// of Moser-de Bruijn Sequence
int gen(int n)
{
    int S[n+1];

    S[0] = 0;
    S[1] = 1;

    for (int i = 2; i <= n; i++)
    {   
        // S(2 * n) = 4 * S(n)
        if (i % 2 == 0)
           S[i] = 4 * S[i / 2];

        // S(2 * n + 1) = 4 * S(n) + 1
        else
           S[i] = 4 * S[i / 2] + 1;
    }

    return S[n];
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
void moserDeBruijn(int n)
{
    for (int i = 0; i < n; i++)
        cout << gen(i) << " ";
    cout << "\n";
}

// Driver Code
int main()
{
    int n = 15;
    cout << "First " << n << " terms of "
         << "Moser-de Bruijn Sequence : \n";
    moserDeBruijn(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to generate first 'n' terms
// of the Moser-de Bruijn Sequence

class GFG
{

// Function to generate nth term
// of Moser-de Bruijn Sequence
static int gen(int n)
{
    int []S = new int [n + 1];

    S[0] = 0;
    if(n != 0)
        S[1] = 1;

    for (int i = 2; i <= n; i++)
    {

        // S(2 * n) = 4 * S(n)
        if (i % 2 == 0)
        S[i] = 4 * S[i / 2];

        // S(2 * n + 1) = 4 * S(n) + 1
        else
        S[i] = 4 * S[i/2] + 1;
    }

    return S[n];
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
static void moserDeBruijn(int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(gen(i)+" ");
}

// Driver Code
public static void main(String[] args)
{
    int n = 15;
    System.out.println("First " + n +
                       " terms of " +
      "Moser-de Bruijn Sequence : ");
    moserDeBruijn(n);
}
}

// This code is contributed by
// Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# python3 code to generate first 'n' terms
# of the Moser-de Bruijn Sequence

# Function to generate nth term
# of Moser-de Bruijn Sequence
def gen( n ):
    S = [0, 1]
    for i in range(2, n+1):

        # S(2 * n) = 4 * S(n)
        if i % 2 == 0:
            S.append(4 * S[int(i / 2)]);

        # S(2 * n + 1) = 4 * S(n) + 1
        else:
            S.append(4 * S[int(i / 2)] + 1);
    z = S[n];
    return z;

# Generating the first 'n' terms
# of Moser-de Bruijn Sequence
def moserDeBruijn(n):
    for i in range(n):
        print(gen(i), end = " ")

# Driver Code
n = 15
print("First", n, "terms of ",
    "Moser-de Brujn Sequence:")
moserDeBruijn(n)

# This code is contributed by mits.
```

## C#

```
// C# code to generate first 'n' terms
// of the Moser-de Bruijn Sequence
using System;

class GFG
{

// Function to generate nth term
// of Moser-de Bruijn Sequence
static int gen(int n)
{
    int []S = new int [n + 1];

    S[0] = 0;
    if(n != 0)
        S[1] = 1;

    for (int i = 2; i <= n; i++)
    {

        // S(2 * n) = 4 * S(n)
        if (i % 2 == 0)
        S[i] = 4 * S[i / 2];

        // S(2 * n + 1) = 4 * S(n) + 1
        else
        S[i] = 4 * S[i/2] + 1;
    }

    return S[n];
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
static void moserDeBruijn(int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(gen(i)+" ");
}

// Driver Code
public static void Main()
{
    int n = 15;
    Console.WriteLine("First " + n +
                      " terms of " +
     "Moser-de Bruijn Sequence : ");
    moserDeBruijn(n);
}
}

// This code is contributed by
// Smitha Dinesh Semwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to generate first 'n' terms
// of the Moser-de Bruijn Sequence

// Function to generate nth term
// of Moser-de Bruijn Sequence
function gen( $n)
{
    $S = array();

    $S[0] = 0;
    $S[1] = 1;

    for ( $i = 2; $i <= $n; $i++)
    {
        // S(2 * n) = 4 * S(n)
        if ($i % 2 == 0)
        $S[$i] = 4 * $S[$i / 2];

        // S(2 * n + 1) = 4 * S(n) + 1
        else
        $S[$i] = 4 * $S[$i/2] + 1;
    }

    return $S[$n];
}

// Generating the first 'n' terms
// of Moser-de Bruijn Sequence
function moserDeBruijn( $n)
{
    for ( $i = 0; $i < $n; $i++)
        echo gen($i) , " ";
    echo "\n";
}

// Driver Code
$n = 15;
echo "First " ,$n ," terms of "
    , "Moser-de Bruijn Sequence : \n";
moserDeBruijn($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript code to generate first 'n' terms
    // of the Moser-de Bruijn Sequence

    // Function to generate nth term
    // of Moser-de Bruijn Sequence
    function gen(n)
    {
        let S = new Array(n + 1);
        S.fill(0);

        S[0] = 0;
        if(n != 0)
            S[1] = 1;

        for (let i = 2; i <= n; i++)
        {

            // S(2 * n) = 4 * S(n)
            if (i % 2 == 0)
                S[i] = 4 * S[parseInt(i / 2, 10)];

            // S(2 * n + 1) = 4 * S(n) + 1
            else
                S[i] = 4 * S[parseInt(i / 2, 10)] + 1;
        }

        return S[n];
    }

    // Generating the first 'n' terms
    // of Moser-de Bruijn Sequence
    function moserDeBruijn(n)
    {
        for (let i = 0; i < n; i++)
            document.write(gen(i)+" ");
    }

    let n = 15;
    document.write("First " + n +
                      " terms of " +
     "Moser-de Bruijn Sequence : " + "</br>");
    moserDeBruijn(n);

</script>
```

**输出:**

```
First 15 terms of Moser-de Bruijn Sequence : 
0 1 4 5 16 17 20 21 64 65 68 69 80 81 84
```