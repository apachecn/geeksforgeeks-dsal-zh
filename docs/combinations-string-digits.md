# 一串数字的组合

> 原文:[https://www.geeksforgeeks.org/combinations-string-digits/](https://www.geeksforgeeks.org/combinations-string-digits/)

给定一个数字输入字符串，找出所有可以用相同顺序的数字组成的数字组合。
**例:**

```
Input : 123 
Output :1 2 3
        1 23
        12 3
        123

Input : 1234
Output : 1 2 3 4 
        1 2 34 
        1 23 4 
        1 234 
        12 3 4 
        12 34 
        123 4 
        1234 
```

这个问题可以用递归来解决。我们跟踪给定输入字符串中的当前索引和到目前为止输出字符串的长度。在对函数的每次调用中，如果输入字符串中没有剩余的数字，则打印当前输出字符串并返回。否则，复制当前数字输出。从这里进行两次调用，一次将下一个数字视为下一个数字的一部分(包括输出字符串中的空格)，另一次将下一个数字视为当前数字的一部分(不包括空格)。如果当前数字后没有剩余的数字，则省略对函数的第二次调用，因为尾随空格不算新组合。

## C++

```
// CPP program to find all combination of numbers
// from a given string of digits
#include <iostream>
#include <cstring>
using namespace std;

// function to print combinations of numbers
// in given input string
void printCombinations(char* input, int index,
                     char* output, int outLength)
{
    // no more digits left in input string
    if (input[index] == '\0')
    {
        // print output string & return
        output[outLength] = '\0';
        cout << output << endl;
        return;
    }

    // place current digit in input string
    output[outLength] = input[index];

    // separate next digit with a space
    output[outLength + 1] = ' ';

    printCombinations(input, index + 1, output,
                                   outLength + 2);

    // if next digit exists make a
    // call without including space
    if(input[index + 1] != '\0')
    printCombinations(input, index + 1, output,
                                    outLength + 1);

}

// driver function to test above function
int main()
{
    char input[] = "1214";
    char *output = new char[100];

    // initialize output with empty string
    output[0] = '\0';

    printCombinations(input, 0, output, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all combinations
// of numbers from a given string of digits
class GFG
{

// function to print combinations of numbers
// in given input string
static void printCombinations(char[] input,
                              int index,
                              char[] output,
                              int outLength)
{
    // no more digits left in input string
    if (input.length == index)
    {
        // print output string & return
        System.out.println(String.valueOf(output));
        return;
    }

    // place current digit in input string
    output[outLength] = input[index];

    // separate next digit with a space
    output[outLength + 1] = ' ';

    printCombinations(input, index + 1, output,
                                outLength + 2);

    // if next digit exists make a
    // call without including space
    if(input.length!=index + 1)
    printCombinations(input, index + 1, output,
                                outLength + 1);
}

// Driver Code
public static void main(String[] args)
{
    char input[] = "1214".toCharArray();
    char []output = new char[100];

    printCombinations(input, 0, output, 0);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find all combination of numbers
# from a given string of digits

# function to print combinations of numbers
# in given input string
def printCombinations(input, index, output, outLength):

    # no more digits left in input string
    if (len(input) == index):

        # print output string & return
        output[outLength] = '\0'
        print(*output[:outLength], sep = "")
        return

    # place current digit in input string
    output[outLength] = input[index]

    # separate next digit with a space
    output[outLength + 1] = ' '
    printCombinations(input, index + 1,
                       output, outLength + 2)

    # if next digit exists make a
    # call without including space
    if(len(input) != (index + 1)):
        printCombinations(input, index + 1,
                          output, outLength + 1)

# Driver code
input = "1214"
output = [0]*100

# initialize output with empty string
output[0] = '\0'

printCombinations(input, 0, output, 0)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find all combinations
// of numbers from a given string of digits
using System;

class GFG
{

// function to print combinations of numbers
// in given input string
static void printCombinations(char[] input,
                              int index,
                              char[] output,
                              int outLength)
{
    // no more digits left in input string
    if (input.Length == index)
    {
        // print output string & return
        Console.WriteLine(String.Join("",
                                output));
        return;
    }

    // place current digit in input string
    output[outLength] = input[index];

    // separate next digit with a space
    output[outLength + 1] = ' ';

    printCombinations(input, index + 1, output,
                                outLength + 2);

    // if next digit exists make a
    // call without including space
    if(input.Length!=index + 1)
    printCombinations(input, index + 1, output,
                                outLength + 1);
}

// Driver Code
public static void Main(String[] args)
{
    char []input = "1214".ToCharArray();
    char []output = new char[100];

    printCombinations(input, 0, output, 0);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find all combinations
// of numbers from a given string of digits

    // function to print combinations of numbers
// in given input string
    function printCombinations(input,index,output,outLength)
    {

        // no more digits left in input string
    if (input.length == index)
    {

        // print output string & return
        document.write(output.join("")+"<br>");
        return;
    }

    // place current digit in input string
    output[outLength] = input[index];

    // separate next digit with a space
    output[outLength + 1] = ' ';

    printCombinations(input, index + 1, output,
                                outLength + 2);

    // if next digit exists make a
    // call without including space
    if(input.length != index + 1)
    printCombinations(input, index + 1, output,
                                outLength + 1);
    }

    // Driver Code
    let input = "1214".split("");
    let output = new Array(100);
    printCombinations(input, 0, output, 0);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
1 2 1 4
1 2 14
1 21 4
1 214
12 1 4
12 14
121 4
1214
```

**备选方案:**

## C++

```
// CPP program to find all combination of
// numbers from a given string of digits
// using bit algorithm used same logic
// as to print power set of string
#include <bits/stdc++.h>
using namespace std;

// function to print combinations of
// numbers in given input string
void printCombinations(char s[]){

    // find length of char array
    int l = strlen(s);

    // we can give space between characters
    // ex. ('1' & '2') or ('2' & '3') or
    // ('3' & '4') or ('3' & '4') or all
    // that`s why here we have maximum
    // space length - 1
    for(int i = 0; i < pow(2, l - 1); i++){
        int k = i, x = 0;

        // first character will be printed
        // as well
        cout << s[x];
        x++;
        for(int j = 0; j < strlen(s) - 1; j++){

            // if bit is set, means provide
            // space
            if(k & 1)
                cout << " ";
            k = k >> 1;
            cout << s[x];

            // always increment index of
            // input string
            x++;
        }
        cout << "\n";
    }
}

