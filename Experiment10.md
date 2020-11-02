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
#include <stdio.h>

typedef struct student Student;

struct student  {
    int id;
    char name[30];
    int score[5];
};

// 测试数据
// 1 Alice 90 95 100 90 95
// 2 Bob 77 76 91 80 88
// 3 Cat 99 99 99 99 99
int main() {
    int n = 3, i, j;
    double temp;
    Student students[n];
    double avg[n];
    FILE *fp;
    fp = fopen("student.txt", "a+");
    if (fp == NULL) {
        printf("文件打开失败");
        return 0;
    }
    for (i = 0; i < n; i++) {
        temp = 0;
        scanf("%d %s", &students[i].id, students[i].name);
        for (j = 0; j < 5; j++) {
            scanf("%d", &students[i].score[j]);
            temp += students[i].score[j];
        }
        avg[i] = temp / 5.0;
        fprintf(fp, "%d %s %d %d %d %d %d %lf\n", students[i].id, students[i].name,
                students[i].score[0],students[i].score[1], students[i].score[2], students[i].score[3],
                students[i].score[4], avg[i]);
    }
    if (fclose(fp) != 0) {
        printf("文件关闭失败！");
    }
    return 0;
}
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
#include <stdio.h>

int main() {
    FILE *fpa, *fpb;
    char text[1000];
    fpa = fopen("source.txt", "r");
    fpb = fopen("dest.txt", "a+");
    if (fpa == NULL || fpb == NULL) {
        printf("文件打开失败");
        return 0;
    }
    fread(text, sizeof(text), 1, fpa);
    fwrite(text, sizeof(text), 1, fpb);
    if (fclose(fpa) != 0 || fclose(fpb) != 0) {
        printf("文件关闭失败！");
    }
    return 0;
}
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
#include <stdio.h>

typedef struct student Student;

struct student  {
    int id;
    char name[30];
    int score[3];
};

// 测试数据
// 1 Alice 90 95 100
// 2 Bob 77 76 91
// 3 Cat 99 99 99
int main() {
    int n = 5, i, j;
    double temp;
    Student students[n];
    double avg[n];
    FILE *fp;
    fp = fopen("stuinfo.txt", "a+");
    if (fp == NULL) {
        printf("文件打开失败");
        return 0;
    }
    for (i = 0; i < n; i++) {
        temp = 0;
        scanf("%d %s", &students[i].id, students[i].name);
        for (j = 0; j < 3; j++) {
            scanf("%d", &students[i].score[j]);
            temp += students[i].score[j];
        }
        avg[i] = temp / 3.0;
        fprintf(fp, "%d %s %d %d %d %lf\n", students[i].id, students[i].name, students[i].score[0],
                students[i].score[1], students[i].score[2], avg[i]);
    }
    if (fclose(fp) != 0) {
        printf("文件关闭失败！");
    }
    return 0;
}
```

[Experiment11 程序设计思想及范例](/Experiment11.md)

[返回首页](/README.md)
