# 实验十 文件

1.代码如下：
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    FILE *fp;
    char filename[12] = {"data.txt"};
    int a[10], i, max, min;
    printf("请输入10个整数：");
    for (i = 0; i < 10; i++) {
        scanf("%d", &a[i]);
    }
    if ((fp = fopen(filename, "w")) == NULL) {
        printf("Can't open the %s\n", filename);
        exit(0);
    }
    printf("输入的10个整数：");
    for (i = 0; i < 10; i++) {
        printf("%d", a[i]);
    }
    fprintf(fp, "输入的10个整数：");
    for (i = 0; i < 10; i++) {
        fprintf(fp, "%d", a[i]);
    }
    max = a[0];
    min = a[0];
    for (i = 1; i < 10; i++) {
        if (a[i] > max) {
            max = a[i];
        }
        if (a[i] < min) {
            min = a[i];
        }
    }
    printf("最大值是%d，最小值是%d\n", max, min);
    fprintf(fp, "最大值是%d，最小值是%d\n", max, min);
    return 0;
}
```

2.代码如下：
```c

```

3.代码如下：
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    FILE *in, *out;
    char infile[20], outfile[20];
    printf("请输入源文件的名称：");
    scanf("%s", infile);
    printf("勤奋输入目标文件的名称：");
    scanf("%s", outfile);
    if ((in = fopen(infile, "r")) == NULL) {
        printf("打开文件%s失败", infile);
        exit(0);
    }
    if ((out = fopen(outfile, "a")) == NULL) {
        printf("打开文件%s失败", infile);
        exit(0);
    }
    while (!feof(in)) {
        fputc(fgetc(in), out);
    }
    fclose(in);
    fclose(out);
    return 0;
}
```

4.代码如下：
```c

```

5.代码如下：
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct student {
    char number[10];
    char name[20];
    int score[3];
} str[5];

int main() {
    int i;
    FILE *fp;
    struct student *p;
    char filename[10] = {"stud.txt"};
    p = str;
    fp = fopen(filename, "r");
    if (fp == NULL) {
        printf("打开文件%s失败", filename);
        exit(0);
    }
    while (!feof(fp)) {
        for (i = 0; i < 5; i++) {
            fscanf(fp, "%s %s %d %d %d", p->number, p->name, &p->score[0], &p->score[1], &p->score[2]);
            p++;
        }
    }
    printf("学号\t姓名\t数学\tC语言\t英语");
    p = str;
    for (i = 0; i < 5; i++) {
        printf("%s\t%s\t%d\t%d\t%d", p->number, p->name, p->score[0], p->score[1], p->score[2]);
        p++;
    }
    fclose(fp);
    return 0;
}
```

6.代码如下：
```c

```

[Experiment11 程序设计思想及范例](/Experiment11.md)

[返回首页](/README.md)
