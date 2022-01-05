# c++中向量相对于数组的优势

> 原文:[https://www . geeksforgeeks . org/c 中矢量相对于阵列的优势/](https://www.geeksforgeeks.org/advantages-of-vector-over-array-in-c/)

我们已经讨论了[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)和[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。在这篇文章中，我们将讨论向量相对于正规数组的优势。

**向量相对于数组的优势**:

1.  Vector 是 ***模板类*** 并且是 ***C++只构造*** 而数组是 ***内置语言构造*** 并且在 C 和 C++中都存在。
2.  向量实现为 ***动态数组*与*列表接口*** 而数组可以实现为 ***静态或动态*** 与 ***原始数据类型*** 接口。

    ```
    #include <bits/stdc++.h>
    using namespace std;

    int main()
    {
        int array[100]; // Static Implementation
        int* arr = new int[100]; // Dynamic Implementation
        vector<int> v; // Vector's Implementation
        return 0;
    }
    ```

3.  **Size of arrays are *fixed*** whereas the **vectors are *resizable*** i.e they can grow and shrink as vectors are allocated on heap memory.

    ```
    #include <bits/stdc++.h>
    using namespace std;

    int main()
    {
        int array[100]; // Static Implementation

        cout << "Size of Array " << sizeof(array) / sizeof(array[0]) << "\n";

        vector<int> v; // Vector's Implementation

        // Inserting Values in Vector
        v.push_back(1);
        v.push_back(2);
        v.push_back(3);
        v.push_back(4);
        v.push_back(5);

        cout << "Size of vector Before Removal=" << v.size() << "\n";

        // Output Values of vector
        for (auto it : v)
            cout << it << " ";

        v.erase(v.begin() + 2); // Remove 3rd element

        cout << "\nSize of vector After removal=" << v.size() << "\n";

        // Output Values of vector
        for (auto it : v)
            cout << it << " ";

        return 0;
    }
    ```

    **输出**:

    ```
    Size of Array 100
    Size of vector Before Removal=5
    1 2 3 4 5 
    Size of vector After removal=4
    1 2 4 5

    ```

4.  如果动态定义，数组**必须被*显式解除分配*** ，而向量是 ***自动从堆内存中解除分配*** 。

    ```
    #include <bits/stdc++.h>
    using namespace std;

    int main()
    {
        int* arr = new int[100]; // Dynamic Implementation
        delete[] arr; // array Explicitly deallocated

        vector<int> v; // Automatic deallocation when variable goes out of scope
        return 0;
    }
    ```

5.  如果**动态分配**，则无法确定数组**的大小**，而矢量的大小可以在**0(1)时间**内确定。
6.  When arrays are passed to a function, a **separate parameter for size is also passed** whereas in case of passing a vector to a function, there is no such need as **vector maintains variables which keeps track of size of container at all times**.

    ```
    #include <bits/stdc++.h>
    using namespace std;

    int main()
    {
        int* arr = new int[100]; // Dynamic Implementation

        cout << "Size of array= ";
        cout << sizeof(arr) / sizeof(*arr) << "\n"; // Pointer cannot be used to get size of
        // block pointed by it
        return 0;
    }
    ```

    **输出**:

    ```
    Size of array= 2

    ```

7.  当数组变满并插入新元素时；**不隐式进行重新分配**而当向量变得大于其容量时，隐式进行重新分配。
8.  **Arrays *cannot be returned **unless dynamically allocated*** from a function** whereas v**ectors *can be returned* from a function**.

    ```
    // Program to demonstrate arrays cannot be returned
    #include <bits/stdc++.h>
    using namespace std;

    int* getValues()
    {

        int arr[10]; // Array defined locally
        for (int i = 0; i < 10; i++) // Putting Values in array
            arr[i] = i + 1;

        return arr; // returning pointer to array
    }

    // main function
    int main()
    {

        int* array; // pointer of int type

        array = getValues(); // Call function to get arr

        for (int i = 0; i < 10; i++) { // Printing Values
            cout << "*(array + " << i << ") : ";
            cout << *(array + i) << endl;
        }

        return 0;
    }
    ```

    **输出**:

    ```
    warning: address of local variable 'arr' returned [-Wreturn-local-addr]
    Segmentation Fault (SIGSEGV)

    ```

    ```
    // Program to demonstrate vector can be returned
    #include <bits/stdc++.h>
    using namespace std;

    // Function returning vector
    vector<int> getValues()
    {

        vector<int> v; // Vector defined locally
        for (int i = 0; i < 10; i++) // Inserting values in Vector
            v.push_back(i + 1);

        return v; // returning pointer to array
    }

    // main function
    int main()
    {

        vector<int> get;

        get = getValues(); // Call function to get v

        // Output Values of vector
        for (auto it : get)
            cout << it << " ";

        return 0;
    }
    ```

    **输出**:

    ```
    1 2 3 4 5 6 7 8 9 10 

    ```

9.  Arrays cannot be copied or assigned directly whereas Vectors can be copied or assigned directly.

    ```
    #include <bits/stdc++.h>
    using namespace std;

    // main function
    int main()
    {
        vector<int> v; // Vector defined locally
        for (int i = 0; i < 10; i++)
            v.push_back(i + 1);

        vector<int> get;

        get = v; // Copying vector v into vector get

        cout << "vector get:\n";
        for (auto it : get)
            cout << it << " ";

        int arr[10];
        for (int i = 0; i < 10; i++) // Putting Values in array
            arr[i] = i + 1;

        int copyArr[10];

        copyArr = arr; // Error

        return 0;
    }
    ```

    **输出**:

    ```
    vector get:
    1 2 3 4 5 6 7 8 9 10

    error: invalid array assignment
        copyArr=arr;

    ```