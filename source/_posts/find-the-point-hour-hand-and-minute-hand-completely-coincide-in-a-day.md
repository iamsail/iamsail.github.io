---
title: 一天中时针和分针完全重合的时间点
date: 2018-08-18 17:33:40
categories: [水题]
---

### ** Preface **

写一个程序，找出一天中时针和分针完全重合的时间点

**********************
```c++

#include <iostream>
using namespace std;

// 系统ubuntu16
// 开发工具Clion

int main() {
    // 时针的速度 360度 / (12 * 60)分 = 0.5度/分
    // 分针的速度 360度/ 60分 = 6度/分
    // 且分针跑得比时针块
    
    // 0.5 * 60 = 30
    int catch_distance_by_one_hour = 30;

    for(int hour = 0; hour < 11; hour++)
    {
        int minute = (hour * catch_distance_by_one_hour) / (6-0.5) + 0.5;
        cout<< hour << ":" << minute <<endl;
        cout<< hour + 12 << ":" << minute <<endl;
    }

    // 程序打印结果为
    // 0:0
    // 12:0
    // 1:5
    // 13:5
    // 2:11
    // 14:11
    // 3:16
    // 15:16
    // 4:22
    // 16:22
    // 5:27
    // 17:27
    // 6:33
    // 18:33
    // 7:38
    // 19:38
    // 8:44
    // 20:44
    // 9:49
    // 21:49
    // 10:55
    // 22:55
    return 0;
}
```
