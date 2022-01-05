# 如何创建一半大写，另一半小写的字符串？

> 原文:[https://www . geeksforgeeks . org/如何创建大写字母一半字符串和小写字母另一半字符串/](https://www.geeksforgeeks.org/how-to-create-half-of-the-string-in-uppercase-and-the-other-half-in-lowercase/)

在解决这类问题时，我们必须牢记的第一件事是字符串是不可变的，即，

如果我拿着下面的绳子

```
var string1 = "geeksforgeeks";
string1[0] = "G";

console.log(string1);
```

由于字符串是不可变的，所以我们不能改变字符串的字符，所以上面代码的输出将如下。

**输出:**

```
geeksforgeeks
```

**进场:**

有几种方法可以解决这个问题。其中一些如下。

*   Split the string into 2 different parts, change the first part to uppercase, and connect the new string to get the output.
*   Create an empty string and use [**for**](https://www.geeksforgeeks.org/javascript-for-loop/) loop to add each character of the string to it.
*   Get the output by using the slice attribute of the string.

**方法 1:** 该方法使用 2 个新变量实现。

*   Add a string to a variable.
*   Use the [string.length](https://www.geeksforgeeks.org/javascript-string-length/) function to store the length of the string into the variable.
*   Create two empty strings to store the newly created strings in the future.
*   Use [to loop](https://www.geeksforgeeks.org/javascript-for-loop/) to traverse the string.
*   Use [T0】 to ppercase() 【T1] to convert the first string to uppercase.
*   Connect two strings to get output.

## c++

```
#include <iostream>
using namespace std;

int main() {
  string str = "geeksforgeeks",ans;
  int len = str.length();

  for(int i = 0;i<len;i++){
    if(i<=len/2){
      char a = toupper(str[i]);
      ans.push_back(a);
    }else
      ans.push_back(str[i]);

  }
  cout<<ans;
  return 0;
}

// This code is co ntributed by rohitsingh07052
```

## python 3

```
import math

string1 = 'geeksforgeeks'
string1_len = len(string1)
part_a = ''
part_b = ''

for i in range(int(math.ceil(string1_len // 2 + 1))):
    part_a += string1[i]

for i in range(int(math.ceil(string1_len // 2)) + 1,
               string1_len):
    part_b += string1[i]

new_part_a = part_a.upper()

changed_string = new_part_a + part_b

print(changed_string)

# This code is contributed by ukasp
```

## Javascript

```
<script>
var string1 = 'geeksforgeeks';
var string1_len = string1.length;
var part_a = '';
var part_b = '';

for(var i=0 ; i<Math.ceil(string1_len/2) ; i++)
{
    part_a+=string1[i];
}

for(var i=Math.ceil(string1_len/2) ; i<string1_len ; i++)
{
    part_b+=string1[i];
}

var new_part_a = part_a.toUpperCase();

var changed_string = new_part_a + part_b;

console.log(changed_string);
</script>
```

**输出:**

```
GEEKSFOrgeeks
```

**方法 2:** 该方法使用单个新变量实现。

*   Add a string to a variable.
*   Use the [string.length](https://www.geeksforgeeks.org/javascript-string-length/) function to store the length of the string into a variable.
*   Create an empty string to store the newly created string in the future.
*   Use [to loop](https://www.geeksforgeeks.org/javascript-for-loop/) to traverse the string.
*   Record the last string and output it.

## Javascript

```
<script>
var string1 = 'gfg';
var string1_len = string1.length;
var changed_string = '';

for(var i=0 ; i<Math.ceil(string1_len/2) ; i++)
{
    changed_string+=string1[i].toUpperCase();
}

for(var i=Math.ceil(string1_len/2) ; i<string1_len ; i++)
{
    changed_string+=string1[i];
}

console.log(changed_string);
</script>
```

## python 3

```
import math

string1 = 'gfg';
string1_len = len(string1)

changed_string = ''

for i in range(math.ceil(string1_len/2)):
    changed_string += string1[i].upper();

for i in range(math.ceil(string1_len/2), string1_len):
    changed_string += string1[i]

print(changed_string)

# This code is contributed by avanitrachhadiya2155
```

**输出:**

```
GFg
```

**方法 3:** 该方法使用 JavaScript [切片](https://www.geeksforgeeks.org/javascript-string-slice/)属性实现。

*   Add a string to a variable.
*   Use the [string.length](https://www.geeksforgeeks.org/javascript-string-length/) function to store the length of the string into the variable.
*   Store the [ceil](https://www.geeksforgeeks.org/javascript-math-ceil-method/) value of half the length of the string in a new variable.
*   Create 2 empty strings to store the newly created strings in the future.
*   Use the string [slice](https://www.geeksforgeeks.org/javascript-string-slice/) attribute to add a string to a variable.
*   Use [to convert the first string into uppercase for display (](https://www.geeksforgeeks.org/javascript-string-touppercase/)).
*   Connect two strings to get output.

## python 3

```
import math

string1 = 'geeks for geeks'

string1_len = len(string1)

half_string = math.ceil(string1_len/2)

part_a = ''
part_b = ''

part_a = string1[:half_string]
new_part_a = part_a.upper()

part_b = string1[half_string:string1_len]

changed_string = new_part_a+part_b

print(changed_string)

# This code is contributed by rag2127
```

## Javascript

```
<script>
var string1 = 'geeks for geeks';
var string1_len = string1.length;
var half_string = Math.ceil(string1_len/2);
var part_a;
var part_b;

part_a = string1.slice(0,half_string);
var new_part_a = part_a.toUpperCase();
part_b = string1.slice(half_string,string1_len);

var changed_string = new_part_a+part_b;

console.log(changed_string);
</script>
```

**输出:**

```
GEEKS FOr geeks
```

通过这些方式，你可以解决这类问题。