// driver code
int main() {

    char input[] = "1214";
    printCombinations(input);

    return 0;
}
// This code is contributed by PRINCE Gupta 2
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all combination of
// numbers from a given string of digits
// using bit algorithm used same logic
// as to print power set of string
import java.util.*;

class GFG
{

// function to print combinations of
// numbers in given input string
static void printCombinations(char s[])
{

    // find length of char array
    int l = s.length;

    // we can give space between characters
    // ex. ('1' & '2') or ('2' & '3') or
    // ('3' & '4') or ('3' & '4') or all
    // that`s why here we have maximum
    // space length - 1
    for(int i = 0;
            i < Math.pow(2, l - 1); i++)
    {
        int k = i, x = 0;

        // first character will be printed
        // as well
        System.out.print(s[x]);
        x++;
        for(int j = 0;
                j < s.length - 1; j++)
        {

            // if bit is set, means provide
            // space
            if(k % 2 == 1)
                System.out.print(" ");
            k = k >> 1;
            System.out.print(s[x]);

            // always increment index of
            // input string
            x++;
        }
        System.out.print("\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    char input[] = "1214".toCharArray();
    printCombinations(input);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to find all
# combination of numbers from
# a given string of digits using
# bit algorithm used same logic
# as to print power set of string

# Function to print combinations of
# numbers in given input string
def printCombinations(s):

    # find length of char array
    l = len(s);

    # we can give space between
    # characters ex. ('1' & '2')
    # or ('2' & '3') or ('3' & '4')
    # or ('3' & '4') or all that`s
    # why here we have maximum
    # space length - 1
    for i in range(pow(2, l - 1)):
        k = i
        x = 0

        # first character will
        # be printed as well
        print(s[x], end = "")
        x += 1

        for j in range(len(s) - 1):

            # if bit is set, means
            # provide space
            if(k & 1):
                print(" ", end = "")
            k = k >> 1
            print(s[x], end = "")

            # always increment index of
            # input string
            x += 1

        print()

# Driver code
if __name__ == "__main__":

    inp = "1214";
    printCombinations(inp);

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find all combination of
// numbers from a given string of digits
// using bit algorithm used same logic
// as to print power set of string
using System;

class GFG
{

// function to print combinations of
// numbers in given input string
static void printCombinations(char []s)
{

    // find length of char array
    int l = s.Length;

    // we can give space between characters
    // ex. ('1' & '2') or ('2' & '3') or
    // ('3' & '4') or ('3' & '4') or all
    // that`s why here we have maximum
    // space length - 1
    for(int i = 0;
            i < Math.Pow(2, l - 1); i++)
    {
        int k = i, x = 0;

        // first character will be printed
        // as well
        Console.Write(s[x]);
        x++;
        for(int j = 0;
                j < s.Length - 1; j++)
        {

            // if bit is set, means provide
            // space
            if(k % 2 == 1)
                Console.Write(" ");
            k = k >> 1;
            Console.Write(s[x]);

            // always increment index of
            // input string
            x++;
        }
        Console.Write("\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    char []input = "1214".ToCharArray();
    printCombinations(input);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find all combination of
// numbers from a given string of digits
// using bit algorithm used same logic
// as to print power set of string

    // function to print combinations of
    // numbers in given input string
    function printCombinations(s)
    {
        // find length of char array
    let l = s.length;

    // we can give space between characters
    // ex. ('1' & '2') or ('2' & '3') or
    // ('3' & '4') or ('3' & '4') or all
    // that`s why here we have maximum
    // space length - 1
    for(let i = 0;
            i < Math.pow(2, l - 1); i++)
    {
        let k = i, x = 0;

        // first character will be printed
        // as well
        document.write(s[x]);
        x++;
        for(let j = 0;
                j < s.length - 1; j++)
        {

            // if bit is set, means provide
            // space
            if(k % 2 == 1)
                document.write(" ");
            k = k >> 1;
            document.write(s[x]);

            // always increment index of
            // input string
            x++;
        }
        document.write("<br>");
    }
    }

    // Driver Code
    let input= "1214".split("");
    printCombinations(input);

    // This code is contributed by rag2127

</script>
```

**输出:**

```
1214
1 214
12 14
1 2 14
121 4
1 21 4
12 1 4
1 2 1 4
```

本文由 [**阿迪提·夏尔马 2**](https://auth.geeksforgeeks.org/profile.php?user=aditi sharma 2&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。