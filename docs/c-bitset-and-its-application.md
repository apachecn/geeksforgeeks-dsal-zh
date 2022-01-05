# C++位集及其应用

> 原文:[https://www.geeksforgeeks.org/c-bitset-and-its-application/](https://www.geeksforgeeks.org/c-bitset-and-its-application/)

一个位集是一个布尔数组，但是每个布尔值并不是单独存储的，而是位集优化了空间，使得每个布尔只占用 1 位空间，因此位集 bs 占用的**空间小于布尔 bs[N]和向量 bs(N)** 的空间。然而，位集的一个限制是， **N 在编译时必须是已知的，即常数**(向量和动态数组没有这个限制)

由于位集以压缩的方式存储相同的信息，因此对位集的操作比数组和向量的操作更快。我们可以在数组索引运算符[]的帮助下单独访问位集的每个位，也就是说，bs[3]就像一个简单的数组一样，在位集 bs 的索引 3 处显示位。请记住，对于 10110，位集开始向后索引，0 位于第 0 和第 3 个索引处，而 1 位于第 1、第 2 和第 4 个索引处。
我们可以通过如下代码所示的构造函数，使用整数和二进制字符串构造一个位集。位集的大小在编译时是固定的，也就是说，它不能在运行时更改。
为位集类定义的**主要功能是运算符[]、计数、大小、设置、重置以及更多，它们将在下面的代码中解释–**

```
// C++ program to demonstrate various functionality of bitset
#include <bits/stdc++.h>
using namespace std;

#define M 32

int main()
{
    // default constructor initializes with all bits 0
    bitset<M> bset1;

    // bset2 is initialized with bits of 20
    bitset<M> bset2(20);

    // bset3 is initialized with bits of specified binary string
    bitset<M> bset3(string("1100"));

    // cout prints exact bits representation of bitset
    cout << bset1 << endl; // 00000000000000000000000000000000
    cout << bset2 << endl; // 00000000000000000000000000010100
    cout << bset3 << endl; // 00000000000000000000000000001100
    cout << endl;

    // declaring set8 with capacity of 8 bits

    bitset<8> set8; // 00000000

    // setting first bit (or 6th index)
    set8[1] = 1; // 00000010
    set8[4] = set8[1]; // 00010010
    cout << set8 << endl;

    // count function returns number of set bits in bitset
    int numberof1 = set8.count();

    // size function returns total number of bits in bitset
    // so there difference will give us number of unset(0)
    // bits in bitset
    int numberof0 = set8.size() - numberof1;

    cout << set8 << " has " << numberof1 << " ones and "
         << numberof0 << " zeros\n";

    // test function return 1 if bit is set else returns 0
    cout << "bool representation of " << set8 << " : ";
    for (int i = 0; i < set8.size(); i++)
        cout << set8.test(i) << " ";

    cout << endl;

    // any function returns true, if atleast 1 bit
    // is set
    if (!set8.any())
        cout << "set8 has no bit set.\n";

    if (!bset1.any())
        cout << "bset1 has no bit set.\n";

    // none function returns true, if none of the bit
    // is set
    if (!bset1.none())
        cout << "bset1 has some bit set\n";

    // bset.set() sets all bits
    cout << set8.set() << endl;

    // bset.set(pos, b) makes bset[pos] = b
    cout << set8.set(4, 0) << endl;

    // bset.set(pos) makes bset[pos] = 1  i.e. default
    // is 1
    cout << set8.set(4) << endl;

    // reset function makes all bits 0
    cout << set8.reset(2) << endl;
    cout << set8.reset() << endl;

    // flip function flips all bits i.e.  1 <-> 0
    // and  0 <-> 1
    cout << set8.flip(2) << endl;
    cout << set8.flip() << endl;

    // Converting decimal number to binary by using bitset
    int num = 100;
    cout << "\nDecimal number: " << num
         << "  Binary equivalent: " << bitset<8>(num);

    return 0;
}
```

输出:

```
00000000000000000000000000000000
00000000000000000000000000010100
00000000000000000000000000001100

00010010
00010010 has 2 ones and 6 zeros
bool representation of 00010010 : 0 1 0 0 1 0 0 0 
bset1 has no bit set.
11111111
11101111
11111111
11111011
00000000
00000100
11111011

Decimal number: 100 Binary equivalent: 01100100

```

对于位集设置，定义了复位和翻转功能。Set 函数设置(1)如果未提供参数，则设置位集的所有位，否则设置其位置作为参数的位。同样，如果在没有参数的情况下调用 reset 和 flip，它们会在整个位集上执行操作，如果提供某个位置作为参数，则它们只在该位置执行操作。
对于位集，所有按位运算符都是重载的，也就是说，它们可以直接应用于位集，而无需任何强制转换或转换，主要重载运算符有&、|、==、！=和移位运算符< >，这使得位集上的操作变得容易。
上述运算符的用法如下代码所示。

```
// C++ program to show applicable operator on bitset.
#include <bits/stdc++.h>
using namespace std;

int main()
{
    bitset<4> bset1(9); // bset1 contains 1001
    bitset<4> bset2(3); // bset2 contains 0011

    // comparison operator
    cout << (bset1 == bset2) << endl; // false 0
    cout << (bset1 != bset2) << endl; // true  1

    // bitwise operation and assignment
    cout << (bset1 ^= bset2) << endl; // 1010
    cout << (bset1 &= bset2) << endl; // 0010
    cout << (bset1 |= bset2) << endl; // 0011

    // left and right shifting
    cout << (bset1 <<= 2) << endl; // 1100
    cout << (bset1 >>= 1) << endl; // 0110

    // not operator
    cout << (~bset2) << endl; // 1100

    // bitwise operator
    cout << (bset1 & bset2) << endl; // 0010
    cout << (bset1 | bset2) << endl; // 0111
    cout << (bset1 ^ bset2) << endl; // 0101
}
```

输出:

```
0
1
1010
0010
0011
1100
0110
1100
0010
0111
0101

```

本文由乌卡什·特里维迪供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。