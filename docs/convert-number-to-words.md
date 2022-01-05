# 将给定数字转换为单词的程序

> 原文:[https://www.geeksforgeeks.org/convert-number-to-words/](https://www.geeksforgeeks.org/convert-number-to-words/)

编写代码将给定的数字转换成单词。例如，如果给定“1234”作为输入，则输出应为“一千二百三十四”。

下面是相同的实现。该代码支持最多 4 位数的数字，即从 0 到 9999 的数字。想法是创建存储输出字符串各个部分的数组。一个数组用于一位数，一个用于 10 到 19 的数字，一个用于 20、30、40、50，..等等，还有一个是 10 的幂。
给定号码分为前两位和后两位，两部分分开打印。

## C

```
/* C program to print a given number in words. The program
handles numbers from 0 to 9999 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* A function that prints given number in words */
void convert_to_words(char* num)
{
    int len = strlen(
        num); // Get number of digits in given number

    /* Base cases */
    if (len == 0) {
        fprintf(stderr, "empty string\n");
        return;
    }
    if (len > 4) {
        fprintf(stderr,
                "Length more than 4 is not supported\n");
        return;
    }

    /* The first string is not used, it is to make
        array indexing simple */
    char* single_digits[]
        = { "zero", "one", "two",   "three", "four",
            "five", "six", "seven", "eight", "nine" };

    /* The first string is not used, it is to make
        array indexing simple */
    char* two_digits[]
        = { "",          "ten",      "eleven",  "twelve",
            "thirteen",  "fourteen", "fifteen", "sixteen",
            "seventeen", "eighteen", "nineteen" };

    /* The first two string are not used, they are to make
        array indexing simple*/
    char* tens_multiple[] = { "",       "",        "twenty",
                              "thirty", "forty",   "fifty",
                              "sixty",  "seventy", "eighty",
                              "ninety" };

    char* tens_power[] = { "hundred", "thousand" };

    /* Used for debugging purpose only */
    printf("\n%s: ", num);

    /* For single digit number */
    if (len == 1) {
        printf("%s\n", single_digits[*num - '0']);
        return;
    }

    /* Iterate while num is not '\0' */
    while (*num != '\0') {

        /* Code path for first 2 digits */
        if (len >= 3) {
            if (*num - '0' != 0) {
                printf("%s ", single_digits[*num - '0']);
                printf("%s ",
                       tens_power[len - 3]); // here len can
                                             // be 3 or 4
            }
            --len;
        }

        /* Code path for last 2 digits */
        else {
            /* Need to explicitly handle 10-19\. Sum of the
            two digits is used as index of "two_digits"
            array of strings */
            if (*num == '1') {
                int sum = *num - '0' + *(num + 1) - '0';
                printf("%s\n", two_digits[sum]);
                return;
            }

            /* Need to explicitly handle 20 */
            else if (*num == '2' && *(num + 1) == '0') {
                printf("twenty\n");
                return;
            }

            /* Rest of the two digit numbers i.e., 21 to 99
             */
            else {
                int i = *num - '0';
                printf("%s ", i ? tens_multiple[i] : "");
                ++num;
                if (*num != '0')
                    printf("%s ",
                           single_digits[*num - '0']);
            }
        }
        ++num;
    }
}

/* Driver program to test above function */
int main(void)
{
    convert_to_words("9923");
    convert_to_words("523");
    convert_to_words("89");
    convert_to_words("8");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print a given number in words. The
// program handles numbers from 0 to 9999

class GFG {
    // A function that prints
    // given number in words
    static void convert_to_words(char[] num)
    {
        // Get number of digits
        // in given number
        int len = num.length;

        // Base cases
        if (len == 0) {
            System.out.println("empty string");
            return;
        }
        if (len > 4) {
            System.out.println(
                "Length more than 4 is not supported");
            return;
        }

        /* The first string is not used, it is to make
            array indexing simple */
        String[] single_digits = new String[] {
            "zero", "one", "two",   "three", "four",
            "five", "six", "seven", "eight", "nine"
        };

        /* The first string is not used, it is to make
            array indexing simple */
        String[] two_digits = new String[] {
            "",          "ten",      "eleven",  "twelve",
            "thirteen",  "fourteen", "fifteen", "sixteen",
            "seventeen", "eighteen", "nineteen"
        };

        /* The first two string are not used, they are to
         * make array indexing simple*/
        String[] tens_multiple = new String[] {
            "",      "",      "twenty",  "thirty", "forty",
            "fifty", "sixty", "seventy", "eighty", "ninety"
        };

        String[] tens_power
            = new String[] { "hundred", "thousand" };

        /* Used for debugging purpose only */
        System.out.print(String.valueOf(num) + ": ");

        /* For single digit number */
        if (len == 1) {
            System.out.println(single_digits[num[0] - '0']);
            return;
        }

        /* Iterate while num
            is not '\0' */
        int x = 0;
        while (x < num.length) {

            /* Code path for first 2 digits */
            if (len >= 3) {
                if (num[x] - '0' != 0) {
                    System.out.print(
                        single_digits[num[x] - '0'] + " ");
                    System.out.print(tens_power[len - 3]
                                     + " ");
                    // here len can be 3 or 4
                }
                --len;
            }

            /* Code path for last 2 digits */
            else {
                /* Need to explicitly handle
                10-19\. Sum of the two digits
                is used as index of "two_digits"
                array of strings */
                if (num[x] - '0' == 1) {
                    int sum
                        = num[x] - '0' + num[x + 1] - '0';
                    System.out.println(two_digits[sum]);
                    return;
                }

                /* Need to explicitly handle 20 */
                else if (num[x] - '0' == 2
                         && num[x + 1] - '0' == 0) {
                    System.out.println("twenty");
                    return;
                }

                /* Rest of the two digit
                numbers i.e., 21 to 99 */
                else {
                    int i = (num[x] - '0');
                    if (i > 0)
                        System.out.print(tens_multiple[i]
                                         + " ");
                    else
                        System.out.print("");
                    ++x;
                    if (num[x] - '0' != 0)
                        System.out.println(
                            single_digits[num[x] - '0']);
                }
            }
            ++x;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        convert_to_words("9923".toCharArray());
        convert_to_words("523".toCharArray());
        convert_to_words("89".toCharArray());
        convert_to_words("8".toCharArray());
    }
}
// This code is contributed
// by Mithun Kumar
```

## 蟒蛇 3

```
# Python program to print a given number in
# words. The program handles numbers
# from 0 to 9999

# A function that prints
# given number in words

def convert_to_words(num):

    # Get number of digits
    # in given number
    l = len(num)

    # Base cases
    if (l == 0):
        print("empty string")
        return

    if (l > 4):
        print("Length more than 4 is not supported")
        return

    # The first string is not used,
    # it is to make array indexing simple
    single_digits = ["zero", "one", "two", "three",
                     "four", "five", "six", "seven",
                     "eight", "nine"]

    # The first string is not used,
    # it is to make array indexing simple
    two_digits = ["", "ten", "eleven", "twelve",
                  "thirteen", "fourteen", "fifteen",
                  "sixteen", "seventeen", "eighteen",
                  "nineteen"]

    # The first two string are not used,
    # they are to make array indexing simple
    tens_multiple = ["", "", "twenty", "thirty", "forty",
                     "fifty", "sixty", "seventy", "eighty",
                     "ninety"]

    tens_power = ["hundred", "thousand"]

    # Used for debugging purpose only
    print(num, ":", end=" ")

    # For single digit number
    if (l == 1):
        print(single_digits[ord(num[0]) - 48])
        return

    # Iterate while num is not '\0'
    x = 0
    while (x < len(num)):

        # Code path for first 2 digits
        if (l >= 3):
            if (ord(num[x]) - 48 != 0):
                print(single_digits[ord(num[x]) - 48],
                      end=" ")
                print(tens_power[l - 3], end=" ")
                # here len can be 3 or 4

            l -= 1

        # Code path for last 2 digits
        else:

            # Need to explicitly handle
            # 10-19\. Sum of the two digits
            # is used as index of "two_digits"
            # array of strings
            if (ord(num[x]) - 48 == 1):
                sum = (ord(num[x]) - 48 +
                       ord(num[x+1]) - 48)
                print(two_digits[sum])
                return

            # Need to explicitly handle 20
            elif (ord(num[x]) - 48 == 2 and
                  ord(num[x + 1]) - 48 == 0):
                print("twenty")
                return

            # Rest of the two digit
            # numbers i.e., 21 to 99
            else:
                i = ord(num[x]) - 48
                if(i > 0):
                    print(tens_multiple[i], end=" ")
                else:
                    print("", end="")
                x += 1
                if(ord(num[x]) - 48 != 0):
                    print(single_digits[ord(num[x]) - 48])
        x += 1

# Driver Code
convert_to_words("9923") # Four Digits
convert_to_words("523") # Three Digits
convert_to_words("89") # Two Digits
convert_to_words("8") # One Digits

# This code is contributed
# by Mithun Kumar
```

## C#

```
// C# program to print a given
// number in words. The program
// handles numbers from 0 to 9999
using System;

class GFG {
    // A function that prints
    // given number in words
    static void convert_to_words(char[] num)
    {
        // Get number of digits
        // in given number
        int len = num.Length;

        // Base cases
        if (len == 0) {
            Console.WriteLine("empty string");
            return;
        }
        if (len > 4) {
            Console.WriteLine("Length more than "
                              + "4 is not supported");
            return;
        }

        /* The first string is not used,
           it is to make array indexing simple */
        string[] single_digits = new string[] {
            "zero", "one", "two",   "three", "four",
            "five", "six", "seven", "eight", "nine"
        };

        /* The first string is not used,
           it is to make array indexing simple */
        string[] two_digits = new string[] {
            "",          "ten",      "eleven",  "twelve",
            "thirteen",  "fourteen", "fifteen", "sixteen",
            "seventeen", "eighteen", "nineteen"
        };

        /* The first two string are not used,
           they are to make array indexing simple*/
        string[] tens_multiple = new string[] {
            "",      "",      "twenty",  "thirty", "forty",
            "fifty", "sixty", "seventy", "eighty", "ninety"
        };

        string[] tens_power
            = new string[] { "hundred", "thousand" };

        /* Used for debugging purpose only */
        Console.Write((new string(num)) + ": ");

        /* For single digit number */
        if (len == 1) {
            Console.WriteLine(single_digits[num[0] - '0']);
            return;
        }

        /* Iterate while num
            is not '\0' */
        int x = 0;
        while (x < num.Length) {

            /* Code path for first 2 digits */
            if (len >= 3) {
                if (num[x] - '0' != 0) {
                    Console.Write(
                        single_digits[num[x] - '0'] + " ");
                    Console.Write(tens_power[len - 3]
                                  + " ");

                    // here len can be 3 or 4
                }
                --len;
            }

            /* Code path for last 2 digits */
            else {
                /* Need to explicitly handle
                10-19\. Sum of the two digits
                is used as index of "two_digits"
                array of strings */
                if (num[x] - '0' == 1) {
                    int sum = num[x] - '0' + num[x + 1] - '0';
                    Console.WriteLine(two_digits[sum]);
                    return;
                }

                /* Need to explicitly handle 20 */
                else if (num[x] - '0' == 2
                         && num[x + 1] - '0' == 0) {
                    Console.WriteLine("twenty");
                    return;
                }

                /* Rest of the two digit
                numbers i.e., 21 to 99 */
                else {
                    int i = (num[x] - '0');
                    if (i > 0)
                        Console.Write(tens_multiple[i]
                                      + " ");
                    else
                        Console.Write("");
                    ++x;
                    if (num[x] - '0' != 0)
                        Console.WriteLine(
                            single_digits[num[x] - '0']);
                }
            }
            ++x;
        }
    }

    // Driver Code
    public static void Main()
    {
        convert_to_words("9923".ToCharArray());
        convert_to_words("523".ToCharArray());
        convert_to_words("89".ToCharArray());
        convert_to_words("8".ToCharArray());
    }
}

// This code is contributed
// by Mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print a given
// number in words. The
// program handles numbers
// from 0 to 9999

// A function that prints
// given number in words
function convert_to_words($num)
{
    // Get number of digits
    // in given number
    $len = strlen($num);

    // Base cases
    if ($len == 0)
    {
        echo "empty string\n";
        return;
    }
    if ($len > 4)
    {
        echo "Length more than 4 " .
               "is not supported\n";
        return;
    }

    /* The first string is not used,
    it is to make array indexing simple */
    $single_digits = array("zero", "one", "two",
                           "three", "four", "five",
                           "six", "seven", "eight",
                                           "nine");

    /* The first string is not used,
    it is to make array indexing simple */
    $two_digits = array("", "ten", "eleven", "twelve",
                        "thirteen", "fourteen", "fifteen",
                        "sixteen", "seventeen", "eighteen",
                                               "nineteen");

    /* The first two string are not used,
    they are to make array indexing simple*/
    $tens_multiple = array("", "", "twenty", "thirty",
                           "forty", "fifty", "sixty",
                           "seventy", "eighty", "ninety");

    $tens_power = array("hundred", "thousand");

    /* Used for debugging purpose only */
    echo $num.": ";

    /* For single digit number */
    if ($len == 1)
    {
        echo $single_digits[$num[0] - '0'] . " \n";
        return;
    }

    /* Iterate while num
        is not '\0' */
    $x = 0;
    while ($x < strlen($num))
    {

        /* Code path for first 2 digits */
        if ($len >= 3)
        {
            if ($num[$x]-'0' != 0)
            {
                echo $single_digits[$num[$x] - '0'] . " ";
                echo $tens_power[$len - 3] . " ";
                // here len can be 3 or 4
            }
            --$len;
        }

        /* Code path for last 2 digits */
        else
        {
            /* Need to explicitly handle
            10-19\. Sum of the two digits
            is used as index of "two_digits"
            array of strings */
            if ($num[$x] - '0' == 1)
            {
                $sum = $num[$x] - '0' +
                       $num[$x] - '0';
                echo $two_digits[$sum] . " \n";
                return;
            }

            /* Need to explicitly handle 20 */
            else if ($num[$x] - '0' == 2 &&
                     $num[$x + 1] - '0' == 0)
            {
                echo "twenty\n";
                return;
            }

            /* Rest of the two digit
            numbers i.e., 21 to 99 */
            else
            {
                $i = $num[$x] - '0';
                if($i > 0)
                echo $tens_multiple[$i] . " ";
                else
                echo "";
                ++$x;
                if ($num[$x] - '0' != 0)
                    echo $single_digits[$num[$x] -
                                     '0'] . " \n";
            }
        }
        ++$x;
    }
}

// Driver Code
convert_to_words("9923");
convert_to_words("523");
convert_to_words("89");
convert_to_words("8");

// This code is contributed
// by Mithun Kumar
?>
```

**输出:**

```
9923: nine thousand nine hundred twenty three
523: five hundred twenty three
89: eighty nine
8989: eight thousand nine hundred eighty nine
```

本文由**纳伦德拉·康拉尔卡尔**整理。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。