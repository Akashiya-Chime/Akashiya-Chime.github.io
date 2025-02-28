---
title: C语言学习-常见标准库
tags: [C]
categories: [编程开发]
index_img: /img/c-lib.png
date: 2023-03-13 18:23:59
---

记录一些看过的标准库，以供复习和查找。

<!--more-->

## <stdio.h>
```c
/*
 * fopen，成功返回文件指针，出错返回NULL并设置errno
 * fclose，成功返回0，出错返回EOF并设置errno
 * perror，将错误信息打印到标准错误输出，首先打印参数`s`所指的字符串，然后打印:号，然后根据当前`errno`的值打印错误原因
 */
FILE *fopen(const char *path, const char *mode);
int fclose(FILE *fp);
void perror(const char *s);

/*
 * fgetc，从指定的文件中读一个字节
 * getchar，从标准输入读一个字节
 * fputc，向指定的文件写一个字节
 * putchar，向标准输出写一个字节
 * 成功返回读到的字节，出错或者读到文件末尾时返回EOF
 */
int fgetc(FILE *stream);
int getchar(void);
int fputc(int c, FILE *stream);
int putchar(int c);

/*
 * fseek，任意移动读写位置，成功返回0，出错返回-1并设置errno
 * ftell，返回当前的读写位置，成功返回当前读写位置，出错返回-1并设置errno
 * rewind，把读写位置移到文件开头
 */
int fseek(FILE *stream, long offset, int whence);
long ftell(FILE *stream);
void rewind(FILE *stream);

/*
 * fgets，从指定的文件中读一行字符到调用者提供的缓冲区中
 * gets，从标准输入读一行字符到调用者提供的缓冲区中
 */
char *fgets(char *s, int size, FILE *stream);
char *gets(char *s);

/*
 * 用于读写记录
 */
size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);

/*
 * 格式化 I/O 函数
 */
int printf(const char *format, ...);
int fprintf(FILE *stream, const char *format, ...);
int sprintf(char *str, const char *format, ...);
int snprintf(char *str, size_t size, const char *format, ...);
```

## <string.h>
```c
/*
 * strerror，错误码errnum所对应的字符串
 * memset，初始化字符串
 * strlen，取字符串长度
 */
char *strerror(int errnum);
void *memset(void *s, int c, size_t n);
size_t strlen(const char *s);

/*
 * 字符串拷贝
 * C99中，memcpy使用了restrict关键字进行优化，要求传进来的指针不允许指向重叠的内存区间
 */
char *strcpy(char *dest, const char *src);
char *strncpy(char *dest, const char *src, size_t n);
void *memcpy(void *dest, const void *src, size_t n);
void *memmove(void *dest, const void *src, size_t n);

/*
 * 连接字符串
 */
char *strcat(char *dest, const char *src);
char *strncat(char *dest, const char *src, size_t n);

/*
 * 比较字符串
 * 负值表示s1小于s2，0表示s1等于s2，正值表示s1大于s2
 */
int memcmp(const void *s1, const void *s2, size_t n);
int strcmp(const char *s1, const char *s2);
int strncmp(const char *s1, const char *s2, size_t n);

/*
 * 搜索字符串
 * strchr和strrchr如果找到字符c，返回字符串s中指向字符c的指针，如果找不到就返回NULL
 * strstr，如果找到子串，返回值指向子串的开头，如果找不到就返回NULL
 */
char *strchr(const char *s, int c);
char *strrchr(const char *s, int c);
char *strstr(const char *haystack, const char *needle);

/*
 * 分割字符串
 */
char *strtok(char *str, const char *delim);
char *strtok_r(char *str, const char *delim, char **saveptr);
```

## <stdlib.h>
```c
/*
 * 数值字符串转换
 */
int atoi(const char *nptr);
long int atol(const char *nptr);
double atof(const char *nptr);
long int strtol(const char *nptr, char **endptr, int base);
double strtod(const char *nptr, char **endptr);

/*
 * 内存分配
 * calloc，用字节0填充
 * realloc，返回新内存空间的首地址，并释放原内存空间
 * alloca，不是在堆上分配空间，而是在调用者函数的栈帧上分配空间
 */
void *malloc(size_t size);
void *calloc(size_t nmemb, size_t size);
void *realloc(void *ptr, size_t size);
#include<alloca.h>
void *alloca(size_t size);
void free(void *ptr);

/*
 * 求随机数
 */
int rand(void)
void srand(unsigned int seed);
long int random(void);
void srandom(unsigned int seed);

/*
 * 数值运算
 */
int abs(int i);
long labs(long i);
long long llabs(long long i);
```

