# 第二章 信息编码与数据类型

1.代码如下：
```c
#include <stdio.h>

int main() {
    char c;
    scanf("%c", &c);
    printf("%c在字母表中的位置是%d", c, c-'a'+1);
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

int main() {
    char c;
    scanf("%c", &c);
    printf("%c加密后的字母是%c", c, (c+4-'a')%26+'a');
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>

int main() {
    double f;
    scanf("%lf", &f);
    printf("%.2lf℉ = %.2lf℃", f, 5*(f-32)/9);
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>

int main() {
    int minutes = 1000;
    printf("%d分钟=%d小时%d分钟", minutes, minutes/60, minutes%60);
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>

int main() {
    double f;
    scanf("%lf", &f);
    // 默认就是四舍五入
    printf("四舍五入后得到%.2lf\n", f);
    // 人工处理
    double result = (int)(f * 100 + 0.5) / 100.0;
    printf("%lf四舍五入得到%.2lf\n", f, result);
    return 0;
}
```

6.代码如下：
```c
#include <stdio.h>

int main() {
    double f1, f2, f3;
    scanf("%lf %lf %lf", &f1, &f2, &f3);
    // 人工处理
    double result = (int)((f1 + f2 + f3) / 3.0 * 100 + 0.5) / 100.0;
    printf("四舍五入得到的平均值为：%.1lf\n", result);
    return 0;
}
```

[Chapter03 基本运算与顺序结构](/Chapter03.md)

[返回首页](/README.md)
