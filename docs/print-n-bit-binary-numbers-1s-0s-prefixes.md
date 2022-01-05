# 打印所有前缀中 1 比 0 多的 N 位二进制数

> 原文:[https://www . geesforgeks . org/print-n-bit-binary-numbers-1s-0s-prefixes/](https://www.geeksforgeeks.org/print-n-bit-binary-numbers-1s-0s-prefixes/)

给定一个正整数 n，打印所有 n 位二进制数，对于该数的任何前缀，该数的 1 大于 0。

**示例:**

```
Input : n = 2
Output : 11 10

Input : n = 4
Output : 1111 1110 1101 1100 1011 1010
```

一个简单但不有效的解决方案是生成所有的 N 位二进制数，并打印那些满足条件的数。这个解的时间复杂度是指数级的。

一个**有效的解决方案**是只生成那些满足给定条件的 N 位数字。我们使用递归。在递归中的每一点，我们将 0 和 1 附加到部分形成的数字上，并用少一个数字重复。

## C++

```
// C++ program to print all N-bit binary
#include <bits/stdc++.h>
using namespace std;

/* function to generate n  digit numbers*/
void printRec(string number, int extraOnes,
              int remainingPlaces)
{
    /* if number generated */
    if (0 == remainingPlaces) {
        cout << number << " ";
        return;
    }

    /* Append 1 at the current number and reduce
       the remaining places by one */
    printRec(number + "1", extraOnes + 1,
             remainingPlaces - 1);

    /* If more ones than zeros, append 0 to the
       current number and reduce the remaining
       places by one*/
    if (0 < extraOnes)
        printRec(number + "0", extraOnes - 1,
                 remainingPlaces - 1);
}

void printNums(int n)
{
    string str = "";
    printRec(str, 0, n);
}

// Driver code
int main()
{
    int n = 4;

    // Function call
    printNums(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all N-bit binary
import java.io.*;

class GFG {
    // function to generate n digit numbers
    static void printRec(String number,
                         int extraOnes,
                         int remainingPlaces)
    {
        // if number generated
        if (0 == remainingPlaces) {
            System.out.print(number + " ");
            return;
        }

        // Append 1 at the current number and
        // reduce the remaining places by one
        printRec(number + "1", extraOnes + 1,
                 remainingPlaces - 1);

        // If more ones than zeros, append 0 to the
        // current number and reduce the remaining
        // places by one
        if (0 < extraOnes)
            printRec(number + "0", extraOnes - 1,
                     remainingPlaces - 1);
    }

    static void printNums(int n)
    {
        String str = "";
        printRec(str, 0, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;

        // Function call
        printNums(n);
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to print all N-bit binary

# function to generate n digit numbers

def printRec(number, extraOnes, remainingPlaces):

    # if number generated
    if (0 == remainingPlaces):
        print(number, end=" ")
        return

    # Append 1 at the current number and
    # reduce the remaining places by one
    printRec(number + "1", extraOnes + 1,
             remainingPlaces - 1)

    # If more ones than zeros, append 0 to
    # the current number and reduce the
    # remaining places by one
    if (0 < extraOnes):
        printRec(number + "0", extraOnes - 1,
                 remainingPlaces - 1)

def printNums(n):
    str = ""
    printRec(str, 0, n)

# Driver Code
if __name__ == '__main__':
    n = 4

    # Function call
    printNums(n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to print all N-bit binary
using System;

class GFG {

    // function to generate n digit numbers
    static void printRec(String number,
                         int extraOnes,
                         int remainingPlaces)
    {

        // if number generated
        if (0 == remainingPlaces)
        {
            Console.Write(number + " ");
            return;
        }

        // Append 1 at the current number and
        // reduce the remaining places by one
        printRec(number + "1", extraOnes + 1,
                 remainingPlaces - 1);

        // If more ones than zeros, append
        // 0 to the current number and
        // reduce the remaining places
        // by one
        if (0 < extraOnes)
            printRec(number + "0", extraOnes - 1,
                     remainingPlaces - 1);
    }
    static void printNums(int n)
    {
        String str = "";
        printRec(str, 0, n);
    }

    // Driver code
    public static void Main()
    {
        int n = 4;

        // Function call
        printNums(n);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all N-bit binary

// function to generate n digit numbers
function printRec($number, $extraOnes,
                  $remainingPlaces)
{
    // if number generated
    if (0 == $remainingPlaces)
    {
        echo( $number . " ");
        return;
    }

    // Append 1 at the current number and
    // reduce the remaining places by one
    printRec($number . "1", $extraOnes + 1,
                      $remainingPlaces - 1);

    // If more ones than zeros, append 0 to the
    // current number and reduce the remaining
    // places by one
    if (0 < $extraOnes)
        printRec($number . "0", $extraOnes - 1,
                          $remainingPlaces - 1);
}

function printNums($n)
{
    $str = "";
    printRec($str, 0, $n);
}

// Driver Code
$n = 4;

// Function call
printNums($n);

// This code is contributed by Mukul Singh.
```

## java 描述语言

```
<script>
// Javascript program to print all N-bit binary

    // function to generate n digit numbers
   function printRec(number, extraOnes, remainingPlaces)
    {
        // if number generated
        if (0 == remainingPlaces) {
            document.write(number + " ");
            return;
        }

        // Append 1 at the current number and
        // reduce the remaining places by one
        printRec(number + "1", extraOnes + 1,
                 remainingPlaces - 1);

        // If more ones than zeros, append 0 to the
        // current number and reduce the remaining
        // places by one
        if (0 < extraOnes)
            printRec(number + "0", extraOnes - 1,
                     remainingPlaces - 1);
    }

    function printNums(n)
    {
        let str = "";
        printRec(str, 0, n);
    }

// driver function

        let n = 4;

        // Function call
        printNums(n);

</script>
```

**Output**

```
1111 1110 1101 1100 1011 1010 
```

也存在非递归解决方案，其思想是直接生成 2^N 到 2^(N-1 范围内的数字)，然后只需要满足以下条件的数字:

## C++

```
// C++ program to print all N-bit binary
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to get the binary representation
// of the number N
string getBinaryRep(int N, int num_of_bits)
{
    string r = "";
    num_of_bits--;

    // loop for each bit
    while (num_of_bits >= 0)
    {
        if (N & (1 << num_of_bits))
            r.append("1");
        else
            r.append("0");
        num_of_bits--;
    }
    return r;
}

vector<string> NBitBinary(int N)
{
    vector<string> r;
    int first = 1 << (N - 1);
    int last = first * 2;

    // generate numbers in the range of (2^N)-1 to 2^(N-1)
    // inclusive
    for (int i = last - 1; i >= first; --i)
    {
        int zero_cnt = 0;
        int one_cnt = 0;
        int t = i;
        int num_of_bits = 0;

        // longest prefix check
        while (t)
        {
            if (t & 1)
                one_cnt++;
            else
                zero_cnt++;
            num_of_bits++;
            t = t >> 1;
        }

        // if counts of 1 is greater than
        // counts of zero
        if (one_cnt >= zero_cnt)
        {
            // do sub-prefixes check
            bool all_prefix_match = true;
            int msk = (1 << num_of_bits) - 2;
            int prefix_shift = 1;
            while (msk)
            {

                int prefix = (msk & i) >> prefix_shift;
                int prefix_one_cnt = 0;
                int prefix_zero_cnt = 0;
                while (prefix)
                {
                    if (prefix & 1)
                        prefix_one_cnt++;
                    else
                        prefix_zero_cnt++;
                    prefix = prefix >> 1;
                }
                if (prefix_zero_cnt > prefix_one_cnt)
                {
                    all_prefix_match = false;
                    break;
                }
                prefix_shift++;
                msk = msk & (msk << 1);
            }
            if (all_prefix_match)
            {
                r.push_back(getBinaryRep(i, num_of_bits));
            }
        }
    }
    return r;
}

// Driver code
int main()
{
    int n = 4;

    // Function call
    vector<string> results = NBitBinary(n);
    for (int i = 0; i < results.size(); ++i)
        cout << results[i] << " ";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all N-bit binary
import java.io.*;
import java.util.*;
class GFG
{

  // Function to get the binary representation
  // of the number N
  static String getBinaryRep(int N, int num_of_bits)
  {
    String r = "";
    num_of_bits--;

    // loop for each bit
    while (num_of_bits >= 0)
    {
      if ((N & (1 << num_of_bits))!=0)
        r += "1";
      else
        r += "0";
      num_of_bits--;
    }
    return r;
  }

  static ArrayList<String> NBitBinary(int N)
  {
    ArrayList<String> r = new ArrayList<String>();
    int first = 1 << (N - 1);
    int last = first * 2;

    // generate numbers in the range of (2^N)-1 to 2^(N-1)
    // inclusive
    for (int i = last - 1; i >= first; --i)
    {
      int zero_cnt = 0;
      int one_cnt = 0;
      int t = i;
      int num_of_bits = 0;

      // longest prefix check
      while (t > 0)
      {
        if ((t & 1) != 0)
          one_cnt++;
        else
          zero_cnt++;
        num_of_bits++;
        t = t >> 1;
      }

      // if counts of 1 is greater than
      // counts of zero
      if (one_cnt >= zero_cnt)
      {
        // do sub-prefixes check
        boolean all_prefix_match = true;
        int msk = (1 << num_of_bits) - 2;
        int prefix_shift = 1;
        while (msk > 0)
        {

          int prefix = (msk & i) >> prefix_shift;
          int prefix_one_cnt = 0;
          int prefix_zero_cnt = 0;
          while (prefix > 0)
          {
            if ((prefix & 1)!=0)
              prefix_one_cnt++;
            else
              prefix_zero_cnt++;
            prefix = prefix >> 1;
          }
          if (prefix_zero_cnt > prefix_one_cnt)
          {
            all_prefix_match = false;
            break;
          }
          prefix_shift++;
          msk = msk & (msk << 1);
        }
        if (all_prefix_match)
        {
          r.add(getBinaryRep(i, num_of_bits));
        }
      }
    }
    return r;
  }

  // Driver code
  public static void main (String[] args)
  {

    int n = 4;

    // Function call
    ArrayList<String> results = NBitBinary(n);
    for (int i = 0; i < results.size(); ++i)
      System.out.print(results.get(i)+" ");
    System.out.println();
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to print
# all N-bit binary

# Function to get the binary
# representation of the number N
def getBinaryRep(N, num_of_bits):

    r = "";
    num_of_bits -= 1

    # loop for each bit
    while (num_of_bits >= 0):   
        if (N & (1 << num_of_bits)):
            r += ("1");
        else:
            r += ("0");
        num_of_bits -= 1

    return r;

def NBitBinary(N):

    r = []
    first = 1 << (N - 1);
    last = first * 2;

    # generate numbers in the range
    # of (2^N)-1 to 2^(N-1) inclusive
    for i in range (last - 1,
                    first - 1, -1):   
        zero_cnt = 0;
        one_cnt = 0;
        t = i;
        num_of_bits = 0;

        # longest prefix check
        while (t):       
            if (t & 1):
                one_cnt += 1
            else:
                zero_cnt += 1
            num_of_bits += 1
            t = t >> 1;       

        # if counts of 1 is greater
        # than counts of zero
        if (one_cnt >= zero_cnt):

            # do sub-prefixes check
            all_prefix_match = True;
            msk = (1 << num_of_bits) - 2;
            prefix_shift = 1;

            while (msk):           
                prefix = ((msk & i) >>
                           prefix_shift);
                prefix_one_cnt = 0;
                prefix_zero_cnt = 0;

                while (prefix):               
                    if (prefix & 1):
                        prefix_one_cnt += 1
                    else:
                        prefix_zero_cnt += 1
                    prefix = prefix >> 1;

                if (prefix_zero_cnt >
                    prefix_one_cnt):               
                    all_prefix_match = False;
                    break;

                prefix_shift += 1
                msk = msk & (msk << 1);

            if (all_prefix_match):           
                r.append(getBinaryRep(i,
                                      num_of_bits));         
    return r

# Driver code
if __name__ == "__main__":

    n = 4;

    # Function call
    results = NBitBinary(n);
    for i in range (len(results)):
        print (results[i],
               end = " ")
    print ()

# This code is contributed by Chitranayal
```

## C#

```
// C# program to print all N-bit binary
using System;
using System.Collections.Generic;

class GFG{

// Function to get the binary representation
// of the number N
static string getBinaryRep(int N, int num_of_bits)
{
    string r = "";
    num_of_bits--;

    // loop for each bit
    while (num_of_bits >= 0)
    {
        if ((N & (1 << num_of_bits)) != 0)
            r += "1";
        else
            r += "0";

        num_of_bits--;
    }
    return r;
}

static List<string> NBitBinary(int N)
{
    List<string> r = new List<string>();
    int first = 1 << (N - 1);
    int last = first * 2;

    // Generate numbers in the range of (2^N)-1 to 2^(N-1)
    // inclusive
    for(int i = last - 1; i >= first; --i)
    {
        int zero_cnt = 0;
        int one_cnt = 0;
        int t = i;
        int num_of_bits = 0;

        // longest prefix check
        while (t > 0)
        {
            if ((t & 1) != 0)
                one_cnt++;
            else
                zero_cnt++;

            num_of_bits++;
            t = t >> 1;
        }

        // If counts of 1 is greater than
        // counts of zero
        if (one_cnt >= zero_cnt)
        {

            // Do sub-prefixes check
            bool all_prefix_match = true;
            int msk = (1 << num_of_bits) - 2;
            int prefix_shift = 1;

            while (msk > 0)
            {
                int prefix = (msk & i) >> prefix_shift;
                int prefix_one_cnt = 0;
                int prefix_zero_cnt = 0;

                while (prefix > 0)
                {
                    if ((prefix & 1)!=0)
                        prefix_one_cnt++;
                    else
                        prefix_zero_cnt++;

                    prefix = prefix >> 1;
                }
                if (prefix_zero_cnt > prefix_one_cnt)
                {
                    all_prefix_match = false;
                    break;
                }
                prefix_shift++;
                msk = msk & (msk << 1);
            }
            if (all_prefix_match)
            {
                r.Add(getBinaryRep(i, num_of_bits));
            }
        }
    }
    return r;
}

// Driver code
static public void Main()
{
    int n = 4;

    // Function call
    List<string> results = NBitBinary(n);
    for (int i = 0; i < results.Count; ++i)
        Console.Write(results[i] + " ");

    Console.WriteLine();
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
    // Javascript program to print all N-bit binary

    // Function to get the binary representation
    // of the number N
    function getBinaryRep(N, num_of_bits)
    {
      let r = "";
      num_of_bits--;

      // loop for each bit
      while (num_of_bits >= 0)
      {
        if ((N & (1 << num_of_bits))!=0)
          r += "1";
        else
          r += "0";
        num_of_bits--;
      }
      return r;
    }

    function NBitBinary(N)
    {
      let r = [];
      let first = 1 << (N - 1);
      let last = first * 2;

      // generate numbers in the range of (2^N)-1 to 2^(N-1)
      // inclusive
      for (let i = last - 1; i >= first; --i)
      {
        let zero_cnt = 0;
        let one_cnt = 0;
        let t = i;
        let num_of_bits = 0;

        // longest prefix check
        while (t > 0)
        {
          if ((t & 1) != 0)
            one_cnt++;
          else
            zero_cnt++;
          num_of_bits++;
          t = t >> 1;
        }

        // if counts of 1 is greater than
        // counts of zero
        if (one_cnt >= zero_cnt)
        {
          // do sub-prefixes check
          let all_prefix_match = true;
          let msk = (1 << num_of_bits) - 2;
          let prefix_shift = 1;
          while (msk > 0)
          {

            let prefix = (msk & i) >> prefix_shift;
            let prefix_one_cnt = 0;
            let prefix_zero_cnt = 0;
            while (prefix > 0)
            {
              if ((prefix & 1)!=0)
                prefix_one_cnt++;
              else
                prefix_zero_cnt++;
              prefix = prefix >> 1;
            }
            if (prefix_zero_cnt > prefix_one_cnt)
            {
              all_prefix_match = false;
              break;
            }
            prefix_shift++;
            msk = msk & (msk << 1);
          }
          if (all_prefix_match)
          {
            r.push(getBinaryRep(i, num_of_bits));
          }
        }
      }
      return r;
    }

    let n = 4;

    // Function call
    let results = NBitBinary(n);
    for (let i = 0; i < results.length; ++i)
      document.write(results[i]+" ");
    document.write("</br>");

// This code is contributed by mukesh07.
</script>
```

**Output**

```
1111 1110 1101 1100 1011 1010 
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。