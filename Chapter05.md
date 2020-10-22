# 第五章 迭代计算与循环结构

1.代码如下：
```c
#include <stdio.h>

int main() {
    int nums[10] = {1, 2, 3 ,4, 5, 6, 7, 8, 9, 10}, i, n = 10;
    printf("交换前的数组：\n");
    for (i = 0; i < n; i++) {
        printf("%d ", nums[i]);
    }
    printf("\n交换后的数组：\n");
    for (i = 0; i < n/2; i++) {
        nums[i] ^= nums[n-i-1];
        nums[n-i-1] = nums[i] ^ nums[n-i-1];
        nums[i] ^= nums[n-i-1];
    }
    for (i = 0; i < n; i++) {
        printf("%d ", nums[i]);
    }
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>
#include <string.h>

int main() {
    int nums[10] = {1, 2, 3 ,14, 25, 36, 47, 85, 99, 100}, i, n = 10, num, j;
    printf("插入前的数组：\n");
    for (i = 0; i < n; i++) {
        printf("%d ", nums[i]);
    }
    printf("\n请输入待插入的数据：");
    scanf("%d", &num);
    int new_nums[n+1];
    memcpy(new_nums, nums, sizeof(int)*n);
    printf("插入后的数组：\n");
    for (i = 0; i < n && nums[i] < num; i++) {}
    for (j = n-1; j >= i; j--) {
        nums[j+1] = nums[j];
    }
    nums[i] = num;
    for (i = 0; i < n+1; i++) {
        printf("%d ", nums[i]);
    }
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>
#include <limits.h>

int main() {
    int n;
    printf("请输入N的数值：");
    scanf("%d", &n);
    double nums[n][n], max = INT_MIN, min = INT_MAX, temp;
    int i, j, max_index = 0, min_index = 0;
    for (i = 0; i < n; i++) {
        printf("请输入N个数值(空格分隔)：\n");
        for (j = 0; j < n; j++) {
            scanf("%lf", &nums[i][j]);
            if (nums[i][j] > max) {
                max = nums[i][j];
                max_index = i;
            }
            if (nums[i][j] < min) {
                min = nums[i][j];
                min_index = i;
            }
        }
    }
    printf("原矩阵为：\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            printf("%.1lf\t", nums[i][j]);
        }
        printf("\n");
    }
    printf("最大元素在第%d行，最小元素在第%d行\n", max_index, min_index);
    for (j = 0; j < n; j++) {
        temp = nums[min_index][j];
        nums[min_index][j] = nums[max_index][j];
        nums[max_index][j] = temp;
    }
    printf("生成的矩阵为：\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            printf("%.1lf\t", nums[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>

int main() {
    double grades[4][5], tempSum;
    int i, j;
    for (i = 0; i < 3; i++) {
        printf("请输入学生%d的四门课成绩(空格分隔)：", i+1);
        tempSum = 0;
        for (j = 0; j < 4; j++) {
            scanf("%lf", &grades[i][j]);
            tempSum += grades[i][j];
        }
        grades[i][4] = tempSum;
    }
    for (j = 0; j < 5; j++) {
        tempSum = 0;
        for (i = 0; i < 3; i++) {
            tempSum += grades[i][j];
        }
        grades[3][j] = tempSum / 3;
    }
    printf("生成的矩阵为：\n");
    for (i = 0; i < 4; i++) {
        for (j = 0; j < 5; j++) {
            printf("%.1lf ", grades[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    printf("请输入一个字符串：");
    char str[50];
    scanf("%s", str);
    int flag = 0, sum = 0;
    for (int i = 0; i < strlen(str); i++) {
        if (isdigit(str[i])) {
            flag = 1;
            sum += (str[i] - '0');
        }
    }
    if (flag) {
        printf("字符串中的各位数字之和为：%d\n", sum);
    } else {
        printf("字符串中没有数字！\n");
    }
    return 0;
}
```

6.代码如下：
```c
#include <stdio.h>
#include <string.h>

int main() {
    printf("请输入一个字符串：");
    char str[50], substr[50];
    scanf("%s", str);
    printf("请输入待查找的子串：");
    scanf("%s", substr);
    int strLen = strlen(str), subLen = strlen(substr), flag = 1, index = -1;
    if (strLen < subLen) {
        flag = 0;
        printf("不存在这样的子串！");
        return 0;
    }
    for (int i = 0; i <= strLen-subLen; i++) {
        flag = 1;
        for (int j = 0; j < subLen; j++) {
            if (str[i+j] != substr[j]) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            index = i;
            break;
        }
    }
    if (flag) {
        printf("子串最初出现的位置是：%d", index);
    } else {
        printf("不存在这样的子串！");
    }
    return 0;
}
```

[Chapter06 集合数据与数组](/Chapter06.md)

[返回首页](/README.md)
