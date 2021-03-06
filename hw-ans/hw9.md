# hw9 参考答案

## 9.11  

* 虚拟地址格式  

`vm = 0x027c` 

| 13 | 12 | 11| 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |   
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |   
| 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 0 | 0 |


* 地址翻译

| 参数 | 值 |
| --- | --- |
| VPN | `0x9` |   
| TLBI | `0x1` |
| TLBT | `0x2` |  
| TLB命中 | 否 |
| 缺页 | 否 |
| PPN | `0x17` |  


* 物理地址格式  

`pm = 0x5fc`    

| 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |   
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |   
| 0 | 1 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 |


* 物理地址引用  

| 参数 | 值 |
| --- | --- |  
| 字节偏移 | 0x0 |  
| 缓存索引 | 0xF |  
| 缓存标记 | 0x17 | 
| 缓存命中 | 否 |  
| 返回的缓存字节 | - |  


## 9.12  

* 虚拟地址格式  

`vm = 0x03a9` 

| 13 | 12 | 11| 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |   
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |   
| 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 |


* 地址翻译

| 参数 | 值 |
| --- | --- |
| VPN | `0xE` |   
| TLBI | `0x2` |
| TLBT | `0x3` |  
| TLB命中 | 否 |
| 缺页 | 否 |
| PPN | `0x11` |  

* 物理地址格式  
`pm = 0x469`    

| 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |   
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |   
| 0 | 1 | 0 | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 0 | 1 |


* 物理地址引用  

| 参数 | 值 |
| --- | --- |  
| 字节偏移 | 0x1 |  
| 缓存索引 | 0xA |  
| 缓存标记 | 0x11 | 
| 缓存命中 | 否 |  
| 返回的缓存字节 | - |  

## 9.13

* 虚拟地址格式  

`vm = 0x0040` 

| 13 | 12 | 11| 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |   
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |   
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |


* 地址翻译

| 参数 | 值 |
| --- | --- |
| VPN | `0x1` |   
| TLBI | `0x1` |
| TLBT | `0x0` |  
| TLB命中 | 否 |
| 缺页 | 是 |
| PPN | - |  

## 9.14  

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>

int main()
{
    int fd;
    char *buf;
    size_t length;
    struct stat stat;
        
    fd = open("hello.txt", O_RDWR, 0);
    fstat(fd, &stat);
    length = stat.st_size;
    
    buf = mmap(NULL, length, PROT_WRITE, MAP_SHARED, fd, 0); 
    buf[0] = 'J';
    munmap(buf, length); 
    close(fd);
    return 0;
}
```
