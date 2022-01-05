# 在 C++中将字符数组转换为字符串

> 原文:[https://www . geesforgeks . org/convert-character-array-to-string-in-c/](https://www.geeksforgeeks.org/convert-character-array-to-string-in-c/)

本文展示了如何在 C++中将字符数组转换为字符串。
c++中的 [std::string](https://www.geeksforgeeks.org/stdstring-class-in-c/) 有很多内置函数，这使得实现比处理字符数组容易得多。因此，如果我们将字符数组转换为字符串，通常会更容易工作。
**示例:**

```
Input: char s[] = { 'g', 'e', 'e', 'k', 's', 'f', 'o',
                     'r', 'g', 'e', 'e', 'k', 's' } ;
Output: string s = "geeksforgeeks" ;

Input: char s[] = { 'c', 'o', 'd', 'i', 'n', 'g' } ;
Output: string s = "coding" ;
```

*   **方法 1:**
    **进场:**
    1.  获取字符数组及其大小。
    2.  创建一个空字符串。
    3.  遍历字符数组。
    4.  迭代时，继续将字符数组中遇到的字符连接到字符串中。
    5.  返回字符串。

下面是上述方法的实现。

## C++

```
// Demonstrates conversion
// from character array to string

#include <bits/stdc++.h>
using namespace std;

// converts character array
// to string and returns it
string convertToString(char* a, int size)
{
    int i;
    string s = "";
    for (i = 0; i < size; i++) {
        s = s + a[i];
    }
    return s;
}

// Driver code
int main()
{
    char a[] = { 'C', 'O', 'D', 'E' };
    char b[] = "geeksforgeeks";

    int a_size = sizeof(a) / sizeof(char);
    int b_size = sizeof(b) / sizeof(char);

    string s_a = convertToString(a, a_size);
    string s_b = convertToString(b, b_size);

    cout << s_a << endl;
    cout << s_b << endl;

    return 0;
}
```

*   **方法 2:**
    [STD::string](https://www.geeksforgeeks.org/stdstring-class-in-c/)有一个内置的构造器为我们工作。这个构造函数接受一个空终止的字符序列作为它的输入。但是，我们只能在字符串声明时使用此方法，并且它不能再次用于同一字符串，因为它使用的构造函数只有在我们声明字符串时才会调用。
    **进近:**
    1.  获取字符数组及其大小。
    2.  声明一个字符串(即字符串类的一个对象)，并在这样做的同时将字符数组作为其构造函数的参数。
    3.  使用语法:string _ name(character _ array _ name)；
    4.  返回字符串。

下面是上述方法的实现。

## C++

```
// Demonstrates conversion
// from character array to string

#include <bits/stdc++.h>
using namespace std;

// uses the constructor in string class
// to convert character array to string
string convertToString(char* a)
{
    string s(a);

    // we cannot use this technique again
    // to store something in s
    // because we use constructors
    // which are only called
    // when the string is declared.

    // Remove commented portion
    // to see for yourself

    /*
    char demo[] = "gfg";
    s(demo); // compilation error
    */

    return s;
}

// Driver code
int main()
{
    char a[] = { 'C', 'O', 'D', 'E' };
    char b[] = "geeksforgeeks";

    string s_a = convertToString(a);
    string s_b = convertToString(b);

    cout << s_a << endl;
    cout << s_b << endl;

    return 0;
}
```

*   **方法 3:**
    另一种方法是使用重载的“=”运算符，该运算符也可以在 [C++ std::string](https://www.geeksforgeeks.org/stdstring-class-in-c/) 中找到。
    **进近:**
    1.  获取字符数组及其大小。
    2.  声明一个字符串。
    3.  使用重载的“=”运算符将字符数组中的字符赋给字符串。
    4.  返回字符串。

下面是上述方法的实现。

## C++

```
// Demonstrates conversion
// from character array to string

#include <bits/stdc++.h>
using namespace std;

// uses overloaded '=' operator from string class
// to convert character array to string
string convertToString(char* a)
{
    string s = a;
    return s;
}

// Driver code
int main()
{
    char a[] = { 'C', 'O', 'D', 'E' };
    char b[] = "geeksforgeeks";

    string s_a = convertToString(a);
    string s_b = convertToString(b);

    cout << s_a << endl;
    cout << s_b << endl;

    return 0;
}
```