# 如何在 Java 中左右旋转数组？

> 原文:[https://www . geesforgeks . org/如何在 java 中向左或向右旋转数组/](https://www.geeksforgeeks.org/how-to-left-or-right-rotate-an-array-in-java/)

给定一个大小为 **N** 和 **D** 索引的数组 **arr[]** ，任务是按照 **D** 索引旋转数组。我们有两种灵活性，可以通过不同的方式向左或向右旋转，我们将通过在两个旋转中实现每种旋转方式来探索。

**方式:**

1.  使用临时数组
2.  逐个递归旋转数组
3.  使用杂耍算法

### **阵列向左旋转**

插图:

```
Input  : arr[] = {1, 2, 3, 4, 5} 
D = 2 
Output : 3 4 5 1 2 
```

**输出解释:**

*   初始数组[1，2，3，4，5]
*   旋转第一个索引[2，3，4，5，1]
*   旋转第二个索引[3，4，5，1，2]

```
Input : arr[] = {10, 34, 56, 23, 78, 12, 13, 65} 
D = 7 
Output: 65 10 34 56 23 78 12 13 
```

**方式 1:** 使用临时数组

**进场:**

在此方法中，只需创建一个临时数组，并将数组 arr[]的元素从 0 复制到第(D-1)个索引。在移动之后，数组的其余元素从索引 D 到 n 排列[]。然后将临时数组元素移动到原始数组。

```
Input arr[] = [1, 2, 3, 4, 5] 
D = 2 
```

*   将前 d 个元素存储在临时数组中: **temp[] = [1，2]**
*   转移 arr[]的剩余部分: **arr[] = [3，4，5]**
*   回存 D 元素: **arr[] = [3，4，5，1，2]**

**示例:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Left Rotate an Array
// by D elements

// Main class
class GFG {

    // Method 1
    // To left rotate arr[]
    // of size N by D
    void leftRotate(int arr[], int d, int n)
    {
        // Creating temp array of size d
        int temp[] = new int[d];

        // Copying first d element in array temp
        for (int i = 0; i < d; i++)
            temp[i] = arr[i];

        // Moving the rest element to index
        // zero to N-d
        for (int i = d; i < n; i++) {
            arr[i - d] = arr[i];
        }

        // Copying the temp array element
        // in origninal array
        for (int i = 0; i < d; i++) {
            arr[i + n - d] = temp[i];
        }
    }

    // Method 2
    // To print an array
    void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Method 3
    // Main driver method
    public static void main(String[] args)
    {
        // Creating an object of class inside main()
        GFG rotate = new GFG();

        // Custom input array
        int arr[] = { 1, 2, 3, 4, 5 };

        // Calling method 1 and 2 as defined above
        rotate.leftRotate(arr, 2, arr.length);
        rotate.printArray(arr, arr.length);
    }
}
```

**Output**

```
3 4 5 1 2 
```

> ***时间复杂度:**O(N)**辅助空间:** O(D)*

**方式二:**逐个旋转

**进场:**

将数组递归地旋转一个元素

```
Input arr[] = [1, 2, 3, 4, 5]
D = 21
```

*   将 arr[0]替换为 arr[1]
*   将 arr[1]替换为 arr[2]
*   将 arr[N-1]替换为 arr[N]
*   重复 1、2、3 到 D 次

为了旋转 1，将 arr[0]存储在临时变量 temp 中，将 arr[1]移动到 arr[0]，将 arr[2]移动到 arr[1]，最后将 temp 移动到 arr[n-1]

插图:

> 让我们举同一个例子 arr[] = [1，2，3，4，5]，d = 2
> 将 arr[]旋转一个 2 倍
> 第一次旋转后我们得到[2，3，4，5，1]，第二次旋转后得到[ 3，4，5，1，2]。

**例**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to left rotate an array
// by Rotate one by one

// Main class
class GFG {

    // Method 1
    // To rotate left by D elements
    void leftRotate(int arr[], int d, int n)
    {
        for (int i = 0; i < d; i++)
            leftRotatebyOne(arr, n);
    }

    // Method 2
    // To rotate left one by one
    void leftRotatebyOne(int arr[], int n)
    {
        int i, temp;
        temp = arr[0];
        for (i = 0; i < n - 1; i++)
            arr[i] = arr[i + 1];
        arr[i] = temp;
    }

    // Method 3
    // To print an array
    void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Method 4
    // Main driver method
    public static void main(String[] args)
    {
        // Creating object of class inside main()
        GFG rotate = new GFG();

        // Custom input array
        int arr[] = { 1, 2, 3, 4, 5 };

        // Calling method to rotate array leftwards
        // and later printing the array elements
        rotate.leftRotate(arr, 2, arr.length);
        rotate.printArray(arr, arr.length);
    }
}
```

**Output**

```
3 4 5 1 2 
```

> ***时间复杂度:**O(N * D)**辅助空间:** O(1)*

**方式三:**使用杂耍算法

**进场:**

这是方法 2 的扩展。不要一个接一个地移动，而是将数组分成不同的集合，集合的数量等于 n 和 d 的 GCD，并在集合内移动元素。

> 对于上面的示例数组(n = 5 和 d = 2)，如果 GCD 为 1，那么元素将仅在一个集合内移动，我们只需从 temp = arr[0]开始，并继续将 arr[I+d]移动到 arr[I]，最后将 temp 存储在正确的位置。

**示例:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to left rotate an array by d elements
// using Juggling Algorithm

// Main class
class GFG {

    // Method 1
    // To left rotate arr[] of siz N by D
    void leftRotate(int arr[], int d, int n)
    {
        // To handle if d >= n
        d = d % n;
        int i, j, k, temp;
        int g_c_d = gcd(d, n);

        for (i = 0; i < g_c_d; i++) {

            // move i-th values of blocks
            temp = arr[i];
            j = i;

            // Performing sets of operations if
            // condition holds true
            while (true) {
                k = j + d;
                if (k >= n)
                    k = k - n;
                if (k == i)
                    break;
                arr[j] = arr[k];
                j = k;
            }
            arr[j] = temp;
        }
    }

    // Method 2
    // To print an array
    void printArray(int arr[], int size)
    {
        int i;
        for (i = 0; i < size; i++)
            System.out.print(arr[i] + " ");
    }

    // Method 3
    // To get gcd of a and b
    int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        else
            return gcd(b, a % b);
    }

    // Method 4
    // main driver method
    public static void main(String[] args)
    {
        // Creating instance of class inside main() method
        GFG rotate = new GFG();

        // Custom array elements
        int arr[] = { 1, 2, 3, 4, 5 };

        // Calling above methods inside main() to
        // left rotate and print the array elements
        rotate.leftRotate(arr, 2, arr.length);
        rotate.printArray(arr, arr.length);
    }
}
```

**Output**

```
3 4 5 1 2 
```

> ***时间复杂度:**O(n)**辅助空间:** O(1)*

## 数组的右旋转

插图:

```
Input  : arr[] = {1, 2, 3, 4, 5} 
         D = 2
