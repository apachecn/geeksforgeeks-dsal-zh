# 关于斐波那契数的有趣事实

> 原文:[https://www . geesforgeks . org/interior-facts-Fibonacci-numbers/](https://www.geeksforgeeks.org/interesting-facts-fibonacci-numbers/)

我们知道[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，**F**n =**F**n-1+**F**n-2。
前几个斐波那契数是 0、1、1、2、3、5、8、13、21、34、55、89、144、233、377、610、987、…。。
这里有一些关于斐波那契数的有趣事实:

**1。斐波那契数列最后几个数字的模式:**
前几个斐波那契数列的最后几个数字是:

```
0, 1, 1, 2, 3, 5, 8, 3, 1, 4, 5, 9, 4, 3, 7, 0, 7, ... 
```

最后一串数字以 60 的周期长度重复(关于这个结果的解释，请参考[这个](https://www.geeksforgeeks.org/program-find-last-digit-nth-fibonnaci-number/))。

## C

```
// C program to demonstrate that sequence of last
// digits of Fibonacci numbers repeats after 60.
#include<stdio.h>
#define max 100
int main()
{
    long long int arr[max];
    arr[0] = 0;
    arr[1] = 1;
    int i = 0;
    // storing Fibonacci numbers
    for (int i = 2; i < max; i++)
        arr[i] = arr[i-1] + arr[i-2];

    // Traversing through store numbers
    for (int i = 1; i < max - 1; i++)
    {
        // Since first two number are 0 and 1
        // so, if any two consecutive number encounter 0 and 1
        // at their unit place, then it clearly means that
        // number is repeating/ since we just have to find
        // the sum of previous two number
        if ((arr[i] % 10 == 0) && (arr[i+1] % 10 == 1))
            break;
    }
    printf("Sequence is repeating after index %d", i);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate that sequence of last
// digits of Fibonacci numbers repeats after 60.

class GFG{
static int max=100;
public static void main(String[] args)
{
    long[] arr=new long[max];
    arr[0] = 0;
    arr[1] = 1;
    int i=0;

    // storing Fibonacci numbers
    for (i = 2; i < max; i++)
        arr[i] = arr[i-1] + arr[i-2];

    // Traversing through store numbers
    for (i = 1; i < max - 1; i++)
    {
        // Since first two number are 0 and 1
        // so, if any two consecutive number encounter 0 and 1
        // at their unit place, then it clearly means that
        // number is repeating/ since we just have to find
        // the sum of previous two number
        if ((arr[i] % 10 == 0) && (arr[i+1] % 10 == 1))
            break;
    }
    System.out.println("Sequence is repeating after index "+i);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to demonstrate that sequence of last
# digits of Fibonacci numbers repeats after 60.

if __name__=='__main__':
    max = 100
    arr = [0 for i in range(max)]
    arr[0] = 0
    arr[1] = 1

# storing Fibonacci numbers
    for i in range(2, max):
        arr[i] = arr[i - 1] + arr[i - 2]

    # Traversing through store numbers
    for i in range(1, max - 1):

    # Since first two number are 0 and 1
    # so, if any two consecutive number encounter 0 and 1
    # at their unit place, then it clearly means that
    # number is repeating/ since we just have to find
    # the sum of previous two number
        if((arr[i] % 10 == 0) and (arr[i + 1] % 10 == 1)):
            break

    print("Sequence is repeating after index", i)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to demonstrate that sequence of last
// digits of Fibonacci numbers repeats after 60.

class GFG{
static int max=100;
public static void Main()
{
    long[] arr=new long[max];
    arr[0] = 0;
    arr[1] = 1;
    int i=0;

    // storing Fibonacci numbers
    for (i = 2; i < max; i++)
        arr[i] = arr[i-1] + arr[i-2];

    // Traversing through store numbers
    for (i = 1; i < max - 1; i++)
    {
        // Since first two number are 0 and 1
        // so, if any two consecutive number encounter 0 and 1
        // at their unit place, then it clearly means that
        // number is repeating/ since we just have to find
        // the sum of previous two number
        if ((arr[i] % 10 == 0) && (arr[i+1] % 10 == 1))
            break;
    }
    System.Console.WriteLine("Sequence is repeating after index "+i);
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to demonstrate that
// sequence of last digits of
// Fibonacci numbers repeats after
// 60\. global $MAX=100

    $arr[0] = 0;
    $arr[1] = 1;

    // storing Fibonacci numbers
    for ($i = 2; $i < 100; $i++)
        $arr[$i] = $arr[$i-1] +
                       $arr[$i-2];

    // Traversing through store
    // numbers
    for ($i = 1; $i <100 - 1; $i++)
    {
        // Since first two number are
        // 0 and 1 so, if any two
        // consecutive number encounter
        // 0 and 1 at their unit place,
        // then it clearly means that
        // number is repeating/ since
        // we just have to find the
        // sum of previous two number
        if (($arr[$i] % 10 == 0) &&
                ($arr[$i+1] % 10 == 1))
            break;
    }
    echo "Sequence is repeating after",
                         " index ", $i;

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to demonstrate that
// sequence of last digits of Fibonacci
// numbers repeats after 60.    
var max = 100;

var arr = Array(max).fill(0);
arr[0] = 0;
arr[1] = 1;
var i = 0;

// Storing Fibonacci numbers
for(i = 2; i < max; i++)
    arr[i] = arr[i - 1] + arr[i - 2];

// Traversing through store numbers
for(i = 1; i < max - 1; i++)
{

    // Since first two number are 0 and 1
    // so, if any two consecutive number encounter 0 and 1
    // at their unit place, then it clearly means that
    // number is repeating since we just have to find
    // the sum of previous two number
    if ((arr[i] % 10 == 0) && (arr[i + 1] % 10 == 1))
        break;
}

// Driver code
document.write("Sequence is repeating after index " + i);

// This code is contributed by gauravrajput1

</script>
```

**输出:**

```
Sequence is repeating after index 60
```

**2。斐波那契数的因素:**仔细观察，我们可以观察到以下几点:

*   每第三个斐波那契数是 2 的倍数
*   每 4 个斐波那契数是 3 的倍数
*   每 5 个斐波那契数是 5 的倍数
*   每 6 个斐波那契数是 8 的倍数

详见[本](https://www.geeksforgeeks.org/efficient-way-check-whether-n-th-fibonacci-number-multiple-10/)。

## C++

```
// C++ program to demonstrate divisibility of Fibonacci
// numbers.
#include<iostream>
using namespace std;
#define MAX 90

int main()
{
    // indexes variable stores index of number that
    // is divisible by 2, 3, 5 and 8
    long long int arr[MAX], index1[MAX], index2[MAX];
    long long int index3[MAX], index4[MAX];

    // storing fibonacci numbers
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i-1] + arr[i-2];

    // c1 keeps track of number of index of number
    // divisible by 2 and others c2, c3 and c4 for
    // 3, 5 and 8
    int c1 = 0, c2 = 0, c3 = 0, c4 = 0;

    // separating fibonacci number into their
    // respective array
    for (int i = 0; i < MAX; i++)
    {
        if (arr[i] % 2 == 0)
            index1[c1++] = i;
        if (arr[i] % 3 == 0)
            index2[c2++] = i;
        if (arr[i] % 5 == 0)
            index3[c3++] = i;
        if (arr[i] % 8 == 0)
            index4[c4++] = i;
    }

    // printing index arrays
    cout<<"Index of Fibonacci numbers divisible by"
           " 2 are :\n";
    for (int i = 0; i < c1; i++)
        cout<<" "<< index1[i];
    cout<<"\n";

    cout<<"Index of Fibonacci number divisible by"
           " 3 are :\n";
    for (int i = 0; i < c2; i++)
        cout<<"  "<< index2[i];
    cout<<"\n";

    cout<<"Index of Fibonacci number divisible by"
           " 5 are :\n";
    for (int i = 0; i < c3; i++)
        cout<<"  "<< index3[i];
    cout<<"\n";

    cout<<"Index of Fibonacci number divisible by"
           " 8 are :\n";
    for (int i = 0; i < c4; i++)
        cout<<" "<<index4[i];
    cout<<"\n";
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to demonstrate divisibility of Fibonacci
// numbers.
#include<stdio.h>
#define MAX 90

int main()
{
    // indexes variable stores index of number that
    // is divisible by 2, 3, 5 and 8
    long long int arr[MAX], index1[MAX], index2[MAX];
    long long int index3[MAX], index4[MAX];

    // storing fibonacci numbers
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i-1] + arr[i-2];

    // c1 keeps track of number of index of number
    // divisible by 2 and others c2, c3 and c4 for
    // 3, 5 and 8
    int c1 = 0, c2 = 0, c3 = 0, c4 = 0;

    // separating fibonacci number into their
    // respective array
    for (int i = 0; i < MAX; i++)
    {
        if (arr[i] % 2 == 0)
            index1[c1++] = i;
        if (arr[i] % 3 == 0)
            index2[c2++] = i;
        if (arr[i] % 5 == 0)
            index3[c3++] = i;
        if (arr[i] % 8 == 0)
            index4[c4++] = i;
    }

    // printing index arrays
    printf("Index of Fibonacci numbers divisible by"
           " 2 are :\n");
    for (int i = 0; i < c1; i++)
        printf("%d  ", index1[i]);
    printf("\n");

    printf("Index of Fibonacci number divisible by"
           " 3 are :\n");
    for (int i = 0; i < c2; i++)
        printf("%d  ", index2[i]);
    printf("\n");

    printf("Index of Fibonacci number divisible by"
           " 5 are :\n");
    for (int i = 0; i < c3; i++)
        printf("%d  ", index3[i]);
    printf("\n");

    printf("Index of Fibonacci number divisible by"
           " 8 are :\n");
    for (int i = 0; i < c4; i++)
        printf("%d  ", index4[i]);
    printf("\n");
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate divisibility of Fibonacci
// numbers.

class GFG
{
static int MAX=90;

// Driver code
public static void main(String[] args)
{
    // indexes variable stores index of number that
    // is divisible by 2, 3, 5 and 8
    long[] arr=new long[MAX];
    long[] index1=new long[MAX];
    long[] index2=new long[MAX];
    long[] index3=new long[MAX];
    long[] index4=new long[MAX];

    // storing fibonacci numbers
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i - 1] + arr[i - 2];

    // c1 keeps track of number of index of number
    // divisible by 2 and others c2, c3 and c4 for
    // 3, 5 and 8
    int c1 = 0, c2 = 0, c3 = 0, c4 = 0;

    // separating fibonacci number into their
    // respective array
    for (int i = 0; i < MAX; i++)
    {
        if (arr[i] % 2 == 0)
            index1[c1++] = i;
        if (arr[i] % 3 == 0)
            index2[c2++] = i;
        if (arr[i] % 5 == 0)
            index3[c3++] = i;
        if (arr[i] % 8 == 0)
            index4[c4++] = i;
    }

    // printing index arrays
    System.out.print("Index of Fibonacci numbers divisible by" +
        " 2 are :\n");
    for (int i = 0; i < c1; i++)
        System.out.print(index1[i] + " ");
    System.out.print("\n");

    System.out.print("Index of Fibonacci number divisible by" +
        " 3 are :\n");
    for (int i = 0; i < c2; i++)
        System.out.print(index2[i] + " ");
    System.out.print("\n");

    System.out.print("Index of Fibonacci number divisible by" +
        " 5 are :\n");
    for (int i = 0; i < c3; i++)
        System.out.print(index3[i] + " ");
    System.out.print("\n");

    System.out.print("Index of Fibonacci number divisible by" +
        " 8 are :\n");
    for (int i = 0; i < c4; i++)
        System.out.print(index4[i] + " ");
    System.out.print("\n");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to demonstrate divisibility
# of Fibonacci numbers.
MAX = 90;

# indexes variable stores index of number
# that is divisible by 2, 3, 5 and 8
arr = [0] * (MAX);
index1 = [0] * (MAX);
index2 = [0] * (MAX);
index3 = [0] * (MAX);
index4 = [0] * (MAX);

# storing fibonacci numbers
arr[0] = 0;
arr[1] = 1;
for i in range(2, MAX):
    arr[i] = arr[i - 1] + arr[i - 2];

# c1 keeps track of number of index
# of number divisible by 2 and others 
# c2, c3 and c4 for 3, 5 and 8
c1, c2, c3, c4 = 0, 0, 0, 0;

# separating fibonacci number into
# their respective array
for i in range(MAX):
    if (arr[i] % 2 == 0):
        index1[c1] = i;
        c1 += 1;
    if (arr[i] % 3 == 0):
        index2[c2] = i;
        c2 += 1;
    if (arr[i] % 5 == 0):
        index3[c3] = i;
        c3 += 1;
    if (arr[i] % 8 == 0):
        index4[c4] = i;
        c4 += 1;

# printing index arrays
print("Index of Fibonacci numbers",
           "divisible by 2 are :");
for i in range(c1):
    print(index1[i], end = " ");
print("");

print("Index of Fibonacci number",
          "divisible by 3 are :");
for i in range(c2):
    print(index2[i], end = " ");
print("");

print("Index of Fibonacci number",
          "divisible by 5 are :");
for i in range(c3):
    print(index3[i], end = " ");
print("");

print("Index of Fibonacci number",
          "divisible by 8 are :");
for i in range(c4):
    print(index4[i], end = " ");
print("");

# This code is contributed by mits
```

## C#

```
// C# program to demonstrate divisibility
// of Fibonacci numbers.

class GFG{
static int MAX = 90;

static void Main()
{
    // indexes variable stores index of number that
    // is divisible by 2, 3, 5 and 8
    long[] arr = new long[MAX];
    long[] index1 = new long[MAX];
    long[] index2 = new long[MAX];
    long[] index3 = new long[MAX];
    long[] index4 = new long[MAX];

    // storing fibonacci numbers
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i-1] + arr[i-2];

    // c1 keeps track of number of index of number
    // divisible by 2 and others c2, c3 and c4 for
    // 3, 5 and 8
    int c1 = 0, c2 = 0, c3 = 0, c4 = 0;

    // separating fibonacci number into their
    // respective array
    for (int i = 0; i < MAX; i++)
    {
        if (arr[i] % 2 == 0)
            index1[c1++] = i;
        if (arr[i] % 3 == 0)
            index2[c2++] = i;
        if (arr[i] % 5 == 0)
            index3[c3++] = i;
        if (arr[i] % 8 == 0)
            index4[c4++] = i;
    }

    // printing index arrays
    System.Console.Write("Index of Fibonacci numbers" +
                    "divisible by 2 are :\n");
    for (int i = 0; i < c1; i++)
        System.Console.Write(index1[i]+" ");
    System.Console.Write("\n");

    System.Console.Write("Index of Fibonacci number "+
                        " divisible by 3 are :\n");
    for (int i = 0; i < c2; i++)
        System.Console.Write(index2[i]+" ");
    System.Console.Write("\n");

    System.Console.Write("Index of Fibonacci number "+
        "divisible by 5 are :\n");
    for (int i = 0; i < c3; i++)
        System.Console.Write(index3[i]+" ");
    System.Console.Write("\n");

    System.Console.Write("Index of Fibonacci number "+
        "divisible by 8 are :\n");
    for (int i = 0; i < c4; i++)
        System.Console.Write(index4[i]+" ");
    System.Console.Write("\n");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to demonstrate divisibility
// of Fibonacci numbers.
$MAX = 90;

// indexes variable stores index of number
// that is divisible by 2, 3, 5 and 8
$arr = array($MAX);
$index1 = array($MAX);
$index2 = array($MAX);
$index3 = array($MAX);
$index4 = array($MAX);

// storing fibonacci numbers
$arr[0] = 0;
$arr[1] = 1;
for ($i = 2; $i < $MAX; $i++)
{
    $arr[$i] = $arr[$i - 1] + $arr[$i - 2];
}

// c1 keeps track of number of index of
// number divisible by 2 and others
// c2, c3 and c4 for 3, 5 and 8
$c1 = 0;
$c2 = 0;
$c3 = 0;
$c4 = 0;

// separating fibonacci number into
// their respective array
for ($i = 0; $i < $MAX; $i++)
{
    if ($arr[$i] % 2 == 0)
        $index1[$c1++] = $i;
    if ($arr[$i] % 3 == 0)
        $index2[$c2++] = $i;
    if ($arr[$i] % 5 == 0)
        $index3[$c3++] = $i;
    if ($arr[$i] % 8 == 0)
        $index4[$c4++] = $i;
}

// printing index arrays
echo "Index of Fibonacci numbers divisible by" .
                                " 2 are :\n";
for ($i = 0; $i < $c1; $i++)
    echo $index1[$i] . " ";
echo "\n";

echo "Index of Fibonacci number divisible by" .
                                " 3 are :\n";
for ($i = 0; $i < $c2; $i++)
    echo $index2[$i] . " ";
echo "\n";

echo "Index of Fibonacci number divisible by" .
    " 5 are :\n";
for ($i = 0; $i < $c3; $i++)
    echo $index3[$i] . " ";
echo "\n";

echo "Index of Fibonacci number divisible by" .
    " 8 are :\n";
for ($i = 0; $i < $c4; $i++)
    echo $index4[$i] . " ";
echo "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
// JavaScript program to demonstrate divisibility of Fibonacci
// numbers.

var MAX=90;

// Driver code

    // indexes variable stores index of number that
    // is divisible by 2, 3, 5 and 8
    var arr=new Array(MAX);
    var index1= new Array(MAX);
    var index2= new Array(MAX);
    var index3= new Array(MAX);
    var index4= new Array(MAX);

    // storing fibonacci numbers
    arr[0] = 0;
    arr[1] = 1;
    for (var i = 2; i < MAX; i++)
        arr[i] = arr[i - 1] + arr[i - 2];

    // c1 keeps track of number of index of number
    // divisible by 2 and others c2, c3 and c4 for
    // 3, 5 and 8
    var c1 = 0, c2 = 0, c3 = 0, c4 = 0;

    // separating fibonacci number into their
    // respective array
    for (var i = 0; i < MAX; i++)
    {
        if (arr[i] % 2 == 0)
            index1[c1++] = i;
        if (arr[i] % 3 == 0)
            index2[c2++] = i;
        if (arr[i] % 5 == 0)
            index3[c3++] = i;
        if (arr[i] % 8 == 0)
            index4[c4++] = i;
    }

    // printing index arrays
    document.write("Index of Fibonacci numbers divisible by" +
        " 2 are :\n");
    for (var i = 0; i < c1; i++)
        document.write(index1[i] + " ");
    document.write("\n");

    document.write("Index of Fibonacci number divisible by" +
        " 3 are :\n");
    for (var i = 0; i < c2; i++)
        document.write(index2[i] + " ");
    document.write("\n");

    document.write("Index of Fibonacci number divisible by" +
        " 5 are :\n");
    for (var i = 0; i < c3; i++)
        document.write(index3[i] + " ");
    document.write("\n");

    document.write("Index of Fibonacci number divisible by" +
        " 8 are :\n");
    for (var i = 0; i < c4; i++)
        document.write(index4[i] + " ");
    document.write("\n");

// This code is contributed by shivanisinghss2110
```

**输出:**

```
Index of Fibonacci numbers divisible by 2 are :
0 3 6 9 12 15 18 21 24 27 30 33 36 39 42 45 
48 51 54 57 60 63 66 69 72 75 78 81 84 87 
Index of Fibonacci number divisible by 3 are :
0 4 8 12 16 20 24 28 32 36 40 44 48 52 
56 60 64 68 72 76 80 84 88 
Index of Fibonacci number divisible by 5 are :
0 5 10 15 20 25 30 35 40 45 50 
55 60 65 70 75 80 85 
Index of Fibonacci number divisible by 8 are :
0 6 12 18 24 30 36 42 48
54 60 66 72 78 84 
```

**3。带指数因子的斐波那契数:**我们有一些斐波那契数像 F(1) = 1 可被 1 整除，F(5) = 5 可被 5 整除，F(12) = 144 可被 12 整除，F(24) = 46368 可被 24 整除，F(25) = 75025 可被 25 整除。这种类型的索引号遵循一定的模式。首先，让我们看看这些指数:
1，5，12，24，25，36，48，60，72，84，96，108，120，125，132，…..

根据观察，这个级数是由 12 的倍数以及满足幂(5，k)条件的所有数组成的，其中 k = 0，1，2，3，4，5，6，7，…。

## C++

```
// C++ program to demonstrate that Fibonacci numbers
// that are divisible by their indexes have indexes
// as either power of 5 or multiple of 12.
#include<iostream>
using namespace std;
#define MAX 100

int main()
{

    // storing Fibonacci numbers
    long long int arr[MAX];
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i-1] + arr[i-2];

    cout<<"Fibonacci numbers divisible by "
          "their indexes are :\n";
    for (int i = 1; i < MAX; i++)
        if (arr[i] % i == 0)
            cout<<"  "<< i;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to demonstrate that Fibonacci numbers
// that are divisible by their indexes have indexes
// as either power of 5 or multiple of 12.
#include<stdio.h>
#define MAX 100

int main()
{
    // storing Fibonacci numbers
    long long int arr[MAX];
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i-1] + arr[i-2];

    printf("Fibonacci numbers divisible by "
          "their indexes are :\n");
    for (int i = 1; i < MAX; i++)
        if (arr[i] % i == 0)
            printf("%d  ", i);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate that Fibonacci numbers
// that are divisible by their indexes have indexes
// as either power of 5 or multiple of 12.

class GFG
{

static int MAX = 100;

public static void main(String[] args)
{
    // storing Fibonacci numbers
    long[] arr = new long[MAX];
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i - 1] + arr[i - 2];

    System.out.print("Fibonacci numbers divisible by "+
        "their indexes are :\n");
    for (int i = 1; i < MAX; i++)
        if (arr[i] % i == 0)
            System.out.print(i + " ");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to demonstrate that Fibonacci numbers
# that are divisible by their indexes have indexes
# as either power of 5 or multiple of 12.

if __name__=='__main__':
    MAX = 100
# storing Fibonacci numbers
    arr = [0 for i in range(MAX)]
    arr[0] = 0
    arr[1] = 1
    for i in range(2, MAX):
        arr[i] = arr[i - 1] + arr[i - 2]

    print("Fibonacci numbers divisible by their indexes are :")
    for i in range(1, MAX):
        if(arr[i] % i == 0):
            print(i,end=" ")

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to demonstrate that Fibonacci
// numbers that are divisible by their
// indexes have indexes as either power of 5
// or multiple of 12.
using System;

class GFG
{
static int MAX = 100;
static void Main()
{
    // storing Fibonacci numbers
    long[] arr = new long[MAX];
    arr[0] = 0;
    arr[1] = 1;
    for (int i = 2; i < MAX; i++)
        arr[i] = arr[i - 1] + arr[i - 2];

    Console.Write("Fibonacci numbers divisible by " +
                           "their indexes are :\n");
    for (int i = 1; i < MAX; i++)
        if (arr[i] % i == 0)
            System.Console.Write(i+" ");
}
}

// This code is contributed by mits
```

## java 描述语言

```
// JavaScript program to demonstrate that Fibonacci numbers
// that are divisible by their indexes have indexes
// as either power of 5 or multiple of 12.

var MAX = 100;

    // storing Fibonacci numbers
    var arr = new Array(MAX);
    arr[0] = 0;
    arr[1] = 1;
    for (var i = 2; i < MAX; i++)
        arr[i] = arr[i - 1] + arr[i - 2];

    document.write("Fibonacci numbers divisible by their indexes are :");
    for (var i = 1; i < MAX; i++)
        if (arr[i] % i == 0)
            document.write(i + " ");

// This code is contributed by shivanisinghss2110
```

**输出:**

```
Fibonacci numbers divisible by their indexes are :
1  5  12  24  25  36  48  60  72  96
```

**4。f(n-1)* f(n+1)–f(n)* f(n)的值为(-1) <sup>n</sup>** 。详见[卡西尼身份](https://www.geeksforgeeks.org/cassinis-identity/)。

**参考:**
[http://www . mathematics . surrey . AC . uk/hosted-sites/R .克诺特/Fibonacci/fib mathematics . html](http://www.maths.surrey.ac.uk/hosted-sites/R.Knott/Fibonacci/fibmaths.html)
本文由 [Aditya Kumar](https://www.linkedin.com/in/aditya-kumar-837315100/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。