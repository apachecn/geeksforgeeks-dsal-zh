# 酒店管理系统

> 原文:[https://www.geeksforgeeks.org/hotel-management-system/](https://www.geeksforgeeks.org/hotel-management-system/)

给定酒店管理和用户数据:
**酒店数据:**

```
Hotel Name     Room Available     Location     Rating      Price per Room
H1                4               Bangalore      5           100
H2                5               Bangalore      5           200
H3                6               Mumbai         3           100
```

**用户数据:**

```
User Name         UserID             Booking Cost
U1                 2                  1000
U2                 3                  1200
U3                 4                  1100
```

任务是回答以下问题。

1.  打印酒店数据。
2.  按名称对酒店进行排序。
3.  按最高等级对酒店进行排序。
4.  打印班加罗尔位置的酒店数据。
5.  按最大可用房间数对酒店进行排序。
6.  打印用户预订数据。

> **机器编码回合**涉及在几个小时内解决一个设计问题。
> 它要求基于一组特定的需求设计和编码一个干净的、模块化的和可扩展的解决方案。

**进场:**

*   为酒店数据和用户数据创建类。
*   初始化存储酒店数据和用户数据的变量。
*   为访问酒店数据和用户数据的酒店和用户类创建对象。
*   初始化保存酒店数据和用户数据的两个向量数组。
*   逐一解答以上问题。

下面是上述方法的实现。

## C++

```
// C++ program to solve
// the given question

#include <algorithm>
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// Create class for hotel data.
class Hotel {
public:
    string name;
    int roomAvl;
    string location;
    int rating;
    int pricePr;
};

// Create class for user data.
class User : public Hotel {
public:
    string uname;
    int uId;
    int cost;
};

// Function to Sort Hotels by
// Bangalore location
bool sortByBan(Hotel& A, Hotel& B)
{
    return A.name > B.name;
}

// Function to sort hotels
// by rating.
bool sortByr(Hotel& A, Hotel& B)
{
    return A.rating > B.rating;
}

// Function to sort hotels
// by rooms availability.
bool sortByRoomAvailable(Hotel& A,
                        Hotel& B)
{
    return A.roomAvl < B.roomAvl;
}

// Print hotels data.
void PrintHotelData(vector<Hotel> hotels)
{
    cout << "PRINT HOTELS DATA:" << endl;
    cout << "HotelName"
         << "   "
         << "Room Available"
         << "    "
         << "Location"
         << "    "
         << "Rating"
         << "    "
         << "PricePer Room:" << endl;

    for (int i = 0; i < 3; i++) {
        cout << hotels[i].name
             << "          "
             << hotels[i].roomAvl
             << "              "
             << hotels[i].location
             << "       "
             << hotels[i].rating
             << "            "
             << hotels[i].pricePr
             << endl;
    }
    cout << endl;
}

// Sort Hotels data by name.
void SortHotelByName(vector<Hotel> hotels)
{
    cout << "SORT BY NAME:" << endl;

    std::sort(hotels.begin(), hotels.end(),
              sortByBan);

    for (int i = 0; i < hotels.size(); i++) {
        cout << hotels[i].name << " "
             << hotels[i].roomAvl << " "
             << hotels[i].location << " "
             << hotels[i].rating << " "
             << " " << hotels[i].pricePr
             << endl;
    }
    cout << endl;
}

// Sort Hotels by rating
void SortHotelByRating(vector<Hotel> hotels)
{
    cout << "SORT BY A RATING:" << endl;

    std::sort(hotels.begin(),
              hotels.end(), sortByr);

    for (int i = 0; i < hotels.size(); i++) {
        cout << hotels[i].name << " "
             << hotels[i].roomAvl << " "
             << hotels[i].location << " "
             << hotels[i].rating << " "
             << " " << hotels[i].pricePr
             << endl;
    }
    cout << endl;
}

// Print Hotels for any city Location.
void PrintHotelBycity(string s,
                      vector<Hotel> hotels)
{
    cout << "HOTELS FOR " << s
         << " LOCATION IS:"
         << endl;
    for (int i = 0; i < hotels.size(); i++) {

        if (hotels[i].location == s) {

            cout << hotels[i].name << " "
                 << hotels[i].roomAvl << " "
                 << hotels[i].location << " "
                 << hotels[i].rating << " "
                 << " " << hotels[i].pricePr
                 << endl;
        }
    }
    cout << endl;
}

// Sort hotels by room Available.
void SortByRoomAvailable(vector<Hotel> hotels)
{
    cout << "SORT BY ROOM AVAILABLE:" << endl;

    std::sort(hotels.begin(), hotels.end(),
              sortByRoomAvailable);

    for (int i = hotels.size() - 1; i >= 0; i--) {

        cout << hotels[i].name << " "
             << hotels[i].roomAvl << " "
             << hotels[i].location << " "
             << hotels[i].rating << " "
             << " " << hotels[i].pricePr
             << endl;
    }
    cout << endl;
}

// Print the user's data
void PrintUserData(string userName[],
                   int userId[],
                   int bookingCost[],
                   vector<Hotel> hotels)
{

    vector<User> user;
    User u;

    // Access user data.
    for (int i = 0; i < 3; i++) {
        u.uname = userName[i];
        u.uId = userId[i];
        u.cost = bookingCost[i];
        user.push_back(u);
    }

    // Print User data.
    cout << "PRINT USER BOOKING DATA:"
         << endl;
    cout << "UserName"
         << " "
         << "UserID"
         << " "
         << "HotelName"
         << " "
         << "BookingCost" << endl;

    for (int i = 0; i < user.size(); i++) {
        cout << user[i].uname
             << "         "
             << user[i].uId
             << "        "
             << hotels[i].name
             << "         "
             << user[i].cost
             << endl;
    }
}

// Functiont to solve
// Hotel Management problem
void HotelManagement(string userName[],
                     int userId[],
                     string hotelName[],
                     int bookingCost[],
                     int rooms[],
                     string locations[],
                     int ratings[],
                     int prices[])
{
    // Initialize arrays that stores
    // hotel data and user data
    vector<Hotel> hotels;

    // Create Objects for
    // hotel and user.
    Hotel h;

    // Initialise the data
    for (int i = 0; i < 3; i++) {
        h.name = hotelName[i];
        h.roomAvl = rooms[i];
        h.location = locations[i];
        h.rating = ratings[i];
        h.pricePr = prices[i];
        hotels.push_back(h);
    }
    cout << endl;

    // Call the various operations
    PrintHotelData(hotels);
    SortHotelByName(hotels);
    SortHotelByRating(hotels);
    PrintHotelBycity("Bangalore",
                     hotels);
    SortByRoomAvailable(hotels);
    PrintUserData(userName,
                  userId,
                  bookingCost,
                  hotels);
}

// Driver Code.
int main()
{

    // Initialize variables to stores
    // hotels data and user data.
    string userName[] = { "U1", "U2", "U3" };
    int userId[] = { 2, 3, 4 };
    string hotelName[] = { "H1", "H2", "H3" };
    int bookingCost[] = { 1000, 1200, 1100 };
    int rooms[] = { 4, 5, 6 };
    string locations[] = { "Bangalore",
                           "Bangalore",
                           "Mumbai" };
    int ratings[] = { 5, 5, 3 };
    int prices[] = { 100, 200, 100 };

    // Function to perform operations
    HotelManagement(userName, userId,
                    hotelName, bookingCost,
                    rooms, locations,
                    ratings, prices);

    return 0;
}
```

**Output**

```
PRINT HOTELS DATA:
HotelName   Room Available    Location    Rating    PricePer Room:
H1          4              Bangalore       5            100
H2          5              Bangalore       5            200
H3          6              Mumbai       3            100

SORT BY NAME:
H3 6 Mumbai 3  100
H2 5 Bangalore 5  200
H1 4 Bangalore 5  100

SORT BY A RATING:
H1 4 Bangalore 5  100
H2 5 Bangalore 5  200
H3 6 Mumbai 3  100

HOTELS FOR Bangalore LOCATION IS:
H1 4 Bangalore 5  100
H2 5 Bangalore 5  200

SORT BY ROOM AVAILABLE:
H3 6 Mumbai 3  100
H2 5 Bangalore 5  200
H1 4 Bangalore 5  100

PRINT USER BOOKING DATA:
UserName UserID HotelName BookingCost
U1         2        H1         1000
U2         3        H2         1200
U3         4        H3         1100
```