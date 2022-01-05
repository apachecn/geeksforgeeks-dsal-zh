# 回文自拍号

> 原文:[https://www.geeksforgeeks.org/palindromic-selfie-numbers/](https://www.geeksforgeeks.org/palindromic-selfie-numbers/)

给定一个数 x，根据自拍乘法法则找到它的回文自拍数。如果不存在这样的号码，则打印“不存在这样的号码”。
回文自拍号满足自拍乘法规则，使得存在另一个编号 y，编号 y 的*x * reverse _ digits _ of(x)= y * reverse _ digits _ of(y)*，条件是编号 y 是通过对 x 中的数字进行某种排序得到的，即 x 和 y 应该具有相同的数字，但顺序不同。
示例:

```
Input : 1224
Output : 2142
Explanation :
Because, 1224 X 4221 = 2142 X 2412
And all digits of 2142 are formed by a different 
permutation of the digits in 1224
(Note: The valid output is either be 2142 or 2412)

Input : 13452
Output : 14532
Explanation :
Because, 13452 X 25431 = 14532 X 23541
And all digits of 14532 are formed by a different 
permutation of the digits in 13452

Input : 12345
Output : No such number exists
Explanation :
Because, with no combination of digits 1, 2, 3, 4, 5 
could we get a number that satisfies 
12345 X 54321 = number X reverse_of_its_digits
```

**进场:**

*   其思想是分解数字，获得数字中数字的所有排列。
*   然后，从获得的排列集合中移除数字及其回文，这将形成我们等式的 LHS。
*   为了检查 RHS，我们现在迭代所有其他置换等式

```
 LHS = current_number X palindrome(current_number) 
```

*   一旦我们得到匹配，我们就以肯定的消息退出循环，否则打印“没有这样的号码可用”。

以下是上述方法的实施:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find palindromic selfie numbers
import java.util.*;

public class palindrome_selfie {
    // To store all permutations of digits in the number
    Set<Integer> all_permutes = new HashSet<Integer>();

    int number; // input number

    public palindrome_selfie(int num)
    {
        number = num;
    }

    // Function to reverse the digits of a number
    public int palindrome(int num)
    {
        int reversednum = 0;
        int d;
        while (num > 0) {
            d = num % 10; // Extract last digit

            // Append it at the beg
            reversednum = reversednum * 10 + d;
            num = num / 10;  // Reduce number until 0
        }

        return reversednum;
    }

    // Function to check palindromic selfie
    public void palin_selfie()
    {
        // Length of the number required for
        // calculating all permutations of the digits
        int l = String.valueOf(number).length() - 1;

        this.permute(number, 0, l); // Calculate all permutations

        /* Remove the number and its palindrome from
           the obtained set as this is the LHS of
           multiplicative equality */
        all_permutes.remove(palindrome(number));
        all_permutes.remove(number);

        boolean flag = false; // Denotes the status result

        // Iterate over all other numbers
        Iterator it = all_permutes.iterator();
        while (it.hasNext()) {
            int number2 = (int)it.next();

            // Check for equality x*palin(x) = y*palin(y)
            if (number * palindrome(number) ==
                         number2 * palindrome(number2)) {
                System.out.println("Palindrome multiplicative" +
                                    "selfie of "+ number + " is  : "
                                     + number2);

                flag = true; // Answer found
                break;
            }
        }

        // If no such number found
        if (flag == false) {
            System.out.println("Given number has no palindrome selfie.");
        }
    }

    // Function to get all possible possible permutations
    // of the digits in num
    public void permute(int num, int l, int r)
    {
        // Adds the new permutation obtained in the set
        if (l == r)
            all_permutes.add(num);

        else {
            for (int i = l; i <= r; i++) {

                // Swap digits to get a different ordering
                num = swap(num, l, i);

                // Recurse to next pair of digits
                permute(num, l + 1, r);
                num = swap(num, l, i); // Swap back
            }
        }
    }

    // Function that swaps the digits i and j in the num
    public int swap(int num, int i, int j)
    {
        char temp;

        // Convert int to char array
        char[] charArray = String.valueOf(num).toCharArray();

        // Swap the ith and jth character
        temp = charArray[i];
        charArray[i] = charArray[j];
        charArray[j] = temp;

        // Convert back to int and return
        return Integer.valueOf(String.valueOf(charArray));
    }

    // Driver Function
    public static void main(String args[])
    {
        // First example, input = 145572
        palindrome_selfie example1 = new palindrome_selfie(145572);
        example1.palin_selfie();

        // Second example, input = 19362
        palindrome_selfie example2 = new palindrome_selfie(19362);
        example2.palin_selfie();

        // Third example, input = 4669
        palindrome_selfie example3 = new palindrome_selfie(4669);
        example3.palin_selfie();
    }
}
```

## C#

```
// C# program to find palindromic selfie numbers
using System;
using System.Collections.Generic;

public class palindrome_selfie
{
    // To store all permutations of digits in the number
    HashSet<int> all_permutes = new HashSet<int>();

    int number; // input number

    public palindrome_selfie(int num)
    {
        number = num;
    }

    // Function to reverse the digits of a number
    public int palindrome(int num)
    {
        int reversednum = 0;
        int d;
        while (num > 0)
        {
            d = num % 10; // Extract last digit

            // Append it at the beg
            reversednum = reversednum * 10 + d;
            num = num / 10; // Reduce number until 0
        }
        return reversednum;
    }

    // Function to check palindromic selfie
    public void palin_selfie()
    {
        // Length of the number required for
        // calculating all permutations of the digits
        int l = String.Join("",number).Length - 1;

        this.permute(number, 0, l); // Calculate all permutations

        /* Remove the number and its palindrome from
        the obtained set as this is the LHS of
        multiplicative equality */
        all_permutes.Remove(palindrome(number));
        all_permutes.Remove(number);

        bool flag = false; // Denotes the status result

        // Iterate over all other numbers
        foreach (var number2 in all_permutes)
        {

            // Check for equality x*palin(x) = y*palin(y)
            if (number * palindrome(number) ==
                        number2 * palindrome(number2))
            {
                Console.WriteLine("Palindrome multiplicative" +
                                    "selfie of "+ number + " is : "
                                    + number2);

                flag = true; // Answer found
                break;
            }
        }

        // If no such number found
        if (flag == false)
        {
            Console.WriteLine("Given number has "+
                            "no palindrome selfie.");
        }
    }

    // Function to get all possible possible
    // permutations of the digits in num
    public void permute(int num, int l, int r)
    {
        // Adds the new permutation obtained in the set
        if (l == r)
            all_permutes.Add(num);

        else
        {
            for (int i = l; i <= r; i++)
            {

                // Swap digits to get a different ordering
                num = swap(num, l, i);

                // Recurse to next pair of digits
                permute(num, l + 1, r);
                num = swap(num, l, i); // Swap back
            }
        }
    }

    // Function that swaps the
    // digits i and j in the num
    public int swap(int num, int i, int j)
    {
        char temp;

        // Convert int to char array
        char[] charArray = String.Join("",num).ToCharArray();

        // Swap the ith and jth character
        temp = charArray[i];
        charArray[i] = charArray[j];
        charArray[j] = temp;

        // Convert back to int and return
        return int.Parse(String.Join("",charArray));
    }

    // Driver code
    public static void Main(String []args)
    {
        // First example, input = 145572
        palindrome_selfie example1 = new palindrome_selfie(145572);
        example1.palin_selfie();

        // Second example, input = 19362
        palindrome_selfie example2 = new palindrome_selfie(19362);
        example2.palin_selfie();

        // Third example, input = 4669
        palindrome_selfie example3 = new palindrome_selfie(4669);
        example3.palin_selfie();
    }
}

// This code contributed by Rajput-Ji
```

**输出:**

```
Palindrome multiplicative selfie of 145572 is  : 157452
Given number has no palindrome selfie.
Palindrome multiplicative selfie of 4669 is  : 6496
```