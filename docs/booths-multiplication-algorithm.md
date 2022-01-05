# 布斯乘法算法

> 原文:[https://www . geesforgeks . org/boots-乘法-算法/](https://www.geeksforgeeks.org/booths-multiplication-algorithm/)

Booth 的算法是一种乘法算法，用 2 的补码表示法将两个有符号的二进制数相乘。
布斯使用了移位比加法更快的台式计算器，并创建了算法来提高它们的速度。布斯的算法在计算机体系结构的研究中很受关注。下面是算法的实现。
**例:**

```
Input : 0110, 0010
Output :  qn      q[n+1]                  AC      QR     sc(step count)
                          initial         0000   0010        4
          0       0       rightShift      0000   0001        3
          1       0       A = A - BR      1010
                          rightShift      1101   0000        2
          0       1       A = A + BR      0011
                          rightShift      0001   1000        1
          0       0       rightShift      0000   1100        0

Result=1100
```

**算法:**

> 将被乘数放入 BR 中，将乘数放入 QR 中
> ，算法按照以下条件工作:
> **1。**如果 Q <sub>n</sub> 和 Q <sub>n+1</sub> 相同，即 00 或 11，则执行 1 位算术移位。
> **2。**如果 Q <sub>n</sub> Q <sub>n+1</sub> = 10，则执行 A= A + BR 并执行 1 位算术移位。
> **3。**如果 Q <sub>n</sub> Q <sub>n+1</sub> = 01，则执行 A = A–BR 并执行 1 位算术移位。

## C++

```
// CPP code to implement booth's algorithm
#include <bits/stdc++.h>

using namespace std;

// function to perform adding in the accumulator
void add(int ac[], int x[], int qrn)
{
    int i, c = 0;

    for (i = 0; i < qrn; i++) {

        // updating accumulator with A = A + BR
        ac[i] = ac[i] + x[i] + c;

        if (ac[i] > 1) {
            ac[i] = ac[i] % 2;
            c = 1;
        }
        else
            c = 0;
    }
}

// function to find the number's complement
void complement(int a[], int n)
{
    int i;
    int x[8] = {0};
    x[0] = 1;

    for (i = 0; i < n; i++) {
        a[i] = (a[i] + 1) % 2;
    }
    add(a, x, n);
}

// function to perform right shift
void rightShift(int ac[], int qr[], int& qn, int qrn)
{
    int temp, i;
    temp = ac[0];
    qn = qr[0];

    cout << "\t\trightShift\t";

    for (i = 0; i < qrn - 1; i++) {
        ac[i] = ac[i + 1];
        qr[i] = qr[i + 1];
    }
    qr[qrn - 1] = temp;
}

// function to display operations
void display(int ac[], int qr[], int qrn)
{
    int i;

    // accumulator content
    for (i = qrn - 1; i >= 0; i--)
        cout << ac[i];
    cout << "\t";

    // multiplier content
    for (i = qrn - 1; i >= 0; i--)
        cout << qr[i];
}

// Function to implement booth's algo
void boothAlgorithm(int br[], int qr[], int mt[], int qrn, int sc)
{

    int qn = 0, ac[10] = { 0 };
    int temp = 0;
    cout << "qn\tq[n+1]\t\tBR\t\tAC\tQR\t\tsc\n";
    cout << "\t\t\tinitial\t\t";

    display(ac, qr, qrn);
    cout << "\t\t" << sc << "\n";

    while (sc != 0) {
        cout << qr[0] << "\t" << qn;

        // SECOND CONDITION
        if ((qn + qr[0]) == 1)
        {
            if (temp == 0) {

                // subtract BR from accumulator
                add(ac, mt, qrn);
                cout << "\t\tA = A - BR\t";

                for (int i = qrn - 1; i >= 0; i--)
                    cout << ac[i];
                temp = 1;
            }

            // THIRD CONDITION
            else if (temp == 1)
            {
                // add BR to accumulator
                add(ac, br, qrn);
                cout << "\t\tA = A + BR\t";

                for (int i = qrn - 1; i >= 0; i--)
                    cout << ac[i];
                temp = 0;
            }
            cout << "\n\t";
            rightShift(ac, qr, qn, qrn);
        }

        // FIRST CONDITION
        else if (qn - qr[0] == 0)
            rightShift(ac, qr, qn, qrn);

        display(ac, qr, qrn);

        cout << "\t";

        // decrement counter
        sc--;
        cout << "\t" << sc << "\n";
    }
}

// driver code
int main(int argc, char** arg)
{

    int mt[10], sc;
    int brn, qrn;

    // Number of multiplicand bit
    brn = 4;

    // multiplicand
    int br[] = { 0, 1, 1, 0 };

    // copy multiplier to temp array mt[]
    for (int i = brn - 1; i >= 0; i--)
        mt[i] = br[i];

    reverse(br, br + brn);

    complement(mt, brn);

    // No. of multiplier bit
    qrn = 4;

    // sequence counter
    sc = qrn;

    // multiplier
    int qr[] = { 1, 0, 1, 0 };
    reverse(qr, qr + qrn);

    boothAlgorithm(br, qr, mt, qrn, sc);

    cout << endl
         << "Result = ";

    for (int i = qrn - 1; i >= 0; i--)
        cout << qr[i];
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement booth's algorithm
class GFG
{

    // function to perform adding in the accumulator
    static void add(int ac[], int x[], int qrn)
    {
        int i, c = 0;

        for (i = 0; i < qrn; i++)
        {

            // updating accumulator with A = A + BR
            ac[i] = ac[i] + x[i] + c;

            if (ac[i] > 1)
            {
                ac[i] = ac[i] % 2;
                c = 1;
            }
            else
            {
                c = 0;
            }
        }
    }

    // function to find the number's complement
    static void complement(int a[], int n)
    {
        int i;
        int[] x = new int[8];
        x[0] = 1;

        for (i = 0; i < n; i++)
        {
            a[i] = (a[i] + 1) % 2;
        }
        add(a, x, n);
    }

    // function ro perform right shift
    static void rightShift(int ac[], int qr[],
                            int qn, int qrn)
    {
        int temp, i;
        temp = ac[0];
        qn = qr[0];

        System.out.print("\t\trightShift\t");

        for (i = 0; i < qrn - 1; i++)
        {
            ac[i] = ac[i + 1];
            qr[i] = qr[i + 1];
        }
        qr[qrn - 1] = temp;
    }

    // function to display operations
    static void display(int ac[], int qr[], int qrn)
    {
        int i;

        // accumulator content
        for (i = qrn - 1; i >= 0; i--)
        {
            System.out.print(ac[i]);
        }
        System.out.print("\t");

        // multiplier content
        for (i = qrn - 1; i >= 0; i--)
        {
            System.out.print(qr[i]);
        }
    }

    // Function to implement booth's algo
    static void boothAlgorithm(int br[], int qr[], int mt[],
                                            int qrn, int sc)
    {

        int qn = 0;
        int[] ac = new int[10];
        int temp = 0;
        System.out.print("qn\tq[n+1]\t\tBR\t\tAC\tQR\t\tsc\n");
        System.out.print("\t\t\tinitial\t\t");

        display(ac, qr, qrn);
        System.out.print("\t\t" + sc + "\n");

        while (sc != 0)
        {
            System.out.print(qr[0] + "\t" + qn);

            // SECOND CONDITION
            if ((qn + qr[0]) == 1)
            {
                if (temp == 0)
                {

                    // subtract BR from accumulator
                    add(ac, mt, qrn);
                    System.out.print("\t\tA = A - BR\t");

                    for (int i = qrn - 1; i >= 0; i--)
                    {
                        System.out.print(ac[i]);
                    }
                    temp = 1;
                }

                // THIRD CONDITION
                else if (temp == 1)
                {
                    // add BR to accumulator
                    add(ac, br, qrn);
                    System.out.print("\t\tA = A + BR\t");

                    for (int i = qrn - 1; i >= 0; i--)
                    {
                        System.out.print(ac[i]);
                    }
                    temp = 0;
                }
                System.out.print("\n\t");
                rightShift(ac, qr, qn, qrn);
            }

            // FIRST CONDITION
            else if (qn - qr[0] == 0)
            {
                rightShift(ac, qr, qn, qrn);
            }

            display(ac, qr, qrn);

            System.out.print("\t");

            // decrement counter
            sc--;
            System.out.print("\t" + sc + "\n");
        }
    }

    static void reverse(int a[])
    {
        int i, k, n = a.length;
        int t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] mt = new int[10];
        int sc;
        int brn, qrn;

        // Number of multiplicand bit
        brn = 4;

        // multiplicand
        int br[] = {0, 1, 1, 0};

        // copy multiplier to temp array mt[]
        for (int i = brn - 1; i >= 0; i--)
        {
            mt[i] = br[i];
        }

        reverse(br);

        complement(mt, brn);

        // No. of multiplier bit
        qrn = 4;

        // sequence counter
        sc = qrn;

        // multiplier
        int qr[] = {1, 0, 1, 0};
        reverse(qr);

        boothAlgorithm(br, qr, mt, qrn, sc);

        System.out.print("\n"
                + "Result = ");

        for (int i = qrn - 1; i >= 0; i--)
        {
            System.out.print(qr[i]);
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## C#

```
// C# code to implement
// booth's algorithm
using System;

class GFG
{
    // function to perform
    // adding in the accumulator
    static void add(int []ac,
                    int []x,
                    int qrn)
    {
        int i, c = 0;

        for (i = 0; i < qrn; i++)
        {

            // updating accumulator
            // with A = A + BR
            ac[i] = ac[i] + x[i] + c;

            if (ac[i] > 1)
            {
                ac[i] = ac[i] % 2;
                c = 1;
            }
            else
                c = 0;
        }
    }

    // function to find
    // the number's complement
    static void complement(int []a, int n)
    {
        int i;
        int []x = new int[8];
        Array.Clear(x, 0, 8);

        x[0] = 1;

        for (i = 0; i < n; i++)
        {
            a[i] = (a[i] + 1) % 2;
        }
        add(a, x, n);
    }

    // function to perform
    // right shift
    static void rightShift(int []ac, int []qr,
                           ref int qn, int qrn)
    {
        int temp, i;
        temp = ac[0];
        qn = qr[0];

        Console.Write("\t\trightShift\t");

        for (i = 0; i < qrn - 1; i++)
        {
            ac[i] = ac[i + 1];
            qr[i] = qr[i + 1];
        }
        qr[qrn - 1] = temp;
    }

    // function to display
    // operations
    static void display(int []ac,
                        int []qr,
                        int qrn)
    {
        int i;

        // accumulator content
        for (i = qrn - 1; i >= 0; i--)
            Console.Write(ac[i]);
        Console.Write("\t");

        // multiplier content
        for (i = qrn - 1; i >= 0; i--)
            Console.Write(qr[i]);
    }

    // Function to implement
    // booth's algo
    static void boothAlgorithm(int []br, int []qr,
                               int []mt, int qrn,
                               int sc)
    {

        int qn = 0;
        int []ac = new int[10];
        Array.Clear(ac, 0, 10);

        int temp = 0;
        Console.Write("qn\tq[n + 1]\tBR\t" +
                       "\tAC\tQR\t\tsc\n");
        Console.Write("\t\t\tinitial\t\t");

        display(ac, qr, qrn);
        Console.Write("\t\t" + sc + "\n");

        while (sc != 0)
        {
            Console.Write(qr[0] + "\t" + qn);

            // SECOND CONDITION
            if ((qn + qr[0]) == 1)
            {
                if (temp == 0)
                {

                    // subtract BR
                    // from accumulator
                    add(ac, mt, qrn);
                    Console.Write("\t\tA = A - BR\t");

                    for (int i = qrn - 1; i >= 0; i--)
                        Console.Write(ac[i]);
                    temp = 1;
                }

                // THIRD CONDITION
                else if (temp == 1)
                {
                    // add BR to accumulator
                    add(ac, br, qrn);
                    Console.Write("\t\tA = A + BR\t");

                    for (int i = qrn - 1; i >= 0; i--)
                        Console.Write(ac[i]);
                    temp = 0;
                }
                Console.Write("\n\t");
                rightShift(ac, qr, ref qn, qrn);
            }

            // FIRST CONDITION
            else if (qn - qr[0] == 0)
                rightShift(ac, qr,
                           ref qn, qrn);

            display(ac, qr, qrn);

            Console.Write("\t");

            // decrement counter
            sc--;
            Console.Write("\t" + sc + "\n");
        }
    }

    // Driver code
    static void Main()
    {

        int []mt = new int[10];
        int sc, brn, qrn;

        // Number of
        // multiplicand bit
        brn = 4;

        // multiplicand
        int []br = new int[]{ 0, 1, 1, 0 };

        // copy multiplier
        // to temp array mt[]
        for (int i = brn - 1; i >= 0; i--)
            mt[i] = br[i];

        Array.Reverse(br);

        complement(mt, brn);

        // No. of
        // multiplier bit
        qrn = 4;

        // sequence
        // counter
        sc = qrn;

        // multiplier
        int []qr = new int[]{ 1, 0, 1, 0 };
        Array.Reverse(qr);

        boothAlgorithm(br, qr,
                       mt, qrn, sc);

        Console.WriteLine();
        Console.Write("Result = ");

        for (int i = qrn - 1; i >= 0; i--)
            Console.Write(qr[i]);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

**输出:**

```
qn    q[n + 1]    BR        AC    QR        sc
            initial        0000    1010        4
0    0        rightShift    0000    0101        3
1    0        A = A - BR    1010
            rightShift    1101    0010        2
0    1        A = A + BR    0011
            rightShift    0001    1001        1
1    0        A = A - BR    1011
            rightShift    1101    1100        0

Result = 1100
```