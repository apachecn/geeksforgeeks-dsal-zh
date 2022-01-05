# 小于 N 的最大数字，其每个数字都是质数

> 原文:[https://www . geesforgeks . org/最大数减 n-what-digit-prime-number/](https://www.geeksforgeeks.org/largest-number-less-n-whose-digit-prime-number/)

给定一个非常大的数字**N**(1<= N<中的位数= 10 <sup>5</sup> )。任务是找到最大的数 X，使得 X < N 和 X 的每个数字都是质数。

**示例:**

```
Input : N = 1000
Output : 777
777 is the largest number less than
1000 which have each digit as prime.

Input : N = 11
Output : 7
```

想法是从数字 N 的最左边的数字遍历到数字 N 的最右边的数字。检查当前数字是否是质数。如果是质数，将数字复制到相应的数字位置输出数字。如果不是素数，复制小于当前数字的最大素数。

现在考虑当前数字是“0”还是“1”。在这种情况下，将“7”复制到输出号码的当前数字位置。同时移动到当前数字的左邻数字，并将其减少到小于它的最大素数。
一旦我们将任何一个数字减少到小于该数字的最大素数，我们就将‘7’复制到输出数字中右边数字的其余部分。

下面是该方法的实现:

## C++

```
// C++ program to find the largest number smaller
// than N whose all digits are prime.
#include <bits/stdc++.h>
using namespace std;

// Number is given as string.
char* PrimeDigitNumber(char N[], int size)
{
    char* ans = (char*)malloc(size * sizeof(char));
    int ns = 0;

    // We stop traversing digits, once it become
    // smaller than current number.
    // For that purpose we use small variable.
    int small = 0;
    int i;

    // Array indicating if index i (represents a
    // digit)  is prime or not.
    int p[] = { 0, 0, 1, 1, 0, 1, 0, 1, 0, 0 };

    // Store largest
    int prevprime[] = { 0, 0, 0, 2, 3, 3, 5, 5, 7, 7 };

    // If there is only one character, return
    // the largest prime less than the number
    if (size == 1) {
        ans[0] = prevprime[N[0] - '0'] + '0';

        ans[1] = '\0';
        return ans;
    }

    // If number starts with 1, return number
    // consisting of 7
    if (N[0] == '1') {
        for (int i = 0; i < size - 1; i++)
            ans[i] = '7';

        ans[size - 1] = '\0';

        return ans;
    }

    // Traversing each digit from right to left
    // Continue traversing till the number we
    // are forming will become less.
    for (i = 0; i < size && small == 0; i++) {

        // If digit is prime, copy it simply.
        if (p[N[i] - '0'] == 1) {
            ans[ns++] = N[i];
        } else {

            // If not prime, copy the largest prime
            // less than current number
            if (p[N[i] - '0'] == 0 &&
                prevprime[N[i] - '0'] != 0) {
                ans[ns++] = prevprime[N[i] - '0'] + '0';
                small = 1;
            }

            // If not prime, and there is no largest
            // prime less than current prime
            else if (p[N[i] - '0'] == 0 &&
                    prevprime[N[i] - '0'] == 0) {

                int j = i;

                // Make current digit as 7
                // Go left of the digit and make it largest
                // prime less than number. Continue do that
                // until we found a digit which has some
                // largest prime less than it
                while (j > 0 && p[N[j] - '0'] == 0 &&
                       prevprime[N[j] - '0'] == 0) {
                    ans[j] = N[j] = '7';
                    N[j - 1] = prevprime[N[j - 1] - '0'] + '0';
                    ans[j - 1] = N[j - 1];
                    small = 1;
                    j--;
                }

                i = ns;
            }
        }
    }

    // If the given number is itself a prime.
    if (small == 0) {

        // Make last digit as highest prime less
        // than given digit.
        if (prevprime[N[size - 1] - '0'] + '0' != '0')
            ans[size - 1] = prevprime[N[size - 1] - '0'] + '0';

        // If there is no highest prime less than
        // current digit.
        else {
            int j = size - 1;
            while (j > 0 && prevprime[N[j] - '0'] == 0) {
                ans[j] = N[j] = '7';
                N[j - 1] = prevprime[N[j - 1] - '0'] + '0';
                ans[j - 1] = N[j - 1];
                small = 1;
                j--;
            }
        }
    }

    // Once one digit become less than any digit of input
    // replace 7 (largest 1 digit prime) till the end of
    // digits of number
    for (; ns < size; ns++)
        ans[ns] = '7';

    ans[ns] = '\0';

    // If number include 0 in the beginning, ignore
    // them. Case like 2200
    int k = 0;
    while (ans[k] == '0')
        k++;

    return ans + k;
}

// Driver Program
int main()
{
    char N[] = "1000";
    int size = strlen(N);
    cout << PrimeDigitNumber(N, size) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest number smaller
// than N whose all digits are prime.
import java.io.*;
class GFG
{

  // Number is given as string.
  static char[] PrimeDigitNumber(char N[], int size)
  {
    char[] ans = new char[size];  
    int ns = 0;

    // We stop traversing digits, once it become
    // smaller than current number.
    // For that purpose we use small variable.
    int small = 0;
    int i;

    // Array indicating if index i (represents a
    // digit)  is prime or not.
    int p[] = { 0, 0, 1, 1, 0, 1, 0, 1, 0, 0 };

    // Store largest
    int prevprime[] = { 0, 0, 0, 2, 3, 3, 5, 5, 7, 7 };

    // If there is only one character, return
    // the largest prime less than the number
    if (size == 1)
    {
      ans[0] = (char)(prevprime[N[0] - '0'] + '0');

      ans[1] = '\0';
      return ans;
    }

    // If number starts with 1, return number
    // consisting of 7
    if (N[0] == '1') {
      for (i = 0; i < size - 1; i++)
        ans[i] = '7';

      ans[size - 1] = '\0';

      return ans;
    }

    // Traversing each digit from right to left
    // Continue traversing till the number we
    // are forming will become less.
    for (i = 0; i < size && small == 0; i++) {

      // If digit is prime, copy it simply.
      if (p[N[i] - '0'] == 1) {
        ans[ns++] = N[i];
      } else {

        // If not prime, copy the largest prime
        // less than current number
        if (p[N[i] - '0'] == 0 &&
            prevprime[N[i] - '0'] != 0) {
          ans[ns++] = (char)(prevprime[N[i] - '0'] + '0');
          small = 1;
        }

        // If not prime, and there is no largest
        // prime less than current prime
        else if (p[N[i] - '0'] == 0 &&
                 prevprime[N[i] - '0'] == 0) {

          int j = i;

          // Make current digit as 7
          // Go left of the digit and make it largest
          // prime less than number. Continue do that
          // until we found a digit which has some
          // largest prime less than it
          while (j > 0 && p[N[j] - '0'] == 0 &&
                 prevprime[N[j] - '0'] == 0) {
            ans[j] = N[j] = '7';
            N[j - 1] = (char)(prevprime[N[j - 1] - '0'] + '0');
            ans[j - 1] = N[j - 1];
            small = 1;
            j--;
          }

          i = ns;
        }
      }
    }

    // If the given number is itself a prime.
    if (small == 0) {

      // Make last digit as highest prime less
      // than given digit.
      if (prevprime[N[size - 1] - '0'] + '0' != '0')
        ans[size - 1] = (char)(prevprime[N[size - 1] - '0'] + '0');

      // If there is no highest prime less than
      // current digit.
      else {
        int j = size - 1;
        while (j > 0 && prevprime[N[j] - '0'] == 0) {
          ans[j] = N[j] = '7';
          N[j - 1] = (char)(prevprime[N[j - 1] - '0'] + '0');
          ans[j - 1] = N[j - 1];
          small = 1;
          j--;
        }
      }
    }

    // Once one digit become less than any digit of input
    // replace 7 (largest 1 digit prime) till the end of
    // digits of number
    for (; ns < size; ns++)
      ans[ns] = '7';

    ans[ns] = '\0';

    // If number include 0 in the beginning, ignore
    // them. Case like 2200
    int k = 0;
    while (ans[k] == '0')
      k++;

    return ans;
  }

  // Driver Program
  public static void main (String[] args)
  {
    char[] N= "1000".toCharArray();
    int size=N.length;
    System.out.println(PrimeDigitNumber(N, size));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to find the largest number smaller
# than N whose all digits are prime.

# Number is given as string.
def PrimeDigitNumber(N, size):
    ans = [""]*size
    ns = 0;

    # We stop traversing digits, once it become
    # smaller than current number.
    # For that purpose we use small variable.
    small = 0;

    # Array indicating if index i (represents a
    # digit)  is prime or not.
    p = [ 0, 0, 1, 1, 0, 1, 0, 1, 0, 0 ]

    # Store largest
    prevprime = [ 0, 0, 0, 2, 3, 3, 5, 5, 7, 7 ]

    # If there is only one character, return
    # the largest prime less than the number
    if (size == 1):
        ans[0] = prevprime[ord(N[0]) - ord('0')] + ord('0');
        ans[1] = '';
        return ''.join(ans);

    # If number starts with 1, return number
    # consisting of 7
    if (N[0] == '1'):
        for i in range(size - 1):
            ans[i] = '7'
        ans[size - 1] = '';
        return ''.join(ans)

    # Traversing each digit from right to left
    # Continue traversing till the number we
    # are forming will become less.
    i = 0
    while (i < size and small == 0):

        # If digit is prime, copy it simply.
        if (p[ord(N[i]) - ord('0')] == 1):
            ans[ns] = N[i]
            ns += 1
        else:

            # If not prime, copy the largest prime
            # less than current number
            if (p[ord(N[i]) - ord('0')] == 0 and
                prevprime[ord(N[i]) - ord('0')] != 0):
                ans[ns] = prevprime[ord(N[i]) - ord('0')] + ord('0');
                small = 1
                ns += 1

            # If not prime, and there is no largest
            # prime less than current prime
            elif (p[ord(N[i]) - ord('0')] == 0 and
                    prevprime[ord(N[i]) - ord('0')] == 0):         
                j = i;

                # Make current digit as 7
                # Go left of the digit and make it largest
                # prime less than number. Continue do that
                # until we found a digit which has some
                # largest prime less than it
                while (j > 0 and p[ord(N[j]) - ord('0')] == 0 and
                       prevprime[ord(N[j]) - ord('0')] == 0):
                    ans[j] = N[j] = '7';
                    N[j - 1] = prevprime[ord(N[j - 1]) - ord('0')] + ord('0');
                    ans[j - 1] = N[j - 1];
                    small = 1;
                    j -= 1              
                i = ns
        i += 1

    # If the given number is itself a prime.
    if (small == 0):

        # Make last digit as highest prime less
        # than given digit.
        if (prevprime[ord(N[size - 1]) - ord('0')] + ord('0') != ord('0')):
            ans[size - 1] = prevprime[ord(N[size - 1]) - ord('0')] + ord('0');

        # If there is no highest prime less than
        # current digit.
        else :
            j = size - 1;
            while (j > 0 and prevprime[ord(N[j]) - ord('0')] == 0):
                ans[j] = N[j] = '7';
                N[j - 1] = prevprime[ord(N[j - 1]) - ord('0')] + ord('0');
                ans[j - 1] = N[j - 1];
                small = 1;
                j -= 1

    # Once one digit become less than any digit of input
    # replace 7 (largest 1 digit prime) till the end of
    # digits of number
    while(ns < size):
        ans[ns] = '7'
        ns += 1

    ans[ns] = '';

    # If number include 0 in the beginning, ignore
    # them. Case like 2200
    k = 0;
    while (ans[k] == '0'):
        k += 1
    return (ans + k)

# Driver Program
if __name__ == "__main__":

    N = "1000";
    size = len(N);
    print(PrimeDigitNumber(N, size))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program to find the largest number smaller
// than N whose all digits are prime.
using System;

class GFG{

// Number is given as string.
static char[] PrimeDigitNumber(char[] N, int size)
{
    char[] ans = new char[size];  
    int ns = 0;

    // We stop traversing digits, once it become
    // smaller than current number.
    // For that purpose we use small variable.
    int small = 0;
    int i;

    // Array indicating if index i (represents a
    // digit)  is prime or not.
    int[] p = { 0, 0, 1, 1, 0, 1, 0, 1, 0, 0 };

    // Store largest
    int[] prevprime = { 0, 0, 0, 2, 3, 3, 5, 5, 7, 7 };

    // If there is only one character, return
    // the largest prime less than the number

    if (size == 1)
    {
        ans[0] = (char)(prevprime[N[0] - '0'] + '0');
        ans[1] = '\0';
        return ans;
    }

    // If number starts with 1, return number
    // consisting of 7
    if (N[0] == '1')
    {
        for (i = 0; i < size - 1; i++)
            ans[i] = '7';

        ans[size - 1] = '\0';

        return ans;
    }

    // Traversing each digit from right to left
    // Continue traversing till the number we
    // are forming will become less.
    for(i = 0; i < size && small == 0; i++)
    {

        // If digit is prime, copy it simply.
        if (p[N[i] - '0'] == 1)
        {
            ans[ns++] = N[i];
        }
        else
        {

            // If not prime, copy the largest prime
            // less than current number
            if (p[N[i] - '0'] == 0 &&
                prevprime[N[i] - '0'] != 0)
            {
                ans[ns++] = (char)(prevprime[N[i] - '0'] + '0');
                small = 1;
            }

            // If not prime, and there is no largest
            // prime less than current prime
            else if (p[N[i] - '0'] == 0 &&
                     prevprime[N[i] - '0'] == 0)
            {

                int j = i;

                // Make current digit as 7
                // Go left of the digit and make it largest
                // prime less than number. Continue do that
                // until we found a digit which has some
                // largest prime less than it
                while (j > 0 && p[N[j] - '0'] == 0 &&
                        prevprime[N[j] - '0'] == 0)
                {
                    ans[j] = N[j] = '7';
                    N[j - 1] = (char)(
                        prevprime[N[j - 1] - '0'] + '0');
                    ans[j - 1] = N[j - 1];
                    small = 1;
                    j--;
                }
                i = ns;
            }
        }
    }

    // If the given number is itself a prime.
    if (small == 0)
    {

        // Make last digit as highest prime less
        // than given digit.
        if (prevprime[N[size - 1] - '0'] + '0' != '0')
            ans[size - 1] = (char)(
                prevprime[N[size - 1] - '0'] + '0');

        // If there is no highest prime less than
        // current digit.
        else
        {
            int j = size - 1;
            while (j > 0 && prevprime[N[j] - '0'] == 0)
            {
                ans[j] = N[j] = '7';
                N[j - 1] = (char)(
                    prevprime[N[j - 1] - '0'] + '0');
                ans[j - 1] = N[j - 1];
                small = 1;
                j--;
            }
        }
    }

    // Once one digit become less than any digit of input
    // replace 7 (largest 1 digit prime) till the end of
    // digits of number
    for(; ns < size; ns++)
        ans[ns] = '7';

    ans[ns] = '\0';

    // If number include 0 in the beginning, ignore
    // them. Case like 2200
    int k = 0;
    while (ans[k] == '0')
        k++;

    return ans;
}

// Driver Code
static public void Main()
{
    char[] N = "1000".ToCharArray();
    int size = N.Length;

    Console.WriteLine(PrimeDigitNumber(N, size));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program to find the largest number smaller
// than N whose all digits are prime.

// Number is given as string.
function PrimeDigitNumber(N,size)
{
    let ans = new Array(size); 
    let ns = 0;

    // We stop traversing digits, once it become
    // smaller than current number.
    // For that purpose we use small variable.
    let small = 0;
    let i;

    // Array indicating if index i (represents a
    // digit)  is prime or not.
    let p = [ 0, 0, 1, 1, 0, 1, 0, 1, 0, 0 ];

    // Store largest
    let prevprime = [ 0, 0, 0, 2, 3, 3, 5, 5, 7, 7 ];

    // If there is only one character, return
    // the largest prime less than the number
    if (size == 1)
    {
      ans[0] = String.fromCharCode(prevprime[N[0].charCodeAt(0) - '0'.charCodeAt(0)] + '0'.charCodeAt(0));

      ans[1] = '\0';
      return ans;
    }

    // If number starts with 1, return number
    // consisting of 7
    if (N[0] == '1') {
      for (i = 0; i < size - 1; i++)
        ans[i] = '7';

      ans[size - 1] = '\0';

      return ans;
    }

    // Traversing each digit from right to left
    // Continue traversing till the number we
    // are forming will become less.
    for (i = 0; i < size && small == 0; i++) {

      // If digit is prime, copy it simply.
      if (p[N[i].charCodeAt(0) - '0'.charCodeAt(0)] == 1) {
        ans[ns++] = N[i];
      } else {

        // If not prime, copy the largest prime
        // less than current number
        if (p[N[i] - '0'] == 0 &&
            prevprime[N[i].charCodeAt(0) - '0'.charCodeAt(0)] != 0) {
          ans[ns++] = String.fromCharCode(prevprime[N[i].charCodeAt(0) - '0'.charCodeAt(0)] + '0'.charCodeAt(0));
          small = 1;
        }

        // If not prime, and there is no largest
        // prime less than current prime
        else if (p[N[i].charCodeAt(0) - '0'.charCodeAt(0)] == 0 &&
                 prevprime[N[i].charCodeAt(0) - '0'.charCodeAt(0)] == 0) {

          let j = i;

          // Make current digit as 7
          // Go left of the digit and make it largest
          // prime less than number. Continue do that
          // until we found a digit which has some
          // largest prime less than it
          while (j > 0 && p[N[j].charCodeAt(0) - '0'.charCodeAt(0)] == 0 &&
                 prevprime[N[j].charCodeAt(0) - '0'.charCodeAt(0)] == 0) {
            ans[j] = N[j] = '7';
            N[j - 1] = String.fromCharCode(prevprime[N[j - 1].charCodeAt(0) - '0'.charCodeAt(0)] + '0'.charCodeAt(0));
            ans[j - 1] = N[j - 1];
            small = 1;
            j--;
          }

          i = ns;
        }
      }
    }

    // If the given number is itself a prime.
    if (small == 0) {

      // Make last digit as highest prime less
      // than given digit.
      if (prevprime[N[size - 1].charCodeAt(0) - '0'.charCodeAt(0)] + '0'.charCodeAt(0) != '0'.charCodeAt(0))
        ans[size - 1] = String.fromCharCode(prevprime[N[size - 1].charCodeAt(0) - '0'.charCodeAt(0)] + '0'.charCodeAt(0));

      // If there is no highest prime less than
      // current digit.
      else {
        let j = size - 1;
        while (j > 0 && prevprime[N[j].charCodeAt(0) - '0'.charCodeAt(0)] == 0) {
          ans[j] = N[j] = '7';
          N[j - 1] = String.fromCharCode(prevprime[N[j - 1].charCodeAt(0) - '0'.charCodeAt(0)] + '0'.charCodeAt(0));
          ans[j - 1] = N[j - 1];
          small = 1;
          j--;
        }
      }
    }

    // Once one digit become less than any digit of input
    // replace 7 (largest 1 digit prime) till the end of
    // digits of number
    for (; ns < size; ns++)
      ans[ns] = '7';

    ans[ns] = '\0';

    // If number include 0 in the beginning, ignore
    // them. Case like 2200
    let k = 0;
    while (ans[k] == '0')
      k++;

    return ans.join("");
}

// Driver Program
let N= "1000".split("");
let size=N.length;
document.write(PrimeDigitNumber(N, size).join(""));

// This code is contributed by ab2127
</script>
```

**输出:**

```
777
```

本文由 **Anuj Chauhan (anuj0503)** 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。