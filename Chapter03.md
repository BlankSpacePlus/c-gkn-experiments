# 第三章 基本运算与顺序结构

1.代码如下：
```c
#include <stdio.h>

int main() {
    double x;
    scanf("%lf", &x);
    printf("sign(%.2lf)=%d\n", x, x > 0 ? 1 : x == 0 ? 0: -1);
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

int main() {
    int x;
    scanf("%d", &x);
    if (x < 10) {
        printf("%d小于10\n", x);
    } else if (x < 100) {
        printf("%d介于10和99之间\n", x);
    } else if (x < 1000) {
        printf("%d介于100和999之间\n", x);
    } else {
        printf("%d大于1000\n", x);
    }
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>

int main() {
    double x, y;
    scanf("%lf", &x);
    if (x < 2) {
        y = x + 1;
    } else if (x < 4) {
        y = (x-2)*(x-2)+1;
    } else {
        y = (x-2)*(x-2)+(x-1)*(x-1);
    }
    printf("x=%.2lf, y=%.2lf\n", x, y);
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>
#include <math.h>

int main() {
    double x, y, z, m, s;
    scanf("%lf %lf %lf", &x, &y, &z);
    if (x+y>z && x+z>y && y+z>x) {
        m = (x + y + z) / 2;
        printf("三角形面积为：%.2lf\n", sqrt(m*(m-x)*(m-y)*(m-z)));
    } else {
        printf("不能构成三角形\n");
    }
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>

int main() {
    int a, b, c;
    scanf("%d, %d, %d", &a, &b, &c);
    switch (a) {
        case 1:
            printf("%d + %d = %d", b, c, b+c);
            break;
        case 2:
            printf("%d - %d = %d", b, c, b-c);
            break;
        case 3:
            printf("%d * %d = %d", b, c, b*c);
            break;
        case 4:
            printf("%d / %d = %d", b, c, b/c);
            break;
    }
    return 0;
}
```

6.代码如下：
```c
#include <stdio.h>

int main() {
    int n, a, b, c, d, e;
    scanf("%d", &n);
    if (n > 99999 || n < 10000) {
        printf("输入的不是5位正整数");
    }
    e = n;
    a = e / 10000;
    e %= 10000;
    b = e / 1000;
    e %= 100;
    d = e / 10;
    e %= 10;
    if (e == a && b == d) {
        printf("%d是回文数", n);
    } else {
        printf("%d不是回文数", n);
    }
    return 0;
}
```

[Chapter04 逻辑判断与选择结构](/Chapter04.md)

[返回首页](/README.md)
