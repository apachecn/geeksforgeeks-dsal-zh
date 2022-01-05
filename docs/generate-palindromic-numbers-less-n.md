# 生成所有小于 n 的回文号

> 原文:[https://www . geesforgeks . org/generate-回文-numbers-less-n/](https://www.geeksforgeeks.org/generate-palindromic-numbers-less-n/)

找出所有小于 n 的数字，它们都是回文。数字可以按任何顺序打印。

**示例:**

```
Input : n = 12
Output : 1, 2, 3, 4, 5, 6, 7, 8, 9, 11

Input : n = 104
Output : 1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 
         22, 33, 44, 55, 66, 77, 88, 99, 101
[Note that below program prints these numbers
 in different order]

```

**蛮力:**我们检查从 1 到 n 的所有数字，看它的十进制表示是不是回文。

**高效方法:**我们从 1 开始，创建奇数和偶数直到 n 的回文。对于每个数字(从 1 开始)，如果我们需要偶数长度的回文数字，我们会在末尾追加它的反码。对于奇数长度的回文，除了最后一个数字外，我们将所有数字的反序追加。

## C++

```
// A C++ program to generate palindromic numbers
// less than n.
#include <iostream>
using namespace std;

// A utility for creating palindrome
int createPalindrome(int input, int b, bool isOdd)
{
    int n = input;
    int palin = input;

    // checks if number of digits is odd or even
    // if odd then neglect the last digit of input in
    // finding reverse as in case of odd number of
    // digits middle element occur once
    if (isOdd)
        n /= b;

    // Creates palindrome by just appending reverse
    // of number to itself
    while (n > 0)
    {
        palin = palin * b + (n % b);
        n /= b;
    }
    return palin;
}

// Function to print decimal palindromic number
void generatePalindromes(int n)
{
    int number;

    // Run two times for odd and even length palindromes
    for (int j = 0; j < 2; j++)
    {
        // Creates palindrome numbers with first half as i.
        // Value of j decided whether we need an odd length
        // of even length palindrome.
        int i = 1;
        while ((number = createPalindrome(i, 10, j % 2)) < n)
        {
            cout << number << " ";
            i++;
        }
    }
}

// Driver Program to test above function
int main()
{
    int n = 104;
    generatePalindromes(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to generate palindromic
// numbers less than n.
class GFG {

// A utility for creating palindrome
static int createPalindrome(int input, int b, int isOdd) {
    int n = input;
    int palin = input;

    // checks if number of digits is odd or even
    // if odd then neglect the last digit of input in
    // finding reverse as in case of odd number of
    // digits middle element occur once
    if (isOdd == 1)
        n /= b;

    // Creates palindrome by just appending reverse
    // of number to itself
    while (n > 0) {
        palin = palin * b + (n % b);
        n /= b;
    }
    return palin;
}

// Function to print decimal
// palindromic number
static void generatePalindromes(int n) {
    int number;

    // Run two times for odd and even
    // length palindromes
    for (int j = 0; j < 2; j++) {

    // Creates palindrome numbers with first
    // half as i. Value of j decided whether
    // we need an odd length of even length
    // palindrome.
        int i = 1;
        while ((number = createPalindrome(i, 10, j % 2)) < n) {
            System.out.print(number + " ");
            i++;
    }
    }
}

// Driver code
public static void main(String[] args) {
    int n = 104;
    generatePalindromes(n);
}
}
// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Generate all palindromic numbers less than n
# A Python program to generate palindromic numbers
# less than n.
def createPalindrome(inp, b, isOdd):
    n = inp
    palin = inp

    # checks if number of digits is odd or even
    # if odd then neglect the last digit of input in
    # finding reverse as in case of odd number of
    # digits middle element occur once
    if (isOdd):
        n = n / b

    # Creates palindrome by just appending reverse
    # of number to itself
    while (n > 0):
        palin = palin * b + (n % b)
        n = n / b
    return palin

# Function to print decimal palindromic number
def generatePalindromes(n):

    # Run two times for odd and even length palindromes
    for j in range(2):
        # Creates palindrome numbers with first half as i.
        # Value of j decided whether we need an odd length
        # of even length palindrome.
        i = 1
        while (createPalindrome(i, 10, j % 2) < n):
            print createPalindrome(i, 10, j % 2),
            i = i + 1

# Driver Program to test above function
n = 104
generatePalindromes(n)

#This code is contributed by Afzal Ansari
```

## C#

```
// A C# program to generate palindromic
// numbers less than n.
using System;

class GFG {

// A utility for creating palindrome
static int createPalindrome(int input, int b,
                            int isOdd)
{
    int n = input;
    int palin = input;

    // checks if number of digits is odd
    // or even if odd then neglect the
    // last digit of input in finding reverse
    // as in case of odd number of digits
    // middle element occur once
    if (isOdd == 1)
        n /= b;

    // Creates palindrome by just appending
    // reverse of number to itself
    while (n > 0)
    {
        palin = palin * b + (n % b);
        n /= b;
    }
    return palin;
}

// Function to print decimal
// palindromic number
static void generatePalindromes(int n)
{
    int number;

    // Run two times for odd and even
    // length palindromes
    for (int j = 0; j < 2; j++)
    {

        // Creates palindrome numbers with first
        // half as i. Value of j decided whether
        // we need an odd length of even length
        // palindrome.
        int i = 1;
        while ((number = createPalindrome(i, 10,
                                    j % 2)) < n)
        {
            Console.Write(number + " ");
            i++;
    }
    }
}

// Driver Code
public static void Main()
{
    int n = 104;
    generatePalindromes(n);
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate
// palindromic numbers less than n.

// A utility function for
// creating palindrome
function createPalindrome($input,
                          $b, $isOdd)
{
    $n = $input;
    $palin = $input;

    // checks if number of digits is
    // odd or even if odd then neglect
    // the last digit of input in finding
    // reverse as in case of odd number
    // of digits middle element occur once
    if ($isOdd)
        $n = intval($n / $b);

    // Creates palindrome by just appending
    // reverse of number to itself
    while ($n > 0)
    {
        $palin = $palin * $b + intval($n % $b);
        $n = intval($n / $b);
    }
    return $palin;
}

// Function to print decimal
// palindromic number
function generatePalindromes($n)
{
    $number = 0;

    // Run two times for odd and
    // even length palindromes
    for ($j = 0; $j < 2; $j++)
    {
        // Creates palindrome numbers
        // with first half as i. Value
        // of j decided whether we need
        // an odd length of even length
        // palindrome.
        $i = 1;
        while (($number =
                   createPalindrome($i, 10,
                                    $j % 2)) < $n)
        {
            echo $number . " ";
            $i++;
        }
    }
}

// Driver Code
$n = 104;
generatePalindromes($n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // A Javascript program to generate palindromic
    // numbers less than n.

    // A utility for creating palindrome
    function createPalindrome(input, b, isOdd)
    {
        let n = input;
        let palin = input;

        // checks if number of digits is odd
        // or even if odd then neglect the
        // last digit of input in finding reverse
        // as in case of odd number of digits
        // middle element occur once
        if (isOdd == 1)
            n = parseInt(n / b, 10);

        // Creates palindrome by just appending
        // reverse of number to itself
        while (n > 0)
        {
            palin = palin * b + (n % b);
            n = parseInt(n / b, 10);
        }
        return palin;
    }

    // Function to print decimal
    // palindromic number
    function generatePalindromes(n)
    {
        let number;

        // Run two times for odd and even
        // length palindromes
        for (let j = 0; j < 2; j++)
        {

            // Creates palindrome numbers with first
            // half as i. Value of j decided whether
            // we need an odd length of even length
            // palindrome.
            let i = 1;
            while ((number = createPalindrome(i, 10, j % 2)) < n)
            {
                document.write(number + " ");
                i++;
            }
        }
    }

    let n = 104;
    generatePalindromes(n);

   // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
11 22 33 44 55 66 77 88 99 1 2 3 4 5 6 7 8 9 101 
```

请注意，上面的程序不会按排序顺序打印输出。为了按排序顺序打印，我们可以将回文存储在一个向量中并对其进行排序，并且不要忘记使用所需的头文件。

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。