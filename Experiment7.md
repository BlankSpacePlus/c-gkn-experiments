# 实验七 指针

1.代码如下：
```c
#include <stdio.h>

int main() {
    int nums[] = {1, 4, 7, 9, 32, 67, 77, 100}, length = 8, insert_num, i;
    printf("请输入一个整数：");
    scanf("%d", &insert_num);
    printf("原数组元素信息：\n");
    for (i = 0; i < length; i++) {
        printf("%d ", nums[i]);
    }
    printf("\n");
    int new_nums[length+1];
    for (i = 0; i < length && nums[i] < insert_num; i++) {
        new_nums[i] = nums[i];
    }
    new_nums[i] = insert_num;
    for (; i < length; i++) {
        new_nums[i+1] = nums[i];
    }
    printf("新数组元素信息：\n");
    for (i = 0; i < length+1; i++) {
        printf("%d ", new_nums[i]);
    }
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

int partition(int *a, int i, int j) {
    int temp = *(a+i);
    while (i < j) {
        while (i < j && *(a+j) >= temp) {
            j--;
        }
        if (i < j) {
            *(a+i) = *(a+j);
            i++;
        }
        while (i < j && *(a+i) <= temp) {
            i++;
        }
        if (i < j) {
            *(a+j) = *(a+i);
            j--;
        }
    }
    *(a+i) = temp;
    return i;
}

void quickSort(int *a, int low, int high) {
    int mid;
    if (low < high) {
        mid = partition(a, low, high);
        quickSort(a, low, mid-1);
        quickSort(a, mid+1, high);
    }
}

void sort(int *a, int n) {
    int low = 0, high = n-1;
    quickSort(a, low, high);
}

int main() {
    int nums[10], i, length = 10;
    printf("请输入10个整数：");
    for (i = 0; i < length; i++) {
        scanf("%d", &nums[i]);
    }
    printf("排序前的数组：\n");
    for (i = 0; i < length; i++) {
        printf("%d ", nums[i]);
    }
    printf("\n");
    sort(nums, length);
    printf("排序后的数组：\n");
    for (i = 0; i < length; i++) {
        printf("%d ", nums[i]);
    }
    return 0;
}
```

3.代码如下：
```c
#include <stdio.h>
#include <string.h>

void upCopy(char *newstr, char *old) {
    int old_len = strlen(old), new_ptr = 0, i;
    for (i = 0; i < old_len; i++) {
        if (old[i] >= 'A' && old[i] <= 'Z') {
            newstr[new_ptr] = old[i];
            new_ptr++;
        }
    }
}

int main() {
    int length = 30;
    char old_str[length], new_str[length];
    printf("请输入一个字符串：");
    scanf("%s", old_str);
    upCopy(new_str, old_str);
    printf("新生成的字符串为：%s", new_str);
    return 0;
}
```

4.代码如下：
```c
#include <stdio.h>
#include <string.h>

void catStr(char *str1, char *str2) {
    int len1 = strlen(str1), len2 = strlen(str2), i;
    for (i = 0; i < len2; i++) {
        str1[len1+i] = str2[i];
    }
}

int main() {
    char str1[] = "123", str2[] = "abc";
    printf("字符串1为：%s，字符串2为：%s\n", str1, str2);
    catStr(str1, str2);
    printf("新生成的字符串为：%s", str1);
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>
#include <string.h>

void delet(char *str, char ch) {
    int len = strlen(str), i, ptr = 0;
    for (i = 0; i < len; i++) {
        if (str[i] != ch) {
            str[ptr] = str[i];
            ptr++;
        }
    }
    str[ptr] = '\0';
}

int main() {
    char str[] = "This is a test of C language.", c;
    printf("请输入待删除的字符：");
    scanf("%c", &c);
    printf("原字符串为：%s\n", str);
    delet(str, c);
    printf("新生成的字符串为：%s", str);
    return 0;
}
```

6.代码如下：
```c
#include <stdio.h>
#include <string.h>

void strMid(char *str1, int m, int n, char *str2) {
    int len = strlen(str1), i, ptr = 0;
    for (i = 0; i < n && i+m+n < len; i++) {
        str2[ptr] = str1[i+m];
        ptr++;
    }
    str2[ptr] = '\0';
}

int main() {
    char str1[30], str2[30];
    int index, n;
    printf("请输入一个字符串：");
    scanf("%s", str1);
    printf("请输入复制开始的下标：");
    scanf("%d", &index);
    printf("请输入待复制的字符数：");
    scanf("%d", &n);
    strMid(str1, index, n, str2);
    printf("新生成的字符串为：%s", str2);
    return 0;
}
```

[Experiment8 结构体](/Experiment8.md)

[返回首页](/README.md)
