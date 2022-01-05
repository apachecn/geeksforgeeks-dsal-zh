# 具有相同设置位数的下一个更高的数字

> 原文:[https://www . geeksforgeeks . org/下一个具有相同位数的更高位数/](https://www.geeksforgeeks.org/next-higher-number-with-same-number-of-set-bits/)

给定一个数 x，在它的二进制表示中找到下一个具有相同位数 1 的数。
例如，考虑 x = 12，其二进制表示为 1100(不包括 32 位机器上的前导零)。它包含两个逻辑 1 位。具有两个逻辑 1 位的下一个较高的数字是 17 (10001 <sub>2</sub> )。
**算法:**
当我们观察从 0 到 2 的二进制序列时<sup>n</sup>–1(n 是位数)，最右边的位(最低有效位)比最左边的位变化快。想法是在 x 中找到最右边的 1 的字符串，并将模式移到最右边，除了模式中最左边的位。将模式中最左边的位(省略的位)移到 x 的左边一个位置。一个例子更清楚了，

```
x = 156
```

<sub>10</sub>T2】

```
x = 10011100
```

<sub>(2)</sub>

```
10011100
00011100 - right most string of 1's in x
00000011 - right shifted pattern except left most bit ------> [A]
00010000 - isolated left most bit of right most 1's pattern
00100000 - shiftleft-ed the isolated bit by one position ------> [B]
10000000 - left part of x, excluding right most 1's pattern ------> [C]
10100000 - add B and C (OR operation) ------> [D]
10100011 - add A and D which is required number 163
```

<sub>(10)</sub>
用很少的例子练习后，就很容易理解了。使用下面给出的程序生成更多的集合。
**程序设计:**
我们需要注意二进制数的几个事实。表达式 x & -x 将隔离 x 中最右边的设置位(确保 x 对负数使用 2 的补码形式)。如果我们把结果加到 x 上，x 中 1 的最右边的字符串将被重置，这个 1 的模式左边的直接“0”将被设置，这是上面解释的[B]部分。例如，如果 x = 156，x & -x 将得到 00000100，将此结果与 x 相加得到 10100000(见 D 部分)。我们留下了模式 1 的右移部分(上面解释的部分 A)。
实现 a 部分有不同的方式，右移本质上是除法运算。我们的除数应该是多少？很明显，它应该是 2 的倍数(避免右移时的 0.5 误差)，并且应该将最右边的 1 模式移至最右端。表达式(x & -x)将用于除数的目的。数字 X 和用于重置最右边位的表达式之间的异或运算将隔离最右边的 1 的模式。
**一个修正因子:**
注意，我们正在向位模式添加最右边的设置位。加法操作导致比特位置的移位。二进制系统的权重是 2，一个移位会导致增加 2 倍。由于增加的数字(代码中的*right one pattern*)被使用了两次，错误传播了两次。这个错误需要改正。向右移动 2 个位置将会纠正结果。
这个节目的通俗名称是**s**ame**n**number**o**f**o**ne**b**its。

## C++

```
#include<iostream>

using namespace std;

typedef unsigned int uint_t;

// this function returns next higher number with same number of set bits as x.
uint_t snoob(uint_t x)
{

  uint_t rightOne;
  uint_t nextHigherOneBit;
  uint_t rightOnesPattern;

  uint_t next = 0;

  if(x)
  {

    // right most set bit
    rightOne = x & -(signed)x;

    // reset the pattern and set next higher bit
    // left part of x will be here
    nextHigherOneBit = x + rightOne;

    // nextHigherOneBit is now part [D] of the above explanation.

    // isolate the pattern
    rightOnesPattern = x ^ nextHigherOneBit;

    // right adjust pattern
    rightOnesPattern = (rightOnesPattern)/rightOne;

    // correction factor
    rightOnesPattern >>= 2;

    // rightOnesPattern is now part [A] of the above explanation.

    // integrate new pattern (Add [D] and [A])
    next = nextHigherOneBit | rightOnesPattern;
  }

  return next;
}

int main()
{
  int x = 156;
  cout<<"Next higher number with same number of set bits is "<<snoob(x);

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation on above approach
class GFG
{

// this function returns next higher
// number with same number of set bits as x.
static int snoob(int x)
{

int rightOne, nextHigherOneBit, rightOnesPattern, next = 0;

if(x > 0)
{

    // right most set bit
    rightOne = x & -x;

    // reset the pattern and set next higher bit
    // left part of x will be here
    nextHigherOneBit = x + rightOne;

    // nextHigherOneBit is now part [D] of the above explanation.

    // isolate the pattern
    rightOnesPattern = x ^ nextHigherOneBit;

    // right adjust pattern
    rightOnesPattern = (rightOnesPattern)/rightOne;

    // correction factor
    rightOnesPattern >>= 2;

    // rightOnesPattern is now part [A] of the above explanation.

    // integrate new pattern (Add [D] and [A])
    next = nextHigherOneBit | rightOnesPattern;
}

return next;
}

// Driver code
public static void main (String[] args)
{
    int x = 156;
    System.out.println("Next higher number with same" +
                    "number of set bits is "+snoob(x));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# This function returns next
# higher number with same
# number of set bits as x.
def snoob(x):

    next = 0
    if(x):

        # right most set bit
        rightOne = x & -(x)

        # reset the pattern and
        # set next higher bit
        # left part of x will
        # be here
        nextHigherOneBit = x + int(rightOne)

        # nextHigherOneBit is
        # now part [D] of the
        # above explanation.
        # isolate the pattern
        rightOnesPattern = x ^ int(nextHigherOneBit)

        # right adjust pattern
        rightOnesPattern = (int(rightOnesPattern) /
                            int(rightOne))

        # correction factor
        rightOnesPattern = int(rightOnesPattern) >> 2

        # rightOnesPattern is now part
        # [A] of the above explanation.

        # integrate new pattern
        # (Add [D] and [A])
        next = nextHigherOneBit | rightOnesPattern
    return next

# Driver Code
x = 156
print("Next higher number with " +
      "same number of set bits is",
                          snoob(x))

# This code is contributed by Smita
```

## C#

```
// C# Implementation on above approach
using System;
class GFG
{

// this function returns next higher
// number with same number of set bits as x.
static int snoob(int x)
{

    int rightOne, nextHigherOneBit,
        rightOnesPattern, next = 0;

    if(x > 0)
    {

        // right most set bit
        rightOne = x & -x;

        // reset the pattern and set next higher bit
        // left part of x will be here
        nextHigherOneBit = x + rightOne;

        // nextHigherOneBit is now part [D]
        // of the above explanation.

        // isolate the pattern
        rightOnesPattern = x ^ nextHigherOneBit;

        // right adjust pattern
        rightOnesPattern = (rightOnesPattern) / rightOne;

        // correction factor
        rightOnesPattern >>= 2;

        // rightOnesPattern is now part [A]
        // of the above explanation.

        // integrate new pattern (Add [D] and [A])
        next = nextHigherOneBit | rightOnesPattern;
    }
    return next;
}

// Driver code
static void Main()
{
    int x = 156;
    Console.WriteLine("Next higher number with same" +
                      "number of set bits is " + snoob(x));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// This function returns next higher number
// with same number of set bits as x.
function snoob($x)
{
    $next = 0;

    if($x)
    {

        // right most set bit
        $rightOne = $x & - $x;

        // reset the pattern and set next higher
        // bit left part of x will be here
        $nextHigherOneBit = $x + $rightOne;

        // nextHigherOneBit is now part [D] of
        // the above explanation.

        // isolate the pattern
        $rightOnesPattern = $x ^ $nextHigherOneBit;

        // right adjust pattern
        $rightOnesPattern = intval(($rightOnesPattern) /
                                            $rightOne);

        // correction factor
        $rightOnesPattern >>= 2;

        // rightOnesPattern is now part [A]
        // of the above explanation.

        // integrate new pattern (Add [D] and [A])
        $next = $nextHigherOneBit | $rightOnesPattern;
    }

    return $next;
}

// Driver Code
$x = 156;
echo "Next higher number with same " .
     "number of set bits is " . snoob($x);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

    // this function returns next higher 
    // number with same number of set bits as x.
    function snoob(x)
    {
        let rightOne, nextHigherOneBit, rightOnesPattern, next = 0;
        if(x > 0)
        {
            // right most set bit
            rightOne = x & -x;

            // reset the pattern and set next higher bit
            // left part of x will be here
            nextHigherOneBit = x + rightOne;

            // nextHigherOneBit is now part [D] of the above explanation.

            // isolate the pattern
            rightOnesPattern = x ^ nextHigherOneBit;

            // right adjust pattern
            rightOnesPattern = (rightOnesPattern)/rightOne;

            // correction factor
            rightOnesPattern >>= 2;

            // rightOnesPattern is now part [A] of the above explanation.

            // integrate new pattern (Add [D] and [A])
            next = nextHigherOneBit | rightOnesPattern;
        }
        return next;
    }

    // Driver code
    let x = 156;
    document.write("Next higher number with same " +
                     "number of set bits is "+snoob(x));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Next higher number with same number of set bits is 163
```

**时间复杂度:** O(1)

**辅助空间:** O(1)

**用法:**查找/生成子集。
T3】变体:T5】

1.  写一个程序找到一个比给定数字小的数字，逻辑 1 位数相同？(很简单)
2.  如何计算或生成给定集合中可用的子集？

**参考文献:**

1.  这里有一个很好的演示。
2.  《黑客之乐》(一本关于各种位魔法算法的优秀短篇书，爱好者必读)
3.  哈比森和斯蒂尔的《C A 参考手册》(一本关于标准 C 的好书，你可以在这里访问这篇文章的代码部分[。](http://www.careferencemanual.com/examples.htm)

–[**文基**](http://www.linkedin.com/in/ramanawithu) 。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。