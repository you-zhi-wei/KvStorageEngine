<style>
    h1 {
        color:green;
        text-align:center;
        counter-reset: h1
        /*font-weight:bold;*/
    }
    h2 {
        color:#ff9933;
        /*text-align:center;*/
        font-weight:bold;
    }
    h3 {
        color:#9933ff;
        /*text-align:center;*/
        font-weight:bold;
    }
    body {
        font-size:20 px;
    }
</style>

# 基于跳表实现的键值型存储引擎

## 项目说明

<font color=green size=6 face="黑体">Key-Value存储引擎</font>

该项目是作者学习数据库技术时整理的项目，非关系型数据库Redis的核心存储引擎使用的数据结构就是跳表，该项目采用C++语言基于跳表结构设计了一个轻量级键值型存储引擎，支持插入、查询、删除、显示、导出、重加载6种基本操作。

## 1.技术栈

+ 基于跳表结构和面向对象思想的节点类、跳表类的开发与封装；
+ 基于父子多进程和匿名管道技术的Stress Bench测试工具；
+ 使用互斥锁，防止并发插入数据时发生冲突；
+ 基于MakeFile的多文件编译方式；

## 2.对外接口

🔹 insert_element  //插入数据

🔸 delete_element  //删除数据

🔹 search_element  //查询数据

🔸 update_element  //更新数据 

🔹 display_list  //打印跳跃表

🔸 dump_file   //数据落盘

🔹 load_file  //加载数据

🔸 size  //返回数据规模

🔹 clear  //清空跳表 

## 3.跳表原理

  对于一个单链表来讲，即使链表中存储的数据是有序的，如果我们想要在其中查找某个数据，也只能从头开到尾的遍历，查询效率低，时间复杂度是O(n)。

  跳表是在一个原始链表中添加了多级索引，通过每一级索引来进行二分搜索的数据结构，其架构如下：

![跳表](https://img-blog.csdnimg.cn/20210430130749617.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTQ4MDc4NQ==,size_16,color_FFFFFF,t_70)

  在上述跳表中，假如查询key=10的记录，则可以从第二级索引开始快速定位：

+ 遍历第二级索引，从1开始，发现7<10<13，7就是该层要找的索引，通过它跳到下一级索引
+ 遍历第一级索引，从7开始，发现9<10<13，9就是该层要找的索引，通过它跳到下一级索引
+ 遍历原始链表，从9开始，发现10=10，10就是该层要找的最终索引

相比于直接遍历原始链表，多级索引的存在使跳表查询效率更快，总结：

**跳表的优点：** 可以实现高效的插入、删除和查询 ，时间复杂度为O(logn).

**跳表的缺点：** 需要存储多级索引，增加了额外的存储空间

**跳表的用途：** 经典的以空间换时间的数据结构，常用于非关系数据库的存储引擎中

## 4.补充说明：

该项目作者：程序员 Carl，公众号：代码随想录。作者对其代码进行学习，并尝试修改。原地址：[SkipList-CPP: A tiny KV storage based on SkipList written in C++ language](https://github.com/youngyangyang04/Skiplist-CPP )