## <pthread.h>(-lpthread)
```c
/*
 * 线程创建
 * 每一个线程都有一个唯一的线程 ID，ID 类型为 pthread_t，这个 ID 是一个无符号长整形数
 * thread: 线程创建成功，会将线程 ID 写入到这个指针指向的内存中
 * attr: 线程的属性，一般情况下使用默认属性即可，NULL
 * start_routine: 函数指针，创建出的子线程的处理动作，也就是该函数在子线程中执行。
 * arg: 作为实参传递到 start_routine 指针指向的函数内部
 * 线程创建成功返回 0，创建失败返回对应的错误号
 */
pthread_t pthread_self(void);
int pthread_create(pthread_t *restrict thread,
	const pthread_attr_t *restrict attr,
	void *(*start_routine)(void*), void *restrict arg);

/*
 * 线程调用 pthread_exit 终止自己
 * pthread_join，线程回收，主线程调用该函数的线程将挂起等待，直到id为`thread`的线程终止
 * 参数：线程退出的时候携带的数据，当前子线程的主线程会得到该数据。如果不需要使用，指定为 NULL
 * 线程分离，线程也可以被置为detach状态，这样的线程一旦终止就立刻回收它占用的所有资源，而不保留终止状态
 * 线程取消，特定情况下一个线程杀死另一个线程
 */
void pthread_exit(void *value_ptr);
int pthread_join(pthread_t thread, void **value_ptr);
int pthread_detach(pthread_t tid);
int pthread_cancel(pthread_t thread);

/*
 * 互斥锁
 * 互斥锁为pthread_mutex_t类型
 * attr: 互斥锁的属性，一般使用默认属性即可，指定为NULL
 */
pthread_mutex_t mutex;
int pthread_mutex_init(pthread_mutex_t *restrict mutex,
           const pthread_mutexattr_t *restrict attr);
int pthread_mutex_destroy(pthread_mutex_t *mutex);
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_trylock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);

/*
 * 读写锁
 * 读锁是共享的，写锁是独占的
 * 写锁比读锁优先级高
 */
pthread_rwlock_t rwlock;
int pthread_rwlock_init(pthread_rwlock_t *restrict rwlock,
           const pthread_rwlockattr_t *restrict attr);
int pthread_rwlock_destroy(pthread_rwlock_t *rwlock);
int pthread_rwlock_rdlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_tryrdlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_wrlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_trywrlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_unlock(pthread_rwlock_t *rwlock);

/*
 * 条件变量
 */
pthread_cond_t cond;
int pthread_cond_init(pthread_cond_t *restrict cond,
      const pthread_condattr_t *restrict attr);
int pthread_cond_destroy(pthread_cond_t *cond);
int pthread_cond_wait(pthread_cond_t *restrict cond, pthread_mutex_t *restrict mutex);
struct timespec {
	time_t tv_sec;      /* Seconds */
	long   tv_nsec;     /* Nanoseconds [0 .. 999999999] */
};
int pthread_cond_timedwait(pthread_cond_t *restrict cond,
           pthread_mutex_t *restrict mutex, const struct timespec *restrict abstime);
int pthread_cond_signal(pthread_cond_t *cond); // 至少有一个被解除阻塞
int pthread_cond_broadcast(pthread_cond_t *cond); // 被阻塞的线程全部解除阻塞
```

## <semaphore.h>
```c
/*
 * 信号量 semaphore
 * PV操作，P请求资源，资源量-1[wait(-1)]，V释放资源，资源量+1[post(+1)]
 */
sem_t sem;
int sem_init(sem_t *sem, int pshared, unsigned int value);
int sem_destroy(sem_t *sem);
int sem_wait(sem_t *sem);
int sem_trywait(sem_t *sem);
int sem_timedwait(sem_t *sem, const struct timespec *abs_timeout);
int sem_post(sem_t *sem);
int sem_getvalue(sem_t *sem, int *sval);
```

