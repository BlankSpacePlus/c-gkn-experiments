# 实验九 预编译和宏定义

1.代码如下：
```c
#include <stdio.h>

#define COMPARE(a, b) c = a > b ? a : b; d = a + b - c;

int main() {
    int a, b, c, d;
    scanf("%d %d", &a, &b);
    COMPARE(a, b);
    printf("较大的数是%d，较小的数是%d", c, d);
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

#define CALCULATE(a, b) c = a + b; d = a - b;

int main() {
    int a, b, c, d;
    scanf("%d %d", &a, &b);
    CALCULATE(a, b);
    printf("%d + %d = %d，%d - %d = %d", a, b, c, a, b, d);
    return 0;
}
```

3.代码如下(没用`do...while`)：
```c
#include <stdio.h>

#define ISDIGIT(a) b = (a == (int)a)

int main() {
    double a;
    int b;
    scanf("%lf", &a);
    ISDIGIT(a);
    printf("%.2lf%s整数", a, b ? "是" : "不是");
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>

#define ISODD(a) b = (a%2==1);

int main() {
    int a;
    int b;
    scanf("%d", &a);
    ISODD(a);
    printf("%d是%s", a, b ? "奇数" : "偶数");
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>

#define COUNT 20;

int main() {
    int i, max, sum = 0, max_index = 0, grades[20];
    double average;
    scanf("%d", &grades[0]);
    sum += grades[0];
    max = grades[0];
    for (i = 1; i < COUNT i++) {
        scanf("%d", &grades[i]);
        sum += grades[i];
        if (grades[i] > max) {
            max = grades[i];
            max_index = i;
        }
    }
    max_index++;
    average = sum / (double)COUNT;
    printf("最高分的同学是第%d位同学，它的成绩为%d\n全班的平均成绩为%.2f", max_index, max, average);
    return 0;
}
```

6.代码如下(不想用题给的那种阴间变量名)：
```c
#include "header.h"

int main() {
    printNum(1, 2, 3);
    return 0;
}
```

头文件`header.h`：
```c
#ifndef TEST_HEADER_H
#define TEST_HEADER_H

#include <stdio.h>

extern void printNum(int a, int b, int c) {
    if (a > b && b > c) {
        printf("%d %d %d", c, b, a);
    } else if (a > c && c > b) {
        printf("%d %d %d", b, c, a);
    } else if (b > a && a > c) {
        printf("%d %d %d", c, a, b);
    } else if (b > c && c > a) {
        printf("%d %d %d", a, c, b);
    } else if (c > a && a > b) {
        printf("%d %d %d", b, a, c);
    } else {
        printf("%d %d %d", a, b, c);
    }
}

#endif //TEST_HEADER_H
```

[Experiment10 文件](/Experiment10.md)

[返回首页](/README.md)
