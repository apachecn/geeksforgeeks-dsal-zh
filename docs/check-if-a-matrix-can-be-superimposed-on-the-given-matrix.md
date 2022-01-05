# 检查矩阵是否可以叠加在给定的矩阵上

> 原文:[https://www . geeksforgeeks . org/check-if-a-matrix-can-叠加在给定的矩阵上/](https://www.geeksforgeeks.org/check-if-a-matrix-can-be-superimposed-on-the-given-matrix/)

给定一个大小为 **N * M** 的矩阵**字母[][]** ，由**“#”**和**“***组成，另一个大小为 **X * Y** 的矩阵**印章[][]** 只包含**“{ content } ”;**。任务是找出较大的一个的所有**' ***是否可以被 **'{content} '代替；**通过在字母矩阵上叠加印章矩阵。

**注意:**在叠加操作中，只有所有字符都为**“***或**“{ content }”的区域；**可以考虑。

**示例:**

> **输入:** N = 3，M =5，X = 2，Y=2
> 字母矩阵:
> # * * *
> # * * *
> # * * *
> 印章矩阵:
> $
> $
> **输出:**可能的
> **解释:**
> 第一步:将字母矩阵从(0，1)叠加到(1，2)，所以，字母看起来会像(记住“#”放置的地方)也是允许的，做到重叠。因此，从(1，1)到(2，3)
> # $ $
> # $ $
> # $ * *
> 最后一步:再次重叠，从(1，3)到(3，4)
> # $ $
> # $ $
> # $
> 
> **输入:** N = 3，M =5，X = 2，Y=2
> 字母矩阵:
> # * * *
> # * * *
> # * * *
> 印章矩阵:
> $
> $
> **输出:**不可能
> **说明:**在(0，3)处的“#”不能叠加。

**做法:**可以通过检查两个**“#”**之间或一行的末尾和开始处的**“***字符的数量来解决问题。如果这些计数中的任何一个小于印记矩阵的行长度，那么解决方案是不可能的，同样也适用于列。按照以下步骤实施该方法:

*   逐行遍历整个较大的矩阵
*   对于每一行，计算行首或行尾之前或两个 **'#'** 之间的连续**' ***的数量。如果此计数小于戳记矩阵行长度，则不可能，并返回不可能作为答案。
*   用这种方法检查整个字母矩阵。
*   对列也应用相同的过程。
*   如果字母矩阵可以叠加，返回 true。否则，返回 false。

下面是上述方法的实现

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if superimpose
// is possible or not
bool solution(int n, int m, int x, int y,
              vector<string>& letter)
{
  // Looping over rows
  for (int i = 0; i < n; i++) {

    // Initialzing a length variable
    // for counting the number of *
    int len = 0;
    for (int j = 0; j < m; j++) {

      // If character encountered
      // is *, then we
      // incrment the length
      if (letter[i][j] == '*')
        len++;

      // If its not then there are
      // two cases
      else {

        // 1st case is length is
        // smaller than number of
        // rows in stamp matrix,
        // that would be impossible
        // to stamp so return false
        if (len != 0 && len < x)
          return false;

        // 2nd case is if its
        // possible, reset len
        else
          len = 0;
      }
    }
  }

  // Do imilarly for columns
  // Looping over columns
  for (int i = 0; i < m; i++) {

    // Initialzing length variable
    int len = 0;
    for (int j = 0; j < n; j++) {

      // If encountered character
      // is *, increment length
      if (letter[j][i] == '*')
        len++;
      else {

        // If its not possible
        // reutrn false
        if (len != 0 && len < y)
          return false;

        // Otherwise reset len
        else
          len = 0;
      }
    }
  }
  return true;
}

// Driver code
int main()
{
  int n = 3, x = 2, y = 2;

  vector<string> letter = { "#***", "#***", "#***" };
  int m = letter[0].size();
  /*
            Stamp Matrix:
            $
            $
            A 2*2 matrix ( x*y)
            */

  if (solution(n, m, x, y, letter))
    cout << "Possibe\n";
  else
    cout << "Impossible\n";

  // 2nd case
  vector<string> letter2 = { "#***", "#*#*", "#***" };

  m = letter2[0].size();

  if (solution(n, m, x, y, letter2))
    cout << "Possibe\n";
  else
    cout << "Impossible\n";

  return 0;
}

// This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;

class GFG {

    // Function to check if superimpose
    // is possible or not
    public static boolean solution(int n,
                                   int m, int x,
                                   int y,
                                   String[] letter)
    {
        // Looping over rows
        for (int i = 0; i < n; i++) {

            // Initialzing a length variable
            // for counting the number of *
            int len = 0;
            for (int j = 0; j < m; j++) {

                // If character encountered
                // is *, then we
                // incrment the length
                if (letter[i].charAt(j)
                    == '*')
                    len++;

                // If its not then there are
                // two cases
                else {

                    // 1st case is length is
                    // smaller than number of
                    // rows in stamp matrix,
                    // that would be impossible
                    // to stamp so return false
                    if (len != 0 && len < x)
                        return false;

                    // 2nd case is if its
                    // possible, reset len
                    else
                        len = 0;
                }
            }
        }

        // Do imilarly for columns
        // Looping over columns
        for (int i = 0; i < m; i++) {

            // Initialzing length variable
            int len = 0;
            for (int j = 0; j < n; j++) {

                // If encountered character
                // is *, increment length
                if (letter[j].charAt(i)
                    == '*')
                    len++;
                else {

                    // If its not possible
                    // reutrn false
                    if (len != 0 && len < y)
                        return false;

                    // Otherwise reset len
                    else
                        len = 0;
                }
            }
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        int n = 3, x = 2, y = 2;

        String[] letter = { "#***",
                           "#***",
                           "#***" };
        int m = letter[0].length();
        /*
        Stamp Matrix:
        $
        $
        A 2*2 matrix ( x*y)
        */

        if (solution(n, m, x, y, letter))
            System.out.println("Possibe");
        else
            System.out.println("Impossible");

        // 2nd case
        String[] letter2 = { "#***",
                            "#*#*",
                            "#***" };

        m = letter2[0].length();

        if (solution(n, m, x, y, letter2))
            System.out.println("Possibe");
        else
            System.out.println("Impossible");
    }
}
```

## C#

```
// C# code to implement the above approach
using System;

class GFG{

// Function to check if superimpose
// is possible or not
public static bool solution(int n, int m, int x, int y,
                            string[] letter)
{

    // Looping over rows
    for(int i = 0; i < n; i++)
    {

        // Initialzing a length variable
        // for counting the number of *
        int len = 0;
        for(int j = 0; j < m; j++)
        {

            // If character encountered
            // is *, then we
            // incrment the length
            if (letter[i][j] == '*')
                len++;

            // If its not then there are
            // two cases
            else
            {

                // 1st case is length is
                // smaller than number of
                // rows in stamp matrix,
                // that would be impossible
                // to stamp so return false
                if (len != 0 && len < x)
                    return false;

                // 2nd case is if its
                // possible, reset len
                else
                    len = 0;
            }
        }
    }

    // Do imilarly for columns
    // Looping over columns
    for(int i = 0; i < m; i++)
    {

        // Initialzing length variable
        int len = 0;
        for(int j = 0; j < n; j++)
        {

            // If encountered character
            // is *, increment length
            if (letter[j][i] == '*')
                len++;
            else
            {

                // If its not possible
                // reutrn false
                if (len != 0 && len < y)
                    return false;

                // Otherwise reset len
                else
                    len = 0;
            }
        }
    }
    return true;
}

// Driver code
public static void Main(string[] args)
{
    int n = 3, x = 2, y = 2;
    string[] letter = { "#***", "#***", "#***" };
    int m = letter.GetLength(0);

    /*
    Stamp Matrix:
    $
    $
    A 2*2 matrix ( x*y)
    */
    if (solution(n, m, x, y, letter))
        Console.WriteLine("Possibe");
    else
        Console.WriteLine("Impossible");

    // 2nd case
    String[] letter2 = { "#***", "#*#*", "#***" };

    m = letter2.GetLength(0);

    if (solution(n, m, x, y, letter2))
        Console.WriteLine("Possibe");
    else
        Console.WriteLine("Impossible");
}
}

// This code is contributed by ukasp
```

**Output**

```
Possibe
Impossible
```

***时间复杂度:*** O(N*M)
***辅助空间:*** O(1)