## <sys/socket.h> / <winsock2.h>(ws2_32.dll)
```c
#define AF_INET // IPv4 格式的 IP 地址 domain
#define AF_INET6 // IPv6 格式的 IP 地址 domain
#define SOCK_STREAM // 面向字节流，用于TCP type
#define SOCK_DGRAM // 面向数据报，用于UDP type

typedef unsigned short  uint16_t;
typedef unsigned int    uint32_t;
typedef uint16_t in_port_t;
typedef uint32_t in_addr_t;
typedef unsigned short int sa_family_t;

struct in_addr
{
    in_addr_t s_addr;
};  
// 在写数据的时候不好用
struct sockaddr {
	sa_family_t sa_family;       // 地址族协议, ipv4
	char        sa_data[14];     // 端口(2字节) + IP地址(4字节) + 填充(8字节)
}
// sizeof(struct sockaddr) == sizeof(struct sockaddr_in)
// 使用下面结构体后使用强制类型转换
struct sockaddr_in
{
    sa_family_t sin_family;     /* 地址族协议: AF_INET */
    in_port_t sin_port;         /* 端口, 2字节-> 大端  */
    struct in_addr sin_addr;    /* IP地址, 4字节 -> 大端  */
    /* 填充 8字节 */
    unsigned char sin_zero[sizeof (struct sockaddr) - sizeof(sin_family) -
                      sizeof (in_port_t) - sizeof (struct in_addr)];
};

// 创建套接字，protocol一般写0
int socket(int domain, int type, int protocol);
// 将文件描述符和本地的IP与端口进行绑定   
int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
// 给监听的套接字设置监听
int listen(int sockfd, int backlog);
// 等待并接受客户端的连接请求, 建立新的连接, 会得到一个新的文件描述符(通信的)		
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
// 接收数据
ssize_t read(int sockfd, void *buf, size_t size);
ssize_t recv(int sockfd, void *buf, size_t size, int flags);
// 发送数据的函数
ssize_t write(int fd, const void *buf, size_t len);
ssize_t send(int fd, const void *buf, size_t len, int flags);
// 成功连接服务器之后, 客户端会自动随机绑定一个端口
// 服务器端调用accept()的函数, 第二个参数存储的就是客户端的IP和端口信息
int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```

## <arpa/inet.h>
```c
// 将一个短整形从主机字节序 -> 网络字节序
uint16_t htons(uint16_t hostshort);	
// 将一个整形从主机字节序 -> 网络字节序
uint32_t htonl(uint32_t hostlong);	
// 将一个短整形从网络字节序 -> 主机字节序
uint16_t ntohs(uint16_t netshort)
// 将一个整形从网络字节序 -> 主机字节序
uint32_t ntohl(uint32_t netlong);

// 主机字节序的IP地址是字符串, 网络字节序IP地址是整形
int inet_pton(int af, const char *src, void *dst); 
// 将大端的整形数, 转换为小端的点分十进制的IP地址        
const char *inet_ntop(int af, const void *src, char *dst, socklen_t size);

// 点分十进制IP -> 大端整形
in_addr_t inet_addr (const char *cp);
// 大端整形 -> 点分十进制IP
char* inet_ntoa(struct in_addr in);
```

## <unistd.h>
```c
// 关闭置顶文件描述符的文件
int close(int fd);
// 读取文件内容并将其保存在指定的缓冲区位置
ssize_t read(int fd, void *buf, size_t size);
// 将指定的内容写入文件
ssize_t write(int fd, const void *buf, size_t size);
// sleep 几秒
unsigned sleep (unsigned seconds);
// sleep 几微妙
int usleep(unsigned useconds)
```

## <math.h>(-lm)
```c
double sin(double angle);
double cos(double angle);
double tan(double angle);
double asin(double angle);
double acos(double angle);
double atan(double angle);

double exp(double x);
double log(double x);
double log10(double x);

double pow(double x, double y);
double sqrt(double x);

double floor(double x);
double ceil(double x);
double trunc(double x);
double round(double x);
double fabs(double x);
double fmod(double x, double y);
```

## <time.h>
```c
time_t time(time_t *date_time);
char *ctime(const time_t *clock);
```