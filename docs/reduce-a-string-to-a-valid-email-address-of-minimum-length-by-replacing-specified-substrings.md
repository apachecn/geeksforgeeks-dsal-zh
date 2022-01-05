# 通过替换指定的子字符串

将字符串缩减为最小长度的有效电子邮件地址

> 原文:[https://www . geesforgeks . org/通过替换指定的子字符串将字符串减少到最小长度的有效电子邮件地址/](https://www.geeksforgeeks.org/reduce-a-string-to-a-valid-email-address-of-minimum-length-by-replacing-specified-substrings/)

给定代表长度为 **N** 的电子邮件地址的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过将**中的“点”**替换为**来找到字符串的最小可能长度**和**“at”**加上**“@”**，这样该字符串就代表了一个有效的电子邮件地址。

> 一个**电子邮件地址**只能有一个**“@”**并且可能有零个或多个点**(“.”)**不能有 **'@'** 或**'**在电子邮件地址的开头和结尾。

**示例:**

> **输入:**S = " geeksforgeikstatgmaildotcom "
> **输出:**geeksforgeeks@gmail.com
> **解释:**
> 将一个**“at”**替换为**“@”**，一个**“dot”**替换为**“”**修饰 S 为 geeksforgeeks@gmail.com
> 
> **输入:**S = " atatadotdotto "
> T3】输出:at @…点
> **说明:**
> 可以多次替换，但我们不能从电子邮件地址的开头替换**【at】**或从结尾替换**【点】**，因为它不会形成有效的电子邮件地址。

**方法:**思路是将所有**【点】**子串替换为**。”**和一个**“at”**子字符串，除了从字符串的开头或结尾开始外，都带有**“@”**。按照以下步骤解决问题:

*   [在指数**【1，N-2】**上遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。
*   如果**S【I，I+2】**为**【点】**，则替换为**。”**。如果**S【I，I+1】**为**“at”**，则替换为**“@”**。
*   打印更新后的字符串作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length by
// replacing at with @ and dot with '.'
// such that the string is valid email
string minEmail(string email)
{

    // Stores string by replacing at
    // with @ and dot with '.'# such
    // that the string is valid email
    string ans = "";
    int len = email.length();

    // append first character
    ans += email[0];

    // Stores index
    int i = 1;

    // Check if at(@) already included
    // or not
    bool notAt = true;

    // Iterate over characters of the string
    while (i < len) {

        // at can be replaced at most once
        if (i < len - 3 && notAt && email[i] == 'a'
            && email[i + 1] == 't') {

            // Update ans
            ans += '@';

            // Update i
            i += 1;

            // Update notAt
            notAt = false;
        }

        // If current substring found dot
        else if (i < len - 4 && email[i] == 'd'
                 && email[i + 1] == 'o'
                 && email[i + 2] == 't') {

            // Update ans
            ans += '.';

            // Update i
            i += 2;
        }
        else {

            // Update ans
            ans += email[i];
        }

        // Update i
        i += 1;
    }
    return ans;
}

// Driver code
int main()
{

    // To display the result
    string email = "geeksforgeeksatgmaildotcom";
    cout << (minEmail(email));
}

// Thi code is contributed by chitranayal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

  // Function to find the minimum length by
  // replacing at with @ and dot with '.'
  // such that the string is valid email
  static String minEmail(String email)
  {

    // Stores string by replacing at
    // with @ and dot with '.'# such
    // that the string is valid email
    String ans = new String("");
    int len = email.length();

    // append first character
    ans += email.charAt(0);

    // Stores index
    int i = 1;

    // Check if at(@) already included
    // or not
    boolean notAt = true;

    // Iterate over characters of the string
    while(i < len){

      // at can be replaced at most once
      if (i < len-3 && notAt
          && email.charAt(i) == 'a' && email.charAt(i+1) == 't')
      {

        // Update ans     
        ans += '@';

        // Update i
        i += 1;

        // Update notAt
        notAt = false;
      }

      // If current substring found dot
      else if( i < len-4 && email.charAt(i) == 'd'
              && email.charAt(i+1) == 'o' && email.charAt(i+2) == 't')
      {

        // Update ans
        ans += '.'; 

        // Update i
        i += 2;
      }
      else
      {

        // Update ans
        ans += email.charAt(i);
      }

      // Update i   
      i += 1;
    }
    return ans;
  }

  // Driver code
  public static void main (String[] args)
  {

    // To display the result
    String email = new String("geeksforgeeksatgmaildotcom");
    System.out.println(minEmail(email));
  }
}

// This code is contributed by rohitsingh07052.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum length by
# replacing at with @ and dot with '.'
# such that the string is valid email
def minEmail(email):

    # Stores string by replacing at
    # with @ and dot with '.'# such
    # that the string is valid email
    ans = ''

    # append first character
    ans += email[0]

    # Stores index
    i = 1

    # Check if at(@) already included
    # or not
    notAt = True

    # Iterate over characters of the string
    while i < len(email):

        # at can be replaced at most once
        if (i < len(email)-3 and notAt
            and email[i:i + 2] == 'at'):

            # Update ans     
            ans += '@'

            # Update i
            i += 1

            # Update notAt
            notAt = False

        # If current substring found dot
        elif i < len(email)-4 and email[i:i + 3] == 'dot':

            # Update ans
            ans += '.'          

            # Update i
            i += 2
        else:

            # Update ans
            ans += email[i]

        # Update i   
        i += 1
    return ans

# Driver Code
if __name__ == '__main__':

    email = 'geeksforgeeksatgmaildotcom'

    # To display the result
    print(minEmail(email))
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the minimum length by
  // replacing at with @ and dot with '.'
  // such that the string is valid email
  static String minEmail(String email)
  {

    // Stores string by replacing at
    // with @ and dot with '.'# such
    // that the string is valid email
    String ans = "";
    int len = email.Length;

    // append first character
    ans += email[0];

    // Stores index
    int i = 1;

    // Check if at(@) already included
    // or not
    bool notAt = true;

    // Iterate over characters of the string
    while(i < len)
    {

      // at can be replaced at most once
      if (i < len-3 && notAt
          && email[i] == 'a' && email[i + 1] == 't')
      {

        // Update ans     
        ans += '@';

        // Update i
        i += 1;

        // Update notAt
        notAt = false;
      }

      // If current substring found dot
      else if( i < len-4 && email[i] == 'd'
              && email[i+1] == 'o' && email[i+2] == 't')
      {

        // Update ans
        ans += '.'; 

        // Update i
        i += 2;
      }
      else
      {

        // Update ans
        ans += email[i];
      }

      // Update i   
      i += 1;
    }
    return ans;
  }

  // Driver code
  public static void Main(String[] args)
  {

    // To display the result
    String email = "geeksforgeeksatgmaildotcom";
    Console.WriteLine(minEmail(email));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    // Function to find the minimum length by
  // replacing at with @ and dot with '.'
  // such that the string is valid email
    function minEmail(email)
    {
        // Stores string by replacing at
    // with @ and dot with '.'# such
    // that the string is valid email
    let ans = "";
    let len = email.length;

    // append first character
    ans += email[0];

    // Stores index
    let i = 1;

    // Check if at(@) already included
    // or not
    let notAt = true;

    // Iterate over characters of the string
    while(i < len){

      // at can be replaced at most once
      if (i < len-3 && notAt
          && email[i] == 'a' && email[i+1] == 't')
      {

        // Update ans    
        ans += '@';

        // Update i
        i += 1;

        // Update notAt
        notAt = false;
      }

      // If current substring found dot
      else if( i < len-4 && email[i] == 'd'
              && email[i+1] == 'o' && email[i+2] == 't')
      {

        // Update ans
        ans += '.';

        // Update i
        i += 2;
      }
      else
      {

        // Update ans
        ans += email[i];
      }

      // Update i  
      i += 1;
    }
    return ans;
    }

    // Driver code

    // To display the result
    let email="geeksforgeeksatgmaildotcom";
    document.write(minEmail(email));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
geeksforgeeks@gmail.com
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)