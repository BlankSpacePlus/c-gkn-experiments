# 实验十四 个体软件开发

1.代码如下：
```c
/**
 * 文件名： main.c
 * 作者：BlankSpace
 * 日期：2020年10月29日
 *
 * 描述：本文件要求程序循环输入10个整数，求阶乘后输出结果
 *
 * 修改：BlankSpace于2020年10月29日规范了子函数命名，规范了返回值变量命名，规范了输出格式，增加了注释
 *
 */

#include <stdio.h>

/**
 * 阶乘运算的子函数
 * 函数名：factor
 * 主调函数：main
 * @param n
 * @return ret
 */
double factor(int n) {
    // 初始化阶乘变量
    double ret = 1;
    // 当循环次数小于等于n次时进行循环
    for (int i = 2; i <= n; i++) {
        ret *= i;
    }
    // 输出每次阶乘的结果
    printf("%.0lf\n", ret);
    return ret;
}

int main() {
    // 初始化输入变量、和值变量及循环变量
    int n = 20;
    double result_sum = 0;
    // 当循环次数小于等于n次时进行循环
    for (int i = 1; i <= n; i++) {
        // 阶乘的累加和
        result_sum += factor(i);
    }
    // 输出最终的阶乘和结果
    printf("阶乘和=%.0lf\n", result_sum);
    return 0;
}
```

2.略

[返回首页](/README.md)
