# C++程序查找所有小于 n 的数字，这些数字在基数 10 和基数 2 是回文。

> 原文:[https://www . geesforgeks . org/find-numbers-less-n-回文-base-10-base-2/](https://www.geeksforgeeks.org/find-numbers-less-n-palindromic-base-10-base-2/)

找出所有小于 n 的数字，它们在第 10 位和第 2 位都是回文。

示例:

```
33 is Palindrome in its decimal representation.
100001(binary equivalent of 33) in Binary is a Palindrome.

313 is Palindrome in its decimal representation.
100111001 (binary equivalent of 313) in Binary is a Palindrome.

```

**蛮力:**
我们检查从 1 到 n 的所有数字，看它的十进制表示是否是回文。
此外，如果一个数在基数 10 中是回文，那么我们检查它的二进制表示。如果我们发现它的两个表示都是回文，那么我们就把它打印出来。

**高效方法:**
我们从 1 开始，创建奇数和偶数直到 n 的回文，并检查其二进制表示是否是回文。
注意:这将减少运算次数，因为我们应该只检查十进制回文，而不是检查从 1 到 n 的所有数字。

这种方法使用两种方法:

**int createpalidome(int input，int b，bool isOdd):**
回文创建者接受一个输入数字和一个基数 b，以及一个告诉回文应该有偶数还是奇数位数的布尔值。它接受输入的数字，将其反转并附加到输入的数字上。如果结果应该有奇数个数字，它会砍掉反转部分的一个数字。

**bool ispalindome(int number，int b)**
取输入的数字，根据基数 b 计算其倒数，返回数字是否等于其倒数的结果。

```
// A C++ program for finding numbers which are
// decimal as well as binary palindrome
#include <iostream>
using namespace std;

// A utility to check if  number is palindrome on base b
bool IsPalindrome(int number, int b)
{
    int reversed = 0;
    int k = number;

    // calculate reverse of number
    while (k > 0) {
        reversed = b * reversed + k % b;
        k /= b;
    }

    // return true/false depending upon number is palindrome or not
    return (number == reversed);
}

// A utility for creating palindrome
int createPalindrome(int input, int b, bool isOdd)
{
    int n = input;
    int palin = input;

    // checks if number of digits is odd or even
    // if odd then neglect the last digit of input in finding reverse
    // as in case of odd number of digits middle element occur once
    if (isOdd)
        n /= b;

    // creates palindrome by just appending reverse of number to itself
    while (n > 0) {
        palin = palin * b + (n % b);
        n /= b;
    }
    return palin;
}

// Function to print decimal and binary palindromic number
void findPalindromic(int n)
{
    int number;
    for (int j = 0; j < 2; j++) {
        bool isOdd = (j % 2 == 0);

        // Creates palindrome of base 10 upto n
        // j always decides digits of created palindrome
        int i = 1;
        while ((number = createPalindrome(i, 10, isOdd)) < n) {
            // if created palindrome of base 10 is
            // binary palindrome
            if (IsPalindrome(number, 2))
                cout << number << " ";
            i++;
        }
    }
}

// Driver Program to test above function
int main()
{
    int n = 1000;
    findPalindromic(n);
    return 0;
}
```

**Output:**

```
1 3 5 7 9 313 585 717 33 99

```

本文由**[Shivam Pradhan(anuj _ charm)](https://www.facebook.com/anuj.charm)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。