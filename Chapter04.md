# 第四章 逻辑判断与选择结构

1.代码如下：
```c
#include <stdio.h>

int main() {
    int num, temp, n, bits = 0, mod = 1, sum = 0;
    scanf("%d", &num);
    n = num;
    while (n > 0) {
        n /= 10;
        bits++;
    }
    n = num;
    for (int i = 1; i < bits; i++) {
        mod *= 10;
    }
    while (mod >= 10) {
        sum += (n / mod);
        n %= mod;
        mod /= 10;
    }
    sum += n;
    printf("整数%d的各位数字之和为%d", num, sum);
    return 0;
}
```

2.代码如下(据题意描述用整数longlong解的，实际应该直接读字符数组来求解)：
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    long long n;
    int len, flag = 1;
    scanf("%lld", &n);
    char str[50];
    lltoa(n, str, 10);
    len = strlen(str);
    for (int i = 0; i < len/2; i++) {
        if (str[i] != str[len-i-1]) {
            flag = 0;
            break;
        }
    }
    printf("整数%lld%s回文数", n, flag ? "是" : "不是");
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>

int gcd(int m, int n) {
    int temp;
    while (n > 0) {
        temp = m % n;
        m = n;
        n = temp;
    }
    return m;
}

int main() {
    int m, n;
    scanf("%d %d", &m, &n);
    int gcdResult = gcd(m, n);
    printf("%d和%d的最大公约数是%d，最小公倍数是%d", m, n, gcdResult, m*n/gcdResult);
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>

int main() {
    int primes[500], ptr = 0, i, j, flag = 1, sum = 0;
    for (i = 2; i < 1000; i++) {
        flag = 1;
        for (j = 2; j < i; j++) {
            if (i % j == 0) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            primes[ptr] = i;
            ptr++;
        }
    }
    for (i = ptr-10; i < ptr-1; i++) {
        printf("%d + ", primes[i]);
        sum += primes[i];
    }
    sum += primes[ptr-1];
    printf("%d = %d", primes[ptr-1], sum);
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>
#include <ctype.h>

int main() {
    int digitNum = 0, upperNum = 0, lowerNum = 0, otherNum = 0;
    printf("请输入一串字符串，以回车结束：");
    char c = getchar();
    while (c != '\n') {
        if (isdigit(c)) {
            digitNum++;
        } else if (isupper(c)) {
            upperNum++;
        } else if (islower(c)) {
            lowerNum++;
        } else {
            otherNum++;
        }
        c = getchar();
    }
    printf("一共有：%d个数字字符、%d个大写字母字符、%d个小写字母字符、%d个其他字符。\n", digitNum, upperNum, lowerNum, otherNum);
    return 0;
}
```

6.代码如下：
```c
#include <stdio.h>

int main() {
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n-i-1; j++) {
            printf(" ");
        }
        for (int j = 0; j <= i; j++) {
            printf("* ");
        }
        printf("\n");
    }
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < i+1; j++) {
            printf(" ");
        }
        for (int j = 0; j < n-i-1; j++) {
            printf("* ");
        }
        printf("\n");
    }
    return 0;
}
```

[Chapter05 迭代计算与循环结构](/Chapter05.md)

[返回首页](/README.md)
