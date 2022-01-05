# 使用递归

将字母‘x’的所有出现从字符串 s 移动到末尾

> 原文:[https://www . geesforgeks . org/move-all-occurrency-of-字母-x-from-string-s-to-end-use-recursion/](https://www.geeksforgeeks.org/move-all-occurrence-of-letter-x-from-the-string-s-to-the-end-using-recursion/)

给定一个**字符串 s** ，我们的任务是使用递归将所有出现的字母 **x** 移动到字符串 s 的末尾。
***注意:**如果给定的字符串中只有字母 x，那么返回字符串不变。*

**示例:**

> **输入:**s = " geekxsforgexxeksxx "
> **输出:** geeksforgeeksxxxxx
> **解释:**
> 字母‘x’的所有出现都移动到最后。
> 
> **输入:** s = "xxxxx"
> **输出:** xxxxx
> **解释:**
> 由于给定字符串中只有字母 x，因此输出不变。

**方法:**
为了解决上面提到的问题，我们可以使用[递归](https://www.geeksforgeeks.org/recursion/)。遍历字符串并递归检查当前字符是否等于字符“x”。如果没有，则打印该字符，否则移动到下一个字符，直到达到字符串的长度。

下面是上述方法的实现:

## C++

```
// C++ implementation to Move all occurrence of letter ‘x’
// from the string s to the end using Recursion
#include <bits/stdc++.h>
using namespace std;

// Function to move all 'x' in the end
void moveAtEnd(string s, int i, int l)
{
    if (i >= l)
        return;

    // Store current character
    char curr = s[i];

    // Check if current character is not 'x'
    if (curr != 'x')
        cout << curr;

    // recursive function call
    moveAtEnd(s, i + 1, l);

    // Check if current character is 'x'
    if (curr == 'x')
        cout << curr;

    return;
}

// Driver code
int main()
{
    string s = "geekxsforgexxeksxx";

    int l = s.length();

    moveAtEnd(s, 0, l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Move all occurrence of letter ‘x’
// from the string s to the end using Recursion
import java.util.*;
class GFG{

// Function to move all 'x' in the end
static void moveAtEnd(String s, int i, int l)
{
    if (i >= l)
        return;

    // Store current character
    char curr = s.charAt(i);

    // Check if current character is not 'x'
    if (curr != 'x')
        System.out.print(curr);

    // recursive function call
    moveAtEnd(s, i + 1, l);

    // Check if current character is 'x'
    if (curr == 'x')
        System.out.print(curr);

    return;
}

// Driver code
public static void main(String args[])
{
    String s = "geekxsforgexxeksxx";

    int l = s.length();

    moveAtEnd(s, 0, l);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation to move all
# occurrences of letter ‘x’ from the
# string s to the end using recursion

# Function to move all 'x' in the end
def moveAtEnd(s, i, l):

    if(i >= l):
       return

    # Store current character
    curr = s[i]

    # Check if current character
    # is not 'x'
    if(curr != 'x'):
        print(curr, end = "")

    # Recursive function call
    moveAtEnd(s, i + 1, l)

    # Check if current character is 'x'
    if(curr == 'x'):
        print(curr, end = "")

    return

# Driver code
if __name__ == '__main__':

    s = "geekxsforgexxeksxx"
    l = len(s)

    moveAtEnd(s, 0, l)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation to Move all occurrence of letter ‘x’
// from the string s to the end using Recursion
using System;
class GFG{

// Function to move all 'x' in the end
static void moveAtEnd(string s, int i, int l)
{
    if (i >= l)
        return;

    // Store current character
    char curr = s[i];

    // Check if current character is not 'x'
    if (curr != 'x')
        Console.Write(curr);

    // recursive function call
    moveAtEnd(s, i + 1, l);

    // Check if current character is 'x'
    if (curr == 'x')
        Console.Write(curr);

    return;
}

// Driver code
public static void Main()
{
    string s = "geekxsforgexxeksxx";

    int l = s.Length;

    moveAtEnd(s, 0, l);
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>

// Javascript implementation to Move
// all occurrence of letter ‘x’ from
// the string s to the end using Recursion

// Function to move all 'x' in the end
function moveAtEnd(s, i, l)
{
    if (i >= l)
        return;

    // Store current character
    let curr = s[i];

    // Check if current character is not 'x'
    if (curr != 'x')
        document.write(curr);

    // Recursive function call
    moveAtEnd(s, i + 1, l);

    // Check if current character is 'x'
    if (curr == 'x')
        document.write(curr);

    return;
}

// Driver code
let s = "geekxsforgexxeksxx";
let l = s.length;

moveAtEnd(s, 0, l);

// This code is contributed by suresh07

</script>
```

**Output**

```
geeksforgeeksxxxxx
```

**涉及字符交换的另一个实现:**

在这种方法中，我们将交换相邻的字符，以在末尾添加“x”。

下面是上述技术的实现:

## C++

```
// C++ program for above approach
#include<bits/stdc++.h>
using namespace std;

// Recursive program to bring 'x'
// to the end
void rec(char *a, int i)
{

    // When the string is completed
    // from reverse direction end of recursion
    if(i == 0)
    {
      cout << a << endl;
      return;
    }

    // If the character x is found
    if(a[i] == 'x')
    {

      // Transverse the whole string
      int j = i;
      while(a[j] != '\0' && a[j+1] != '\0')
      {

        // Swap the x so that
        // it moves to the last
        swap(a[j], a[j+1]);
        j++;
      }
    }

    // call to the smaller problem now
    rec(a, i - 1);
}

// Driver Code
int main()
{
    char a[] = {'g', 'e', 'e', 'k', 'x',
            's', 'x', 'x', 'k', 's', '\0'};

    // Size of a
    int n = 10;

    // Call to rec
    rec(a,n-1);
}
/* This code is contributed by Harsh kedia */
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class Main{

// Recursive program to
// bring 'x' to the end
public static void rec(char a[],
                       int i)
{        
  // When the string is completed
  // from reverse direction end
  // of recursion
  if(i == 0)
  {
    System.out.println(a);
    return;
  }

  // If the character x is found
  if(a[i] == 'x')
  {

    // Transverse the whole string
    int j = i;
    while(a[j] != '\0' &&
          a[j + 1] != '\0')
    {
      // Swap the x so that
      // it moves to the last
      char temp = a[j];
      a[j] = a[j + 1];
      a[j + 1] = temp;
      j++;
    }
  }

  // call to the smaller
  // problem now
  rec(a, i - 1);
}  

// Driver code
public static void main(String[] args)
{
  char a[] = {'g', 'e', 'e', 'k',
              'x', 's', 'x', 'x',
              'k', 's', '\0'};

  // Size of a
  int n = 10;

  // Call to rec
  rec(a,n-1);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for above approach

# Recursive program to bring 'x'
# to the end
def rec(a, i):

    # When the string is completed
    # from reverse direction end
    # of recursion
    if (i == 0):
        a.pop()
        print("".join(a))
        return

    # If the character x is found
    if (a[i] == 'x'):

      # Transverse the whole string
      j = i
      while(a[j] != '\0' and
            a[j + 1] != '\0'):

        # Swap the x so that
        # it moves to the last
        (a[j], a[j + 1]) = (a[j + 1], a[j])
        j += 1

    # Call to the smaller problem now
    rec(a, i - 1)

# Driver code
if __name__=="__main__":

    a = [ 'g', 'e', 'e', 'k', 'x',
          's', 'x', 'x', 'k', 's', '\0' ]

    # Size of a
    n = 10

    # Call to rec
    rec(a, n - 1)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the
// above approach
using System;
class GFG
{

    // Recursive program to
    // bring 'x' to the end
    static void rec(char[] a, int i)
    {

      // When the string is completed
      // from reverse direction end
      // of recursion
      if(i == 0)
      {
        Console.WriteLine(a);
        return;
      }

      // If the character x is found
      if(a[i] == 'x')
      {

        // Transverse the whole string
        int j = i;
        while(a[j] != '\0' &&
              a[j + 1] != '\0')
        {

          // Swap the x so that
          // it moves to the last
          char temp = a[j];
          a[j] = a[j + 1];
          a[j + 1] = temp;
          j++;
        }
      }

      // call to the smaller
      // problem now
      rec(a, i - 1);
    }

  // Driver code    
  static void Main()
  {
      char[] a = {'g', 'e', 'e', 'k',
              'x', 's', 'x', 'x',
              'k', 's', '\0'};

      // Size of a
      int n = 10;

      // Call to rec
      rec(a,n-1);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Recursive program to
    // bring 'x' to the end
    function rec(a, i)
    {

      // When the string is completed
      // from reverse direction end
      // of recursion
      if(i == 0)
      {
        document.write(a.join(""));
        return;
      }

      // If the character x is found
      if(a[i] == 'x')
      {

        // Transverse the whole string
        let j = i;
        while(a[j] != '\0' &&
              a[j + 1] != '\0')
        {

          // Swap the x so that
          // it moves to the last
          let temp = a[j];
          a[j] = a[j + 1];
          a[j + 1] = temp;
          j++;
        }
      }

      // call to the smaller
      // problem now
      rec(a, i - 1);
    }

    let a = ['g', 'e', 'e', 'k', 'x', 's', 'x', 'x', 'k', 's', '\0'];

    // Size of a
    let n = 10;

    // Call to rec
    rec(a, n - 1);

    // This code is contributed by decode2207.
</script>
```

**Output**

```
geeksksxxx
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。
**辅助空间:** O(N)。