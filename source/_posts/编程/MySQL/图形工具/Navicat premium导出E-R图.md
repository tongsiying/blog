---
title: Navicat premium导出E-R图
categories: 
  - 编程
  - MySQL
  - 图形工具
date: 2019-11-23 23:05:36
updated: 2021-03-20 10:20:32
abbrlink: 50cd694e
---
<div id='my_toc'><a href="/blog/50cd694e/#大学数据库模式" class="header_1">大学数据库模式</a>&nbsp;<br><a href="/blog/50cd694e/#逆向数据库到模型" class="header_1">逆向数据库到模型</a>&nbsp;<br><a href="/blog/50cd694e/#切换E-R图-表示方式" class="header_1">切换E-R图 表示方式</a>&nbsp;<br><a href="/blog/50cd694e/#UML格式的E-R图如下所示" class="header_2">UML格式的E-R图如下所示</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 大学数据库模式
下面以数据库系统概念第6版的[大学数据库模式](https://www.db-book.com/db6/lab-dir/sample_tables-dir/index.html)作为示例
创建一个数据库名为:
```
university
```
然后进入这个数据库,执行如下建表命令:
```sql
create table classroom
    (building        varchar(15),
     room_number        varchar(7),
     capacity        numeric(4,0),
     primary key (building, room_number)
    );
create table department
    (dept_name        varchar(20), 
     building        varchar(15), 
     budget                numeric(12,2) check (budget > 0),
     primary key (dept_name)
    );
create table course
    (course_id        varchar(8), 
     title            varchar(50), 
     dept_name        varchar(20),
     credits        numeric(2,0) check (credits > 0),
     primary key (course_id),
     foreign key (dept_name) references department(dept_name)
        on delete set null
    );
create table instructor
    (ID            varchar(5), 
     name            varchar(20) not null, 
     dept_name        varchar(20), 
     salary            numeric(8,2) check (salary > 29000),
     primary key (ID),
     foreign key (dept_name) references department(dept_name)
        on delete set null
    );
create table section
    (course_id        varchar(8), 
         sec_id            varchar(8),
     semester        varchar(6)
        check (semester in ('Fall', 'Winter', 'Spring', 'Summer')), 
     year            numeric(4,0) check (year > 1701 and year < 2100), 
     building        varchar(15),
     room_number        varchar(7),
     time_slot_id        varchar(4),
     primary key (course_id, sec_id, semester, year),
     foreign key (course_id) references course(course_id)
        on delete cascade,
     foreign key (building, room_number) references classroom(building, room_number)
        on delete set null
    );
create table teaches
    (ID            varchar(5), 
     course_id        varchar(8),
     sec_id            varchar(8), 
     semester        varchar(6),
     year            numeric(4,0),
     primary key (ID, course_id, sec_id, semester, year),
     foreign key (course_id,sec_id, semester, year) references section(course_id,sec_id, semester, year)
        on delete cascade,
     foreign key (ID) references instructor(ID)
        on delete cascade
    );
create table student
    (ID            varchar(5), 
     name            varchar(20) not null, 
     dept_name        varchar(20), 
     tot_cred        numeric(3,0) check (tot_cred >= 0),
     primary key (ID),
     foreign key (dept_name) references department(dept_name)
        on delete set null
    );
create table takes
    (ID            varchar(5), 
     course_id        varchar(8),
     sec_id            varchar(8), 
     semester        varchar(6),
     year            numeric(4,0),
     grade                varchar(2),
     primary key (ID, course_id, sec_id, semester, year),
     foreign key (course_id,sec_id, semester, year) references section(course_id,sec_id, semester, year)
        on delete cascade,
     foreign key (ID) references student(ID)
        on delete cascade
    );
create table advisor
    (s_ID            varchar(5),
     i_ID            varchar(5),
     primary key (s_ID),
     foreign key (i_ID) references instructor (ID)
        on delete set null,
     foreign key (s_ID) references student (ID)
        on delete cascade
    );
create table time_slot
    (time_slot_id        varchar(4),
     day            varchar(1),
     start_hr        numeric(2) check (start_hr >= 0 and start_hr < 24),
     start_min        numeric(2) check (start_min >= 0 and start_min < 60),
     end_hr            numeric(2) check (end_hr >= 0 and end_hr < 24),
     end_min        numeric(2) check (end_min >= 0 and end_min < 60),
     primary key (time_slot_id, day, start_hr, start_min)
    );
create table prereq
    (course_id        varchar(8), 
     prereq_id        varchar(8),
     primary key (course_id, prereq_id),
     foreign key (course_id) references course(course_id)
        on delete cascade,
     foreign key (prereq_id) references course(course_id)
    );
```
# 逆向数据库到模型
**逆向数据库到模型**可以将mysql中创建好的表转成E-R图。
步骤如下图所示:
![图片](https://raw.githubusercontent.com/lanlan2017/images/master/mysql/navicat/2ER/1.png)
这样就得到`E-R`图了,如下所示:
![图片](https://raw.githubusercontent.com/lanlan2017/images/master/mysql/navicat/2ER/2.png)
# 切换E-R图 表示方式
![图片](https://raw.githubusercontent.com/lanlan2017/images/master/mysql/navicat/2ER/3.png)
## UML格式的E-R图如下所示
![图片](https://raw.githubusercontent.com/lanlan2017/images/master/mysql/navicat/2ER/4.png)