Output : 4 5 1 2 3 
```

**输出解释:**

*   初始数组[1，2，3，4，5]
*   旋转第一个索引[2，3，4，5，1]
*   旋转第二个索引[3，4，5，1，2]
*   旋转第三个索引[4，5，1，2，3]

```
Input: arr[] : {10, 34, 56, 23, 78, 12, 13, 65} 
               D = 5 
Output       : 56 23 78 12 13 65 10 34  
```

**方式 1:** 使用温度数组

**进场:**

在此方法中，只需创建一个临时数组，并将数组 arr[]的元素从 0 复制到**N–D**索引。在移动之后，数组的其余元素从索引 D 到 n 排列[]。然后将临时数组元素移动到原始数组。如下图所示:

```
Input arr[] = [1, 2, 3, 4, 5], D = 2
1) Store the first d elements in a temp array
   temp[] = [1, 2, 3]
2) Shift rest of the arr[]
   arr[] = [4, 5]
3) Store back the D elements
   arr[] = [4, 5, 1, 2, 3]
```

**示例:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rotate an array by D elements

// Main class
class GFG {

    // Method 1
    // To right rotate arr[] of size N by D
    void rightRotate(int arr[], int d, int n)
    {

        // If arr is rotated n times then
        // you get the same array
        while (d > n) {
            d = d - n;
        }

        // Creating a temporary array of size d
        int temp[] = new int[n - d];

        // Now copying first N-D element in array temp
        for (int i = 0; i < n - d; i++)
            temp[i] = arr[i];

        // Moving the rest element to index zero to D
        for (int i = n - d; i < n; i++) {
            arr[i - n + d] = arr[i];
        }

        // Copying the temp array element
        // in origninal array
        for (int i = 0; i < n - d; i++) {
            arr[i + d] = temp[i];
        }
    }

    // Method 2
    // To print an array
    void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)

            // Printing elements of an array
            System.out.print(arr[i] + " ");
    }

    // Method 3
    // Main driver method
    public static void main(String[] args)
    {

        // Creating object of class inside main() method
        GFG rotate = new GFG();

        // Custom input array
        int arr[] = { 1, 2, 3, 4, 5 };

        // Calling method1 to rotate array
        rotate.rightRotate(arr, 2, arr.length);

        // Calling method 2 to print array
        rotate.printArray(arr, arr.length);
    }
}
```

**Output**

```
4 5 1 2 3 
```