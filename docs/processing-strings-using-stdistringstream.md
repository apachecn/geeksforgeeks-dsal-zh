# 使用 STD::isting stream 处理字符串

> 原文:[https://www . geeksforgeeks . org/processing-strings-using-stdistingstream/](https://www.geeksforgeeks.org/processing-strings-using-stdistringstream/)

**STD::is tingstream**是一个字符串类对象，用于[将字符串](https://www.geeksforgeeks.org/stringstream-c-applications/)流式传输到不同的变量中，类似的文件也可以流式传输到字符串中。此类的对象使用包含一系列字符的字符串缓冲区。这个字符序列可以作为字符串对象来访问。
**头文件:**

```
#include <sstream>
```

**<u>1。从带有 STD::istingstream 的字符串中流式传输整数</u>**

对字符串进行流式处理的一种方法是使用标题中的输入字符串流对象**STD::isting stream**。一旦创建了一个 **std::istringstream** 对象，就可以使用[提取操作符](https://www.geeksforgeeks.org/manipulators-in-c-with-examples/) ( **> >** )对字符串进行流式传输和存储。提取操作符将一直读取，直到到达空白或流失败。
以下是**标准的说明:** :

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate std::istringstream
#include <iostream>
#include <sstream>
#include <string>
using std::istringstream;
using std::string;
using std::cout;

// Driver Code
int main()
{
    // Input string
    string a("1 2 3");

    // Object class of istringstream
    istringstream my_stream(a);

    // Variable to store number n
    int n;

    // Stream a number till white space
    // is encountered
    my_stream >> n;

    // Print the number
    cout << n << "\n";
}
```

**Output:** 

```
1
```

**STD::is tingstream**对象也可以用作布尔值来确定最后一次提取操作是否失败。如果流中没有更多的字符串，就会发生这种情况，**例如，**如果流中仍然有更多的字符，那么我们就可以再次对字符串进行流式处理。
提取运算符 **> >** 将流写入运算符右侧的变量，并返回**STD::is tingstream**对象，因此整个表达式 **my_stream > > n** 是一个 STD::is tingstream 对象，它返回一个布尔值，即如果流是可能的，则返回 true，否则返回 false。
以下是通过上述方式使用**STD::isting stream**的实现:

## 类型 1

```
// C++ program to illustrate std::istringstream
#include <iostream>
#include <sstream>
#include <string>
using std::istringstream;
using std::string;
using std::cout;

// Driver Code
int main()
{
    // Input string
    string a("1 2 3");

    // Object class of istringstream
    istringstream my_stream(a);

    // Variable to store number n
    int n;

    // Testing to see if the stream was
    // successful and printing results.
    while (my_stream) {

        // Streaming until space is
        // encountered
        my_stream >> n;

        // If my_stream is not empty
        if (my_stream) {
            cout << "That stream was successful: "
                 << n << "\n";
        }

        // Else print not successful
        else {
            cout << "That stream was NOT successful!"
                 << "\n";
        }
    }

    return 0;
}
```

## 类型 2

```
// C++ program to illustrate std::istringstream
#include <iostream>
#include <sstream>
#include <string>
using std::istringstream;
using std::string;
using std::cout;

// Driver Code
int main()
{
    // Input string
    string a("1 2 3");

    // Object class of istringstream
    istringstream my_stream(a);

    // Variable to store number n
    int n;

    // Testing to see if the stream was
    // successful and printing results.
    while (my_stream >> n) {

        cout << "That stream was successful: "
             << n << "\n";
    }

    cout << "That stream was NOT successful!"
         << "\n";
    return 0;
}
```

**Output:** 

```
That stream was successful: 1
That stream was successful: 2
That stream was successful: 3
That stream was NOT successful!
```

**<u>2。混合类型琴弦</u>T3**

在上图中，字符串只包含空格和可以转换为 int 的字符。如果字符串具有混合类型，即它在流中包含不止一种数据类型，则可以使用它，如下所示。
以下是混合类型的**标准:行政流**:
**程序 1:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate std::istringstream
// when string has integer followed by character
#include <iostream>
#include <sstream>
#include <string>
using std::istringstream;
using std::string;
using std::cout;

// Driver Code
int main()
{
    // Input string
    string str("1, 2, 3");

    // Object class of istringstream
    istringstream my_stream(str);

    // Variable to store the number n
    // and character ch
    char c;
    int n;

    // Traverse till input stream is valid
    while (my_stream >> n >> c) {

        cout << "That stream was successful: "
             << n << " " << c << "\n";
    }
    cout << "The stream has failed."
         << "\n";

    return 0;
}
```

**Output:** 

```
That stream was successful: 1,
That stream was successful: 2,
The stream has failed.
```

**节目 2:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate std::istringstream
// to tokenize the string
#include <iostream>
#include <sstream>
#include <string>
using std::istringstream;
using std::string;
using std::cout;

// Driver Code
int main()
{
    // Input string
    string str("abc, def,   ghi");

    // Object class of istringstream
    istringstream my_stream(str);

    // To store the stream string
    string token;

    size_t pos = -1;

    // Traverse till stream is valid
    while (my_stream >> token) {

        // If ',' is found then tokenize
        // the string token
        while ((pos = token.rfind(','))
               != std::string::npos) {
            token.erase(pos, 1);
        }

        // Print the tokenize string
        cout << token << '\n';
    }
}
```

**Output:** 

```
abc
def
ghi
```

**参考:**T2http://www.cplusplus.com/reference/sstream/istringstream/