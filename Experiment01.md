# 实验一 熟悉实验环境

1.代码如下：
```c
#include <stdio.h>

int main() {
    printf("Hello World!");
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

int main() {
    int a, b;
    scanf("%d, %d", &a, &b);
    printf("%d + %d = %d", a, b, a+b);
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>

int main() {
    int a, b, c;
    scanf("%d, %d, %d", &a, &b, &c);
    printf("%d + %d + %d = %d\navg = %.2lf", a, b, c, a+b+c, (a+b+c)/3.0);
    return 0;
}
```

[Experiment02 简单程序设计](/Experiment02.md)

[返回首页](/README.md)
