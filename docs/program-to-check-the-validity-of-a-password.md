# 检查密码有效性的程序

> 原文:[https://www . geesforgeks . org/程序检查密码有效性/](https://www.geeksforgeeks.org/program-to-check-the-validity-of-a-password/)

密码检查程序主要根据下面提到的密码策略检查密码是否有效:

*   密码不应包含任何空格。
*   密码应至少包含一个数字(0-9)。
*   密码长度应该在 8 到 15 个字符之间。
*   密码应至少包含一个小写字母(a-z)。
*   密码应至少包含一个大写字母(A-Z)。
*   密码应至少包含一个特殊字符(@、#、%、&、！，$，等等…).

**示例:**

```
Input: GeeksForGeeks 
Output: Invalid Password!
This input contains lowercase 
as well as uppercase letters 
but does not contain digits 
and special characters.

Input: Geek$ForGeeks7
Output: Valid Password
This input satisfies all password
policies mentioned above.

```

**进场:**

在这个节目中，

*   我们正在使用 [String contains()方法](https://www.geeksforgeeks.org/java-string-contains-method-example/)来检查密码。此方法接受 CharSequence 作为参数，如果参数存在于字符串中，则返回 true，否则返回 false。
*   首先必须检查密码的长度，然后检查它是否包含大写、小写、数字和特殊字符。
*   如果它们都存在，则方法**为有效(字符串密码)**返回真。

以下是上述方法的实现:

## C++

```
// C++ code to validate a password 
#include<bits/stdc++.h>
using namespace std;

// A utility function to check 
// whether a password is valid or not 
bool isValid(string password) 
{ 

    // For checking if password length 
    // is between 8 and 15 
    if (!((password.length() >= 8) && 
          (password.length() <= 15)))
        return false; 

    // To check space 
    if (password.find(" ") !=
        std::string::npos)
        return false; 

    if (true)
    { 
        int count = 0; 

        // Check digits from 0 to 9 
        for(int i = 0; i <= 9; i++)
        { 

            // To convert int to string 
            string str1 = to_string(i); 

            if (password.find(str1) != 
                std::string::npos) 
                count = 1; 
        } 
        if (count == 0) 
            return false; 
    } 

    // For special characters 
    if (!((password.find("@") != std::string::npos) ||
          (password.find("#") != std::string::npos) ||
          (password.find("!") != std::string::npos) ||
          (password.find("~") != std::string::npos) ||
          (password.find("{content}quot;) != std::string::npos) ||
          (password.find("%") != std::string::npos) ||
          (password.find("^") != std::string::npos) ||
          (password.find("&") != std::string::npos) ||
          (password.find("*") != std::string::npos) ||
          (password.find("(") != std::string::npos) ||
          (password.find(")") != std::string::npos) ||
          (password.find("-") != std::string::npos) ||
            (password.find("+") != std::string::npos) ||
          (password.find("/") != std::string::npos) ||
          (password.find(":") != std::string::npos) ||
          (password.find(".") != std::string::npos) ||
          (password.find(",") != std::string::npos) ||
          (password.find("<") != std::string::npos) ||
          (password.find(">") != std::string::npos) ||
          (password.find("?") != std::string::npos) ||
          (password.find("|") != std::string::npos)))
        return false;

    if (true)
    { 
        int count = 0; 

        // Checking capital letters 
        for(int i = 65; i <= 90; i++) 
        { 

            // Type casting 
            char c = (char)i;
            string str1(1, c);

            if (password.find(str1) !=
                std::string::npos) 
                count = 1; 
        } 
        if (count == 0) 
            return false; 
    } 

    if (true)
    { 
        int count = 0; 

        // Checking small letters 
        for(int i = 90; i <= 122; i++)
        { 

            // Type casting 
            char c = (char)i; 
            string str1(1, c); 

            if (password.find(str1) != 
                std::string::npos)
                count = 1;
        } 
        if (count == 0) 
            return false;
    } 

    // If all conditions fails 
    return true; 
} 

// Driver code 
int main() 
{ 
    string password1 = "GeeksForGeeks"; 

    if (isValid(password1)) 
        cout << "Valid Password" << endl; 
    else
        cout << "Invalid Password" << endl;

    string password2 = "Geek$ForGeeks7";

    if (isValid(password2)) 
        cout << "Valid Password" << endl; 
    else
        cout << "Invalid Password" << endl;
} 

// This code is contributed by Yash_R
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to validate a password

public class PasswordValidator {

    // A utility function to check
    // whether a password is valid or not
    public static boolean isValid(String password)
    {

        // for checking if password length
        // is between 8 and 15
        if (!((password.length() >= 8)
              && (password.length() <= 15))) {
            return false;
        }

        // to check space
        if (password.contains(" ")) {
            return false;
        }
        if (true) {
            int count = 0;

            // check digits from 0 to 9
            for (int i = 0; i <= 9; i++) {

                // to convert int to string
                String str1 = Integer.toString(i);

                if (password.contains(str1)) {
                    count = 1;
                }
            }
            if (count == 0) {
                return false;
            }
        }

        // for special characters
        if (!(password.contains("@") || password.contains("#")
              || password.contains("!") || password.contains("~")
              || password.contains("{content}quot;) || password.contains("%")
              || password.contains("^") || password.contains("&")
              || password.contains("*") || password.contains("(")
              || password.contains(")") || password.contains("-")
              || password.contains("+") || password.contains("/")
              || password.contains(":") || password.contains(".")
              || password.contains(", ") || password.contains("<")
              || password.contains(">") || password.contains("?")
              || password.contains("|"))) {
            return false;
        }

        if (true) {
            int count = 0;

            // checking capital letters
            for (int i = 65; i <= 90; i++) {

                // type casting
                char c = (char)i;

                String str1 = Character.toString(c);
                if (password.contains(str1)) {
                    count = 1;
                }
            }
            if (count == 0) {
                return false;
            }
        }

        if (true) {
            int count = 0;

            // checking small letters
            for (int i = 90; i <= 122; i++) {

                // type casting
                char c = (char)i;
                String str1 = Character.toString(c);

                if (password.contains(str1)) {
                    count = 1;
                }
            }
            if (count == 0) {
                return false;
            }
        }

        // if all conditions fails
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {

        String password1 = "GeeksForGeeks";

        if (isValid(password1)) {
            System.out.println("Valid Password");
        }
        else {
            System.out.println("Invalid Password!!!");
        }

        String password2 = "Geek$ForGeeks7";
        if (isValid(password2)) {
            System.out.println("Valid Password");
        }
        else {
            System.out.println("Invalid Password!!!");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 code to validate a password

# A utility function to check
# whether a password is valid or not
def isValid(password):

    # for checking if password length
    # is between 8 and 15
    if (len(password) < 8 or len(password) > 15):
        return False

    # to check space
    if (" " in password):
        return False

    if (True):
        count = 0

        # check digits from 0 to 9
        arr = ['0', '1', '2', '3', 
        '4', '5', '6', '7', '8', '9']

        for i in password:
            if i in arr:
                count = 1
                break

        if count == 0:
            return False

    # for special characters
    if True:
        count = 0

        arr = ['@', '#','!','~','{content}apos;,'%','^',
                '&','*','(',',','-','+','/',
                ':','.',',','<','>','?','|']

        for i in password:
            if i in arr:
                count = 1
                break
        if count == 0:
            return False

    if True:
        count = 0

        # checking capital letters
        for i in range(65, 91):

            if chr(i) in password:
                count = 1

        if (count == 0):
            return False

    if (True):
        count = 0

        # checking small letters
        for i in range(90, 123):

            if chr(i) in password:
                count = 1

        if (count == 0):
            return False

    # if all conditions fails
    return True

# Driver code
password1 = "GeeksForGeeks"

if (isValid([i for i in password1])):
    print("Valid Password")
else:
    print("Invalid Password!!!")

password2 = "Geek$ForGeeks7"
if (isValid([i for i in password2])):
    print("Valid Password")
else:
    print("Invalid Password!!!")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code to validate a password
using System;

class PasswordValidator 
{

    // A utility function to check
    // whether a password is valid or not
    public static bool isValid(String password)
    {

        // for checking if password length
        // is between 8 and 15
        if (!((password.Length >= 8)
            && (password.Length <= 15)))
        {
            return false;
        }

        // to check space
        if (password.Contains(" "))
        {
            return false;
        }
        if (true) 
        {
            int count = 0;

            // check digits from 0 to 9
            for (int i = 0; i <= 9; i++)
            {

                // to convert int to string
                String str1 = i.ToString();

                if (password.Contains(str1)) 
                {
                    count = 1;
                }
            }
            if (count == 0)
            {
                return false;
            }
        }

        // for special characters
        if (!(password.Contains("@") || password.Contains("#")
            || password.Contains("!") || password.Contains("~")
            || password.Contains("{content}quot;) || password.Contains("%")
            || password.Contains("^") || password.Contains("&")
            || password.Contains("*") || password.Contains("(")
            || password.Contains(")") || password.Contains("-")
            || password.Contains("+") || password.Contains("/")
            || password.Contains(":") || password.Contains(".")
            || password.Contains(", ") || password.Contains("<")
            || password.Contains(">") || password.Contains("?")
            || password.Contains("|"))) 
        {
            return false;
        }

        if (true)
        {
            int count = 0;

            // checking capital letters
            for (int i = 65; i <= 90; i++)
            {

                // type casting
                char c = (char)i;

                String str1 = c.ToString();
                if (password.Contains(str1))
                {
                    count = 1;
                }
            }
            if (count == 0)
            {
                return false;
            }
        }

        if (true)
        {
            int count = 0;

            // checking small letters
            for (int i = 90; i <= 122; i++) 
            {

                // type casting
                char c = (char)i;
                String str1 = c.ToString();

                if (password.Contains(str1)) 
                {
                    count = 1;
                }
            }
            if (count == 0)
            {
                return false;
            }
        }

        // if all conditions fails
        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {

        String password1 = "GeeksForGeeks";

        if (isValid(password1))
        {
            Console.WriteLine("Valid Password");
        }
        else 
        {
            Console.WriteLine("Invalid Password!!!");
        }

        String password2 = "Geek$ForGeeks7";
        if (isValid(password2)) 
        {
            Console.WriteLine("Valid Password");
        }
        else 
        {
            Console.WriteLine("Invalid Password!!!");
        }
    }
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
Invalid Password!!!
Valid Password

```