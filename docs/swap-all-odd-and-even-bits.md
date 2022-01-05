# 交换所有奇数和偶数位

> 原文:[https://www.geeksforgeeks.org/swap-all-odd-and-even-bits/](https://www.geeksforgeeks.org/swap-all-odd-and-even-bits/)

给定一个无符号整数，用偶数位交换所有奇数位。例如，给定的数字为 23(**0**0**0**1**0**1**1**1)，则应转换为 43(0**0**1**0**1**0**1**1**)。每个偶数位置位与右侧的相邻位交换(偶数位置位以 23 的二进制表示突出显示)，每个奇数位置位与左侧的相邻位交换。

## 蛮力

很难记住**0x aaaaaaaaaa**是在所有偶数位设置的 32 位的数字，而 **0x55555555** 是在所有奇数位设置的 32 位的数字。所以对此还有另一个解决方案。这里我们需要以暴力的方式执行操作。

1.  找一点 **i** 和 **i+1。**
2.  要交换位，请减去并加上相应的值。
3.  将第 **i <sup>个</sup>T3】位移至第 **i+1** 位。我们需要**减去 i_bit < < i** 并将其添加到 **i+1** 位置，为此我们需要**添加 i_bit < < (i+1)** 。**
4.  对于第(i+1) <sup>位</sup>也同样如此。把它从 i+1 移到 I。

## C++

```
// C++ program to swap even and
// odd bits of a given number
#include <bits/stdc++.h>
using namespace std;

// Function to swap even
// and odd bits
unsigned int swapBits(unsigned int x)
{
    for(int i=0; i<32; i+=2){
        int i_bit = ( x >> i ) & 1; // find i th bit
        int i_1_bit = (x >> ( i+1 )) & 1;  // find i+1 th bit

        x = x - ( i_bit << i) // remove i_bit
              - ( i_1_bit << ( i+1 ) ) // remove i+1 th bit
              + ( i_bit << ( i+1 ) ) // put i_bit at i+1 location
              + ( i_1_bit << i );  // put i+1 bit at i location
    }
    return x;
}

// Driver code
int main()
{
    unsigned int x =23; // 00010111

    // Output is 43 (00101011)
    cout<<swapBits(x);

    return 0;
}

// This code is contributed by Amandeep Gupta
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap even and
// odd bits of a given number
import java.io.*;

class GFG {

    // Function to swap even
    // and odd bits
    static int swapBits(int x)
    {
        for (int i = 0; i < 32; i += 2) {
            int i_bit = (x >> i) & 1; // find i th bit
            int i_1_bit
                = (x >> (i + 1)) & 1; // find i+1 th bit

            x = x - (i_bit << i) // remove i_bit
                - (i_1_bit << (i + 1)) // remove i+1 th bit
                + (i_bit
                   << (i + 1)) // put i_bit at i+1 location
                + (i_1_bit
                   << i); // put i+1 bit at i location
        }
        return x;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 23; // 00010111

        // Output is 43 (00101011)
        System.out.print(swapBits(x));
    }
}

// This code is contributed by subham348.
```

## C#

```
// C# program to swap even and
// odd bits of a given number
using System;

class GFG {

    // Function to swap even
    // and odd bits
    static int swapBits(int x)
    {
        for (int i = 0; i < 32; i += 2) {
            int i_bit = (x >> i) & 1; // find i th bit
            int i_1_bit
                = (x >> (i + 1)) & 1; // find i+1 th bit

            x = x - (i_bit << i) // remove i_bit
                - (i_1_bit << (i + 1)) // remove i+1 th bit
                + (i_bit
                   << (i + 1)) // put i_bit at i+1 location
                + (i_1_bit
                   << i); // put i+1 bit at i location
        }
        return x;
    }

    // Driver code
    public static void Main()
    {
        int x = 23; // 00010111

        // Output is 43 (00101011)
        Console.Write(swapBits(x));
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>
// JavaScript Program to implement
// the above approach

// Function to swap even
// and odd bits
function swapBits( x)
{
    for(let i = 0; i < 32; i += 2){
        let i_bit = ( x >> i ) & 1; // find i th bit
        let i_1_bit = (x >> ( i+1 )) & 1;  // find i+1 th bit

        x = x - ( i_bit << i) // remove i_bit
              - ( i_1_bit << ( i+1 ) ) // remove i+1 th bit
              + ( i_bit << ( i+1 ) ) // put i_bit at i+1 location
              + ( i_1_bit << i );  // put i+1 bit at i location
    }
    return x;
}

// Driver code
    let x =23; // 00010111

    // Output is 43 (00101011)
    document.write(swapBits(x));

    // This code is contributed by Potta Lokesh
    </script>
```

输出:

```
 43 
```

***时间复杂度:** O(常数)*

***辅助空间:** O(1)*

如果我们仔细看一下这个例子，我们可以观察到，我们基本上需要将所有偶数位(>>)右移 1(在上面的例子中，23 的偶数位被突出显示)，使它们成为奇数位(在 43 中突出显示)，然后左移(<让输入数为 x
1)通过对 x 与 0xAAAAAAAA 进行按位“与”得到 x 的所有偶数位。数字 0xAAAAAAAA 是一个 32 位数字，所有偶数位设置为 1，所有奇数位设置为 0。
2)通过对 x 与 0x55555555 进行按位“与”运算，获取 x 的所有奇数位。数字 0x55555555 是一个 32 位数字，所有奇数位设置为 1，所有偶数位设置为 0。
3)右移所有偶数位。
4)左移所有奇数位。
5)合并新的奇偶位并返回。

