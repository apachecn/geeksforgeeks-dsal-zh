# 检查给定的电子邮件地址在 C++中是否有效

> 原文:[https://www . geesforgeks . org/check-if-given-email-address-is-valid-or-not-in-CPP/](https://www.geeksforgeeks.org/check-if-given-email-address-is-valid-or-not-in-cpp/)

给定一个表示[电子邮件地址](https://en.wikipedia.org/wiki/Email_address)的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **电子邮件**，任务是检查给定的字符串是否是有效的电子邮件 id。如果发现为真，则打印**“有效”**。否则，打印**“无效”**。有效的电子邮件地址由电子邮件前缀和电子邮件域组成，两者都采用可接受的格式:

*   电子邮件地址必须以字母开头(没有数字或符号)。
*   字符串中的某个点之前一定有一个 **@** 。
*   在 **@** 符号之后但在点之前必须有文本。
*   圆点后必须有圆点和文字。

**示例:**

> **输入:**email = " contribute @ geeks forgeeks . org " ****输出:** Valid
> **解释:**
> 给定的字符串遵循有效电子邮件字符串的所有标准。**
> 
> ****输入:**email = " contribute @ geeks forgeeks..组织"
> **输出:**无效**

****[字符串遍历](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)基于方法:**遵循以下步骤:**

1.  **检查电子邮件 id 字符串的第一个字符是否是字母。如果没有，那么邮件就是**无效**。**
2.  **现在遍历字符串**电子邮件**找到**“@”**和**的位置。**如果**“@”**或**”**不存在，则电子邮件为**无效**。**
3.  **如果**。”**“@”**后**不存在，则邮件为**无效**。**
4.  **如果**。”**是字符串**电子邮件**的最后一个字符，则电子邮件 id 为**无效**。**
5.  **否则，邮件为**有效**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check the character
// is an alphabet or not
bool isChar(char c)
{
    return ((c >= 'a' && c <= 'z')
            || (c >= 'A' && c <= 'Z'));
}

// Function to check the character
// is an digit or not
bool isDigit(const char c)
{
    return (c >= '0' && c <= '9');
}

// Function to check email id is
// valid or not
bool is_valid(string email)
{
    // Check the first character
    // is an alphabet or not
    if (!isChar(email[0])) {

        // If it's not an alphabet
        // email id is not valid
        return 0;
    }
    // Variable to store position
    // of At and Dot
    int At = -1, Dot = -1;

    // Traverse over the email id
    // string to find position of
    // Dot and At
    for (int i = 0;
         i < email.length(); i++) {

        // If the character is '@'
        if (email[i] == '@') {

            At = i;
        }

        // If character is '.'
        else if (email[i] == '.') {

            Dot = i;
        }
    }

    // If At or Dot is not present
    if (At == -1 || Dot == -1)
        return 0;

    // If Dot is present before At
    if (At > Dot)
        return 0;

    // If Dot is present at the end
    return !(Dot >= (email.length() - 1));
}

// Driver Code
int main()
{
    // Given string email
    string email = "contribute@geeksforgeeks.org";

    // Function Call
    bool ans = is_valid(email);

    // Print the result
    if (ans) {
        cout << email << " : "
             << "valid" << endl;
    }
    else {
        cout << email << " : "
             << "invalid" << endl;
    }

    return 0;
}
```

****Output:**

```
contribute@geeksforgeeks.org : valid

```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**

****[正则表达式](https://www.geeksforgeeks.org/regex-regular-expression-in-c/)基方法:**给定的问题也可以用正则表达式来解决。以下是步骤:**

*   **获取**电子邮件**字符串。**
*   **如下所述，创建一个正则表达式来检查有效的电子邮件:**

> *****regex =*****(\ \ w+)(\ \。|_)?(\\w*)@(\\w+)(\\。(\\w+))+"****

*   **将给定的字符串**电子邮件**与正则表达式匹配。在 [C++](https://www.geeksforgeeks.org/c-plus-plus/) 中，这可以通过使用 [regex_match()](https://www.geeksforgeeks.org/regex-regular-expression-in-c/) 来完成。**
*   **打印**“有效”**如果给定字符串**电子邮件**与给定正则表达式匹配，否则返回**“无效”**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <iostream>
#include <regex>
using namespace std;

// Function to check the email id
// is valid or not
bool isValid(const string& email)
{

    // Regular expression definition
    const regex pattern(
        "(\\w+)(\\.|_)?(\\w*)@(\\w+)(\\.(\\w+))+");

    // Match the string pattern
    // with regular expression
    return regex_match(email, pattern);
}

// Driver Code
int main()
{
    // Given string email
    string email
        = "contribute@geeksforgeeks.org";

    // Function Call
    bool ans = isValid(email);

    // Print the result
    if (ans) {
        cout << email << " : "
             << "valid" << endl;
    }
    else {
        cout << email << " : "
             << "invalid" << endl;
    }
}
```

****Output:**

```
contribute@geeksforgeeks.org : valid

```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**