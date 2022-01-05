# 生成所有没有连续 1 的二进制字符串

> 原文:[https://www . geesforgeks . org/generate-binary-strings-不带连续-1s/](https://www.geeksforgeeks.org/generate-binary-strings-without-consecutive-1s/)

给定一个整数 K。任务是打印大小为 K(给定数字)的所有二进制字符串。
示例:

```
Input : K = 3  
Output : 000 , 001 , 010 , 100 , 101 

Input : K  = 4 
Output :0000 0001 0010 0100 0101 1000 1001 1010
```

背后的想法是，如果字符串以“1”结尾，那么我们只在结尾放“0”。如果字符串以“0”结尾，那么我们将“0”和“1”放在字符串的末尾，以生成新的字符串。
下面是算法

```
K : size of string 
First We Generate All string starts with '0'
initialize n = 1 . 
GenerateALLString ( K  , Str , n )
  a. IF n == K 
     PRINT str.
  b. IF previous character is '1' :: str[n-1] == '1'
     put str[n] = '0'
     GenerateAllString ( K , str , n+1 )
  c. IF previous character is '0' :: str[n-1] == '0'
     First We Put zero at end and call function 
      PUT  str[n] = '0'
           GenerateAllString ( K , str , n+1 )  
      PUT  str[n] = '1'
           GenerateAllString ( K , str , n+1 )

Second Generate all binary string starts with '1'
DO THE SAME PROCESS
```

下面是递归实现:

## C++

```
// C++ program to Generate
// all binary string without
// consecutive 1's of size K
#include<bits/stdc++.h>
using namespace std ;

// A utility function generate all string without
// consecutive 1'sof size K
void generateAllStringsUtil(int K, char str[], int n)
{

    // Print binary string without consecutive 1's
    if (n  == K)
    {

        // Terminate binary string
        str[n] = '\0' ;
        cout << str << " ";
        return ;
    }

    // If previous character is '1' then we put
    // only 0 at end of string
    //example str = "01" then new string be "010"
    if (str[n-1] == '1')
    {
        str[n] = '0';
        generateAllStringsUtil (K , str , n+1);
    }

    // If previous character is '0' than we put
    // both '1' and '0' at end of string
    // example str = "00" then
    // new string "001" and "000"
    if (str[n-1] == '0')
    {
        str[n] = '0';
        generateAllStringsUtil(K, str, n+1);
        str[n] = '1';
        generateAllStringsUtil(K, str, n+1) ;
    }
}

// Function generate all binary string without
// consecutive 1's
void generateAllStrings(int K )
{
    // Base case
    if (K <= 0)
        return ;

    // One by one stores every
    // binary string of length K
    char str[K];

    // Generate all Binary string
    // starts with '0'
    str[0] = '0' ;
    generateAllStringsUtil ( K , str , 1 ) ;

    // Generate all Binary string
    // starts with '1'
    str[0] = '1' ;
    generateAllStringsUtil ( K , str , 1 );
}

// Driver program to test above function
int main()
{
    int K = 3;
    generateAllStrings (K) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Generate all binary string without
// consecutive 1's of size K
import java.util.*;
import java.lang.*;

public class BinaryS {

    // Array conversion to String--
    public static String toString(char[] a) {
        String string = new String(a);
        return string;
    }

    static void generate(int k, char[] ch, int n) {

        // Base Condition when we
        // reached at the end of Array**
        if (n == k) {

            // Printing the Generated String**
            // Return to the previous case*
            System.out.print(toString(ch)+" ");
            return;

        }

        // If the first Character is
        //Zero then adding**
        if (ch[n - 1] == '0') {
            ch[n] = '0';
            generate(k, ch, n + 1);
            ch[n] = '1';
            generate(k, ch, n + 1);
        }

        // If the Character is One
        // then add Zero to next**
        if (ch[n - 1] == '1') {

            ch[n] = '0';

            // Calling Recursively for the
            // next value of Array
            generate(k, ch, n + 1);

        }
    }

    static void fun(int k) {

        if (k <= 0) {
            return;
        }

        char[] ch = new char[k];

        // Initializing first character to Zero
        ch[0] = '0';

        // Generating Strings starting with Zero--
        generate(k, ch, 1);

        // Initialized first Character to one--
        ch[0] = '1';
        generate(k, ch, 1);

    }

    public static void main(String args[]) {

        int k = 3;

        //Calling function fun with argument k
        fun(k);

        //This code is Contributed by Praveen Tiwari
    }
}
```

## 蟒蛇 3

```
# Python3 program to Generate all binary string
# without consecutive 1's of size K

# A utility function generate all string without
# consecutive 1'sof size K
def generateAllStringsUtil(K, str, n):

    # print binary string without consecutive 1's
    if (n == K):

        # terminate binary string
        print(*str[:n], sep = "", end = " ")
        return

    # if previous character is '1' then we put
    # only 0 at end of string
    # example str = "01" then new string be "000"
    if (str[n-1] == '1'):
        str[n] = '0'
        generateAllStringsUtil (K, str, n + 1)

    # if previous character is '0' than we put
    # both '1' and '0' at end of string
    # example str = "00" then new string "001" and "000"
    if (str[n-1] == '0'):
        str[n] = '0'
        generateAllStringsUtil(K, str, n + 1)
        str[n] = '1'
        generateAllStringsUtil(K, str, n + 1)

# function generate all binary string without
# consecutive 1's
def generateAllStrings(K):

    # Base case
    if (K <= 0):
        return

    # One by one stores every
    # binary string of length K
    str = [0] * K

    # Generate all Binary string starts with '0'
    str[0] = '0'
    generateAllStringsUtil (K, str, 1)

    # Generate all Binary string starts with '1'
    str[0] = '1'
    generateAllStringsUtil (K, str, 1)

# Driver code
K = 3
generateAllStrings (K)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to Generate
// all binary string without
// consecutive 1's of size K
using System;
class GFG {

  // Array conversion to String--
  static string toString(char[] a) {
    string String = new string(a);
    return String;
  }

  static void generate(int k, char[] ch, int n) {

    // Base Condition when we
    // reached at the end of Array**
    if (n == k) {

      // Printing the Generated String**
      // Return to the previous case*
      Console.Write(toString(ch)+" ");
      return;

    }

    // If the first Character is
    //Zero then adding**
    if (ch[n - 1] == '0') {
      ch[n] = '0';
      generate(k, ch, n + 1);
      ch[n] = '1';
      generate(k, ch, n + 1);
    }

    // If the Character is One
    // then add Zero to next**
    if (ch[n - 1] == '1') {

      ch[n] = '0';

      // Calling Recursively for the
      // next value of Array
      generate(k, ch, n + 1);

    }
  }

  static void fun(int k)
  {
    if (k <= 0)
    {
      return;
    }
    char[] ch = new char[k];

    // Initializing first character to Zero
    ch[0] = '0';

    // Generating Strings starting with Zero--
    generate(k, ch, 1);

    // Initialized first Character to one--
    ch[0] = '1';
    generate(k, ch, 1);

  }

  // Driver code
  static void Main()
  {
    int k = 3;

    //Calling function fun with argument k
    fun(k);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// Javascript implementation

// A utility function generate all string without
// consecutive 1'sof size K
function generateAllStringsUtil(K, str, n)
{

    // Print binary string without consecutive 1's
    if (n  == K)
    {

        // Terminate binary string
        str[n] = '\0' ;
        document.write(str.join("") + " ");
        return ;
    }

    // If previous character is '1' then we put
    // only 0 at end of string
    //example str = "01" then new string be "010"
    if (str[n-1] == '1')
    {
        str[n] = '0';
        generateAllStringsUtil (K , str , n+1);
    }

    // If previous character is '0' than we put
    // both '1' and '0' at end of string
    // example str = "00" then
    // new string "001" and "000"
    if (str[n-1] == '0')
    {
        str[n] = '0';
        generateAllStringsUtil(K, str, n+1);
        str[n] = '1';
        generateAllStringsUtil(K, str, n+1) ;
    }
}

// Function generate all binary string without
// consecutive 1's
function generateAllStrings(K )
{
    // Base case
    if (K <= 0)
        return ;

    // One by one stores every
    // binary string of length K
    var str = new Array(K);

    // Generate all Binary string
    // starts with '0'
    str[0] = '0' ;
    generateAllStringsUtil ( K , str , 1 ) ;

    // Generate all Binary string
    // starts with '1'
    str[0] = '1' ;
    generateAllStringsUtil ( K , str , 1 );
}

/* Driver code */
var K = 3;
generateAllStrings(K);

// This is code is contributed
// by shivani
</script>
```

**输出:**

```
 000 001 010 100 101
```

本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。