## C++

```
// C++ program to swap even and
// odd bits of a given number
#include <bits/stdc++.h>
using namespace std;

// Function to swap even
// and odd bits
unsigned int swapBits(unsigned int x)
{
    // Get all even bits of x
    unsigned int even_bits = x & 0xAAAAAAAA;

    // Get all odd bits of x
    unsigned int odd_bits = x & 0x55555555;

    even_bits >>= 1; // Right shift even bits
    odd_bits <<= 1; // Left shift odd bits

    return (even_bits | odd_bits); // Combine even and odd bits
}

// Driver code
int main()
{
    unsigned int x = 23; // 00010111

    // Output is 43 (00101011)
    cout<<swapBits(x);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to swap even and
// odd bits of a given number
#include <stdio.h>

// Function to swap even
// and odd bits
unsigned int swapBits(unsigned int x)
{
    // Get all even bits of x
    unsigned int even_bits = x & 0xAAAAAAAA;

    // Get all odd bits of x
    unsigned int odd_bits  = x & 0x55555555;

    even_bits >>= 1;  // Right shift even bits
    odd_bits <<= 1;   // Left shift odd bits

    return (even_bits | odd_bits); // Combine even and odd bits
}

// Driver program to test above function
int main()
{
    unsigned int x = 23; // 00010111

    // Output is 43 (00101011)
    printf("%u ", swapBits(x));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap even
// and odd bits of a given number

class GFG{

    // Function to swap even
    // and odd bits
    static int swapBits(int x)
    {
        // Get all even bits of x
        int even_bits = x & 0xAAAAAAAA;

        // Get all odd bits of x
        int odd_bits = x & 0x55555555;

        // Right shift even bits
        even_bits >>= 1;

        // Left shift even bits
        odd_bits <<= 1;

        // Combine even and odd bits
        return (even_bits | odd_bits);
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int x = 23; // 00010111

        // Output is 43 (00101011)
        System.out.println(swapBits(x));
    }
}

// This code is contributed by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to swap even
# and odd bits of a given number

# Function for swapping even
# and odd bits
def swapBits(x) :

    # Get all even bits of x
    even_bits = x & 0xAAAAAAAA

    # Get all odd bits of x
    odd_bits = x & 0x55555555

    # Right shift even bits
    even_bits >>= 1

    # Left shift odd bits
    odd_bits <<= 1

    # Combine even and odd bits
    return (even_bits | odd_bits)

# Driver program
# 00010111
x = 23

# Output is 43 (00101011)
print(swapBits(x))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to swap even and odd bits
// of a given number
using System;

class GFG {

    // Function to swap even
    // and odd bits
    static long swapBits(int x)
    {
        // Get all even bits of x
        long even_bits = x & 0xAAAAAAAA;

        // Get all odd bits of x
        long odd_bits = x & 0x55555555;

        // Right shift even bits
        even_bits >>= 1;

        // Left shift even bits
        odd_bits <<= 1;

        // Combine even and odd bits
        return (even_bits | odd_bits);
    }

    // Driver program to test above function
    public static void Main()
    {

        int x = 23; // 00010111

        // Output is 43 (00101011)
        Console.Write(swapBits(x));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to swap even and
// odd bits of a given number

// Function to swap even
// and odd bits
function swapBits( $x)
{

    // Get all even bits of x
    $even_bits = $x & 0xAAAAAAAA;

    // Get all odd bits of x
    $odd_bits = $x & 0x55555555;

    // Right shift even bits
    $even_bits >>= 1;

    // Left shift odd bits
    $odd_bits <<= 1;

    // Combine even and odd bits
    return ($even_bits | $odd_bits);
}

// Driver Code

// 00010111
$x = 23;

// Output is 43 (00101011)
echo swapBits($x);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
// java script program to swap even and
// odd bits of a given number

// Function to swap even
// and odd bits
function swapBits( x)
{

    // Get all even bits of x
    even_bits = x & 0xAAAAAAAA;

    // Get all odd bits of x
    odd_bits = x & 0x55555555;

    // Right shift even bits
    even_bits >>= 1;

    // Left shift odd bits
    odd_bits <<= 1;

    // Combine even and odd bits
    return (even_bits | odd_bits);
}

// Driver Code

// 00010111
let x = 23;

// Output is 43 (00101011)
document.write(swapBits(x));

// This code is contributed by sravan kumar

</script>
```

输出:

```
 43 
```

时间复杂度:0(1)

辅助空间:O(1)

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。