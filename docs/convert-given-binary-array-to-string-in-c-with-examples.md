# 在 C++中将给定的二进制数组转换为字符串，示例

> 原文:[https://www . geesforgeks . org/convert-given-binary-array-to-string-in-c-with-examples/](https://www.geeksforgeeks.org/convert-given-binary-array-to-string-in-c-with-examples/)

给定一个包含 **N** 整数元素的二进制数组 **arr[]** ，任务是创建一个包含所有 **N** 元素的字符串 **s** ，其索引与数组 **arr[]** 中的索引相同。

**示例:**

> ***输入:** arr[] = {0，1，0，1}*
> ***输出:**字符串**=**【0101*****
> 
> *********输入:*** *arr[] = { 1，1，0，0，1，1}*
> ***输出:****string = " 110011 "*******

****在 C++中将二进制数组转换为字符串的不同方法有:****

1.  ****使用 to_string()函数。****
2.  ****使用字符串流。****
3.  ****向每个整数添加字符“0”。****
4.  ****使用类型铸造。****
5.  ****使用推回功能。****
6.  ****使用 transform()函数。****

****让我们开始详细讨论这些功能。****

******<u>使用 to_string()功能</u>******

****[to_string()函数](https://www.geeksforgeeks.org/stdto_string-in-cpp/)接受单个整数，并将整数值转换为字符串。****

******语法:******

> ****string to _ string(int val)；****
> 
> ******参数:**
> 值–数值。****
> 
> ******返回值:**
> 一个字符串对象，包含作为字符序列的 val 表示。****

****下面是实现上述方法的 C++程序:****

## ****C++****

```
**// C++ program to implement
// the above approach
#include <iostream>
#include <string>
using namespace std;

// Driver code
int main()
{
  int arr[5] = {1, 0, 1, 0, 1};
  int size = sizeof(arr) / sizeof(arr[0]);

  // Creating an empty string
  string s = "";
  for(int i = 0; i < size; i++) 
  {
    s += to_string(arr[i]);
  }

  cout << s;
  return 0;
}**
```

******输出:******

> ****Ten thousand one hundred and one****

******<u>使用弦流</u>******

****[stringstream 类](https://www.geeksforgeeks.org/stringstream-c-applications/)在解析输入时非常有用。stringstream 将一个字符串对象与一个流相关联，允许您像读取流一样读取该字符串(如 cin)。要使用 stringstream 类，**流头文件**需要包含在代码中。****

****基本方法有:****

> ******清除():**清除溪流****
> 
> ******str():** 获取并设置流中存在内容的字符串对象。****
> 
> ******操作符< <** 给 stringstream 对象添加一个字符串。****
> 
> ******操作符> >** 从 stringstream 对象中读取一些东西，****

****stringstream 类可用于以下列方式将整数值转换为字符串值:****

1.  ****使用 **' < < '** 运算符将数据插入流中。****
2.  ****使用 **' > > '** 运算符或使用 str()函数从流中提取数据。****
3.  ****将提取的数据与字符串**的**连接起来。****

****下面是实现上述方法的 C++程序:****

## ****C++****

```
**// C++ program to implement
// the above approach
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

// Driver code
int main()
{
  int arr[5] = {1, 0, 1, 0, 1};
  int size = sizeof(arr) / sizeof(arr[0]);

  // Creating an empty string
  string s = "";
  for(int i = 0; i < size; i++) 
  {
    // Creating an empty stringstream
    stringstream temp;

    // Inserting data into the stream
    temp << arr[i];

    // Extracting data from stream using 
    // .str() function
    s += temp.str();
  }

  // Printing the string 
  cout << s;
}**
```

******输出:******

> ****Ten thousand one hundred and one****

******<u>给每个整数加上字符“0”</u>******

****向每个整数添加字符“0”的方法非常简单。****

1.  ****第一步是声明一个空字符串。****
2.  ****迭代数组的每个元素，并通过将字符“0”的 ASCII 值与字符串 s 相加来连接每个整数****

******逻辑:**
用整数 0 和 1 相加字符“0”的 ASCII 值的结果由编译器计算如下:****

> ******字符“0”的十进制值为 48。******
> 
> ****字符串+= 0+' 0 '
> /+= 0+48
> /+= 48
> 十进制 48 的字符值为 **'0'** 。****
> 
> ****字符串+= 1+' 0 '
> /+= 1+48
> /+= 49
> 十进制 49 的 Char 值为 **'1'** 。****

****下面是实现上述方法的 C++程序:****

## ****C++****

```
**// C++ program to implement 
// the above approach
#include <iostream>
#include <string>
using namespace std;

// Driver code
int main() 
{
  int arr[5] = {1, 1, 1, 0, 1};
  int size = sizeof(arr) / sizeof(arr[0]);
  string s = "";

  // Creating an empty string
  for(int i = 0; i < size; i++) 
  {
    // arr[i] + 48
    // adding ASCII of value of 0 
    // i.e., 48
    s += arr[i] + '0'; 
  }

  // Printing the string 
  cout << s;
}**
```

******输出:******

> ****Eleven thousand one hundred and one****

******<u>采用</u>式铸造******

****在类型转换和连接之前，需要在整数上加上 48，否则会在输出端产生一些奇怪的符号。这是因为在 ASCII 表中，从 0 到 9 的数字有一个从 48 到 57 开始的字符值。在二进制数组的情况下，整数将是 0 或 1。****

1.  ****如果为 0，则添加后为 48，然后在类型转换**后，字符“0”**与字符串连接。****
2.  ****如果是 1，相加后将是 49，然后在类型转换**后，字符“1”**与字符串连接。****

****下面是实现上述方法的 C++程序:****

## ****C++****

```
**// C++ program to implement
// the above approach
#include <iostream>
#include <string>
using namespace std;

// Driver code
int main()
{
  int arr[5] = {1, 1, 1, 0, 1};
  int size = sizeof(arr) / sizeof(arr[0]);

  // Creating an empty string
  string s = "";
  for(int i = 0; i < size; i++) 
  {
    arr[i] += 48;
    s += (char) arr[i];
  }

  // Printing the string
  cout << s;
}**
```

******输出:******

> ****Eleven thousand one hundred and one****

******<u>使用 push_back()功能</u>******

****提供 [push_back()](https://www.geeksforgeeks.org/stdstringpush_back-in-cpp/) 成员函数追加字符。将字符 c 追加到字符串的末尾，使其长度增加一。****

******语法:******

> ****void string:: push_back (char c)****
> 
>  ******参数:**
> 要追加的字符。
> 
> **返回值:**
> 无
> 
> **错误:**
> 如果结果大小超过最大字符数(max_size)，将抛出 length_error。****

******注:**
加**字符‘0’**背后的逻辑已经在方法“整数加‘0’”中讨论过。****

****下面是实现上述方法的 C++程序:****

## ****C++****

```
**// C++ program to implement 
// the above approach
#include <iostream>
#include <vector>
using namespace std;

// Driver code
int main() 
{
  int arr[5] = {1, 0, 1, 0, 1};
  int size = sizeof(arr) / sizeof(arr[0]);
  vector<char> s;
  for(int i = 0; i < size; i++) 
  {
    s.push_back(arr[i] + '0');
  }
  for(auto it : s) 
  {
    cout << it;
  }
}**
```

******输出:******

> ****Ten thousand one hundred and one****

******<u>使用变换()功能</u>******

****[transform()函数](https://www.geeksforgeeks.org/transform-c-stl-perform-operation-elements/)依次对一个数组的元素进行运算，并将结果存储在另一个输出数组中。要使用 transform()函数，请包含算法头文件。****

****下面是实现上述方法的 C++程序:****

## ****C++****

```
**// C++ program to implement
// the above method
#include <iostream>
#include <algorithm>
using namespace std;

// define int to char function
char intToChar(int i) 
{
  // logic behind adding 48 to integer 
  // is discussed in Method "using type
  // casting".
  return i + 48;
}

// Driver code
int main() 
{
  int arr[5] = {1, 0, 1, 0, 1};
  int size = sizeof(arr) / sizeof(arr[0]);
  char str[size + 1]; 
  transform(arr, arr + 5, str, intToChar);

  // Printing the string
  cout << str;
}**
```

******输出:******

> ****Ten thousand one hundred and one****