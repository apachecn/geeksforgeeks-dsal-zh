# O(N)空间中的 N 皇后

> 原文:[https://www.geeksforgeeks.org/n-queen-in-on-space/](https://www.geeksforgeeks.org/n-queen-in-on-space/)

给定 n，在 n×n 的棋盘上，找到皇后在棋盘上的正确位置。
**之前的进场:** [N 皇后](https://www.geeksforgeeks.org/branch-and-bound-set-4-n-queen-problem/)

**算法:**

```
Place(k, i)
// Returns true if a queen can be placed
// in kth row and ith column. Otherwise it
// returns false. X[] is a global array
// whose first (k-1) values have been set.
// Abs( ) returns absolute value of r
{
   for j := 1 to k-1 do

        // Two in the same column
        // or in the same diagonal
        if ((x[j] == i)  or
            (abs(x[j] – i) = Abs(j – k)))
           then return false;

   return true;
}
```

**算法队列(k，n) :**

```
// Using backtracking, this procedure prints all 
// possible placements of n queens on an n×n 
// chessboard so that they are nonattacking.
{
      for i:= 1 to n do
      {
         if Place(k, i) then
         {
             x[k] = i;
             if (k == n)
                write (x[1:n]);
             else 
               NQueens(k+1, n);
         }
      }
} 
```

## C++

```
// CPP code to for n Queen placement
#include <bits/stdc++.h>

#define breakLine cout << "\n---------------------------------\n";
#define MAX 10

using namespace std;

int arr[MAX], no;

void nQueens(int k, int n);
bool canPlace(int k, int i);
void display(int n);

// Function to check queens placement
void nQueens(int k, int n){

    for (int i = 1;i <= n;i++){
        if (canPlace(k, i)){
            arr[k] = i;
            if (k == n)
                display(n);
            else
                nQueens(k + 1, n);
        }
    }
}

// Helper Function to check if queen can be placed
bool canPlace(int k, int i){
    for (int j = 1;j <= k - 1;j++){
        if (arr[j] == i ||
            (abs(arr[j] - i) == abs(j - k)))
           return false;
    }
    return true;
}

// Function to display placed queen
void display(int n){
    breakLine
    cout << "Arrangement No. " << ++no;
    breakLine

    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= n; j++){
            if (arr[i] != j)
                cout << "\t_";
            else
                cout << "\tQ";
        }
        cout << endl;
    }

    breakLine
}

// Driver Code
int main(){
    int n = 4;   
    nQueens(1, n);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to for n Queen placement
class GfG
{

    static void breakLine()
    {
        System.out.print("\n---------------------------------\n");
    }
    static int MAX = 10;

    static int arr[] = new int[MAX], no;

    // Function to check queens placement
    static void nQueens(int k, int n)
    {

        for (int i = 1; i <= n; i++)
        {
            if (canPlace(k, i))
            {
                arr[k] = i;
                if (k == n)
                {
                    display(n);
                }
                else
                {
                    nQueens(k + 1, n);
                }
            }
        }
    }

    // Helper Function to check if queen can be placed
    static boolean canPlace(int k, int i)
    {
        for (int j = 1; j <= k - 1; j++)
        {
            if (arr[j] == i ||
                (Math.abs(arr[j] - i) == Math.abs(j - k)))
            {
                return false;
            }
        }
        return true;
    }

    // Function to display placed queen
    static void display(int n)
    {
        breakLine();
        System.out.print("Arrangement No. " + ++no);
        breakLine();

        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= n; j++)
            {
                if (arr[i] != j)
                {
                    System.out.print("\t_");
                }
                else
                {
                    System.out.print("\tQ");
                }
            }
            System.out.println("");
        }

        breakLine();
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        nQueens(1, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code to for n Queen placement
class GfG:
    def __init__(self):
        self.MAX = 10
        self.arr = [0] * self.MAX
        self.no = 0

    def breakLine(self):
        print("\n------------------------------------------------")

    def canPlace(self, k, i):

        # Helper Function to check
        # if queen can be placed
        for j in range(1, k):
            if (self.arr[j] == i or
               (abs(self.arr[j] - i) == abs(j - k))):
                return False
        return True

    def display(self, n):

        # Function to display placed queen
        self.breakLine()
        self.no += 1
        print("Arrangement No.", self.no, end = " ")
        self.breakLine()

        for i in range(1, n + 1):
            for j in range(1, n + 1):
                if self.arr[i] != j:
                    print("\t_", end = " ")
                else:
                    print("\tQ", end = " ")
            print()

        self.breakLine()

    def nQueens(self, k, n):

        # Function to check queens placement
        for i in range(1, n + 1):
            if self.canPlace(k, i):
                self.arr[k] = i
                if k == n:
                    self.display(n)
                else:
                    self.nQueens(k + 1, n)

# Driver Code
if __name__ == '__main__':
    n = 4
    obj = GfG()
    obj.nQueens(1, n)

# This code is contributed by vibhu4agarwal
```

## C#

```
// C# code to for n Queen placement
using System;

class GfG
{

    static void breakLine()
    {
        Console.Write("\n---------------------------------\n");
    }
    static int MAX = 10;

    static int []arr = new int[MAX];
    static int no;

    // Function to check queens placement
    static void nQueens(int k, int n)
    {

        for (int i = 1; i <= n; i++)
        {
            if (canPlace(k, i))
            {
                arr[k] = i;
                if (k == n)
                {
                    display(n);
                }
                else
                {
                    nQueens(k + 1, n);
                }
            }
        }
    }

    // Helper Function to check if queen can be placed
    static bool canPlace(int k, int i)
    {
        for (int j = 1; j <= k - 1; j++)
        {
            if (arr[j] == i ||
                (Math.Abs(arr[j] - i) == Math.Abs(j - k)))
            {
                return false;
            }
        }
        return true;
    }

    // Function to display placed queen
    static void display(int n)
    {
        breakLine();
        Console.Write("Arrangement No. " + ++no);
        breakLine();

        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= n; j++)
            {
                if (arr[i] != j)
                {
                    Console.Write("\t_");
                }
                else
                {
                    Console.Write("\tQ");
                }
            }
            Console.WriteLine("");
        }

        breakLine();
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 4;
        nQueens(1, n);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to for n Queen placement

    function breakLine()
    {
        document.write("<br />");
        document.write("---------------------------------");
        document.write("<br />");
    }
    let MAX = 10;

    let arr = [];
    let no = 0;

    // Function to check queens placement
    function nQueens(k, n)
    {

        for (let i = 1; i <= n; i++)
        {
            if (canPlace(k, i))
            {
                arr[k] = i;
                if (k == n)
                {
                    display(n);
                }
                else
                {
                    nQueens(k + 1, n);
                }
            }
        }
    }

    // Helper Function to check if queen can be placed
    function canPlace(k, i)
    {
        for (let j = 1; j <= k - 1; j++)
        {
            if (arr[j] == i ||
                (Math.abs(arr[j] - i) == Math.abs(j - k)))
            {
                return false;
            }
        }
        return true;
    }

    // Function to display placed queen
    function display(n)
    {
        breakLine();
        document.write("Arrangement No. " + ++no);
        breakLine();

        for (let i = 1; i <= n; i++)
        {
            for (let j = 1; j <= n; j++)
            {
                if (arr[i] != j)
                {
                    document.write("\t_");
                }
                else
                {
                    document.write("\tQ");
                }
            }
            document.write("<br/>");
        }

        breakLine();
    }

// Driver code

        let n = 4;
        nQueens(1, n);

</script>
```

**Output:** 

```
---------------------------------
Arrangement No. 1
---------------------------------
    _    Q    _    _
    _    _    _    Q
    Q    _    _    _
    _    _    Q    _

---------------------------------

---------------------------------
Arrangement No. 2
---------------------------------
    _    _    Q    _
    Q    _    _    _
    _    _    _    Q
    _    Q    _    _

---------------------------------
```