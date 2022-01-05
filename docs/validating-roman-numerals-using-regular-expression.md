# 使用正则表达式验证罗马数字

> 原文:[https://www . geesforgeks . org/validating-Roman-numbers-use-正则表达式/](https://www.geeksforgeeks.org/validating-roman-numerals-using-regular-expression/)

给定一个**字符串**，你必须验证给定的字符串是否是有效的罗马数字。如果有效，打印“真”或“假”。
**注**:数字在 1 到 3999 之间。
**例:**

```
Input: String = IX  
Output: True 

Input: String = 54IVC 
Output: False
```

罗马数字基于以下符号。

```
SYMBOL       VALUE
I             1
IV            4
V             5
IX            9
X             10
XL            40
L             50
XC            90
C             100
CD            400
D             500
CM            900 
M             1000       
```

罗马数字中的数字是由这些符号按降序排列而成的字符串(例如，先写 M，后写 D，等等)。).但是，在少数特定情况下，为了避免四个字符连续重复(如 IIII 或 XXXX)，经常使用**减法符号**如下:

*   **I** 放在 **V** 或 **X** 前面表示少一个，所以四是 **IV** (少一个 5)，九是 IX(少一个 10)。
*   **X** 放在 **L** 或 **C** 前面表示少了十个，所以四十是 **XL** (少了 10 个 50 个)而 90 是 **XC** (少了 10 个 100 个)。
*   **C** 放在 **D** 或 **M** 前面表示少一百，所以四百是 **CD** (少一百五百)九百是 **CM** (少一百一千)。

**进场:**

*   检查字符串是否为有效罗马数字的正则表达式是这样的:

```
 ^M{0,3}(CM|CD|D?C{0,3})(XC|XL|L?X{0,3})(IX|IV|V?I{0,3})$
```

*   其中，
    1.  **M{0，3}** 指定千段，基本限制在 0-4000 之间

    2.  **(CM|CD|D？C{0，3})** 为百节。

    3.  **(XC|XL|L？X{0，3})** 为十位。

    4.  最后， **(IX|IV|V？I{0，3})** 是单位部分。

*   导入正则表达式，在表达式中搜索输入字符串，如果字符串存在，返回真，否则返回假

下面是上述方法的实现。

## 蟒蛇 3

```
# Python3 program to Validate the Roman numeral

# Function to Validate the Roman numeral
def ValidationOfRomanNumerals(string):

    # Importing regular expression
    import re

    # Searching the input string in expression and
    # returning the boolean value
    print(bool(re.search(r"^M{0,3}(CM|CD|D?C{0,3})(XC|XL|L?X{0,3})(IX|IV|V?I{0,3}){content}quot;,string)))

# Driver code

# Given string
string="XI"

# Function call
ValidationOfRomanNumerals(string)
```

**Output:** 

```
True
```