# 实验十一 程序设计思想及范例

1.代码如下：
```c
#include <stdio.h>
#include <math.h>

double circleR(double coorX, double coorY) {
    return sqrt(coorX * coorX + coorY * coorY);
}

int main() {
    double x, y, disR;
    printf("请输入坐标点(x,y)的值：");
    scanf("%lf %lf", &x, &y);
    disR = circleR(x, y);
    if (disR <= 35) {
        printf("坐标点在基站覆盖范围内\n");
    } else {
        printf("坐标点不在基站覆盖范围内\n");
    }
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

double getH(int t) {
    return -0.12*t*t*t*t + 12*t*t*t - 380*t*t +4100*t + 220;
}

double getV(int t) {
    return -0.48*t*t*t + 36*t*t - 760*t + 4100;
}

int main() {
    for (int i = 0; i <= 48; i++) {
        printf("第%dh时探空气球的高度为：%.2lfm，速度为%.2lfm/s\n", i, getH(i), getV(i));
    }
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>
#include <math.h>

#define g 9.8

double flyTimeCompute(double distance, double velocity, double theta) {
    return distance / (velocity*cos(theta));
}

double verHeightCompute(double velocity, double theta, double time, double t) {
    return velocity*sin(theta)*time - g*t*t/2;
}

int main() {
    double distance, velocity, theta, t, time, verHeight;
    printf("请输入水平距离、炮弹速度、发射仰角、某时刻的值：");
    scanf("%lf %lf %lf %lf", &distance, &velocity, &theta, &t);
    time = flyTimeCompute(distance, velocity, theta);
    verHeight = verHeightCompute(velocity, theta, time, t);
    printf("炮弹飞行时间为%lf，垂直高度为%lf\n", time, verHeight);
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>

int unit[5] = {16, 32, 12, 1, 14};

int nums[20][5] = {
        {2, 3, 1, 0, 7},
        {2, 6, 4, 0, 15},
        {4, 4, 1, 0, 6},
        {2, 3, 1, 1, 7},
        {3, 0, 2, 0, 10},
        {4, 5, 1, 0, 8},
        {2, 6, 3, 0, 10},
        {2, 6, 1, 0, 13},
        {2, 2, 1, 0, 5},
        {3, 4, 2, 0, 8},
        {2, 3, 1, 0, 7},
        {2, 6, 1, 0, 13},
        {2, 6, 2, 0, 15},
        {2, 5, 1, 1, 11},
        {2, 9, 1, 0, 11},
        {3, 3, 1, 0, 7},
        {3, 4, 1, 0, 9},
        {2, 11, 2, 0, 11},
        {3, 9, 1, 0, 11},
        {2, 5, 1, 0, 11}
};

char names[20][20] = {
        "丙氨酸",
        "精氨酸",
        "天冬氨酸",
        "半胱氨酸",
        "谷氨酰胺",
        "谷氨酸",
        "组氨酸",
        "异亮氨酸",
        "甘氨酸",
        "天冬酰胺",
        "亮氨酸",
        "赖氨酸",
        "甲硫氨酸",
        "苯丙氨酸",
        "脯氨酸",
        "丝氨酸",
        "苏氨酸",
        "色氨酸",
        "酪氨酸",
        "缬氨酸"
};

int main() {
    int sum, i, j;
    for (i = 0; i < 20; i++) {
        sum = 0;
        for (j = 0; j < 5; j++) {
            sum += unit[j] * nums[i][j];
        }
        printf("%s的分子量是%d\n", names[i], sum);
    }
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>

#define ROU 1.23

double getF(double area, double cd, double velocity) {
    return 0.5 * ROU * area * cd * velocity * velocity;
}

int main() {
    double a, cd, v;
    int i;
    printf("请输入车的投影面积(平方米)：");
    scanf("%lf", &a);
    printf("请输入空气阻力系数(0.2~0.5)：");
    scanf("%lf", &cd);
    for (i = 0; i <= 20; i++) {
        v = i;
        printf("速度为%dm/s时的空气阻力为%lf牛顿\n", i, getF(a, cd, v));
    }
    return 0;
}
```

[Experiment12 面向对象程序设计](/Experiment12.md)

[返回首页](/README.md)
