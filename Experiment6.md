# 实验六 函数

1.代码如下：
```c
#include <stdio.h>

// 暴力求解
int primeNum(int x) {
    for (int i = 2; i < x; i++) {
        if (x % i == 0) {
            return 0;
        }
    }
    return 1;
}

int main() {
    printf("1000以内的素数有：\n");
    for (int i = 1; i < 1000; i++) {
        if (primeNum(i)) {
            printf("%d ", i);
        }
    }
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

double getMax(double a, double b) {
    return a > b ? a : b;
}
double getMin(double a, double b) {
    return a < b ? a : b;
}

int main() {
    printf("请输入三个实数：");
    double a, b, c;
    scanf("%lf %lf %lf", &a, &b, &c);
    printf("%.2lf、%.2lf、%.2lf中，最大值是%.2lf、最小值是%.2lf", a, b, c, getMax(a, getMax(b, c)), getMin(a, getMin(b, c)));
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>

int factorial(int x) {
    int result = 1;
    for (int i = 2; i <= x; i++) {
        result *= i;
    }
    return result;
}

int fun(int m, int n) {
    return factorial(m) / (factorial(n) * factorial(m-n));
}

int main() {
    int m, n;
    scanf("%d %d", &m, &n);
    printf("p的取值是：%d", fun(m, n));
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>

int fib(int n) {
    if (n == 0) {
        return 0;
    } else if (n == 1) {
        return 1;
    }
    return fib(n-2) + fib(n-1);
}

int main() {
    printf("请输入一个正整数：");
    int n;
    scanf("%d", &n);
    if (n < 0) {
        printf("输入不合法！\n");
        return -1;
    }
    printf("第%d个斐波那契数是：%d", n, fib(n));
    return 0;
}
```

5.代码如下(选择新建一个字符串而非将str2接在str1后)：
```c
#include <stdio.h>

int lenStr(char str[]) {
    int counter = 0;
    char temp = str[0];
    while (temp != '\0') {
        counter++;
        temp = str[counter];
    }
    return counter;
}

void catStr(char str1[], char str2[], char str3[]) {
    int len1 = lenStr(str1), len2 = lenStr(str2), i;
    for (i = 0; i < len1; i++) {
        str3[i] = str1[i];
    }
    for (i = 0; i < len2; i++) {
        str3[len1+i] = str2[i];
    }
}

int main() {
    printf("请输入一个字符串：");
    char str1[50], str2[50], str3[100];
    scanf("%s", str1);
    printf("请再输入一个字符串：");
    scanf("%s", str2);
    printf("原字符串1为：%s，长度为：%d\n", str1, lenStr(str1));
    printf("原字符串2为：%s，长度为：%d\n", str2, lenStr(str2));
    catStr(str1, str2, str3);
    printf("连接后字符串为：%s，长度为：%d\n", str3, lenStr(str3));
    return 0;
}
```

6.代码如下：
```c
#include <stdio.h>
#include <string.h>

void delet(char str[]) {
    int length = strlen(str), temp_index = 0, i;
    char temp = str[0];
    if (length % 2 == 0) {
        for (i = 1; i < length; i++) {
            if (str[i] < temp) {
                temp = str[i];
                temp_index = i;
            }
        }
    } else {
        for (i = 1; i < length; i++) {
            if (str[i] > temp) {
                temp = str[i];
                temp_index = i;
            }
        }
    }
    for (i = temp_index; i < length-1; i++) {
        str[i] = str[i+1];
    }
    str[length-1] = '\0';
}

int main() {
    printf("请输入一个字符串：");
    char str[50];
    scanf("%s", str);
    printf("原字符串为：%s\n", str);
    delet(str);
    printf("修改后字符串为：%s\n", str);
    return 0;
}
```

[Experiment7 指针](/Experiment7.md)

[返回首页](/README.md)
