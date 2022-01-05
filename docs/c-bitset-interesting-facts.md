# C++位集有趣的事实

> 原文:[https://www.geeksforgeeks.org/c-bitset-interesting-facts/](https://www.geeksforgeeks.org/c-bitset-interesting-facts/)

[位集](https://www.geeksforgeeks.org/c-bitset-and-its-application/)是 C++标准模板库中的一个容器，用于处理位级的数据。

1.位集存储位(只有两个可能值的元素:0 或 1)。然而，我们可以通过向位集构造函数提供位置来获得字符串的一部分(位置是相对于从左到右的字符串位置)

示例:

## C++

```
// C++ program to demonstrate that we can get part of a
// bit string in bitset.
#include <bitset>
#include <string>
#include <iostream>

int main()
{
  std::string bit_string = "110010";
  std::bitset<8> b1(bit_string);             // [0, 0, 1, 1, 0, 0, 1, 0]

  // string from position 2 till end
  std::bitset<8> b2(bit_string, 2);      // [0, 0, 0, 0, 0, 0, 1, 0]

  // string from position 2 till next 3 positions
  std::bitset<8> b3(bit_string, 2, 3);   // [0, 0, 0, 0, 0, 0, 0, 1]

  std::cout << b1 << '\n' << b2 << '\n' << b3 << '\n';

  return 0;
}
```

输出:

```
00110010
00000010
00000001
```

2.我们可以使用 std::basic_string _str 中的字符构造一个位集。可以提供可选的起始位置和长度，以及表示 set(_ 1)和 unset(_ 0)位的替代值的字符。

**语法:**

```
std::bitset b1(str, pos, n, zero, one);
str    : string used to initialize the bitset
pos    : a starting offset into str
n    : number of characters to use from str
zero    : alternate character for unset bits in str
one    : alternate characters for set bits in str 
```

*   如果 _pos > str.size()，此构造函数将引发 std::out_of_range。
*   如果在 _str 中检查的任何字符不是零或一，它将抛出 STD::invalid _ 引数。

## C++

```
// C++ program to demonstrate that we can construct bitset using
// alternate characters for set and unset bits.
#include <bitset>
#include <string>
#include <iostream>

int main()
{
    // string constructor using custom zero/one digits
    std::string alpha_bit_string = "aBaaBBaB";
    std::bitset<8> b1(alpha_bit_string, 0, alpha_bit_string.size(),
                    'a', 'B');         // [0,1,0,0,1,1,0,1]

    std::cout << b1 << '\n';
}
```

输出:

```
01001101
```

3.构造一个类位集的对象，将 N 个位初始化为与 c 风格的 0 和 1 字符串中提供的字符相对应的值。您可以在不将字符串转换为字符串类型的情况下调用构造函数。它还有两个可选参数，_Zero 和 _One，分别指示 _Str 中的哪个字符将被解释为 0 位和 1 位。

## C++

```
#include <bitset>
#include <iostream>

int main()
{
    // char* constructor using custom digits
    std::bitset<8> b1("XXXXYYYY", 8, 'X', 'Y'); // [0, 0, 0, 0, 1, 1, 1, 1]
    std::cout << b1 << '\n';
}
```

输出:

```
00001111
```

**位组操作**

**1。STD::bitset::to _ string()**
将位集的内容转换为字符串。使用零表示值为假的位，使用一表示值为真的位。结果字符串包含 N 个字符，第一个字符对应于最后(第 N-1)位，最后一个字符对应于第一位。此外，我们可以通过参数传递用于打印真值和假值的字符。

示例:

## C++

```
// C++ program to demonstrate that we can convert contents
// of bitset to a string.
#include <iostream>
#include <bitset>

int main()
{
    std::bitset<8> b(42);
    std::cout << b.to_string() << '\n'
              << b.to_string('*') << '\n'
              << b.to_string('O', 'X') << '\n';
}
```

输出:

```
00101010
**1*1*1*
OOXOXOXO
```

**2。STD::bitset::to _ ulong():**
将位集的内容转换为无符号长整数。位组的第一位对应于数字的最低有效位，最后一位对应于最高有效位。如果值不能用无符号长整型表示，函数将引发 std::overflow_error。

示例:

## C++

```
// C++ program to demonstrate that we can get value of bitset
// as  unsigned long integer.
#include <iostream>
#include <bitset>

int main()
{
    std::bitset<5> b(5);
    std::cout << b.to_ulong() << '\n';
}
```

输出:

```
5
```