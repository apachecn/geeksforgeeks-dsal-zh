# 递归打印所有可以从词表列表中形成的句子

> 原文:[https://www . geeksforgeeks . org/递归打印所有可以从单词列表中形成的句子/](https://www.geeksforgeeks.org/recursively-print-all-sentences-that-can-be-formed-from-list-of-word-lists/)

给定一个单词列表如何通过递归一次从列表中取出一个单词来打印所有可能的句子？
**例:**

```
Input: {{"you", "we"},
        {"have", "are"},
        {"sleep", "eat", "drink"}}

Output:
  you have sleep
  you have eat
  you have drink
  you are sleep
  you are eat
  you are drink
  we have sleep
  we have eat
  we have drink
  we are sleep
  we are eat
  we are drink 

```

**我们强烈建议尽量减少你的浏览器，先自己试试这个。**
这个想法基于一个简单的深度优先遍历。我们从第一个列表中的每个单词开始，作为输出句子的第一个单词，然后对其余列表重复。
下面是上述思路的 C++实现。在下面的实现中，列表的输入列表被视为 2D 数组。如果我们仔细观察，可以观察到代码非常接近图的 [DFS。](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 

## C++

```
// C++ program to print all possible sentences from a list of word list
#include <iostream>
#include <string>

#define R 3
#define C 3
using namespace std;

// A recursive function to print all possible sentences that can be formed
// from a list of word list
void printUtil(string arr[R][C], int m, int n, string output[R])
{
    // Add current word to output array
    output[m] = arr[m][n];

    // If this is last word of current output sentence, then print
    // the output sentence
    if (m==R-1)
    {
        for (int i=0; i<R; i++)
           cout << output[i] << " ";
        cout << endl;
        return;
    }

    // Recur for next row
    for (int i=0; i<C; i++)
       if (arr[m+1][i] != "")
          printUtil(arr, m+1, i, output);
}

// A wrapper over printUtil()
void print(string arr[R][C])
{
   // Create an array to store sentence
   string output[R];

   // Consider all words for first row as starting points and
   // print all sentences
   for (int i=0; i<C; i++)
     if (arr[0][i] != "")
        printUtil(arr, 0, i, output);
}

// Driver program to test above functions
int main()
{
   string arr[R][C]  = {{"you", "we"},
                        {"have", "are"},
                        {"sleep", "eat", "drink"}};

   print(arr);

   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// all possible sentences
// from a list of word list
class GFG{

static final int R= 3;
static final int C =3;

// A recursive function to
// print all possible sentences
// that can be formed 
// from a list of word list
static void printUtil(String [][]arr,
                      int m, int n,
                      String []output)
{
  // Add current word to output array
  output[m] = arr[m][n];

  // If this is last word of
  // current output sentence,
  // then print the output sentence
  if (m == R - 1)
  {
    for (int i = 0; i < R; i++)
      System.out.print(output[i] + " ");
    System.out.println();
    return;
  }

  // Recur for next row
  for (int i = 0; i < C; i++)
    if (arr[m + 1][i] != "" && m < C)
      printUtil(arr, m + 1, i, output);
}

// A wrapper over printUtil()
static void print(String [][]arr)
{
  // Create an array to store sentence
  String []output = new String[R];

  // Consider all words for first
  // row as starting points and
  // print all sentences
  for (int i = 0; i < C; i++)
    if (arr[0][i] != "")
      printUtil(arr, 0, i, output);
}

// Driver program to test above functions
public static void main(String[] args)
{
  String [][]arr  = {{"you", "we", ""},
                     {"have", "are", ""},
                     {"sleep", "eat", "drink"}};
  print(arr);
}
}

// This code is contributed by gauravrajput1
```

## 计算机编程语言

```
# Python program recursively print all sentences that can be
# formed from list of word lists
R = 3
C = 3

# A recursive function to print all possible sentences that can
# be formed from a list of word list
def printUtil(arr, m, n, output):

    # Add current word to output array
    output[m] = arr[m][n]

    # If this is last word of current output sentence, then print
    # the output sentence
    if m==R-1:
        for i in xrange(R):
            print output[i] + " ",
        print "\n",
        return

    # Recur for next row
    for i in xrange(C):
        if arr[m+1][i] != "":
            printUtil(arr, m+1, i, output)

# A wrapper over printUtil
def printf(arr):

    # Create an array to store sentence
    output = [""] * R

    # Consider all words for first row as starting
    #  points and print all sentences
    for i in xrange(C):
        if arr[0][i] != "":
            printUtil(arr, 0, i, output)

# Driver program
arr = [ ["you", "we",""],
        ["have", "are",""],
        ["sleep", "eat", "drink"]]
printf(arr)
# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to print
// all possible sentences
// from a list of word list
using System;
class GFG{

static readonly int R= 3;
static readonly int C =3;

// A recursive function to
// print all possible sentences
// that can be formed 
// from a list of word list
static void printUtil(String [,]arr,
                      int m, int n,
                      String []output)
{
  // Add current word to output array
  output[m] = arr[m, n];

  // If this is last word of
  // current output sentence,
  // then print the output sentence
  if (m == R - 1)
  {
    for (int i = 0; i < R; i++)
      Console.Write(output[i] + " ");
    Console.WriteLine();
    return;
  }

  // Recur for next row
  for (int i = 0; i < C; i++)
    if (arr[m + 1, i] != "" && m < C)
      printUtil(arr, m + 1, i, output);
}

// A wrapper over printUtil()
static void print(String [,]arr)
{
  // Create an array to store sentence
  String []output = new String[R];

  // Consider all words for first
  // row as starting points and
  // print all sentences
  for (int i = 0; i < C; i++)
    if (arr[0, i] != "")
      printUtil(arr, 0, i, output);
}

// Driver program to test above functions
public static void Main(String[] args)
{
  String [,]arr  = {{"you", "we", ""},
                    {"have", "are", ""},
                    {"sleep", "eat", "drink"}};
  print(arr);
}
}

// This code is contributed by gauravrajput1
```

输出:

```
  you have sleep
  you have eat
  you have drink
  you are sleep
  you are eat
  you are drink
  we have sleep
  we have eat
  we have drink
  we are sleep
  we are eat
  we are drink 

```

本文由 **Kartik** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息