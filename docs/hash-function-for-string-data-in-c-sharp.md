# C# 中字符串数据的哈希函数

> 原文：[https://www.geeksforgeeks.org/hash-function-for-string-data-in-c-sharp/](https://www.geeksforgeeks.org/hash-function-for-string-data-in-c-sharp/)

**问题**：用 C# 编写代码以哈希键数组并显示其哈希码。

答案：哈希表是一种广泛使用的数据结构，用于存储以其哈希码索引的值（即键）。 哈希码是哈希函数的结果，用作存储键的索引的值。 如果两个不同的键散列到相同的值，则将这种情况称为*冲突*，并且良好的散列函数可以最大程度地减少冲突。

**问题**：如何选择适合该数据的哈希函数？

答案：如果您的数据由整数组成，那么最简单的哈希函数是返回键除法和表大小的余数。 保持表的大小为质数很重要。 但是可以编写更复杂的函数来避免冲突。 如果您的数据由字符串组成，则可以将字母的所有 ASCII 值相加，然后将和与表的大小取模（以下代码对此进行了描述）。

**示例 1**：

```
// C# Program to create a Hash
// Function for String data
using System;
class Geeks {
// Main Method
public static void Main(String []args)
{
// Declaring the an string array
string [] values = new
string str;
// Values of the keys stored
string [] keys = new string [] { "Alphabets" ,
"Roman" , "Numbers" , "Alphanumeric" ,
"Tallypoints" };
int hashCode;
for ( int k = 0; k < 5; k++) {
str = keys[k];
// calling HashFunction
hashCode = HashFunction(str, values);
[
// Storing keys at their hashcode's index
values[hashCode] = str;
}
// Displaying Hashcodes along with key values
for ( int k = 0; k < (values.GetUpperBound(0)); k++) {
if (values[k] != null )
Console.WriteLine(k + " " + values[k]);
}
}

// Defining the hash function
static int HashFunction( string s, string [] array)
{
int total = 0;
char [] c;
c = s.ToCharArray();
// Summing up all the ASCII values
// of each alphabet in the string
for ( int k = 0; k <= c.GetUpperBound(0); k++)
total += ( int )c[k];
[
return total % array.GetUpperBound(0);
}
}
```

**输出**：

```
11 Tallypoints
16 Alphanumeric
19 Roman
34 Alphabets
46 Numbers

```

**示例 2**：

```
// C# Program to create a Hash
// Function for String data
using System;
class Geeks {
// Main Method
public static void Main(String []args)
{
// Declaring the an string array
string [] values = new string [50];
string str;
// Values of the keys stored
string [] keys = new string [] { "C" , "C++" ,
"Java" , "Python" , "C#" , "HTML" };
int hashCode;
for ( int k = 0; k < 5; k++) { [HT G191]
str = keys[k];
hashCode = HashFunction2(str, values);
// Storing keys at their hashcode's index
values[hashCode] = str;
}
// Displaying Hashcodes along with key values
for ( int k = 0; k < (values.GetUpperBound(0)); k++) {
if (values[k] != null )
Console.WriteLine(k + " " + values[k]);
}
}
// Defining the hash function
static int HashFunction2( string s, string [] array)
{
long total = 0;
char [] c;
c = s.ToCharArray();
[ HTG23 6]   [
// Horner's rule for generating a polynomial
// of 11 using ASCII values of the characters
for ( int k = 0; k <= c.GetUpperBound(0); k++)
total += 11 * total + ( int )c[k];
total = total % array.GetUpperBound(0);
if (total < 0)
total += array.GetUpperBound(0);
return ( int )total;
}
}
```

**输出**：

```
6 C#
15 C++
18 C
19 Python
28 Java

```

**说明**：在`HashFunction`中，我们将参数作为要散列的字符串以及字符串数据`"value"`传递。 方法[`ToCharArray`](https://www.geeksforgeeks.org/c-tochararray-method/)将字符串转换为字符数组，然后从字符数组的开始到结尾开始`for`循环。 在`for`循环内，我们计算数组中每个字符的 ASCII 值的总和。 方法[`GetUpperBound`](https://www.geeksforgeeks.org/c-finding-the-index-of-last-element-in-the-array/)返回数组最高索引的值。 然后，哈希函数以数组的上限返回总和的模（在本例中为 49，因为`string[] values = new string[50]`）。 在`HashFunction2`中，我们传递了相同的参数，但是此函数发生冲突的可能性较小。 除了此处我们使用 Horner 规则计算 11 的多项式函数外，所有内容基本相同。



* * *

* * *



