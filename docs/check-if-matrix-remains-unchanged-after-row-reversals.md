# 检查行反转后矩阵是否保持不变

> 原文:[https://www . geesforgeks . org/check-if-matrix-保持不变-行后-反转/](https://www.geeksforgeeks.org/check-if-matrix-remains-unchanged-after-row-reversals/)

给定一个 NxN 矩阵。任务是检查在反转给定矩阵的所有行后，矩阵是否保持不变。

**示例:**

```
Input : N = 3
1 2 1
2 2 2
3 4 3 
Output : Yes 
If all the rows are reversed then matrix will become:
1 2 1
2 2 2
3 4 3 
which is same.

Input : N = 3
1 2 2
2 2 2
3 4 3
Output : No 
```

**接近**:

1.  一个最重要的观察是，行反转后矩阵是相同的，每一行必须回文。
2.  现在检查一行是否是回文，保持两个指针，一个指向开始，另一个指向行尾。开始比较当前值，并开始++和结束–。重复该过程，直到所有元素都被选中，直到行的中间。如果每一步的元素都是相同的，那么该行就是回文，否则就不是。
3.  如果任何一行不是回文，那么答案是否定的

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to check Palindromic Condition
void specialMatrix(int matrix[3][3], int N)
{
    for (int i = 0; i < N; i++) {

        // Pointer to start of row
        int start = 0;

        // Pointer to end of row
        int end = N - 1;

        while (start <= end) {

            // Single Mismatch means row is not palindromic
            if (matrix[i][start] != matrix[i][end]) {
                cout << "No" << endl;
                return;
            }

            start++;
            end--;
        }
    }

    cout << "Yes" << endl;
    return;
}

// Driver Code
int main()
{
    int matrix[3][3] = { { 1, 2, 1 },
                         { 2, 2, 2 },
                         { 3, 4, 3 } };
    int N = 3;
    specialMatrix(matrix, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to check Palindromic Condition
static void specialMatrix(int matrix[][], int N)
{
    for (int i = 0; i < N; i++)
    {

        // Pointer to start of row
        int start = 0;

        // Pointer to end of row
        int end = N - 1;

        while (start <= end)
        {

            // Single Mismatch means
            // row is not palindromic
            if (matrix[i][start] != matrix[i][end])
            {
                System.out.println("No");
                return;
            }

            start++;
            end--;
        }
    }

    System.out.println("Yes");
    return;
}

// Driver Code
public static void main(String[] args)
{
    int matrix[][] = { { 1, 2, 1 },
                        { 2, 2, 2 },
                        { 3, 4, 3 } };
    int N = 3;
    specialMatrix(matrix, N);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to check Palindromic Condition
def specialMatrix(matrix, N):
    for i in range(N):

        # Pointer to start of row
        start = 0

        # Pointer to end of row
        end = N - 1

        while (start <= end):

            # Single Mismatch means row is not palindromic
            if (matrix[i][start] != matrix[i][end]):
                print("No")
                return

            start += 1
            end -= 1

    print("Yes")
    return

# Driver Code
if __name__ == '__main__':
    matrix = [[1, 2, 1], [2, 2, 2], [3, 4, 3]]
    N = 3
    specialMatrix(matrix, N)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to check Palindromic Condition
static void specialMatrix(int [,]matrix, int N)
{
    for (int i = 0; i < N; i++)
    {

        // Pointer to start of row
        int start = 0;

        // Pointer to end of row
        int end = N - 1;

        while (start <= end)
        {

            // Single Mismatch means
            // row is not palindromic
            if (matrix[i, start] != matrix[i, end])
            {
                Console.WriteLine("No");
                return;
            }

            start++;
            end--;
        }
    }
    Console.WriteLine("Yes");
    return;
}

// Driver Code
public static void Main(String[] args)
{
    int [,]matrix = { { 1, 2, 1 },
                        { 2, 2, 2 },
                        { 3, 4, 3 } };
    int N = 3;
    specialMatrix(matrix, N);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to check Palindromic Condition
function specialMatrix($matrix, $N)
{
    for ($i = 0; $i < $N; $i++)
    {

        // Pointer to start of row
        $start = 0;

        // Pointer to end of row
        $end = ($N - 1);

        while ($start <= $end)
        {

            // Single Mismatch means row is not palindromic
            if ($matrix[$i][$start] != $matrix[$i][$end])
            {
                echo "No", "\n";
                return;
            }

            $start++;
            $end--;
        }
    }

    echo "Yes", "\n";
    return;
}

// Driver Code
$matrix = array(array(1, 2, 1),
                array(2, 2, 2),
                array(3, 4, 3));
$N = 3;
specialMatrix($matrix, $N);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to check Palindromic Condition
    function specialMatrix(matrix, N)
    {
        for (let i = 0; i < N; i++)
        {

            // Pointer to start of row
            let start = 0;

            // Pointer to end of row
            let end = N - 1;

            while (start <= end)
            {

                // Single Mismatch means
                // row is not palindromic
                if (matrix[i][start] != matrix[i][end])
                {
                    document.write("No");
                    return;
                }

                start++;
                end--;
            }
        }

        document.write("Yes");
        return;
    }

    let matrix = [ [ 1, 2, 1 ],
                  [ 2, 2, 2 ],
                  [ 3, 4, 3 ] ];
    let N = 3;
    specialMatrix(matrix, N);

</script>
```

**Output:** 

```
Yes
```