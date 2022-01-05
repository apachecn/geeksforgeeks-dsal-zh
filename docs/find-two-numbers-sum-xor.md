# 从两个数的和中找出两个数并异或

> 原文:[https://www.geeksforgeeks.org/find-two-numbers-sum-xor/](https://www.geeksforgeeks.org/find-two-numbers-sum-xor/)

给定两个数 **X** 和 **Y** 的和与异或![\in [0, 2^{64}-1]](img/277bd3945096ff73874fa5d5f16ddbf5.png "Rendered by QuickLaTeX.com")，我们需要找到使 **X** 的值最小的数。

**示例:**

```
Input : S = 17
        X = 13
Output : a = 2
         b = 15

Input : S = 1870807699 
        X = 259801747
Output : a = 805502976
         b = 1065304723

Input : S = 1639
        X = 1176
Output : No such numbers exist

```

> **使用的变量:**
> X == >两个数的异或
> S == >两个数的和
> X[I]= =>X 中第 I 位的值
> S[I]=>S 中第 I 位的值

一个**简单的解决方案**是用给定的异或生成所有可能的对。要生成所有对，我们可以遵循以下规则。

1.  如果 X[i]是 1，那么 a[i]和 b[i]应该是不同的，我们有两种情况。
2.  If X[i] is 0, then both a[i] and b[i] should be same. we have two cases.

    所以我们生成 2^n 可能对，其中 n 是 x 中的位数，然后对于每一对，我们检查它的和是否为 s。

    一个**有效的解决方案**是基于以下事实。

    > S = X + 2*A
    > 其中 A = a 和 b
    > 
    > 我们可以使用求和过程来验证上述事实。总之，每当我们看到两个位都为 1(即 and 为 1)时，我们将结果位设为 0，并将 1 相加作为进位，这意味着 AND 中的每个位都左移 1，AND 的 OR 值乘以 2 并相加。

    所以我们可以找到 A =(S–X)/2。

    一旦我们找到 A，我们就可以使用下面的规则找到‘A’和‘b’的所有位。

    1.  如果 X[i] = 0，A[i] = 0，那么 a[i] = b[i] = 0。这一点只有一种可能。
    2.  如果 X[i] = 0，A[i] = 1，那么 a[i] = b[i] = 1。这一点只有一种可能。
    3.  如果 X[i] = 1 和 A[i] = 0，那么(a[i] = 1 和 b[i] = 0)或(a[i] = 0 和 b[i] = 1)，我们可以选择这两者中的任何一个。
    4.  如果 X[i] = 1 且 A[i] = 1，则结果不可能(注意 X[i] = 1 表示不同的位)

    设求和为 S，异或为 x。

    下面是上述方法的实现:

    ## C++

    ```
    // CPP program to find two numbers with
    // given Sum and XOR such that value of
    // first number is minimum.
    #include <iostream>
    using namespace std;

    // Function that takes in the sum and XOR
    // of two numbers and generates the two 
    // numbers such that the value of X is
    // minimized
    void compute(unsigned long int S, 
                unsigned long int X)
    {
        unsigned long int A = (S - X)/2;

        int a = 0, b = 0;

        // Traverse through all bits
        for (int i=0; i<8*sizeof(S); i++)
        {
            unsigned long int Xi = (X & (1 << i));
            unsigned long int Ai = (A & (1 << i));
            if (Xi == 0 && Ai == 0)
            {
                // Let us leave bits as 0.
            }
            else if (Xi == 0 && Ai > 0)
            {
                a = ((1 << i) | a); 
                b = ((1 << i) | b); 
            }
            else if (Xi > 0 && Ai == 0)
            {
                a = ((1 << i) | a); 

                // We leave i-th bit of b as 0.
            }
            else // (Xi == 1 && Ai == 1)
            {
                cout << "Not Possible";
                return;
            }
        }

        cout << "a = " << a << endl << "b = " << b;
    }

    // Driver function
    int main()
    {
        unsigned long int S = 17, X = 13;
        compute(S, X);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to find two numbers with 
    // given Sum and XOR such that value of 
    // first number is minimum. 
    class GFG {

    // Function that takes in the sum and XOR 
    // of two numbers and generates the two 
    // numbers such that the value of X is 
    // minimized 
    static void compute(long S, long  X) 
    { 
        long A = (S - X)/2; 
        int a = 0, b = 0; 
            final int LONG_FIELD_SIZE     = 8;

        // Traverse through all bits 
        for (int i=0; i<8*LONG_FIELD_SIZE; i++) 
        { 
            long Xi = (X & (1 << i)); 
            long Ai = (A & (1 << i)); 
            if (Xi == 0 && Ai == 0) 
            { 
                // Let us leave bits as 0. 
            } 
            else if (Xi == 0 && Ai > 0) 
            { 
                a = ((1 << i) | a); 
                b = ((1 << i) | b); 
            } 
            else if (Xi > 0 && Ai == 0) 
            { 
                a = ((1 << i) | a); 

                // We leave i-th bit of b as 0. 
            } 
            else // (Xi == 1 && Ai == 1) 
            { 
                System.out.println("Not Possible"); 
                return; 
            } 
        } 

        System.out.println("a = " + a +"\nb = " + b); 
    } 

    // Driver function 
        public static void main(String[] args) {
            long S = 17, X = 13; 
        compute(S, X); 

        }
    }
    // This code is contributed by RAJPUT-JI
    ```

    ## 蟒蛇 3

    ```
    # Python program to find two numbers with
    # given Sum and XOR such that value of
    # first number is minimum.

    # Function that takes in the sum and XOR
    # of two numbers and generates the two 
    # numbers such that the value of X is
    # minimized
    def compute(S, X):
        A = (S - X)//2
        a = 0
        b = 0

        # Traverse through all bits
        for i in range(64):
            Xi = (X & (1 << i))
            Ai = (A & (1 << i))
            if (Xi == 0 and Ai == 0):
                # Let us leave bits as 0.
                pass

            elif (Xi == 0 and Ai > 0):
                a = ((1 << i) | a) 
                b = ((1 << i) | b) 

            elif (Xi > 0 and Ai == 0):
                a = ((1 << i) | a) 
                # We leave i-th bit of b as 0.

            else: # (Xi == 1 and Ai == 1)
                print("Not Possible")
                return

        print("a = ",a)
        print("b =", b)

    # Driver function
    S = 17
    X = 13
    compute(S, X)

    # This code is contributed by ankush_953
    ```

    ## C#

    ```
    // C# program to find two numbers with 
    // given Sum and XOR such that value of 
    // first number is minimum. 
    using System;

    public class GFG {

    // Function that takes in the sum and XOR 
    // of two numbers and generates the two 
    // numbers such that the value of X is 
    // minimized 
    static void compute(long S, long  X) 
    { 
        long A = (S - X)/2; 
        int a = 0, b = 0; 

        // Traverse through all bits 
        for (int i=0; i<8*sizeof(long); i++) 
        { 
            long Xi = (X & (1 << i)); 
            long Ai = (A & (1 << i)); 
            if (Xi == 0 && Ai == 0) 
            { 
                // Let us leave bits as 0. 
            } 
            else if (Xi == 0 && Ai > 0) 
            { 
                a = ((1 << i) | a); 
                b = ((1 << i) | b); 
            } 
            else if (Xi > 0 && Ai == 0) 
            { 
                a = ((1 << i) | a); 

                // We leave i-th bit of b as 0. 
            } 
            else // (Xi == 1 && Ai == 1) 
            { 
                Console.WriteLine("Not Possible"); 
                return; 
            } 
        } 

        Console.WriteLine("a = " + a +"\nb = " + b); 
    } 

    // Driver function 
        public static void Main() {
            long S = 17, X = 13; 
            compute(S, X); 
        }
    }
    // This code is contributed by RAJPUT-JI
    ```

    **Output**

    ```
    a = 15
    b = 2

    ```

    上述方法的时间复杂度![O(b)](img/c76fa0ae4ab2b539e7c29db6d8cc7038.png "Rendered by QuickLaTeX.com")，其中 b 是 s 中的位数