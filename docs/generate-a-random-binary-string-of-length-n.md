# 生成长度为 N 的随机二进制字符串

> 原文:[https://www . geesforgeks . org/generate-a-random-binary-string-of-length-n/](https://www.geeksforgeeks.org/generate-a-random-binary-string-of-length-n/)

给定一个正整数 **N** ，任务是生成一个长度为 **N** 的随机[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)。

**示例:**

> **输入:**N = 7
> T3】输出: 1000001
> 
> **输入:**N = 5
> T3】输出: 01001

**方法:**给定的问题可以通过使用 [rand()函数](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)来解决，该函数在范围**【0，**[**RAND _ MAX**](https://www.geeksforgeeks.org/generating-random-number-range-c/)**】**内生成随机数，借助该函数返回的值，可以将任意范围**【L，R】**内的任意数生成为**(RAND()%(R–L+1))+L**。按照以下步骤解决问题:

*   初始化一个空的[字符串](https://www.geeksforgeeks.org/string-data-structure/)，比如 **S** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**并执行以下步骤:
    *   使用[兰德()功能](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)在【0，1】范围内存储一个[随机数。](https://www.geeksforgeeks.org/generating-random-number-range-c/)
    *   将随机生成的 **0** 或 **1** 追加到字符串 **S** 的末尾。
*   完成上述步骤后，[将字符串](https://www.geeksforgeeks.org/puts-vs-printf-for-printing-a-string/) **S** 打印为生成的二进制字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find a random
// number between 0 or 1
int findRandom()
{
    // Generate the random number
    int num = ((int)rand() % 2);

    // Return the generated number
    return num;
}

// Function to generate a random
// binary string of length N
void generateBinaryString(int N)
{
    srand(time(NULL));

    // Stores the empty string
    string S = "";

    // Iterate over the range [0, N - 1]
    for (int i = 0; i < N; i++) {

        // Store the random number
        int x = findRandom();

        // Append it to the string
        S += to_string(x);
    }

    // Print the resulting string
    cout << S;
}

// Driver Code
int main()
{
    int N = 7;
    generateBinaryString(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find a random
// number between 0 or 1
static int findRandom()
{

    // Generate the random number
    int num = (1 + (int)(Math.random() * 100)) % 2;

    // Return the generated number
    return num;
}

// Function to generate a random
// binary string of length N
static void generateBinaryString(int N)
{

    // Stores the empty string
    String S = "";

    // Iterate over the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Store the random number
        int x = findRandom();

        // Append it to the string
        S = S + String.valueOf(x);
    }

    // Print the resulting string
    System.out.println(S);
}

// Driver Code
public static void main (String[] args)
{
    int N = 7;

    generateBinaryString(N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach
import random

# Function to find a random
# number between 0 or 1
def findRandom():

    # Generate the random number
    num = random.randint(0, 1)

    # Return the generated number
    return num

# Function to generate a random
# binary string of length N
def generateBinaryString(N):

    # Stores the empty string
    S = ""

    # Iterate over the range [0, N - 1]
    for i in range(N):

        # Store the random number
        x = findRandom()

        # Append it to the string
        S += str(x)

    # Print the resulting string
    print(S)

# Driver Code
N = 7

generateBinaryString(N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG {

// Function to find a random
// number between 0 or 1
static int findRandom()
{

    // For random generator
    Random rand = new Random();

    // Generate the random number
    int num =  rand.Next() % 2;

    // Return the generated number
    return num;
}

// Function to generate a random
// binary string of length N
static void generateBinaryString(int N)
{

    // Stores the empty string
    string S = "";

    // Iterate over the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Store the random number
        int x = findRandom();

        // Append it to the string
        S = S + x.ToString();
    }

    // Print the resulting string
    Console.WriteLine(S);
}

// Driver Code
public static void Main (string[] args)
{

    int N = 7;
    generateBinaryString(N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

     // Javascript program for the above approach

     // Function to find a random
     // number between 0 or 1
     function findRandom() {
         // Generate the random number
         let num =
         (1 + parseInt((Math.random() * 100))) % 2;

         // Return the generated number
         return num;
     }

     // Function to generate a random
     // binary string of length N
     function generateBinaryString(N) {

         // Stores the empty string
         let S = "";

         // Iterate over the range [0, N - 1]
         for (let i = 0; i < N; i++) {

             // Store the random number
             let x = findRandom();

             // Append it to the string
             S += (x).toString();
         }

         // Print the resulting string
         document.write(S)
     }

     // Driver Code
     let N = 7;
     generateBinaryString(N);

     // This code is contributed by Hritik

 </script>
```

**Output:** 

```
0101101
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)