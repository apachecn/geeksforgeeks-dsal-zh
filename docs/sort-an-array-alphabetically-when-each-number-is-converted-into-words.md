# 当每个数字转换为单词时，按字母顺序对数组进行排序

> 原文:[https://www . geesforgeks . org/sort-a-array-按字母顺序-当每个数字被转换成单词时/](https://www.geeksforgeeks.org/sort-an-array-alphabetically-when-each-number-is-converted-into-words/)

给定一个包含非负整数 **N** 的数组**arr【】**，任务是当[每个数字转换成单词](https://www.geeksforgeeks.org/convert-number-to-words/)时，按字母顺序对这些整数进行排序。

**示例:**

> **输入:** arr[] = {12，10，102，31，15}
> **输出:** 15 102 10 31 12
> **解释:**
> 以上一组数字按字母顺序排序。即:
> 15 - >十五
> 102 - >一百零二
> 10 - >十
> 31 - >三十一
> 12 - >十二
> 
> **输入:** arr[] = { 1，2，3，4，5，6，7，8，9，10 }
> **输出:** 8 5 4 9 1 7 6 10 3 2
> **解释:**
> 以上一组数字按字母顺序排序。即:
> 8 - >八
> 5 - >五
> 4 - >四
> 9 - >九
> 1 - >一
> 7 - >七
> 6 - >六
> 10 - >十
> 3 - >三
> 2 - >二

**方法:**为了按字母顺序对数字进行排序，我们首先需要将数字转换为其单词形式。因此，想法是将每个元素及其[词形](https://www.geeksforgeeks.org/program-to-convert-a-given-number-to-words-set-2/)存储在一个[向量对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)中，然后根据数字的相应单词对向量的所有元素进行排序。因此:

*   预计算并存储数组中所有单位数字的单词形式。
*   预计算并将所有十位数的单词形式存储在另一个数组中。
*   对于所有剩余的大于 2 位数的数字，数字被除，单词形式被加。
*   迭代数组 arr[]中数字的每个数字，并将数字的相应单词形式作为一对存储在向量中。
*   遍历向量，并根据单词对向量进行排序。
*   最后，打印排序顺序。

下面是上述方法的实现:

## C++

```
// C++ program to sort an array of
// integers alphabetically

#include <bits/stdc++.h>
using namespace std;

// Variable to store the word form of
// units digit and up to twenty
string one[]
    = { "", "one ", "two ", "three ",
        "four ", "five ", "six ",
        "seven ", "eight ", "nine ", "ten ",
        "eleven ", "twelve ", "thirteen ",
        "fourteen ", "fifteen ", "sixteen ",
        "seventeen ", "eighteen ", "nineteen " };

// Variable to store the word form of
// tens digit
string ten[]
    = { "", "", "twenty ",
        "thirty ", "forty ",
        "fifty ", "sixty ",
        "seventy ", "eighty ",
        "ninety " };

// Function to convert a two digit number
// to the word by using the above defined arrays
string numToWords(int n, string s)
{
    string str = "";

    // If n is more than 19, divide it
    if (n > 19)
        str += ten[n / 10] + one[n % 10];
    else
        str += one[n];

    // If n is non-zero
    if (n)
        str += s;

    return str;
}

// Function to print a given number in words
string convertToWords(int n)
{
    // Stores the word representation
    // of the given number n
    string out;

    // Handles digits at ten millions
    // and hundred millions places
    out += numToWords((n / 10000000),
                      "crore ");

    // Handles digits at hundred thousands
    // and one millions places
    out += numToWords(((n / 100000) % 100),
                      "lakh ");

    // Handles digits at thousands and
    // tens thousands places
    out += numToWords(((n / 1000) % 100),
                      "thousand ");

    // Handles digit at hundreds places
    out += numToWords(((n / 100) % 10),
                      "hundred ");

    if (n > 100 && n % 100)
        out += "and ";

    // Call the above function to convert
    // the number into words
    out += numToWords((n % 100), "");

    return out;
}

// Function to sort the array according to
// the albhabetical order
void sortArr(int arr[], int n)
{
    // Vector to store the number in words
    // with respective elements
    vector<pair<string, int> > vp;

    // Inserting number in words
    // with respective elements in vector pair
    for (int i = 0; i < n; i++) {
        vp.push_back(make_pair(
            convertToWords(arr[i]), arr[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the alphabetical order.
    sort(vp.begin(), vp.end());

    // Print the sorted vector content
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second << " ";
}

// Driver code
int main()
{
    int arr[] = { 12, 10, 102, 31, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortArr(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to sort an array of
# integers alphabetically

# Variable to store the word form of
# units digit and up to twenty
one = [ "", "one ", "two ", "three ",
        "four ", "five ", "six ",
        "seven ", "eight ", "nine ", "ten ",
        "eleven ", "twelve ", "thirteen ",
        "fourteen ", "fifteen ", "sixteen ",
        "seventeen ", "eighteen ", "nineteen " ]

# Variable to store the word form of
# tens digit
ten = [ "", "", "twenty ",
        "thirty ", "forty ",
        "fifty ", "sixty ",
        "seventy ", "eighty ",
        "ninety " ]

# Function to convert a two digit number
# to the word by using the above defined arrays
def numToWords(n, s):

    st = ""

    # If n is more than 19, divide it
    if (n > 19):
        st += ten[n // 10] + one[n % 10]
    else:
        st += one[n]

    # If n is non-zero
    if (n):
        st += s

    return st

# Function to print a given number in words
def convertToWords(n):

    # Stores the word representation
    # of the given number n
    out = ""

    # Handles digits at ten millions
    # and hundred millions places
    out += numToWords((n // 10000000),
                      "crore ")

    # Handles digits at hundred thousands
    # and one millions places
    out += numToWords(((n // 100000) % 100),
                      "lakh ")

    # Handles digits at thousands and
    # tens thousands places
    out += numToWords(((n // 1000) % 100),
                      "thousand ")

    # Handles digit at hundreds places
    out += numToWords(((n // 100) % 10),
                      "hundred ")

    if (n > 100 and n % 100):
        out += "and "

    # Call the above function to convert
    # the number into words
    out += numToWords((n % 100), "")

    return out

# Function to sort the array according to
# the albhabetical order
def sortArr(arr, n):

    # Vector to store the number in words
    # with respective elements
    vp = []

    # Inserting number in words
    # with respective elements in vector pair
    for i in range(n):
        vp.append((convertToWords(arr[i]),
                                  arr[i]));

    # Sort the vector, this will sort the pair
    # according to the alphabetical order.
    vp.sort()

    # Print the sorted vector content
    for i in range(len(vp)):
        print (vp[i][1], end = " ")

# Driver code
if __name__ == "__main__":

    arr = [ 12, 10, 102, 31, 15 ]
    n = len(arr)

    sortArr(arr, n)

# This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Variable to store the word form of
// units digit and up to twenty
var one
    = [ "", "one ", "two ", "three ",
        "four ", "five ", "six ",
        "seven ", "eight ", "nine ", "ten ",
        "eleven ", "twelve ", "thirteen ",
        "fourteen ", "fifteen ", "sixteen ",
        "seventeen ", "eighteen ", "nineteen " ];

// Variable to store the word form of
// tens digit
var ten
    = ["", "", "twenty ",
        "thirty ", "forty ",
        "fifty ", "sixty ",
        "seventy ", "eighty ",
        "ninety " ];

// Function to convert a two digit number
// to the word by using the above defined arrays
function numToWords(n, s)
{
    var str = "";

    // If n is more than 19, divide it
    if (n > 19)
        str += ten[Math.floor(n / 10)] + one[n % 10];
    else
        str += one[n];

    // If n is non-zero
    if (n)
        str += s;

    return str;
}

// Function to print a given number in words
function convertToWords(n)
{
    // Stores the word representation
    // of the given number n
    var out;

    // Handles digits at ten millions
    // and hundred millions places
    out += numToWords(Math.floor(n / 10000000),
                      "crore ");

    // Handles digits at hundred thousands
    // and one millions places
    out += numToWords((Math.floor(n / 100000) % 100),
                      "lakh ");

    // Handles digits at thousands and
    // tens thousands places
    out += numToWords((Math.floor(n / 1000) % 100),
                      "thousand ");

    // Handles digit at hundreds places
    out += numToWords((Math.floor(n / 100) % 10),
                      "hundred ");

    if (n > 100 && n % 100)
        out += "and ";

    // Call the above function to convert
    // the number into words
    out += numToWords((n % 100), "");

    return out;
}

// Function to sort the array according to
// the albhabetical order
function sortArr(arr, n)
{
    // Vector to store the number in words
    // with respective elements
    var vp = new Array(n);

    // Inserting number in words
    // with respective elements in vector pair
    for (var i = 0; i < n; i++) {
        vp[i] = [convertToWords(arr[i]), arr[i]];
    }

    // Sort the vector, this will sort the pair
    // according to the alphabetical order.
    vp.sort();

    // Print the sorted vector content
    for (var i = 0; i < n; i++)
        document.write(vp[i][1]+" ");
}

// Driver Code
var arr = [ 12, 10, 102, 31, 15 ];
var n = arr.length;

sortArr(arr, n);

</script>
```

**Output:** 

```
15 102 10 31 12
```

**时间复杂度:** *O(N * log(N))* ，其中 N 为数组的大小

**辅助空间:**T2【O(N)T4】