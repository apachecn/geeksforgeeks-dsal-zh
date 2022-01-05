# 生成 N 个随机十六进制数

> 原文:[https://www . geesforgeks . org/generate-n-random-十六进制-numbers/](https://www.geeksforgeeks.org/generate-n-random-hexadecimal-numbers/)

给定一个正整数 **N** ，任务是生成 **N** 随机的[十六进制整数](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)。

**示例:**

> **输入:**N = 3
> T3】输出:T5】f9ad0d 9
> e19b 24 CD 01
> A5E

**方法:**借助用于生成随机整数的[兰德()函数](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)可以解决给定的问题。可以创建字符[数组](https://www.geeksforgeeks.org/array-data-structure/)，该数组将所有可能的字符存储在[十六进制符号](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)中，并从该数组中随机选择字符。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Maximum length of the random integer
const int maxSize = 10;

// Function to generate N Hexadecimal
// integers
void randomHexInt(int N)
{
    srand(time(0));

    // Stores all the possible characters
    // in the Hexadecimal notation
    char hexChar[]
        = { '0', '1', '2', '3', '4', '5',
            '6', '7', '8', '9', 'A', 'B',
            'C', 'D', 'E', 'F' };

    // Loop to print N integers
    for (int i = 0; i < N; i++) {

        // Randomly select length of the
        // int in the range [1, maxSize]
        int len = rand() % maxSize + 1;

        // Print len characters
        for (int j = 0; j < len; j++) {

            // Print a randomly selected
            // character
            cout << hexChar[rand() % 16];
        }
        cout << '\n';
    }
}

// Driver Code
int main()
{
    int N = 3;
    randomHexInt(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Maximum length of the random integer
static int maxSize = 10;

// Function to generate N Hexadecimal
// integers
static void randomHexInt(int N)
{

    // Stores all the possible characters
    // in the Hexadecimal notation
    char hexChar[]
        = { '0', '1', '2', '3', '4', '5',
            '6', '7', '8', '9', 'A', 'B',
            'C', 'D', 'E', 'F' };

    // Loop to print N integers
    for (int i = 0; i < N; i++) {

        // Randomly select length of the
        // int in the range [1, maxSize]
        int len = (1 + (int)(Math.random() * 100)) % maxSize + 1;

        // Print len characters
        for (int j = 0; j < len; j++) {

            // Print a randomly selected
            // character
            System.out.print(hexChar[(1 + (int)(Math.random() * 100)) % 16]);
        }
        System.out.println();
    }
}

// Driver Code
public static void main (String[] args)
{
    int N = 3;
    randomHexInt(N);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import random,math

# Maximum length of the random integer
maxSize = 10;

# Function to generate N Hexadecimal
# integers
def randomHexInt(N) :

    # Stores all the possible characters
    # in the Hexadecimal notation
    hexChar = [ '0', '1', '2', '3', '4', '5',
            '6', '7', '8', '9', 'A', 'B',
            'C', 'D', 'E', 'F'];

    # Loop to print N integers
    for i in range(N) :

        # Randomly select length of the
        # int in the range [1, maxSize]
        Len = math.floor(random.random() * (maxSize - 1) + 1)

        # Print len characters
        for j in range(Len) :

            # Print a randomly selected
            # character
            print(hexChar[math.floor(random.random() * 16)],end = "");

        print();

# Driver Code
if __name__ == "__main__" :

    N = 3;
    randomHexInt(N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG {

// Maximum length of the random integer
static int maxSize = 10;

// Function to generate N Hexadecimal
// integers
static void randomHexInt(int N)
{

    // Stores all the possible characters
    // in the Hexadecimal notation
    char[] hexChar
        = { '0', '1', '2', '3', '4', '5',
            '6', '7', '8', '9', 'A', 'B',
            'C', 'D', 'E', 'F' };

    // For random generator
    Random rand = new Random();

    // Loop to print N integers
    for (int i = 0; i < N; i++) {

        // Randomly select length of the
        // int in the range [1, maxSize]
        int len = rand.Next() % maxSize + 1;

        // Print len characters
        for (int j = 0; j < len; j++) {

            // Print a randomly selected
            // character
            Console.Write(hexChar[rand.Next() % 16]);
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main (string[] args) {

    int N = 3;
    randomHexInt(N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Maximum length of the random integer
        const maxSize = 10;

        // Function to generate N Hexadecimal
        // integers
        function randomHexInt(N) {

            // Stores all the possible characters
            // in the Hexadecimal notation
            let hexChar
                = ['0', '1', '2', '3', '4', '5',
                    '6', '7', '8', '9', 'A', 'B',
                    'C', 'D', 'E', 'F'];

            // Loop to print N integers
            for (let i = 0; i < N; i++) {

                // Randomly select length of the
                // int in the range [1, maxSize]
                let len = Math.random() * (maxSize - 1) + 1;

                // Print len characters
                for (let j = 0; j < len; j++) {

                    // Print a randomly selected
                    // character
                    document.write(hexChar[Math.floor(Math.random() * (16))]);
                }
                document.write("<br>")
            }
        }

        // Driver Code
        let N = 3;
        randomHexInt(N);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
B71C3
EC3BBC90
82410C0D
```

***时间复杂度:** O(N*M)，其中 M 代表随机字符串的最大长度。*
***辅助空间:** O(1)*