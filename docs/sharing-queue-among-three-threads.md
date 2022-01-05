# 在三个线程之间共享一个队列

> 原文:[https://www . geesforgeks . org/sharing-三线程队列/](https://www.geeksforgeeks.org/sharing-queue-among-three-threads/)

根据给定的规范，在三个线程 A、B、C 之间共享一个队列:

*   线程 A 生成随机整数，并将它们推入共享队列。
*   线程 B 和 C 相互竞争，从队列中抓取一个整数。
*   线程 B 和 C 计算它们从队列中获取的整数之和。
*   比较乙和丙计算的总和。最大的是赢家。

**先决条件:-** [多线程](https://www.geeksforgeeks.org/multithreading-c-2/)

**方法:-** 创建一个在所有三个线程间共享的全局队列。首先创建所有三个线程，并调用与它们相关联的相应函数。

*   **producter fun**生成随机数并将其推入队列
*   **add_B** 函数复制线程 B，并消耗一定数量的队列。
*   **add_C** 函数复制线程 C，并消耗一定数量的队列。

***注意:-*** 每个函数都有互斥锁，避免任何争用情况。

## C++

```
// CPP program to demonstrate the given task
#include <iostream>
#include <pthread.h>
#include <queue>
#include <stdlib.h>

#define MAX 10

using namespace std;

// Declaring global variables
int sum_B = 0, sum_C = 0;
int consumerCount1 = 0;
int consumerCount2 = 0;

// Shared queue
queue<int> Q;

// Function declaration of all required functions
void* producerFun(void*);
void* add_B(void*);
void* add_C(void*);

// Getting the mutex
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

pthread_cond_t dataNotProduced =
                    PTHREAD_COND_INITIALIZER;
pthread_cond_t dataNotConsumed =
                    PTHREAD_COND_INITIALIZER;

// Function to generate random numbers and
// push them into queue using thread A

void* producerFun(void*)
{
    static int producerCount = 0;

    // Initialising the seed
    srand(time(NULL));

    while (1) {
        // Getting the lock on queue using mutex
        pthread_mutex_lock(&mutex);

        if (Q.size() < MAX && producerCount < MAX)
        {

            // Getting the random number
            int num = rand() % 10 + 1;
            cout << "Produced:  " << num << endl;

            // Pushing the number into queue
            Q.push(num);

            producerCount++;

            pthread_cond_broadcast(&dataNotProduced);
        }

        // If queue is full, release the lock and return
        else if (producerCount == MAX) {
            pthread_mutex_unlock(&mutex);
            return NULL;
        }

        // If some other thread is executing, wait
        else {
            cout << ">> Producer is in wait.." << endl;
            pthread_cond_wait(&dataNotConsumed, &mutex);
        }

        // Get the mutex unlocked
        pthread_mutex_unlock(&mutex);
    }
}

// Function definition for consumer thread B
void* add_B(void*)
{

    while (1) {

        // Getting the lock on queue using mutex
        pthread_mutex_lock(&mutex);

        // Pop only when queue has at least 1 element
        if (Q.size() > 0) {
            // Get the data from the front of queue
            int data = Q.front();

            cout << "B thread consumed: " << data << endl;

            // Add the data to the integer variable
            // associated with thread B
            sum_B += data;

            // Pop the consumed data from queue
            Q.pop();

            consumerCount1++;

            pthread_cond_signal(&dataNotConsumed);
        }

        // Check if consumed numbers from both threads
        // has reached to MAX value
        else if (consumerCount2 + consumerCount1 == MAX) {
            pthread_mutex_unlock(&mutex);
            return NULL;
        }

        // If some other thread is executing, wait
        else {
            cout << "B is in wait.." << endl;
            pthread_cond_wait(&dataNotProduced, &mutex);
        }

        // Get the mutex unlocked
        pthread_mutex_unlock(&mutex);
    }
}

// Function definition for consumer thread C
void* add_C(void*)
{

    while (1) {

        // Getting the lock on queue using mutex
        pthread_mutex_lock(&mutex);

        // Pop only when queue has at least 1 element
        if (Q.size() > 0) {

            // Get the data from the front of queue
            int data = Q.front();
            cout << "C thread consumed: " << data << endl;

            // Add the data to the integer variable
            // associated with thread B
            sum_C += data;

            // Pop the consumed data from queue
            Q.pop();
            consumerCount2++;

            pthread_cond_signal(&dataNotConsumed);
        }

        // Check if consumed numbers from both threads
        // has reached to MAX value
        else if (consumerCount2 + consumerCount1 == MAX)
        {
            pthread_mutex_unlock(&mutex);
            return NULL;
        }

        // If some other thread is executing, wait
        else {
            cout << ">> C is in wait.." << endl;
            // Wait on a condition
            pthread_cond_wait(&dataNotProduced, &mutex);
        }

        // Get the mutex unlocked
        pthread_mutex_unlock(&mutex);
    }
}

// Driver code
int main()
{
    // Declaring integers used to
    // identify the thread in the system
    pthread_t producerThread, consumerThread1, consumerThread2;

    // Function to create a threads
    // (pthread_create() takes 4 arguments)
    int retProducer = pthread_create(&producerThread,
                      NULL, producerFun, NULL);
    int retConsumer1 = pthread_create(&consumerThread1,
                       NULL, *add_B, NULL);
    int retConsumer2 = pthread_create(&consumerThread2,
                       NULL, *add_C, NULL);

    // pthread_join suspends execution of the calling
    // thread until the target thread terminates
    if (!retProducer)
        pthread_join(producerThread, NULL);
    if (!retConsumer1)
        pthread_join(consumerThread1, NULL);
    if (!retConsumer2)
        pthread_join(consumerThread2, NULL);

    // Checking for the final value of thread
    if (sum_C > sum_B)
        cout << "Winner is  Thread C" << endl;
    else if (sum_C < sum_B)
        cout << "Winner is  Thread B" << endl;
    else
        cout << "Both has same score" << endl;

    return 0;
}
```

```
Output:
B is in wait..
Produced:  10
Produced:  1
Produced:  6
Produced:  6
Produced:  4
C thread consumed: 10
C thread consumed: 1
C thread consumed: 6
C thread consumed: 6
Produced:  1
Produced:  9
Produced:  9
Produced:  6
C thread consumed: 4
C thread consumed: 1
C thread consumed: 9
C thread consumed: 9
C thread consumed: 6
>> C is in wait..
Produced:  5
C thread consumed: 5
Winner is  Thread C
```

注意:每次代码运行时，输出会有所不同。