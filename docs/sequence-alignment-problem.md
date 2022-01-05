# 序列比对问题

> 原文:[https://www.geeksforgeeks.org/sequence-alignment-problem/](https://www.geeksforgeeks.org/sequence-alignment-problem/)

给定两个字符串作为输入，![X    ](img/e52a0e452a04eee6d56d40d1071d6de0.png "Rendered by QuickLaTeX.com") = ![x_{1} x_{2}... x_{m}    ](img/d296efe51893c6f93eef44c30eb792d9.png "Rendered by QuickLaTeX.com")，![Y    ](img/0c449a840200698bed1d645f019c0afe.png "Rendered by QuickLaTeX.com") = ![y_{1} y_{2}... y_{m}    ](img/71fc32de16e297e6e886a4ca43c46d03.png "Rendered by QuickLaTeX.com")，逐个字符地输出字符串的对齐方式，这样净惩罚为**最小化**。违约金计算为:
1。如果在绳子之间插入一个间隙，将受到![p_{gap}    ](img/bfcbac7ad83512ef489307de2d4bc7d0.png "Rendered by QuickLaTeX.com")的惩罚。
2。误匹配![X    ](img/e52a0e452a04eee6d56d40d1071d6de0.png "Rendered by QuickLaTeX.com")和![Y    ](img/0c449a840200698bed1d645f019c0afe.png "Rendered by QuickLaTeX.com")字符将被罚款![p_{xy}    ](img/0f818f28a9d23ca73ba44afbd62cc850.png "Rendered by QuickLaTeX.com")。

**示例:**

```
Input : X = CG, Y = CA, p_gap = 3, p_xy = 7
Output : X = CG_, Y = C_A, Total penalty = 6

Input : X = AGGGCT, Y = AGGCA, p_gap = 3, p_xy = 2
Output : X = AGGGCT, Y = A_GGCA, Total penalty = 5

Input : X = CG, Y = CA, p_gap = 3, p_xy = 5
Output : X = CG, Y = CA, Total penalty = 5
```

**问题历史简述**
序列比对问题是生物科学的基本问题之一，旨在寻找两个氨基酸序列的相似性。比较氨基酸对人类来说至关重要，因为它提供了进化和发展的重要信息。索尔·尼德曼和克里斯蒂安·温施设计了一个解决这个问题的动态规划算法，并于 1970 年发表。从那以后，为了提高时间复杂度和空间复杂度，已经做了许多改进，但是这些都超出了本文的讨论范围。

**解**我们可以用动态规划来解决这个问题。可行的解决方案是在琴弦中引入间隙，从而使长度相等。因为可以容易地证明，在均衡长度之后增加额外的间隙只会导致罚分的增加。

**最优子结构**
从最优解可以观察到，例如从给定的样本输入，最优解缩小到只有**三个**候选。
1。![x_{m}    ](img/dbb54de967acc637110ad3c72e27e397.png "Rendered by QuickLaTeX.com")和![y_{n}    ](img/0dfb3405a2eea036145ac88fd1e34732.png "Rendered by QuickLaTeX.com")。
2。![x_{m}    ](img/dbb54de967acc637110ad3c72e27e397.png "Rendered by QuickLaTeX.com")还有差距。
3。间隙和![y_{n}    ](img/0dfb3405a2eea036145ac88fd1e34732.png "Rendered by QuickLaTeX.com")。
最优子结构的证明。
我们很容易通过矛盾来证明。让![X - x_{m}    ](img/73086de99a9a1a6675aa24dab4ac75d4.png "Rendered by QuickLaTeX.com")成为![X^'    ](img/250269cba8660d91f3eb64035b0970c4.png "Rendered by QuickLaTeX.com")，![Y - y_{n}    ](img/8e876746c44c0bde1c3e2c9b7b5aa0ec.png "Rendered by QuickLaTeX.com")成为![Y^'    ](img/a2ace93fa07585e13df5adc9a6d483dc.png "Rendered by QuickLaTeX.com")。假设![X^'    ](img/250269cba8660d91f3eb64035b0970c4.png "Rendered by QuickLaTeX.com")、![Y^'    ](img/a2ace93fa07585e13df5adc9a6d483dc.png "Rendered by QuickLaTeX.com")的诱导对位有一些处罚![P    ](img/f4b9d7fc8f46f0884bcac106001eeed9.png "Rendered by QuickLaTeX.com")，一个竞争对手对位有处罚![P^*    ](img/1d1af4a1fc20e15a564c42d1a15ae154.png "Rendered by QuickLaTeX.com")，有![P^* < P    ](img/c0d6a7111ac84a639def22f149b13feb.png "Rendered by QuickLaTeX.com")。
现在，附加![x_{m}    ](img/dbb54de967acc637110ad3c72e27e397.png "Rendered by QuickLaTeX.com")和![y_{n}    ](img/0dfb3405a2eea036145ac88fd1e34732.png "Rendered by QuickLaTeX.com")，我们得到一个带有惩罚![P^* + p_{xy} < P + p_{xy}    ](img/6dd1114f6179b9a96a7d603853597f0e.png "Rendered by QuickLaTeX.com")的对齐。这与![X, Y    ](img/bad0a9bfa0cb5d78ebb1efc4e559fa4d.png "Rendered by QuickLaTeX.com")的初始对齐的最优性相矛盾。
于是，证明了。
让![dp[i][j]    ](img/96f45eee19d0ac07cae358d47a8ff0e9.png "Rendered by QuickLaTeX.com")成为![X_{i}    ](img/d13c5072058b06ee91916b5415a83ccf.png "Rendered by QuickLaTeX.com")和![Y_{i}    ](img/3efb81bdc7b78e3e1f2ed6b8e50f9365.png "Rendered by QuickLaTeX.com")最佳对中的惩罚。然后，从最优子结构出发，![dp[i][j] = min(dp[i-1][j-1] + p_{xy}, dp[i-1][j] + p_{gap}, dp[i][j-1] + p_{gap})    ](img/5dbc6360b8b80b119c204e7339be911c.png "Rendered by QuickLaTeX.com")。
总的最低处罚是![dp[m][n]    ](img/8f3b4e2a0540108da6c48b6fd411f73e.png "Rendered by QuickLaTeX.com")。

**重构解**
重构，
1。从![dp[m][n]    ](img/8f3b4e2a0540108da6c48b6fd411f73e.png "Rendered by QuickLaTeX.com")开始，追溯满满的表格。
2。当![(i, j)    ](img/442c8c0f1b2b50c26358c4020dc7aec4.png "Rendered by QuickLaTeX.com")
…..2a .如果使用案例 1 填充，请转至![(i-1, j-1)    ](img/882952074e183266c2d740130d49f2e1.png "Rendered by QuickLaTeX.com")。
…..2b。如果使用案例 2 填充，请转至![(i-1, j)    ](img/9c383f180115a46f8a48ea8fc4b42b4f.png "Rendered by QuickLaTeX.com")。
…..2c。如果使用案例 3 填充，请转至![(i, j-1)    ](img/59bca49881e3101962abe213e00dca62.png "Rendered by QuickLaTeX.com")。
3。如果 i = 0 或 j = 0，则用间隙匹配剩余的子字符串。

下面是上述解决方案的实现。

## C++

```
// CPP program to implement sequence alignment
// problem.
#include <bits/stdc++.h>

using namespace std;

// function to find out the minimum penalty
void getMinimumPenalty(string x, string y, int pxy, int pgap)
{
    int i, j; // initialising variables

    int m = x.length(); // length of gene1
    int n = y.length(); // length of gene2

    // table for storing optimal substructure answers
    int dp[m+1][n+1] = {0};

    // initialising the table
    for (i = 0; i <= (n+m); i++)
    {
        dp[i][0] = i * pgap;
        dp[0][i] = i * pgap;
    }   

    // calculating the minimum penalty
    for (i = 1; i <= m; i++)
    {
        for (j = 1; j <= n; j++)
        {
            if (x[i - 1] == y[j - 1])
            {
                dp[i][j] = dp[i - 1][j - 1];
            }
            else
            {
                dp[i][j] = min({dp[i - 1][j - 1] + pxy ,
                                dp[i - 1][j] + pgap    ,
                                dp[i][j - 1] + pgap    });
            }
        }
    }

    // Reconstructing the solution
    int l = n + m; // maximum possible length

    i = m; j = n;

    int xpos = l;
    int ypos = l;

    // Final answers for the respective strings
    int xans[l+1], yans[l+1];

    while ( !(i == 0 || j == 0))
    {
        if (x[i - 1] == y[j - 1])
        {
            xans[xpos--] = (int)x[i - 1];
            yans[ypos--] = (int)y[j - 1];
            i--; j--;
        }
        else if (dp[i - 1][j - 1] + pxy == dp[i][j])
        {
            xans[xpos--] = (int)x[i - 1];
            yans[ypos--] = (int)y[j - 1];
            i--; j--;
        }
        else if (dp[i - 1][j] + pgap == dp[i][j])
        {
            xans[xpos--] = (int)x[i - 1];
            yans[ypos--] = (int)'_';
            i--;
        }
        else if (dp[i][j - 1] + pgap == dp[i][j])
        {
            xans[xpos--] = (int)'_';
            yans[ypos--] = (int)y[j - 1];
            j--;
        }
    }
    while (xpos > 0)
    {
        if (i > 0) xans[xpos--] = (int)x[--i];
        else xans[xpos--] = (int)'_';
    }
    while (ypos > 0)
    {
        if (j > 0) yans[ypos--] = (int)y[--j];
        else yans[ypos--] = (int)'_';
    }

    // Since we have assumed the answer to be n+m long,
    // we need to remove the extra gaps in the starting
    // id represents the index from which the arrays
    // xans, yans are useful
    int id = 1;
    for (i = l; i >= 1; i--)
    {
        if ((char)yans[i] == '_' && (char)xans[i] == '_')
        {
            id = i + 1;
            break;
        }
    }

    // Printing the final answer
    cout << "Minimum Penalty in aligning the genes = ";
    cout << dp[m][n] << "\n";
    cout << "The aligned genes are :\n";
    for (i = id; i <= l; i++)
    {
        cout<<(char)xans[i];
    }
    cout << "\n";
    for (i = id; i <= l; i++)
    {
        cout << (char)yans[i];
    }
    return;
}

// Driver code
int main(){
    // input strings
    string gene1 = "AGGGCT";
    string gene2 = "AGGCA";

    // initialising penalties of different types
    int misMatchPenalty = 3;
    int gapPenalty = 2;

    // calling the function to calculate the result
    getMinimumPenalty(gene1, gene2,
        misMatchPenalty, gapPenalty);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// sequence alignment problem.
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
// function to find out
// the minimum penalty
static void getMinimumPenalty(String x, String y,
                              int pxy, int pgap)
{
    int i, j; // initialising variables

    int m = x.length(); // length of gene1
    int n = y.length(); // length of gene2

    // table for storing optimal
    // substructure answers
    int dp[][] = new int[n + m + 1][n + m + 1];

    for (int[] x1 : dp)
    Arrays.fill(x1, 0);

    // initialising the table
    for (i = 0; i <= (n + m); i++)
    {
        dp[i][0] = i * pgap;
        dp[0][i] = i * pgap;
    }

    // calculating the
    // minimum penalty
    for (i = 1; i <= m; i++)
    {
        for (j = 1; j <= n; j++)
        {
            if (x.charAt(i - 1) == y.charAt(j - 1))
            {
                dp[i][j] = dp[i - 1][j - 1];
            }
            else
            {
                dp[i][j] = Math.min(Math.min(dp[i - 1][j - 1] + pxy ,
                                             dp[i - 1][j] + pgap) ,
                                             dp[i][j - 1] + pgap );
            }
        }
    }

    // Reconstructing the solution
    int l = n + m; // maximum possible length

    i = m; j = n;

    int xpos = l;
    int ypos = l;

    // Final answers for
    // the respective strings
    int xans[] = new int[l + 1];
    int yans[] = new int[l + 1];

    while ( !(i == 0 || j == 0))
    {
        if (x.charAt(i - 1) == y.charAt(j - 1))
        {
            xans[xpos--] = (int)x.charAt(i - 1);
            yans[ypos--] = (int)y.charAt(j - 1);
            i--; j--;
        }
        else if (dp[i - 1][j - 1] + pxy == dp[i][j])
        {
            xans[xpos--] = (int)x.charAt(i - 1);
            yans[ypos--] = (int)y.charAt(j - 1);
            i--; j--;
        }
        else if (dp[i - 1][j] + pgap == dp[i][j])
        {
            xans[xpos--] = (int)x.charAt(i - 1);
            yans[ypos--] = (int)'_';
            i--;
        }
        else if (dp[i][j - 1] + pgap == dp[i][j])
        {
            xans[xpos--] = (int)'_';
            yans[ypos--] = (int)y.charAt(j - 1);
            j--;
        }
    }
    while (xpos > 0)
    {
        if (i > 0) xans[xpos--] = (int)x.charAt(--i);
        else xans[xpos--] = (int)'_';
    }
    while (ypos > 0)
    {
        if (j > 0) yans[ypos--] = (int)y.charAt(--j);
        else yans[ypos--] = (int)'_';
    }

    // Since we have assumed the
    // answer to be n+m long,
    // we need to remove the extra
    // gaps in the starting id
    // represents the index from
    // which the arrays xans,
    // yans are useful
    int id = 1;
    for (i = l; i >= 1; i--)
    {
        if ((char)yans[i] == '_' &&
            (char)xans[i] == '_')
        {
            id = i + 1;
            break;
        }
    }

    // Printing the final answer
    System.out.print("Minimum Penalty in " +
                     "aligning the genes = ");
    System.out.print(dp[m][n] + "\n");
    System.out.println("The aligned genes are :");
    for (i = id; i <= l; i++)
    {
        System.out.print((char)xans[i]);
    }
    System.out.print("\n");
    for (i = id; i <= l; i++)
    {
        System.out.print((char)yans[i]);
    }
    return;
}

// Driver code
public static void main(String[] args)
{
    // input strings
    String gene1 = "AGGGCT";
    String gene2 = "AGGCA";

    // initialising penalties
    // of different types
    int misMatchPenalty = 3;
    int gapPenalty = 2;

    // calling the function to
    // calculate the result
    getMinimumPenalty(gene1, gene2,
        misMatchPenalty, gapPenalty);
}
}
```

## C#

```
// C# program to implement sequence alignment
// problem.
using System;

class GFG
{
    // function to find out the minimum penalty
    public static void getMinimumPenalty(string x, string y, int pxy, int pgap)
    {
        int i, j; // initialising variables

        int m = x.Length; // length of gene1
        int n = y.Length; // length of gene2

        // table for storing optimal substructure answers
        int[,] dp = new int[n+m+1,n+m+1];
        for(int q = 0; q < n+m+1; q++)
            for(int w = 0; w < n+m+1; w++)
                dp[q,w] = 0;

        // initialising the table 
        for (i = 0; i <= (n+m); i++)
        {
            dp[i,0] = i * pgap;
            dp[0,i] = i * pgap;
        }    

        // calculating the minimum penalty
        for (i = 1; i <= m; i++)
        {
            for (j = 1; j <= n; j++)
            {
                if (x[i - 1] == y[j - 1])
                {
                    dp[i,j] = dp[i - 1,j - 1];
                }
                else
                {
                    dp[i,j] = Math.Min(Math.Min(dp[i - 1,j - 1] + pxy , 
                                    dp[i - 1,j] + pgap)    , 
                                    dp[i,j - 1] + pgap    );
                }
            }
        }

        // Reconstructing the solution
        int l = n + m; // maximum possible length

        i = m; j = n;

        int xpos = l;
        int ypos = l;

        // Final answers for the respective strings
        int[] xans = new int[l+1];
        int [] yans = new int[l+1];

        while ( !(i == 0 || j == 0))
        {
            if (x[i - 1] == y[j - 1])
            {
                xans[xpos--] = (int)x[i - 1];
                yans[ypos--] = (int)y[j - 1];
                i--; j--;
            }
            else if (dp[i - 1,j - 1] + pxy == dp[i,j])
            {
                xans[xpos--] = (int)x[i - 1];
                yans[ypos--] = (int)y[j - 1];
                i--; j--;
            }
            else if (dp[i - 1,j] + pgap == dp[i,j])
            {
                xans[xpos--] = (int)x[i - 1];
                yans[ypos--] = (int)'_';
                i--;
            }
            else if (dp[i,j - 1] + pgap == dp[i,j])
            {
                xans[xpos--] = (int)'_';
                yans[ypos--] = (int)y[j - 1];
                j--;
            }
        }
        while (xpos > 0)
        {
            if (i > 0) xans[xpos--] = (int)x[--i];
            else xans[xpos--] = (int)'_';
        }
        while (ypos > 0)
        {
            if (j > 0) yans[ypos--] = (int)y[--j];
            else yans[ypos--] = (int)'_';
        }

        // Since we have assumed the answer to be n+m long, 
        // we need to remove the extra gaps in the starting 
        // id represents the index from which the arrays
        // xans, yans are useful
        int id = 1;
        for (i = l; i >= 1; i--)
        {
            if ((char)yans[i] == '_' && (char)xans[i] == '_')
            {
                id = i + 1;
                break;
            }
        }

        // Printing the final answer
        Console.Write("Minimum Penalty in aligning the genes = " + dp[m,n] + "\n");
        Console.Write("The aligned genes are :\n");
        for (i = id; i <= l; i++)
        {
            Console.Write((char)xans[i]);
        }
        Console.Write("\n");
        for (i = id; i <= l; i++)
        {
            Console.Write((char)yans[i]);
        }
        return;
    }

    // Driver code
    static void Main()
    {
        // input strings
        string gene1 = "AGGGCT";
        string gene2 = "AGGCA";

        // initialising penalties of different types
        int misMatchPenalty = 3;
        int gapPenalty = 2;

        // calling the function to calculate the result
        getMinimumPenalty(gene1, gene2, 
            misMatchPenalty, gapPenalty);
    }
    //This code is contributed by DrRoot_
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// sequence alignment problem.

// function to find out
// the minimum penalty
function getMinimumPenalty($x, $y,
                           $pxy, $pgap)
{
    $i; $j; // initializing variables

    $m = strlen($x); // length of gene1
    $n = strlen($y); // length of gene2

    // table for storing optimal
    // substructure answers
    $dp[$n + $m + 1][$n + $m + 1] = array(0);

    // initialising the table
    for ($i = 0; $i <= ($n+$m); $i++)
    {
        $dp[$i][0] = $i * $pgap;
        $dp[0][$i] = $i * $pgap;
    }

    // calculating the
    // minimum penalty
    for ($i = 1; $i <= $m; $i++)
    {
        for ($j = 1; $j <= $n; $j++)
        {
            if ($x[$i - 1] == $y[$j - 1])
            {
                $dp[$i][$j] = $dp[$i - 1][$j - 1];
            }
            else
            {
                $dp[$i][$j] = min($dp[$i - 1][$j - 1] + $pxy ,
                                  $dp[$i - 1][$j] + $pgap ,
                                  $dp[$i][$j - 1] + $pgap );
            }
        }
    }

    // Reconstructing the solution
    $l = $n + $m; // maximum possible length

    $i = $m; $j = $n;

    $xpos = $l;
    $ypos = $l;

    // Final answers for
    // the respective strings
    // $xans[$l + 1]; $yans[$l + 1];

    while ( !($i == 0 || $j == 0))
    {
        if ($x[$i - 1] == $y[$j - 1])
        {
            $xans[$xpos--] = $x[$i - 1];
            $yans[$ypos--] = $y[$j - 1];
            $i--; $j--;
        }
        else if ($dp[$i - 1][$j - 1] +
                 $pxy == $dp[$i][$j])
        {
            $xans[$xpos--] = $x[$i - 1];
            $yans[$ypos--] = $y[$j - 1];
            $i--; $j--;
        }
        else if ($dp[$i - 1][$j] +
                 $pgap == $dp[$i][$j])
        {
            $xans[$xpos--] = $x[$i - 1];
            $yans[$ypos--] = '_';
            $i--;
        }
        else if ($dp[$i][$j - 1] +
                 $pgap == $dp[$i][$j])
        {
            $xans[$xpos--] = '_';
            $yans[$ypos--] = $y[$j - 1];
            $j--;
        }
    }
    while ($xpos > 0)
    {
        if ($i > 0) $xans[$xpos--] = $x[--$i];
        else $xans[$xpos--] = '_';
    }
    while ($ypos > 0)
    {
        if ($j > 0)
            $yans[$ypos--] = $y[--$j];
        else
            $yans[$ypos--] = '_';
    }

    // Since we have assumed the
    // answer to be n+m long,
    // we need to remove the extra
    // gaps in the starting
    // id represents the index
    // from which the arrays
    // xans, yans are useful
    $id = 1;
    for ($i = $l; $i >= 1; $i--)
    {
        if ($yans[$i] == '_' &&
            $xans[$i] == '_')
        {
            $id = $i + 1;
            break;
        }
    }

    // Printing the final answer
    echo "Minimum Penalty in ".
         "aligning the genes = ";
    echo $dp[$m][$n] . "\n";
    echo "The aligned genes are :\n";
    for ($i = $id; $i <= $l; $i++)
    {
        echo $xans[$i];
    }
    echo "\n";
    for ($i = $id; $i <= $l; $i++)
    {
        echo $yans[$i];
    }
    return;
}

// Driver code

// input strings
$gene1 = "AGGGCT";
$gene2 = "AGGCA";

// initialising penalties
// of different types
$misMatchPenalty = 3;
$gapPenalty = 2;

// calling the function
// to calculate the result
getMinimumPenalty($gene1, $gene2,
    $misMatchPenalty, $gapPenalty);

// This code is contributed by Abhinav96
?>
```

**Output:** 

```
Minimum Penalty in aligning the genes = 5
The aligned genes are :
AGGGCT
A_GGCA
```

**时间复杂度:** ![\mathcal{O}(n*m)    ](img/3f8046eaad40b445d594cc4473b4f109.png "Rendered by QuickLaTeX.com")
**空间复杂度:** ![\mathcal{O}(n*m)    ](img/3f8046eaad40b445d594cc4473b4f109.png "Rendered by QuickLaTeX.com")