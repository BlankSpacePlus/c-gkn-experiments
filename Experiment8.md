# 实验八 结构体

1.代码如下：
```c
#include <stdio.h>

struct date {
    int year;
    int month;
    int day;
};

int main() {
    struct date d;
    printf("请输入年份：");
    scanf("%d", &d.year);
    printf("请输入月份：");
    scanf("%d", &d.month);
    printf("请输入日期：");
    scanf("%d", &d.day);
    int month_days[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    if (d.year % 400 == 0 || (d.year % 4 == 0 && d.year % 100 != 0)) {
        month_days[2]++;
    }
    int sum = 0;
    for (int i = 1; i < d.month; i++) {
        sum += month_days[i];
    }
    sum += d.day;
    printf("这是该年中的第%d天", sum);
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>

struct people  {
    char name[30];
    int age;
};

typedef struct people People;

int main() {
    People peoples[3] = {{"Sam", 12}, {"Tom", 18}, {"Bob", 20}}, *p;
    int max = peoples[0].age, max_index = 0, min, min_index = 0, i, n = 3;
    for (i = 0; i < n; i++) {
        p = &peoples[i];
        if (p->age > max) {
            max = p->age;
            max_index = i;
        }
        if (p->age < min) {
            min = p->age;
            min_index = i;
        }
    }
    // 精髓
    p = &peoples[n-max_index-min_index];
    printf("三人中年龄居中者的姓名是：%s，年龄是：%d\n", p->name, p->age);
    return 0;
}
```

3.代码如下(私自将float改为了double)：
```c
#include <stdio.h>

const int g_n = 3, p_n = 5;

struct student  {
    int snum;
    char name[30];
    int score[3];
    double sum; // 平均成绩
};

typedef struct student Student;

void sumScore(Student *s) {
    int sum = 0;
    for (int i = 0; i < g_n; i++) {
        sum += s->score[i];
    }
    s->sum = sum/3.0;
}

int main() {
    int i, j;
    Student students[5];
    for (i = 0; i < p_n; i++) {
        printf("请输入第%d位学生的学号、姓名、三门课程的成绩：\n", i+1);
        scanf("%d %s", &students[i].snum, students[i].name);
        for (j = 0; j < g_n; j++) {
            scanf("%d", &students[i].score[j]);
        }
        sumScore(&students[i]);
    }
    for (i = 0; i < p_n; i++) {
        printf("第%d位学生的学号是%d，姓名是%s，总成绩是%.2lf\n", i+1, students[i].snum, students[i].name, students[i].sum);
    }
    return 0;
}
```

4.代码如下(使用了内置的qsort函数)：
```c
#include <stdio.h>
#include <stdlib.h>

const int g_n = 3, p_n = 5;

struct student  {
    int snum;
    char name[30];
    int score[3];
    double sum; // 平均成绩
};

typedef struct student Student;

void sumScore(Student *s) {
    int sum = 0;
    for (int i = 0; i < g_n; i++) {
        sum += s->score[i];
    }
    s->sum = sum/3.0;
}

int cmp(const void *a,const void *b){
    Student pa = *(Student*)a, pb = *(Student*)b;
    int grade_cmp = pa.sum > pb.sum ? 1 : pa.sum == pb.sum ? 0 : -1;
    if (grade_cmp == 0) {
        return pa.snum - pb.snum;
    }
    return -grade_cmp;
}

int main() {
    int i, j;
    Student students[5];
    for (i = 0; i < p_n; i++) {
        printf("请输入第%d位学生的学号、姓名、三门课程的成绩：\n", i+1);
        scanf("%d %s", &students[i].snum, students[i].name);
        for (j = 0; j < g_n; j++) {
            scanf("%d", &students[i].score[j]);
        }
        sumScore(&students[i]);
    }
    qsort(students, p_n, sizeof(Student), cmp);
    for (i = 0; i < p_n; i++) {
        printf("第%d位学生的学号是%d，姓名是%s，总成绩是%.2lf\n", i+1, students[i].snum, students[i].name, students[i].sum);
    }
    return 0;
}
```

5.代码如下：
```c
#include <stdio.h>
#include <stdlib.h>

const int g_n = 3, p_n = 5;

typedef struct student Student;

struct student  {
    int id;
    char name[30];
    int sex; // 1->男、0->女
    char class[30];
    char major[30];
    Student *next;
};

typedef struct linkedlist LinkedList;

// 保存首尾结点的无序单链表
struct linkedlist {
    Student *head;
    Student *rear;
};

void add(LinkedList *list, Student *s) {
    if (list->head == NULL) {
        list->head = s;
        list->rear = s;
        list->head->next = NULL;
        list->rear->next = NULL;
        return;
    } else if (list->head == list->rear) {
        list->head->next = s;
    }
    s->next = NULL;
    list->rear->next = s;
    list->rear = s;
}

void show(LinkedList *list) {
    Student *s = list->head;
    if (list->head == NULL) {
        printf("学生信息列表为空!\n");
        return;
    }
    while (s != list->rear) {
        printf("学号：%d，姓名：%s，性别：%s，班级：%s，专业：%s\n", s->id, s->name, s->sex?"男":"女", s->class, s->major);
        s = s->next;
    }
    printf("学号：%d，姓名：%s，性别：%s，班级：%s，专业：%s\n", s->id, s->name, s->sex?"男":"女", s->class, s->major);
}

int main() {
    int operate;
    char choice;
    LinkedList *students = (LinkedList *)malloc(sizeof(LinkedList));
    students->head = NULL;
    students->rear = NULL;
    while (1) {
        printf("请选择操作类型：\n1\t录入学生数据\n2\t查看所有学生数据\n");
        scanf("%d", &operate);
        switch (operate) {
            case 1:
                puts("请输入学号、姓名、性别(男1女0)、班级、专业");
                Student *s = (Student *)malloc(sizeof(Student));
                puts("请输入学号：");
                scanf("%d", &s->id);
                getchar();
                puts("请输入姓名：");
                gets(s->name);
                puts("请输入性别：");
                scanf("%d", &s->sex);
                getchar();
                puts("请输入班级：");
                gets(s->class);
                puts("请输入专业：");
                gets(s->major);
                add(students, s);
                break;
            case 2:
                show(students);
                break;
        }
        printf("是否继续(Y/N)？\n");
        getchar();
        choice = getchar();
        if (choice == 'N' || choice == 'n') {
            break;
        }
    }
    Student *s = students->head;
    while (s != students->rear) {
        free(s);
    }
    free(students->rear);
    free(students);
    return 0;
}
```

6.代码如下：
```c

```

[Experiment9 预编译和宏定义](/Experiment9.md)

[返回首页](/README.md)
