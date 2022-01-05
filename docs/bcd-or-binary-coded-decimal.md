# BCD 或二进制编码十进制

> 原文:[https://www.geeksforgeeks.org/bcd-or-binary-coded-decimal/](https://www.geeksforgeeks.org/bcd-or-binary-coded-decimal/)

**二进制编码十进制**或 **BCD** 是将十进制数转换为二进制等价数的另一个过程。

*   这是一种二进制编码形式，十进制数中的每个数字都以位的形式表示。
*   这种编码可以用 4 位或 8 位来完成(通常 4 位是优选的)。
*   与现有的二进制系统相比，这是一种将十进制数转换为二进制数的快速有效的系统。
*   这些通常用于数字显示器，在数字显示器中，数据处理是一项相当艰巨的任务。
*   因此，脑机接口在这里起着重要的作用，因为处理是将每个数字作为一个单独的子电路来完成的。

许多十进制值在二进制中有无限的位值表示，但在二进制编码的十进制中有有限的位值。例如，二进制中的 0.2 是. 001100…而 BCD 中的 0.0010。它避免了分数误差，也用于巨大的金融计算。

考虑下面的真值表，并关注这些是如何表示的。

**二进制编码十进制真值表**

<figure class="table">

| 小数 | BCD |
| --- | --- |
| Zero | 0000 |
| one | 0001 |
| Two | 0010 |
| three | 0011 |
| four | 0100 |
| five | 0101 |
| six | 0110 |
| seven | 0111 |
| eight | One thousand |
| nine | One thousand and one |

</figure>

在 **BCD 编号系统**中，给定的十进制数被分成四位的块，用于该数中的每个十进制数字。每个十进制数字都被转换成它的直接二进制形式(通常用 4 位表示)。

**例如:**

> 1.以 BCD 格式转换(123)10
> 
> 从上表的真值表来看，
> 1->0001
> 2->0010
> 3->0011
> 这样，BCD 就变成了- > 0001 0010 0011

> 2.以 BCD 格式转换(324)10
> 
> (324)10 -> 0011 0010 0100 (BCD)
> 
> 再从真值表上看，
> 3->0011
> 2->0010
> 4->0100
> 这样，BCD 就变成了- > 0011 0010 0100

这就是十进制数如何转换成它们的等价 BCD。

*   值得注意的是，BCD 只不过是十进制数每个数字的二进制表示。
*   不可忽视的是，给定十进制数的 BCD 表示使用了额外的位，这使得它权重很大。

**相关文章:**

1.  [将 BCD 数转换为十进制数的程序](https://www.geeksforgeeks.org/program-to-convert-bcd-number-into-decimal-number/)

2.  [数字逻辑中的 BCD 加法器](https://www.geeksforgeeks.org/bcd-adder-in-digital-logic/)

3.  [BCD 至 7 段解码器](https://www.geeksforgeeks.org/bcd-to-7-segment-decoder/)