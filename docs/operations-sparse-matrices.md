# 稀疏矩阵上的运算

> 原文:[https://www.geeksforgeeks.org/operations-sparse-matrices/](https://www.geeksforgeeks.org/operations-sparse-matrices/)

给定两个稀疏矩阵([稀疏矩阵及其表示|集合 1(使用数组和链表)](https://www.geeksforgeeks.org/sparse-matrix-representation/))，执行操作，例如矩阵本身的稀疏形式的加法、乘法或转置。结果应该由三个稀疏矩阵组成，一个通过将两个输入矩阵相加获得，一个通过将两个矩阵相乘获得，一个通过第一个矩阵的转置获得。

**示例:**注意，矩阵的其他条目将为零，因为矩阵是稀疏的。

```
Input : 

Matrix 1: (4x4)
Row Column Value
1   2       10
1   4       12
3   3       5
4   1       15
4   2       12

Matrix 2: (4X4)
Row Column Value
1   3       8
2   4       23
3   3       9
4   1       20
4   2       25

Output :

Result of Addition: (4x4)
Row Column Value
1   2      10
1   3      8
1   4      12
2   4      23
3   3      14
4   1      35
4   2      37

Result of Multiplication: (4x4)
Row Column Value
1   1      240
1   2      300
1   4      230
3   3      45
4   3      120
4   4      276

Result of transpose on the first matrix: (4x4)
Row Column Value
1   4      15
2   1      10
2   4      12
3   3      5
4   1      12

```

程序中任何地方使用的稀疏矩阵都是根据其行值排序的。具有相同行值的两个元素根据它们的列值进一步排序。

现在将**添加到**矩阵中，我们简单地逐个元素遍历这两个矩阵，并将较小的元素(行和列值较小的元素)插入到结果矩阵中。如果我们遇到具有相同行和列值的元素，我们只需将它们的值相加，并将相加的数据插入到结果矩阵中。

要将矩阵**转置**，我们可以简单地将每一列的值改为行的值，反之亦然，然而，在这种情况下，结果矩阵不会按照我们的要求进行排序。因此，我们最初确定的元素数量少于当前元素要插入的列，以便获得当前元素应该放置的结果矩阵的精确索引。这是通过维护数组索引[]来实现的，该索引的 ith 值表示矩阵中元素的数量少于列 I。

为了将矩阵相乘，我们首先计算第二个矩阵的转置，以简化比较并保持排序顺序。因此，结果矩阵是通过遍历两个矩阵的整个长度并对适当的相乘值求和而获得的。
第一个矩阵中等于 x 的任何行值和第二个矩阵中等于 y 的行值(转置的一个)将对结果[x][y]有贡献。这是通过将两个矩阵中具有列值的所有元素相乘，并只将第一个矩阵中行为 x，第二个转置矩阵中行为 y 的元素相加，得到结果[x][y]。

**例如:**考虑 2 个矩阵:

```
Row Col Val      Row Col Val
1   2   10       1   1   2
1   3   12       1   2   5
2   1   1        2   2   1
2   3   2        3   1   8

```

乘法后的结果矩阵将获得如下:

```
Transpose of second matrix:

Row Col Val      Row Col Val
1   2   10       1   1   2
1   3   12       1   3   8
2   1   1        2   1   5
2   3   2        2   2   1

Summation of multiplied values:

result[1][1] = A[1][3]*B[1][3] = 12*8 = 96
result[1][2] = A[1][2]*B[2][2] = 10*1 = 10
result[2][1] = A[2][1]*B[1][1] + A[2][3]*B[1][3] = 2*1 + 2*8 = 18
result[2][2] = A[2][1]*B[2][1] = 1*5 = 5

Any other element cannot be obtained 
by any combination of row in 
Matrix A and Row in Matrix B.

Hence the final resultant matrix will be:

Row Col Val 
1   1   96 
1   2   10 
2   1   18  
2   2   5  

```

以下是上述方法的实施:

## C++

```
// C++ code to perform add, multiply 
// and transpose on sparse matrices
#include <iostream>
using namespace std;

class sparse_matrix
{

    // Maximum number of elements in matrix
    const static int MAX = 100;

    // Double-pointer initialized by 
    // the constructor to store 
    // the triple-represented form
    int **data;

    // dimensions of matrix
    int row, col;

    // total number of elements in matrix
    int len;

public:
    sparse_matrix(int r, int c)
    {

        // initialize row
        row = r;

        // initialize col
        col = c;

        // initialize length to 0
        len = 0;

        //Array of Pointer to make a matrix
        data = new int *[MAX];

        // Array representation
        // of sparse matrix
        //[,0] represents row
        //[,1] represents col
        //[,2] represents value
        for (int i = 0; i < MAX; i++)
            data[i] = new int[3];
    }

    // insert elements into sparse matrix
    void insert(int r, int c, int val)
    {

        // invalid entry
        if (r > row || c > col)
        {
            cout << "Wrong entry";
        }
        else
        {

            // insert row value
            data[len][0] = r;

            // insert col value
            data[len][1] = c;

            // insert element's value
            data[len][2] = val;

            // increment number of data in matrix
            len++;
        }
    }

    void add(sparse_matrix b)
    {

        // if matrices don't have same dimensions
        if (row != b.row || col != b.col)
        {
            cout << "Matrices can't be added";
        }

        else
        {
            int apos = 0, bpos = 0;
            sparse_matrix result(row, col);

            while (apos < len && bpos < b.len)
            {

                // if b's row and col is smaller
                if (data[apos][0] > b.data[bpos][0] ||
                   (data[apos][0] == b.data[bpos][0] &&
                    data[apos][1] > b.data[bpos][1]))

                {

                    // insert smaller value into result
                    result.insert(b.data[bpos][0],
                                  b.data[bpos][1],
                                  b.data[bpos][2]);

                    bpos++;
                }

                // if a's row and col is smaller
                else if (data[apos][0] < b.data[bpos][0] ||
                        (data[apos][0] == b.data[bpos][0] &&
                         data[apos][1] < b.data[bpos][1]))

                {

                    // insert smaller value into result
                    result.insert(data[apos][0],
                                  data[apos][1],
                                  data[apos][2]);

                    apos++;
                }

                else
                {

                    // add the values as row and col is same
                    int addedval = data[apos][2] + 
                                 b.data[bpos][2];

                    if (addedval != 0)
                        result.insert(data[apos][0],
                                      data[apos][1],
                                      addedval);
                    // then insert
                    apos++;
                    bpos++;
                }
            }

            // insert remaining elements
            while (apos < len)
                result.insert(data[apos][0],
                              data[apos][1],
                              data[apos++][2]);

            while (bpos < b.len)
                result.insert(b.data[bpos][0],
                              b.data[bpos][1],
                              b.data[bpos++][2]);

            // print result
            result.print();
        }
    }

    sparse_matrix transpose()
    {

        // new matrix with inversed row X col
        sparse_matrix result(col, row);

        // same number of elements
        result.len = len;

        // to count number of elements in each column
        int *count = new int[col + 1];

        // initialize all to 0
        for (int i = 1; i <= col; i++)
            count[i] = 0;

        for (int i = 0; i < len; i++)
            count[data[i][1]]++;

        int *index = new int[col + 1];

        // to count number of elements having 
        // col smaller than particular i

        // as there is no col with value < 0
        index[0] = 0;

        // initialize rest of the indices
        for (int i = 1; i <= col; i++)

            index[i] = index[i - 1] + count[i - 1];

        for (int i = 0; i < len; i++)
        {

            // insert a data at rpos and 
            // increment its value
            int rpos = index[data[i][1]]++;

            // transpose row=col
            result.data[rpos][0] = data[i][1];

            // transpose col=row
            result.data[rpos][1] = data[i][0];

            // same value
            result.data[rpos][2] = data[i][2];
        }

        // the above method ensures
        // sorting of transpose matrix
        // according to row-col value
        return result;
    }

    void multiply(sparse_matrix b)
    {
        if (col != b.row)
        {

            // Invalid multiplication
            cout << "Can't multiply, Invalid dimensions";
            return;
        }

        // transpose b to compare row
        // and col values and to add them at the end
        b = b.transpose();
        int apos, bpos;

        // result matrix of dimension row X b.col
        // however b has been transposed,
        // hence row X b.row
        sparse_matrix result(row, b.row);

        // iterate over all elements of A
        for (apos = 0; apos < len;)
        {

            // current row of result matrix
            int r = data[apos][0];

            // iterate over all elements of B
            for (bpos = 0; bpos < b.len;)
            {

                // current column of result matrix
                // data[,0] used as b is transposed
                int c = b.data[bpos][0];

                // temporary pointers created to add all
                // multiplied values to obtain current
                // element of result matrix
                int tempa = apos;
                int tempb = bpos;

                int sum = 0;

                // iterate over all elements with
                // same row and col value
                // to calculate result[r]
                while (tempa < len && data[tempa][0] == r &&
                       tempb < b.len && b.data[tempb][0] == c)
                {
                    if (data[tempa][1] < b.data[tempb][1])

                        // skip a
                        tempa++;

                    else if (data[tempa][1] > b.data[tempb][1])

                        // skip b
                        tempb++;
                    else

                        // same col, so multiply and increment
                        sum += data[tempa++][2] * 
                             b.data[tempb++][2];
                }

                // insert sum obtained in result[r]
                // if its not equal to 0
                if (sum != 0)
                    result.insert(r, c, sum);

                while (bpos < b.len && 
                       b.data[bpos][0] == c)

                    // jump to next column
                    bpos++;
            }
            while (apos < len && data[apos][0] == r)

                // jump to next row
                apos++;
        }
        result.print();
    }

    // printing matrix
    void print()
    {
        cout << "\nDimension: " << row << "x" << col;
        cout << "\nSparse Matrix: \nRow\tColumn\tValue\n";

        for (int i = 0; i < len; i++)
        {
            cout << data[i][0] << "\t " << data[i][1] 
                 << "\t " << data[i][2] << endl;
        }
    }
};

// Driver Code
int main()
{

    // create two sparse matrices and insert values
    sparse_matrix a(4, 4);
    sparse_matrix b(4, 4);

    a.insert(1, 2, 10);
    a.insert(1, 4, 12);
    a.insert(3, 3, 5);
    a.insert(4, 1, 15);
    a.insert(4, 2, 12);
    b.insert(1, 3, 8);
    b.insert(2, 4, 23);
    b.insert(3, 3, 9);
    b.insert(4, 1, 20);
    b.insert(4, 2, 25);

    // Output result
    cout << "Addition: ";
    a.add(b);
    cout << "\nMultiplication: ";
    a.multiply(b);
    cout << "\nTranspose: ";
    sparse_matrix atranspose = a.transpose();
    atranspose.print();
}

// This code is contributed
// by Bharath Vignesh J K
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to perform add,
// multiply and transpose on sparse matrices

public class sparse_matrix {

    // Maximum number of elements in matrix
    int MAX = 100;

    // Array representation
    // of sparse matrix
    //[][0] represents row
    //[][1] represents col
    //[][2] represents value
    int data[][] = new int[MAX][3];

    // dimensions of matrix
    int row, col;

    // total number of elements in matrix
    int len;

    public sparse_matrix(int r, int c)
    {

        // initialize row
        row = r;

        // initialize col
        col = c;

        // initialize length to 0
        len = 0;
    }

    // insert elements into sparse matrix
    public void insert(int r, int c, int val)
    {

        // invalid entry
        if (r > row || c > col) {
            System.out.println("Wrong entry");
        }

        else {

            // insert row value
            data[len][0] = r;

            // insert col value
            data[len][1] = c;

            // insert element's value
            data[len][2] = val;

            // increment number of data in matrix
            len++;
        }
    }

    public void add(sparse_matrix b)
    {

        // if matrices don't have same dimensions
        if (row != b.row || col != b.col) {
            System.out.println("Matrices can't be added");
        }

        else {

            int apos = 0, bpos = 0;
            sparse_matrix result = new sparse_matrix(row, col);

            while (apos < len && bpos < b.len) {

                // if b's row and col is smaller
                if (data[apos][0] > b.data[bpos][0] || 
                  (data[apos][0] == b.data[bpos][0] && 
                   data[apos][1] > b.data[bpos][1]))

                {

                    // insert smaller value into result
                    result.insert(b.data[bpos][0],
                                  b.data[bpos][1],
                                  b.data[bpos][2]);

                    bpos++;
                }

                // if a's row and col is smaller
                else if (data[apos][0] < b.data[bpos][0] || 
                (data[apos][0] == b.data[bpos][0] && 
                  data[apos][1] < b.data[bpos][1]))

                {

                    // insert smaller value into result
                    result.insert(data[apos][0],
                                  data[apos][1],
                                  data[apos][2]);

                    apos++;
                }

                else {

                    // add the values as row and col is same
                    int addedval = data[apos][2] + b.data[bpos][2];

                    if (addedval != 0)
                        result.insert(data[apos][0],
                                      data[apos][1],
                                      addedval);
                    // then insert
                    apos++;
                    bpos++;
                }
            }

            // insert remaining elements
            while (apos < len)
                result.insert(data[apos][0],
                              data[apos][1],
                              data[apos++][2]);

            while (bpos < b.len)
                result.insert(b.data[bpos][0],
                              b.data[bpos][1],
                              b.data[bpos++][2]);

            // print result
            result.print();
        }
    }

    public sparse_matrix transpose()
    {

        // new matrix with inversed row X col
        sparse_matrix result = new sparse_matrix(col, row);

        // same number of elements
        result.len = len;

        // to count number of elements in each column
        int count[] = new int[col + 1];

        // initialize all to 0
        for (int i = 1; i <= col; i++)
            count[i] = 0;

        for (int i = 0; i < len; i++)
            count[data[i][1]]++;

        int[] index = new int[col + 1];

        // to count number of elements having col smaller
        // than particular i

        // as there is no col with value < 1
        index[1] = 0;

        // initialize rest of the indices
        for (int i = 2; i <= col; i++)

            index[i] = index[i - 1] + count[i - 1];

        for (int i = 0; i < len; i++) {

            // insert a data at rpos and increment its value
            int rpos = index[data[i][1]]++;

            // transpose row=col
            result.data[rpos][0] = data[i][1];

            // transpose col=row
            result.data[rpos][1] = data[i][0];

            // same value
            result.data[rpos][2] = data[i][2];
        }

        // the above method ensures
        // sorting of transpose matrix
        // according to row-col value
        return result;
    }

    public void multiply(sparse_matrix b)
    {

        if (col != b.row) {

            // Invalid multiplication
            System.out.println("Can't multiply, "
                               + "Invalid dimensions");

            return;
        }

        // transpose b to compare row
        // and col values and to add them at the end
        b = b.transpose();
        int apos, bpos;

        // result matrix of dimension row X b.col
        // however b has been transposed, hence row X b.row
        sparse_matrix result = new sparse_matrix(row, b.row);

        // iterate over all elements of A
        for (apos = 0; apos < len;) {

            // current row of result matrix
            int r = data[apos][0];

            // iterate over all elements of B
            for (bpos = 0; bpos < b.len;) {

                // current column of result matrix
                // data[][0] used as b is transposed
                int c = b.data[bpos][0];

                // temporary pointers created to add all
                // multiplied values to obtain current
                // element of result matrix
                int tempa = apos;
                int tempb = bpos;

                int sum = 0;

                // iterate over all elements with
                // same row and col value
                // to calculate result[r]
                while (tempa < len && data[tempa][0] == r
                       && tempb < b.len && b.data[tempb][0] == c) {

                    if (data[tempa][1] < b.data[tempb][1])

                        // skip a
                        tempa++;

                    else if (data[tempa][1] > b.data[tempb][1])

                        // skip b
                        tempb++;
                    else

                        // same col, so multiply and increment
                        sum += data[tempa++][2] * b.data[tempb++][2];
                }

                // insert sum obtained in result[r]
                // if its not equal to 0
                if (sum != 0)
                    result.insert(r, c, sum);

                while (bpos < b.len && b.data[bpos][0] == c)

                    // jump to next column
                    bpos++;
            }

            while (apos < len && data[apos][0] == r)

                // jump to next row
                apos++;
        }

        result.print();
    }

    // printing matrix
    public void print()
    {
        System.out.println("Dimension: " + row + "x" + col);
        System.out.println("Sparse Matrix: \nRow Column Value");

        for (int i = 0; i < len; i++) {

            System.out.println(data[i][0] + " " 
                             + data[i][1] + " " + data[i][2]);
        }
    }

    public static void main(String args[])
    {

        // create two sparse matrices and insert values
        sparse_matrix a = new sparse_matrix(4, 4);
        sparse_matrix b = new sparse_matrix(4, 4);

        a.insert(1, 2, 10);
        a.insert(1, 4, 12);
        a.insert(3, 3, 5);
        a.insert(4, 1, 15);
        a.insert(4, 2, 12);
        b.insert(1, 3, 8);
        b.insert(2, 4, 23);
        b.insert(3, 3, 9);
        b.insert(4, 1, 20);
        b.insert(4, 2, 25);

        // Output result
        System.out.println("Addition: ");
        a.add(b);
        System.out.println("\nMultiplication: ");
        a.multiply(b);
        System.out.println("\nTranspose: ");
        sparse_matrix atranspose = a.transpose();
        atranspose.print();
    }
}

// This code is contributed by Sudarshan Khasnis
```

## C#

```
// C# code to perform add, 
// multiply and transpose on sparse matrices 

public class sparse_matrix { 

    // Maximum number of elements in matrix 
    static int MAX = 100; 

    // Array representation 
    // of sparse matrix 
    //[,0] represents row 
    //[,1] represents col 
    //[,2] represents value 
    int[,] data = new int[MAX,3]; 

    // dimensions of matrix 
    int row, col; 

    // total number of elements in matrix 
    int len; 

    public sparse_matrix(int r, int c) 
    { 

        // initialize row 
        row = r; 

        // initialize col 
        col = c; 

        // initialize length to 0 
        len = 0; 
    } 

    // insert elements into sparse matrix 
    public void insert(int r, int c, int val) 
    { 

        // invalid entry 
        if (r > row || c > col) { 
            System.Console.WriteLine("Wrong entry"); 
        } 

        else { 

            // insert row value 
            data[len,0] = r; 

            // insert col value 
            data[len,1] = c; 

            // insert element's value 
            data[len,2] = val; 

            // increment number of data in matrix 
            len++; 
        } 
    } 

    public void add(sparse_matrix b) 
    { 

        // if matrices don't have same dimensions 
        if (row != b.row || col != b.col) { 
            System.Console.WriteLine("Matrices can't be added"); 
        } 

        else { 

            int apos = 0, bpos = 0; 
            sparse_matrix result = new sparse_matrix(row, col); 

            while (apos < len && bpos < b.len) { 

                // if b's row and col is smaller 
                if (data[apos,0] > b.data[bpos,0] || 
                (data[apos,0] == b.data[bpos,0] && 
                data[apos,1] > b.data[bpos,1])) 

                { 

                    // insert smaller value into result 
                    result.insert(b.data[bpos,0], 
                                b.data[bpos,1], 
                                b.data[bpos,2]); 

                    bpos++; 
                } 

                // if a's row and col is smaller 
                else if (data[apos,0] < b.data[bpos,0] || 
                (data[apos,0] == b.data[bpos,0] && 
                data[apos,1] < b.data[bpos,1])) 

                { 

                    // insert smaller value into result 
                    result.insert(data[apos,0], 
                                data[apos,1], 
                                data[apos,2]); 

                    apos++; 
                } 

                else { 

                    // add the values as row and col is same 
                    int addedval = data[apos,2] + b.data[bpos,2]; 

                    if (addedval != 0) 
                        result.insert(data[apos,0], 
                                    data[apos,1], 
                                    addedval); 
                    // then insert 
                    apos++; 
                    bpos++; 
                } 
            } 

            // insert remaining elements 
            while (apos < len) 
                result.insert(data[apos,0], 
                            data[apos,1], 
                            data[apos++,2]); 

            while (bpos < b.len) 
                result.insert(b.data[bpos,0], 
                            b.data[bpos,1], 
                            b.data[bpos++,2]); 

            // print result 
            result.print(); 
        } 
    } 

    public sparse_matrix transpose() 
    { 

        // new matrix with inversed row X col 
        sparse_matrix result = new sparse_matrix(col, row); 

        // same number of elements 
        result.len = len; 

        // to count number of elements in each column 
        int[] count = new int[col + 1]; 

        // initialize all to 0 
        for (int i = 1; i <= col; i++) 
            count[i] = 0; 

        for (int i = 0; i < len; i++) 
            count[data[i,1]]++; 

        int[] index = new int[col + 1]; 

        // to count number of elements having col smaller 
        // than particular i 

        // as there is no col with value < 1 
        index[1] = 0; 

        // initialize rest of the indices 
        for (int i = 2; i <= col; i++) 

            index[i] = index[i - 1] + count[i - 1]; 

        for (int i = 0; i < len; i++) { 

            // insert a data at rpos and increment its value 
            int rpos = index[data[i,1]]++; 

            // transpose row=col 
            result.data[rpos,0] = data[i,1]; 

            // transpose col=row 
            result.data[rpos,1] = data[i,0]; 

            // same value 
            result.data[rpos,2] = data[i,2]; 
        } 

        // the above method ensures 
        // sorting of transpose matrix 
        // according to row-col value 
        return result; 
    } 

    public void multiply(sparse_matrix b) 
    { 

        if (col != b.row) { 

            // Invalid multiplication 
            System.Console.WriteLine("Can't multiply, "
                            + "Invalid dimensions"); 

            return; 
        } 

        // transpose b to compare row 
        // and col values and to add them at the end 
        b = b.transpose(); 
        int apos, bpos; 

        // result matrix of dimension row X b.col 
        // however b has been transposed, hence row X b.row 
        sparse_matrix result = new sparse_matrix(row, b.row); 

        // iterate over all elements of A 
        for (apos = 0; apos < len;) { 

            // current row of result matrix 
            int r = data[apos,0]; 

            // iterate over all elements of B 
            for (bpos = 0; bpos < b.len;) { 

                // current column of result matrix 
                // data[,0] used as b is transposed 
                int c = b.data[bpos,0]; 

                // temporary pointers created to add all 
                // multiplied values to obtain current 
                // element of result matrix 
                int tempa = apos; 
                int tempb = bpos; 

                int sum = 0; 

                // iterate over all elements with 
                // same row and col value 
                // to calculate result[r] 
                while (tempa < len && data[tempa,0] == r 
                    && tempb < b.len && b.data[tempb,0] == c) { 

                    if (data[tempa,1] < b.data[tempb,1]) 

                        // skip a 
                        tempa++; 

                    else if (data[tempa,1] > b.data[tempb,1]) 

                        // skip b 
                        tempb++; 
                    else

                        // same col, so multiply and increment 
                        sum += data[tempa++,2] * b.data[tempb++,2]; 
                } 

                // insert sum obtained in result[r] 
                // if its not equal to 0 
                if (sum != 0) 
                    result.insert(r, c, sum); 

                while (bpos < b.len && b.data[bpos,0] == c) 

                    // jump to next column 
                    bpos++; 
            } 

            while (apos < len && data[apos,0] == r) 

                // jump to next row 
                apos++; 
        } 

        result.print(); 
    } 

    // printing matrix 
    public void print() 
    { 
        System.Console.WriteLine("Dimension: " + row + "x" + col); 
        System.Console.WriteLine("Sparse Matrix: \nRow Column Value"); 

        for (int i = 0; i < len; i++) { 

            System.Console.WriteLine(data[i,0] + " "
                            + data[i,1] + " " + data[i,2]); 
        } 
    } 

    public static void Main() 
    { 

        // create two sparse matrices and insert values 
        sparse_matrix a = new sparse_matrix(4, 4); 
        sparse_matrix b = new sparse_matrix(4, 4); 

        a.insert(1, 2, 10); 
        a.insert(1, 4, 12); 
        a.insert(3, 3, 5); 
        a.insert(4, 1, 15); 
        a.insert(4, 2, 12); 
        b.insert(1, 3, 8); 
        b.insert(2, 4, 23); 
        b.insert(3, 3, 9); 
        b.insert(4, 1, 20); 
        b.insert(4, 2, 25); 

        // Output result 
        System.Console.WriteLine("Addition: "); 
        a.add(b); 
        System.Console.WriteLine("\nMultiplication: "); 
        a.multiply(b); 
        System.Console.WriteLine("\nTranspose: "); 
        sparse_matrix atranspose = a.transpose(); 
        atranspose.print(); 
    } 
} 

// This code is contributed by mits
```

**Output:**

```
Addition: 
Dimension: 4x4
Sparse Matrix: 
Row Column Value
1 2 10
1 3 8
1 4 12
2 4 23
3 3 14
4 1 35
4 2 37

Multiplication: 
Dimension: 4x4
Sparse Matrix: 
Row Column Value
1 1 240
1 2 300
1 4 230
3 3 45
4 3 120
4 4 276

Transpose: 
Dimension: 4x4
Sparse Matrix: 
Row Column Value
1 4 15
2 1 10
2 4 12
3 3 5
4 1 12

```

**最坏情况时间复杂度:**加法运算线性遍历矩阵，因此时间复杂度为 O(n)，其中 n 是两个矩阵中较大矩阵中非零元素的数量。转置的时间复杂度为 O(n+m)，其中 n 是列数，m 是矩阵中非零元素的个数。然而，乘法的时间复杂度为 O(x*n + y*m)，其中(x，m)是第二矩阵中的列数和项数；和(y，n)是第一矩阵中的行数和项数。