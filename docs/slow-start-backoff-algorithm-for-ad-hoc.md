# 自组织的慢启动退避算法

> 原文:[https://www . geeksforgeeks . org/慢速启动-回退-算法换 ad-hoc/](https://www.geeksforgeeks.org/slow-start-backoff-algorithm-for-ad-hoc/)

如果接收者宣称一个大的窗口大小，比网络在途中所能管理的更大，那么总会有分组丢失。所以也会有转播。但是，发送方不能发送所有未收到确认的数据包。因为这种方式，会造成网络更加拥堵。此外，发送方无法确定由于传输而丢失的数据包。这可能是唯一丢失的数据包。也不知道接收器实际接收和缓冲了多少分组。在这种情况下，发送方将多余地发送各种数据包。
因此数据包的重新传输也遵循慢启动退避机制。然而，我们确实需要保持数据包大小的上限，因为它在慢速启动时会增加，以防止它在无界时增加并导致拥塞。在慢启动退避机制
中，阈值窗口大小是拥塞窗口大小的一半。
**先决条件:**[CSMA/光盘后退算法](https://www.geeksforgeeks.org/back-off-algorithm-csmacd/)
**慢启动机制算法:-**

```
repeat
 if ACK frame received then successful transmission
  if current backoff window size <= Wm then
   if current backoff window size = W0 then
    current backoff window size = W0
  else
  current backoff window size =  current backoff window size ÷ 2
 else
 current backoff window size = current backoff window size-W0
else
 if current backoff window size < Wm then
 current backoff window size = current backoff window size × 2
  else frame lost due to collision or interference
   if current backoff window size = Wn then
   current backoff window size = Wn
   else
 current backoff window size = current backoff window size +W0
until no more frame to transmit
end

```

**例:**

> 这表示传输成功，因为阈值窗口小于当前窗口。
> **输入:**
> 输入阈值:–>512
> 输入当前退避窗口大小:–>64
> **输出:**
> 退避窗口大小为:–>128
> 退避窗口大小为:–>96
> 成功传输
> 退避窗口大小为:–>32
> 成功传输
> 退避窗口大小为
> **输入:**
> 输入阈值:–>512
> 输入当前退避窗口大小:–>1024
> **输出:**
> 帧因碰撞或干扰丢失退避窗口大小为:–>1056
> 成功传输
> 退避窗口大小为:–>512
> 成功传输
> 退避窗口大小

**符号:-**T2]

```
W0 -->  Initial backoff window size
Wm -->  Threshold
Wn -->  Maximum backoff window size
ACK --> Acknowledgement
Curr_BT --> Current  backoff window size

```

**实施慢启动机制:-**

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <cstdlib>
#include <iostream>
#include <math.h>
#include <random>
#include <string>
#include <time.h>

using namespace std;

void signal(int array_ACK[])
{
    srand(time_t(0));
    for (int i = 0; i < 5; i++) {
        array_ACK[i] = rand() % 2;
    }
}

void Slow_Start_Backoff(int Wm, int Wo, int Wn,
                        int Curr_BT, int array_ACK[])
{
    // Taking ACK Binary values in
    // array by user one by one

    // backoff_win_size defines
    // backoff window size

    int backoff_win_size = 0;

    // Printing of backoff window size takes place

    for (int j = 0; j < 5; j++) {
        if (array_ACK[j] == 1) {
            cout << "Successful transmission" << endl;
            if (Curr_BT <= Wm) {
                if (Curr_BT == Wo) {
                    Curr_BT = Wo;
                    cout << "Backoff Window Size is:-->"
                            << Curr_BT << endl;
                }
                else {
                    Curr_B= Curr_BT / 2;
                    cout << "Backoff Window Size is:-->"
                            << Curr_BT << endl;
                }
            }
            else {
                Curr_BT = Curr_BT - Wo;
                cout << "Backoff Window Size is:-->"
                        << Curr_BT << endl;
            }
        }
        else {
            if (Curr_BT < Wm) {
                Curr_BT = Curr_BT * 2;
                cout << "Backoff Window Size is:-->"
                        << Curr_BT << endl;
            }
            else {
                cout << "Frame lost due to collision"
                        <<" or interference";
            }
            if (Curr_BT == Wn) {
                Curr_BT = Wn;
                cout << "Backoff Window Size is:-->"
                        << Curr_BT << endl
                            << endl;
            }
            else {
                Curr_BT = Curr_BT + Wo;
                cout << "Backoff Window Size is:-->"
                        << Curr_BT << endl;
            }
        }
    }
}

// Driver Code
int main()
{
    int Wm, Wo, Wn, Curr_BT;
    int array_ACK[5];

    Wo = 32; // Initial backoff window size
    Wn = 1024; // Maximum backoff window size

    // Curr_BT defines the current backoff window size

    cout << "Enter the Threshold value:-->";
    cin >> Wm; // Threshold backoff window size
    cout << "Enter the Current backoff window size:-->";
    cin >> Curr_BT;
    signal(array_ACK);
    Slow_Start_Backoff(Wm, Wo, Wn, Curr_BT, array_ACK);

    return 0;
}
```

**通过网络以数据包形式发送的数据:-**
任何类型的数据都被转换成二进制格式，这种二进制格式包含 0 和 1 字节
，它被分成称为数据包的二进制小比特序列。
现在，我们正在实现代码，其中 0 和 1 的随机矩阵生成并假设二进制文件位序列以固定长度按行排列在矩阵中(取长度 10)。然后，矩阵的每一行代表将要传输的单个数据包。
**随机矩阵生成器的实现:-**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to construct the
// Random Matrix Generator.
#include <iostream>
#include <iterator>
#include <list>
#include <random>
#include <string>
using namespace std;

void showlist(list<string> l1)
{
    list<string>::iterator it;
    cout << "list of frame packets are "
            <<"show as below :-> " << endl;
    cout << endl;

    for (it = l1.begin(); it != l1.end(); ++it)
        cout << *it << endl;
    cout << '\n';
}

// Driver Code
int main()
{
    int x, y, k = 1;
    string s, s1, s2;

    list<string> l1;

    srand(time_t(0));

    cout << "Rows: " << endl;
    cin >> x;

    cout << "Columns: " << endl;
    cin >> y;

    int randomNums[x][y];
    std::string temp[x];

    int random;

    for (int i = 0; i < x; i++) {

        // This loop is for the row
        for (int p = 0; p < y; p++) {

            // Here you would randomize each
            // element for the array.
            random = rand() % 2;
            randomNums[i][p] = random;
        }
    }

    for (int i = 0; i < x; i++) {

        // This loop is for the row
        for (int p = 0; p < y; p++) {

            // Here you would randomize each
            // element for the array.
            cout << randomNums[i][p] << "\t";
        }

        cout << endl;
    }
    cout << endl;

    // concatenation of the bits in the matrix row
    // to form a single data packet
    for (int i = 0; i < x; i++) {

        temp[i] = to_string(randomNums[i][0]);

        for (int j = 0; j < y; ++j) {

            s1 = temp[i];
            s2 = to_string(randomNums[i][j]);

            s = s1 + s2;

            temp[i] = s;
            k++;
        }

        temp[i].erase(temp[i].begin() + 1);
        l1.push_back(temp[i]);
    }

    showlist(l1);
    return 0;
}
```

**例:**

> **输入:**
> 行:
> 10
> 列:
> 10
> **输出:**
> 0 1 0 1 1 0 1 0 1 0 1 1
> 0 0 0 1 1 0 0
> 0 1 0 1 1 0 1 1 1
> 0 1 0 0 0 1 0 0 0 0 0 1 0
> 0 1 0 1 0 1 0 0 0
> 0 0 0 1 0 1 1 1 1 0 0
> 0 0 1 1 0 1 1 0 1 0 1
> 1 0 1 0 1 0 0 1
> 1 0 1 0 1 0 1 1 1 1
> 0 1 0 1 0 1 0 1 1 1 1
> 帧包列表如下:->
> 011011010101
> 0000001100
> 0110110111
> 01000010000000001

**参考:** [自组织无线网络的慢启动退避算法](https://ieeexplore.ieee.org/document/5683905)