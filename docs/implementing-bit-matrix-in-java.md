# 在 Java 中实现位矩阵

> 原文:[https://www . geesforgeks . org/impering-bit-matrix-in-Java/](https://www.geeksforgeeks.org/implementing-bit-matrix-in-java/)

BitMatrix 是一个二维数组，其中每个元素不是 0 就是 1。我们将实现一个位矩阵，促进基本的位操作，如或、与、异或。

**进场:**

1.  从 java.util 包导入 BitSet 类。
2.  使用 BitSet 初始化一个大小为行 x 列的位数组。默认情况下，集合中的所有位最初的值都为 false。
3.  现在，通过使用 BitSet 类提供的方法，我们可以操作数组。
4.  BitSet 类中的方法有 Set、clear、xor、or 和。
5.  使用显示方法显示位矩阵。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate the
// implementation of BitMatrix

import java.util.BitSet;

public class BitMatrix {
    public static void main(String[] args)
    {

        System.out.println("Bit Matrix Implementation");

        try {
            MatrixBuilder bmat = new MatrixBuilder(2, 2);

            // All the bitsets in the bitArray will be
            // displayed using display(). The values in
            // bitset refer to the columns which are set
            // to 1.
            bmat.set(0, 0);
            bmat.display();

            bmat.set(0, 1);
            bmat.display();

            bmat.set(1, 0);
            bmat.display();

            bmat.set(1, 1);
            bmat.display();

            bmat.clear(0, 1);
            bmat.display();

            bmat.and(0, 1);
            bmat.display();

            bmat.xor(0, 1);
            bmat.display();

            bmat.or(0, 1);
            bmat.display();
        }
        catch (Exception e) {
            System.out.println("Error due to " + e);
        }
    }
}

class MatrixBuilder {
    public BitSet[] bitArray;

    public MatrixBuilder(int rows, int cols)
    {
        // initializing a bit matrix of size rows x cols.
        bitArray = new BitSet[rows];

        int i = 0;

        while (i < rows) {
            bitArray[i] = new BitSet(cols);
            i++;
        }
    }

    // Method to clear entire array.
    public void clear()
    {
        // Getting the value of number of rows.
        int rows = bitArray.length;

        // Getting the value number of columns.
        int cols = bitArray[0].size();

        // To clear the bitArray Initialize it once again.
        bitArray = new BitSet[rows];

        int i = 0;
        while (i < rows) {
            bitArray[i] = new BitSet(cols);
            i++;
        }
    }

    // Method to XOR two rows
    public void xor(int row1, int row2)
    {
        bitArray[row1].xor(bitArray[row2]);
    }

    // Here clear() method is overloaded.
    // Method to clear specific bit.
    public void clear(int r, int c)
    {
        bitArray[r].clear(c);
    }

    // Method to get a specific bit
    public boolean get(int r, int c)
    {
        return bitArray[r].get(c);
    }

    // Method to set a specific bit
    public void set(int r, int c) { bitArray[r].set(c); }

    // Method to And two rows
    public void and(int row1, int row2)
    {
        bitArray[row1].and(bitArray[row2]);
    }

    // Method to OR two rows
    public void or(int row1, int row2)
    {
        bitArray[row1].or(bitArray[row2]);
    }

    // Method to display the bit matrix
    public void display()
    {
        System.out.println("\nBit Matrix : ");

        // Here each bitset can be referred as each row
        // we will print all the rows using for loop.
        for (BitSet bs : bitArray)
            System.out.println(bs);

        System.out.println();
    }
}
```

**Output**

```
Bit Matrix Implementation

Bit Matrix : 
{0}
{}

Bit Matrix : 
{0, 1}
{}

Bit Matrix : 
{0, 1}
{0}

Bit Matrix : 
{0, 1}
{0, 1}

Bit Matrix : 
{0}
{0, 1}

Bit Matrix : 
{0}
{0, 1}

Bit Matrix : 
{1}
{0, 1}

Bit Matrix : 
{0, 1}
{0, 1}
```