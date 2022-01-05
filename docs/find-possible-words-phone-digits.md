# 从电话号码中打印所有可能的单词

> 原文:[https://www . geesforgeks . org/find-可能的单词-电话-数字/](https://www.geeksforgeeks.org/find-possible-words-phone-digits/)

在 QWERTY 键盘出现之前，文本和数字被放在同一个键上。例如，2 有“ABC”如果我们想写任何以“A”开头的东西，我们需要键入一次键 2。如果我们想输入“B”，按两次键 2，三次键输入“C”。下面是这样一个小键盘的图片。

![Mobile-keypad](img/7e82a5f8eea3ad5277c67de46daa9a8e.png)

**给定一个如图所示的键盘和一个 n 位数，通过按下这些数字列出所有可能的单词。**

**示例:**

```
Input number: 234
Output:
adg adh adi aeg aeh aei afg afh 
afi bdg bdh bdi beg beh bei bfg 
bfh bfi cdg cdh cdi ceg ceh cei 
cfg cfh cfi
Explanation: All possible words which can be 
formed are (Alphabetical order):
adg adh adi aeg aeh aei afg afh 
afi bdg bdh bdi beg beh bei bfg 
bfh bfi cdg cdh cdi ceg ceh cei 
cfg cfh cfi
If 2 is pressed then the alphabet
can be a, b, c, 
Similarly, for 3, it can be 
d, e, f, and for 4 can be g, h, i. 

Input number: 5
Output: j k l
Explanation: All possible words which can be 
formed are (Alphabetical order):
j, k, l, only these three alphabets 
can be written with j, k, l.
```

**方法:**可以观察到每个数字可以代表 3 到 4 个不同的字母(除了 0 和 1)。所以这个想法是形成一个递归函数。然后用可能的字母串来映射数字，即 2 代表“abc”，3 代表“def”等。现在递归函数将尝试所有字母，按字母顺序映射到当前数字，并再次调用下一个数字的递归函数，并将传递当前输出字符串。

**示例:**

```
If the number is 23,

Then for 2, the alphabets are a, b, c
So 3 recursive function will be called 
with output string as a, b, c respectively 
and for 3 there are 3 alphabets d, e, f
So, the output will be ad, ae and af for 
the recursive function with output string.
Similarly, for b and c, the output will be: 
bd, be, bf and cd, ce, cf respectively.
```

**算法:**

1.  用可能的字母串来映射数字，例如 2 代表“abc”，3 代表“def”等。
2.  创建一个递归函数，该函数接受以下参数、输出字符串、数字数组、当前索引和数字数组的长度
3.  如果当前索引等于数字数组的长度，则打印输出字符串。
4.  从地图中提取*数字【current _ index】*处的字符串，该数字为输入数字数组。
5.  运行循环以从头到尾遍历字符串
6.  对于每个索引，再次调用递归函数，输出字符串与字符串的第 I 个字符和 current_index + 1 连接在一起。

**实现:**注意，为了简化代码，输入的数字表示为数组。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible combinations by
// replacing key's digits with characters of the
// corresponding list
void findCombinations(vector<char> keypad[],
                      int input[], string res, int index, int n)
{
    // If processed every digit of key, print result
    if (index == n) {
        cout << res << " ";
        return;
    }

    // Stores current digit
    int digit = input[index];

    // Size of the list corresponding to current digit
    int len = keypad[digit].size();

    // One by one replace the digit with each character in the
    // corresponding list and recur for next digit
    for (int i = 0; i < len; i++) {
        findCombinations(keypad, input, res + keypad[digit][i], index + 1, n);
    }
}

// Driver Code
int main()
{
    // Given mobile keypad
    vector<char> keypad[] =
    {
        {}, {},        // 0 and 1 digit don't have any characters associated
        { 'a', 'b', 'c' },
        { 'd', 'e', 'f' },
        { 'g', 'h', 'i' },
        { 'j', 'k', 'l' },
        { 'm', 'n', 'o' },
        { 'p', 'q', 'r', 's'},
        { 't', 'u', 'v' },
        { 'w', 'x', 'y', 'z'}
    };

    // Given input array
    int input[] = { 2, 3, 4 };

    // Size of the array
    int n = sizeof(input)/sizeof(input[0]);

    // Function call to find all combinations
    findCombinations(keypad, input, string(""), 0, n );

    return 0;
}
```

## C

```
#include <stdio.h>
#include <string.h>

// hashTable[i] stores all characters that correspond to
// digit i in phone
const char hashTable[10][5]
    = { "",    "",    "abc",  "def", "ghi",
        "jkl", "mno", "pqrs", "tuv", "wxyz" };

// A recursive function to print all possible words that can
// be obtained by input number[] of size n.  The output
// words are one by one stored in output[]
void printWordsUtil(int number[], int curr_digit,
                    char output[], int n)
{
    // Base case, if current output word is prepared
    int i;
    if (curr_digit == n) {
        printf("%s ", output);
        return;
    }

    // Try all 3 possible characters for current digir in
    // number[] and recur for remaining digits
    for (i = 0; i < strlen(hashTable[number[curr_digit]]);
         i++) {
        output[curr_digit]
            = hashTable[number[curr_digit]][i];
        printWordsUtil(number, curr_digit + 1, output, n);
        if (number[curr_digit] == 0
            || number[curr_digit] == 1)
            return;
    }
}

// A wrapper over printWordsUtil().  It creates an output
// array and calls printWordsUtil()
void printWords(int number[], int n)
{
    char result[n + 1];
    result[n] = '\0';
    printWordsUtil(number, 0, result, n);
}

// Driver program
int main(void)
{
    int number[] = { 2, 3, 4 };
    int n = sizeof(number) / sizeof(number[0]);
    printWords(number, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;
import java.lang.*;
import java.io.*;
class NumberPadString{

static Character[][] numberToCharMap;

private static List<String> printWords(int[] numbers,
                                       int len,
                                       int numIndex,
                                       String s)
{
  if(len == numIndex)
  {
    return new ArrayList<>(Collections.singleton(s));
  }

  List<String> stringList = new ArrayList<>();

  for(int i = 0;
          i < numberToCharMap[numbers[numIndex]].length; i++)
  {
    String sCopy =
           String.copyValueOf(s.toCharArray());
    sCopy = sCopy.concat(
            numberToCharMap[numbers[numIndex]][i].toString());
    stringList.addAll(printWords(numbers, len,
                                 numIndex + 1,
                                 sCopy));
  }
  return stringList;
}

private static void printWords(int[] numbers)
{
  generateNumberToCharMap();
  List<String> stringList =
       printWords(numbers, numbers.length, 0, "");
  stringList.stream().forEach(System.out :: println);
}

private static void generateNumberToCharMap()
{
  numberToCharMap = new Character[10][5];
  numberToCharMap[0] = new Character[]{'\0'};
  numberToCharMap[1] = new Character[]{'\0'};
  numberToCharMap[2] = new Character[]{'a','b','c'};
  numberToCharMap[3] = new Character[]{'d','e','f'};
  numberToCharMap[4] = new Character[]{'g','h','i'};
  numberToCharMap[5] = new Character[]{'j','k','l'};
  numberToCharMap[6] = new Character[]{'m','n','o'};
  numberToCharMap[7] = new Character[]{'p','q','r','s'};
  numberToCharMap[8] = new Character[]{'t','u','v'};
  numberToCharMap[9] = new Character[]{'w','x','y','z'};
}

// Driver code 
public static void main(String[] args)
{
  int number[] = {2, 3, 4};
  printWords(number);
}
}

// This code is contributed by ankit pachori 1
```

## 蟒蛇 3

```
# hashTable[i] stores all characters
# that correspond to digit i in phone
hashTable = ["", "", "abc", "def", "ghi", "jkl",
             "mno", "pqrs", "tuv", "wxyz"]

# A recursive function to print all
# possible words that can be obtained
# by input number[] of size n. The
# output words are one by one stored
# in output[]

def printWordsUtil(number, curr, output, n):
    if(curr == n):
        print(output)
        return

    # Try all 3 possible characters
    # for current digir in number[]
    # and recur for remaining digits
    for i in range(len(hashTable[number[curr]])):
        output.append(hashTable[number[curr]][i])
        printWordsUtil(number, curr + 1, output, n)
        output.pop()
        if(number[curr] == 0 or number[curr] == 1):
            return

# A wrapper over printWordsUtil().
# It creates an output array and
# calls printWordsUtil()

def printWords(number, n):
    printWordsUtil(number, 0, [], n)

# Driver function
if __name__ == '__main__':
    number = [2, 3, 4]
    n = len(number)
    printWords(number, n)

# This code is contributed by prajmsidc
```

## java 描述语言

```
<script>

// Javascript program to implement the
// above approach
let hashTable = [ "", "", "abc", "def", "ghi", "jkl",
                  "mno", "pqrs", "tuv", "wxyz" ];

// A recursive function to print all possible
// words that can be obtained by input number[]
// of size n. The output words are one by one
// stored in output[]
function printWordsUtil(number, curr, output, n)
{

    // Base case, if current output
    // word is prepared
    if (curr == n)
      {
        document.write(output.join("") + "<br>")
        return;
      }

      // Try all 3 possible characters for current
      // digir in number[] and recur for remaining digits
    for(let i = 0;
            i < hashTable[number[curr]].length;
            i++)
    {
        output.push(hashTable[number[curr]][i]);
        printWordsUtil(number, curr + 1, output, n);

        output.pop();

        if(number[curr] == 0 || number[curr] == 1)
            return
    }
}

// A wrapper over printWordsUtil(). It creates
// an output array and calls printWordsUtil()
function printWords(numbers, n)
{
    printWordsUtil(number, 0, [], n);
}

// Driver code
let number = [ 2, 3, 4 ];
let n = number.length;

printWords(number, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
adg adh adi aeg aeh aei afg afh afi bdg 
bdh bdi beg beh bei bfg bfh bfi cdg cdh 
cdi ceg ceh cei cfg cfh cfi
Process returned 0 (0x0)   execution time : 0.025 s
Press any key to continue.
```

**复杂度分析:**

*   **时间复杂度:** O(4 <sup>n</sup> ，其中 n 为输入数字的位数。
    一个数字的每个数字有 3 或 4 个字母，所以可以说每个数字有 4 个字母作为选项。如果有 n 个数字，那么第一个数字有 4 个选项，第二个数字的每个字母表有 4 个选项，也就是说，每次递归调用 4 个以上的递归(如果它不匹配基本情况)。所以时间复杂度为 O(4 <sup>n</sup> )。
*   **空间复杂度:** O(1)。
    因为不需要额外的空间。

**参考:**
[购买编程面试曝光:从 Flipkart.com 找到下一份工作的秘诀第三版](http://www.flipkart.com/programming-interviews-exposed-secrets-landing-your-next-job-3rd/p/itmdvjwferhug3gh?pid=9788126539116&affid=sandeepgfg)
本文由**吉登德拉·桑加**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息