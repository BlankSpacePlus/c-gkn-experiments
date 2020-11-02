# 实验十二 面向对象程序设计

1.代码如下：
```cpp
#include <iostream>
#include <string>

#define NumOfStudent 5

using namespace std;

class Student {
private:
    string id;
    string name;
    double math;
    double english;
    double program;
    double sum;
public:
    void init();
    void run();
};

Student stu[NumOfStudent];

void Student::init() {
    int i;
    cout << "请分别输入5个学生的学号、姓名、数学成绩、英语成绩、计算机成绩：" << endl;
    for (i = 0; i < NumOfStudent; i++) {
        cin >> stu[i].id >> stu[i].name >> stu[i].math >> stu[i].english >> stu[i].program;
    }
}

void Student::run() {
    int i, m;
    double max = 0;
    // 求最大值
    for (i = 0; i < NumOfStudent; i++) {
        stu[i].sum = stu[i].math + stu[i].english +stu[i].program;
        if (stu[i].sum > max) {
            max = stu[i].sum;
            m = i;
        }
    }
    cout << endl;
    cout << "总分最高的学生成绩为：" << endl;
    cout << "Id\tName\tMath\tEnglish\tProgram\t" << endl;
    cout << stu[m].id << "\t" << stu[m].name << "\t" << stu[m].math << "\t" << stu[m].english << "\t"
        << stu[m].program << endl;
}

int main() {
    Student student;
    student.init();
    student.run();
    return 0;
}
```

2.代码如下：
```cpp
#include <iostream>

using namespace std;

class Calendar {
private:
    int year;
    int month;
    int day;
public:
    Calendar() {}
    Calendar(int year, int month, int day) {
        this->year = year;
        this->month = month;
        this->day = day;
    }
    int getYear() {
        return year;
    }
    int getMonth() {
        return month;
    }
    int getDay() {
        return day;
    }
    int isLeapYear() {
        return (year % 400 == 0) || (year % 4 == 0 && year % 100 != 0);
    }
};

int main() {
    Calendar calendar;
    cout << "请输入年月日：";
    int year, month, day;
    cin >> year >> month >> day;
    calendar = Calendar(year, month, day);
    cout << calendar.getYear() << "年" << calendar.getMonth() << "月" << calendar.getDay() << "日 此年"
        << (calendar.isLeapYear() ? "是" : "不是") << "闰年";
    return 0;
}
```

3.代码如下：
```cpp
#include <iostream>

#define PI 3.1415927

using namespace std;

class Shape {
protected:
    double area;
    double r;
    double width;
    double height;
public:
    Shape() {}
    virtual void calculateArea() {
        area = 0;
    }
    void display() {
        cout << "面积：" << area << endl;
    }
};

class Circle : public Shape {
public:
    Circle(double rCircle) {
        r = rCircle;
    }
    virtual void calculateArea() {
        area = PI * r * r;
    }
};

class Rectangle : public Shape {
public:
    Rectangle(double widthRec, double heightRec) {
        width = widthRec;
        height = heightRec;
    }
    virtual void calculateArea() {
        area = width * height;
    }
};

int main() {
    Circle circle(2.0);
    circle.calculateArea();
    Rectangle rectangle(3.0, 4.0);
    rectangle.calculateArea();
    circle.display();
    rectangle.display();
    return 0;
}
```

4.代码如下(这里只写一个简单的Demo)：
```cpp
#include <iostream>

using namespace std;

class RMB {
protected:
    int value;
public:
    RMB() {}
    RMB(int value) {
        this->value = value;
    }
};

class Interest : RMB {
protected:
    double rate;
public:
    Interest() {}
    Interest(int value, int level) {
        this->value = value;
        switch (level) {
            case 0:
                rate = 0.36;
                break;
            case 1:
                rate = 1.91;
                break;
            case 2:
                rate = 2.20;
                break;
            case 3:
                rate = 2.50;
                break;
            case 4:
                rate = 3.25;
                break;
            case 5:
                rate = 3.85;
                break;
            case 6:
                rate = 4.20;
                break;
        }
    }
    double calculate() {
        return value * (1+rate/100);
    }
};

int main() {
    Interest interest = Interest(100000, 5);
    cout << interest.calculate();
    return 0;
}
```

[Experiment13 并行程序设计](/Experiment13.md)

[返回首页](/README.md)
