# 一个句子中每个单词的 ASCII 值之和

> 原文:[https://www . geeksforgeeks . org/sums-of-ascii-每句话中每个单词的值/](https://www.geeksforgeeks.org/sums-of-ascii-values-of-each-word-in-a-sentence/)

给我们一个英语语言的句子(也可以包含数字)，我们需要计算并打印该句子中每个单词的字符的 ASCII 值之和。
**例:**

```
Input :  GeeksforGeeks, a computer science portal for geeks
Output : Sentence representation as sum of ASCII each character in a word:
         1361 97 879 730 658 327 527 
         Total sum -> 4579
Here, [GeeksforGeeks, ] -> 1361, [a] -> 97, [computer] -> 879, [science] -> 730
      [portal] -> 658, [for] -> 327, [geeks] -> 527 

Input : I am a geek
Output : Sum of ASCII values:
         73 206 97 412 
         Total sum -> 788
```

**进场:**

1.  迭代字符串的长度，并继续将字符转换为它们的 [ASCII](https://write.geeksforgeeks.org/geek/python-sort-a-list-according-to-the-length-of-the-elements/)
2.  一直把这些值加起来，直到句子结束。
3.  当我们遇到一个空格字符时，我们存储为该单词计算的总和，并将总和再次设置为零。
4.  稍后，我们打印元素

## C++

```
// C++ implementation for representing
// each word in a sentence as sum of
// ASCII values of each word
#include <iostream>
#include <string>
#include <vector>
using namespace std;

// Function to compute the sum of ASCII values of each
// word separated by a space and return the total sum
// of the ASCII values, excluding the space.
long long int ASCIIWordSum(string str,
                          vector<long long int>& sumArr)
{

    int l = str.length();
    int sum = 0;
    long long int bigSum = 0L;
    for (int i = 0; i < l; i++) {

        // Separate each word by
        // a space and store values
        // corresponding to each word
        if (str[i] == ' ') {

            bigSum += sum;
            sumArr.push_back(sum);
            sum = 0;
        }
        else

            // Implicit type casting
            sum +=  str[i];       
    }

    // Storing the value of last word
    sumArr.push_back(sum);
    bigSum += sum;
    return bigSum;
}
// Driver function
int main()
{
    string str = "GeeksforGeeks a computer science "
                 "portal for Geeks";
    vector<long long int> sumArr;

    // Calling function
    long long int sum = ASCIIWordSum(str, sumArr);

    cout << "Sum of ASCII values:" << std::endl;
    for (auto x : sumArr)
        cout << x << " ";
    cout << endl  << "Total sum -> " << sum;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for representing
// each word in a sentence as sum of
// ASCII values of each word
import java.util.*;
import java.lang.*;

class Rextester {

    // Function to compute the sum of ASCII values of
    // each word separated by a space and return the
    // total sum of the ASCII values, excluding the
    // space.
    static long ASCIIWordSum(String str, long sumArr[])
    {
        int l = str.length();
        int pos = 0;
        long sum = 0;
        long bigSum = 0;
        for (int i = 0; i < l; i++) {

            // Separate each word by
            // a space and store values
            // corresponding to each word
            if (str.charAt(i) == ' ') {

                bigSum += sum;
                sumArr[pos++] = sum;
                sum = 0;
            }
            else

                // Implicit type casting
                sum += str.charAt(i);           
        }

        // Storing the sum of last word
        sumArr[pos] = sum;
        bigSum += sum;
        return bigSum;
    }

    // Driver function
    public static void main(String args[])
    {

        String str = "GeeksforGeeks, a computer science portal for geeks";

        // Counting the number of words in the input sentence
        int ctr = 0;
        for (int i = 0; i < str.length(); i++)
            if (str.charAt(i) == ' ')
                ctr++;

        long sumArr[] = new long[ctr + 1];

        // Calling function
        long sum = ASCIIWordSum(str, sumArr);

        // Printing equivalent sum of the words in the
        // sentence
        System.out.println("Sum of ASCII values:");
        for (int i = 0; i <= ctr; i++)
            System.out.print(sumArr[i] + " ");
        System.out.println();
        System.out.print("Total sum -> " + sum);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation for representing
# each word in a sentence as sum of
# ASCII values of each word

# Function to compute the sum of ASCII
# values of each word separated by a space
# and return the total sum of the ASCII
# values, excluding the space.
def ASCIIWordSum(str, sumArr):

    l = len(str)
    sum = 0
    bigSum = 0
    for i in range(l):

        # Separate each word by a space
        # and store values corresponding
        # to each word
        if (str[i] == ' '):

            bigSum += sum
            sumArr.append(sum)
            sum = 0

        else:

            # Implicit type casting
            sum += ord(str[i])    

    # Storing the value of last word
    sumArr.append(sum)
    bigSum += sum
    return bigSum

# Driver Code
if __name__ == "__main__":

    str = "GeeksforGeeks a computer science portal for Geeks"
    sumArr = []

    # Calling function
    sum = ASCIIWordSum(str, sumArr)

    print("Sum of ASCII values:" )
    for x in sumArr:
        print(x, end = " ")

    print()
    print("Total sum -> ", sum)

# This code is contributed by ita_c
```

## C#

```
// C# program for representing each
// word in a sentence as sum of
// ASCII values of each word
using System;

class GFG {

    // Function to compute the sum of ASCII
    // values of each word separated by a
    // space and return the total sum of
    // the ASCII values, excluding the space.
    static long ASCIIWordSum(String str, long []sumArr)
    {
        int l = str.Length;
        int pos = 0;
        long sum = 0;
        long bigSum = 0;
        for (int i = 0; i < l; i++) {

            // Separate each word by
            // a space and store values
            // corresponding to each word
            if (str[i] == ' ')
            {
                bigSum += sum;
                sumArr[pos++] = sum;
                sum = 0;
            }
            else

                // Implicit type casting
                sum += str[i];        
        }

        // Storing the sum of last word
        sumArr[pos] = sum;
        bigSum += sum;
        return bigSum;
    }

    // Driver function
    public static void Main()
    {
        String str = "GeeksforGeeks, a computer " +
                     "science portal for geeks";

        // Counting the number of words
        // in the input sentence
        int ctr = 0;
        for (int i = 0; i < str.Length; i++)
            if (str[i] == ' ')
                ctr++;

        long []sumArr = new long[ctr + 1];

        // Calling function
        long sum = ASCIIWordSum(str, sumArr);

        // Printing equivalent sum of
        // the words in the sentence
        Console.WriteLine("Sum of ASCII values:");
        for (int i = 0; i <= ctr; i++)
            Console.Write(sumArr[i] + " ");

        Console.WriteLine();
        Console.Write("Total sum -> " + sum);
    }
}

// This code is contributed by nitin mittal
```

## java 描述语言

```
<script>

// Javascript program for representing
// each word in a sentence as sum of
// ASCII values of each word

    // Function to compute the sum of ASCII values of
    // each word separated by a space and return the
    // total sum of the ASCII values, excluding the
    // space.
    function ASCIIWordSum(str,sumArr)
    {
        let l = str.length;
        let pos = 0;
        let sum = 0;
        let bigSum = 0;
        for (let i = 0; i < l; i++) {

            // Separate each word by
            // a space and store values
            // corresponding to each word
            if (str[i] == ' ') {

                bigSum += sum;
                sumArr[pos++] = sum;
                sum = 0;
            }
            else

                // Implicit type casting
                sum += str[i].charCodeAt(0);           
        }

        // Storing the sum of last word
        sumArr[pos] = sum;
        bigSum += sum;
        return bigSum;
    }

    // Driver function

    let str = "GeeksforGeeks, a computer
    science portal for geeks";

        // Counting the number of words
        // in the input sentence
        let ctr = 0;
        for (let i = 0; i < str.length; i++)
            if (str[i] == ' ')
                ctr++;

        let sumArr = new Array(ctr + 1);

        // Calling function
        let sum = ASCIIWordSum(str, sumArr);

        // Printing equivalent sum of the words in the
        // sentence
        document.write("Sum of ASCII values:<br>");
        for (let i = 0; i <= ctr; i++)
             document.write(sumArr[i] + " ");
        document.write("<br>");
        document.write("Total sum -> " + sum);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Sum of ASCII values:
1317 97 879 730 658 327 495 
Total sum -> 4503
```

方法的复杂性是![O(len)  ](img/3fd354b9c86b0c85b24d7645bff3b134.png "Rendered by QuickLaTeX.com")

https://youtu.be/B3dghSG2R

-Y