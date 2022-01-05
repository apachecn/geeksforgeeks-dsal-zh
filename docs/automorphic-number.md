# 自同构数

> 原文:[https://www.geeksforgeeks.org/automorphic-number/](https://www.geeksforgeeks.org/automorphic-number/)

给定一个数 N，任务是检查这个数是否是自同构数。当且仅当一个数的平方与数本身的位数相同时，这个数称为自同构数。
**例:**

```
Input  : N = 76 
Output : Automorphic
Explanation: As 76*76 = 5776

Input  : N = 25
Output : Automorphic
As 25*25 = 625

Input : N = 7
Output : Not Automorphic
As 7*7 = 49
```

```
1\. Store the square of given number.
2\. Loop until N becomes 0 as we have to match 
   all digits with its square.
    i) Check if (n%10 == sq%10) i.e. last digit 
       of number = last digit of square or not
        a) if not equal, return false.
    ii) Otherwise continue i.e. reduce number and 
        square i.e. n = n/10 and sq = sq/10;
3- Return true if all digits matched.
```

## C++

```
// C++ program to check if a number is Authomorphic
#include <iostream>
using namespace std;

// Function to check Automorphic number
bool isAutomorphic(int N)
{
    // Store the square
    int sq = N * N;

    // Start Comparing digits
    while (N > 0) {
        // Return false, if any digit of N doesn't
        // match with its square's digits from last
        if (N % 10 != sq % 10)
            return false;

        // Reduce N and square
        N /= 10;
        sq /= 10;
    }

    return true;
}

// Driver code
int main()
{
    int N = 5;

    isAutomorphic(N) ? cout << "Automorphic"
                     : cout << "Not Automorphic";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is Authomorphic
class Test {
    // Function to check Automorphic number
    static boolean isAutomorphic(int N)
    {
        // Store the square
        int sq = N * N;

        // Start Comparing digits
        while (N > 0) {
            // Return false, if any digit of N doesn't
            // match with its square's digits from last
            if (N % 10 != sq % 10)
                return false;

            // Reduce N and square
            N /= 10;
            sq /= 10;
        }

        return true;
    }

    // Driver method
    public static void main(String[] args)
    {
        int N = 5;

        System.out.println(isAutomorphic(N) ? "Automorphic" : "Not Automorphic");
    }
}
```

## 计算机编程语言

```
# Python program to check if a number is Authomorphic

# Function to check Automorphic number
def isAutomorphic(N) :

    # Store the square
    sq = N * N

    # Start Comparing digits
    while (N > 0) :

        # Return false, if any digit of N doesn't
        # match with its square's digits from last
        if (N % 10 != sq % 10) :
            return False

        # Reduce N and square
        N /= 10
        sq /= 10

    return True

# Driver code
N = 5
if isAutomorphic(N) :
    print "Automorphic"
else :
    print  "Not Automorphic"

# This Code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check if a
// number is Authomorphic
using System;

class GFG {

    // Function to check Automorphic number
    static bool isAutomorphic(int N)
    {

        // Store the square
        int sq = N * N;

        // Start Comparing digits
        while (N > 0) {
            // Return false, if any digit
            // of N doesn't match with its
            // square's digits from last
            if (N % 10 != sq % 10)
                return false;

            // Reduce N and square
            N /= 10;
            sq /= 10;
        }

        return true;
    }

    // Driver Code
    public static void Main()
    {
        int N = 5;

        Console.Write(isAutomorphic(N) ? "Automorphic" : "Not Automorphic");
    }
}

// This code is Contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is Authomorphic

// Function to check
// Automorphic number
function isAutomorphic($N)
{
    // Store the square
    $sq = $N * $N;

    // Start Comparing digits
    while ($N > 0)
    {
        // Return false, if any 
        // digit of N doesn't
        // match with its square's
        // digits from last
        if ($N % 10 != $sq % 10)
            return -1;

        // Reduce N and square
        $N /= 10;
        $sq /= 10;
    }

    return 1;
}

// Driver code
$N = 5;

$geeks = isAutomorphic($N) ? 
             "Automorphic" : 
          "Not Automorphic";
    echo $geeks;

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to check if
// a number is Authomorphic

// Function to check
// Automorphic number
function isAutomorphic(N)
{
    // Store the square
    let sq = N * N;

    // Start Comparing digits
    while (N > 0)
    {
        // Return false, if any 
        // digit of N doesn't
        // match with its square's
        // digits from last
        if (N % 10 != sq % 10)
            return -1;

        // Reduce N and square
        N /= 10;
        sq /= 10;
    }

    return 1;
}

// Driver code
let N = 5;

let geeks = isAutomorphic(N) ? 
             "Automorphic" : 
          "Not Automorphic";
    document.write(geeks);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
Automorphic
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。