# 实验十三 并行程序设计

1.代码如下：
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include "mpi.h"

// 避开由mpicxx.h导致的编译错误
#define MPICH_SKIP_MPICXX

int main(int argc, char *argv[]) {
    // 当前进程标识
    int rank;
    // 返回值
    int nRet;
    // 进程数量
    int nProcess;
    // 源进程标识
    int source;
    // 目标进程标识
    int dest;
    // 消息标识
    int tag = 0;
    // 消息存储区
    char message[128];
    // 消息接收状态
    MPI_Status status;
    // 初始化MPI环境
    nRet = MPI_Init(&argc, &argv);
    if (nRet != MPI_SUCCESS) {
        printf("Call MPI_Init failed !\n");
        exit(0);
    }
    // 获得当前空间进程数量
    MPI_Comm_size(MPI_COMM_WORLD, &nProcess);
    // 获得当前进程ID
    nRet = MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    if (nRet != MPI_SUCCESS) {
        printf("Call MP_Comm_rank failed !\n");
        exit(0);
    }
    if (rank != 0) {
        // 当前进程不是0号进程
        sprintf(message, "你好0号进程，来自进程%d的问候！\n", rank);
        // 目标进程为0号
        dest = 0;
        // 向进程0发送消息，由于包括字符串结束标志\0
        // 所以字符数量应当为strlen(message)+1
        MPI_Send(message, strlen(message)+1, MPI_CHAR, dest, tag, MPI_COMM_WORLD);
    } else {
        for (source = 1; source < nProcess; source++) {
            // 接收所有消息
            MPI_Recv(message, 100, MPI_CHAR, source, tag, MPI_COMM_WORLD, &status);
            // 输出消息
            printf("%s\n", message);
        }
    }
    MPI_Finalize();
    return 0;
}
```

2.代码如下：
```c
#include <stdio.h>
#include <math.h>

#include "mpi.h"

// 避开由mpicxx.h导致的编译错误
#define MPICH_SKIP_MPICXX

unsigned long segmenty(unsigned long n, unsigned long m, unsigned long step) {
    unsigned long y = 0;
    unsigned long i;
    for (i = n; i <= m; i+=step) {
        y += i;
    }
    return y;
}

int main(int argc, char *argv[]) {
    int my_id, num_process, i;
    unsigned long n = 100000L, temp_sum, y;
    int name_len;
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    MPI_Status status;
    // 初始化MPI环境
    MPI_Init(&argc, &argv);
    // 获得当前空间进程数量
    MPI_Comm_size(MPI_COMM_WORLD, &num_process);
    // 获得当前进程ID
    MPI_Comm_rank(MPI_COMM_WORLD, &my_id);
    // 获得进程的详细名称
    MPI_Get_processor_name(processor_name, &name_len);
    printf("全部进程数量为%d进程%d运行在计算机%s\n", num_process, my_id, processor_name);
    // 立即清空输出缓冲区，并输出缓冲区内容
    fflush(stdout);
    temp_sum = segmenty(my_id + 1, n, num_process);
    if (my_id == 0) {
        // 编号为0的进程负责从其他进程收集计算结果
        y = temp_sum;
        for (i = 1; i < num_process; i++) {
            MPI_Recv(&temp_sum, 1, MPI_UNSIGNED_LONG, i, 0, MPI_COMM_WORLD, &status);
            y += temp_sum;
        }
        printf("Sum=%lu", y);
        // 清理输出流
        fflush(stdout);
    } else {
        // 其他进程负责将计算结果发送到编号为0的进程
        MPI_Send(&temp_sum, 1, MPI_UNSIGNED_LONG, 0, 0, MPI_COMM_WORLD);
    }
    MPI_Finalize();
    return 0;
}
```

[Experiment14 个体软件开发](/Experiment14.md)

[返回首页](/README.md)
