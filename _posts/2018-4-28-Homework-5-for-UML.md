---
layout: post
title:  Homework 5 for UML
teaser: 系统分析与设计
date: 2018-4-28 12:00:10+00:00
category: UML
tags: [UML, HW]
---

### 1、 领域建模

- ##### a. 阅读 Asg_RH 文档，按用例构建领域模型。

  - ##### 按 Task2 要求，请使用工具 UMLet，截图格式务必是 png 并控制尺寸

  - ##### 说明：请不要受 PCMEF 层次结构影响。你需要识别实体（E）和 中介实体（M，也称状态实体）

    - ##### 在单页面应用（如 vue）中，E 一般与数据库构建有关， M 一般与 [store 模式](https://cn.vuejs.org/v2/guide/state-management.html) 有关

    - ##### 在 java web 应用中，E 一般与数据库构建有关， M 一般与 session 有关





![domain](..\i\domain.png)







- ##### b. 数据库建模(E-R 模型)

  ##### \- 按 Task 3 要求，给出系统的 E-R 模型（数据逻辑模型）

  ##### \- 建模工具 PowerDesigner（简称PD） 或开源工具 [OpenSystemArchitect](http://www.codebydesign.com/)

  ##### \- 不负责的链接 <http://www.cnblogs.com/mcgrady/archive/2013/05/25/3098588.html>

  ##### \- 导出 Mysql 物理数据库的脚本

  ##### \- 简单叙说 数据库逻辑模型 与 领域模型 的异同



![ER](..\i\ER.png)





脚本如下：

```

drop table credit_card;

drop table customer;

drop table hotel;

drop table location;

drop table reservation;

drop table room;

/*==============================================================*/
/* Table: credit_card                                           */
/*==============================================================*/
create table credit_card (
   card_number          CHAR(10)             not null,
   email                CHAR(10)             null,
   card_security_code   CHAR(10)             null,
   expiry_date          DATE                 null,
   constraint PK_CREDIT_CARD primary key (card_number)
);

/*==============================================================*/
/* Table: customer                                              */
/*==============================================================*/
create table customer (
   customer_name        VARCHAR(1)           null,
   email                CHAR(10)             not null,
   special_requirement  CHAR(10)             null,
   smoking              bool                 null,
   constraint PK_CUSTOMER primary key (email)
);

/*==============================================================*/
/* Table: hotel                                                 */
/*==============================================================*/
create table hotel (
   hotel_name           VARCHAR(1)           not null,
   city_id              INT4                 null,
   star_rating          CHAR(10)             null,
   room_type            CHAR(10)             null,
   constraint PK_HOTEL primary key (hotel_name)
);

/*==============================================================*/
/* Table: location                                              */
/*==============================================================*/
create table location (
   city_id              INT4                 not null,
   city_name            VARCHAR(1)           null,
   constraint PK_LOCATION primary key (city_id)
);

/*==============================================================*/
/* Table: reservation                                           */
/*==============================================================*/
create table reservation (
   customer_name        VARCHAR(1)           null,
   email                CHAR(10)             null,
   hotel_name           VARCHAR(1)           null,
   city_id              INT4                 null,
   room_type            VARCHAR(1)           null,
   check_in_date        DATE                 null,
   check_out_date       DATE                 null
);

/*==============================================================*/
/* Table: room                                                  */
/*==============================================================*/
create table room (
   hotel_name           VARCHAR(1)           null,
   room_type            CHAR(10)             null,
   price                FLOAT8               null
);

alter table credit_card
   add constraint FK_CREDIT_C_REFERENCE_CUSTOMER foreign key (email)
      references customer (email)
      on delete restrict on update restrict;

alter table hotel
   add constraint FK_HOTEL_REFERENCE_LOCATION foreign key (city_id)
      references location (city_id)
      on delete restrict on update restrict;

alter table reservation
   add constraint FK_RESERVAT_REFERENCE_CUSTOMER foreign key (email)
      references customer (email)
      on delete restrict on update restrict;

alter table reservation
   add constraint FK_RESERVAT_REFERENCE_HOTEL foreign key (hotel_name)
      references hotel (hotel_name)
      on delete restrict on update restrict;

alter table room
   add constraint FK_ROOM_REFERENCE_HOTEL foreign key (hotel_name)
      references hotel (hotel_name)
      on delete restrict on update restrict;




```



同：

- 都将概念抽象化，并将需求以图的形式表现出来

异：

- 领域模型是描述业务用例实现的对象模型，它是对业务角色和业务实体之间应该如何联系和协作以执行业务的一种抽象。它注重业务中承担的角色及其当前职责。
- 数据库逻辑模型是一个软件开发领域的概念，主要是为了表述数据库中的结构