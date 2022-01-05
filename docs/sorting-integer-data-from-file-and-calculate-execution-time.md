# 从文件中排序整数数据，计算执行时间

> 原文:[https://www . geesforgeks . org/sorting-integer-data-from-file-and-compute-execution-time/](https://www.geeksforgeeks.org/sorting-integer-data-from-file-and-calculate-execution-time/)

**先决条件:** [选择排序](https://www.geeksforgeeks.org/selection-sort/)

在本文中，我们将应用选择排序算法，其中输入的来源是**一个包含 10000 个整数的文件**，输出将是排序所花费的总时间。

 **要使用的重要功能:**

*   **rand():** 用于生成随机数。
*   **fopen():** 用于打开文件。
*   **fscanf():** 用于扫描文件中的数据。
*   **时钟():**返回时钟周期数

**在文件“random.txt”中生成随机数的程序**

```
// C program to generate random numbers
#include <stdio.h>
#include <stdlib.h>

// Driver program
int main(void)
{
    // This program will create same sequence of
    // random numbers on every program run
    FILE* fptr;

    // creating a file "random.txt" in "write" mode
    fptr = fopen("random.txt", "w"); 
    int i;
    if (fptr == NULL) {
        printf("ERROR");
        exit(1);
    }

    for (i = 0; i < 10000; i++) {

        // to generate number less than 100000
        int val = rand() % 100000; 

        // storing data to file
        fprintf(fptr, "%d ", val); 
    }

    // closing the file
    fclose(fptr); 
    printf("numbers generated successfully !! ");
    return 0;
}
```

*   **clock_t** 或 clock ticks 是具有恒定但系统特定长度的时间单位，如函数 Clock 返回的时间单位。

**该程序的算法:**

1.  使用 fopen()打开文件。
2.  使用 fscanf()扫描文件并将其复制到阵列中。
3.  应用任何你想要的排序算法。
4.  打印到控制台。

**以下是上述算法的实现。**

```
#include <stdio.h>
#include <time.h>
int main()
{

    // data type for calculating time
    clock_t starttime, endtime; 

    // variable for calculating total time of execution
    double totaltime; 
    int i = 0, j, n = 0, min, index;

    // declaring array to store data from file
    int arr[100000];

    // declaring file pointer  
    FILE* fptr; 

    // opening the integer file.
    fptr = fopen("random.txt", "r"); 

    // scanning integer from file to array
    while (fscanf(fptr, "%d", &arr[i]) == 1) 
    {

        // for counting the number of elements
        n++; 

        // for incrementing the array index
        i++; 
    }

    // logic for selection sort....
    // starts here...

    // calculating clock when sorting starts..
    starttime = clock(); 
    printf("start time : %f\n", (float)starttime);
    for (i = 0; i < n - 1; i++) {
        min = arr[i];
        for (j = i + 1; j < n; j++) {
            if (arr[j] < min) {
                min = arr[j];
                index = j;
            }
        }

        // swapping the smallest number with 
        // the current arr[i]th value
        int temp = arr[i];
        arr[i] = min;
        arr[index] = temp;
    }
    // selection sort logic ends here

    // calculating clock when sorting  ends
    endtime = clock(); 
    printf("%f\n", (float)endtime);

    totaltime = ((double)(endtime - starttime)) / CLOCKS_PER_SEC;

    // printing the sorted array...
    for (i = 0; i < n; i++)
        printf("%d ", arr[i]);

    printf("\n\nendtime : %f\n", (float)endtime);
    printf("\n\ntotal time of execution = %f", totaltime);

    return 0;
}
```

**参考文献:**

*   [https://www.geeksforgeeks.org/selection-sort/](https://www.geeksforgeeks.org/selection-sort/)
*   [https://www . geesforgeks . org/如何测量 c 中程序花费的时间/](https://www.geeksforgeeks.org/how-to-measure-time-taken-by-a-program-in-c/)
*   [https://www.geeksforgeeks.org/basics-file-handling-c/](https://www.geeksforgeeks.org/basics-file-handling-c/)