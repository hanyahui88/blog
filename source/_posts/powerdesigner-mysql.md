---
title: powerdesigner添加mysql的字符集支持、设置默认值 
date: 2016-08-29 14:44:27
categories:  技术 
tags: [powerdesigner,默认值  ]
---

powerdesigner添加mysql的字符集支持、设置默认值<br/>
database->edit current DBMS<br/>
![database](/path/to/3366722196437246315.png)<br/><!--more-->
然后，选中：MYSQL50::Script/Objects/Table/Options<br/>
在options末尾添加： <br/>
ENGINE = %s : list = BDB | HEAP | ISAM | InnoDB | MERGE | MRG_MYISAM | MYISAM, default = InnoDB<br/>
DEFAULT CHARACTER SET = %s : list = utf8 | gbk, default = utf8 <br/>
COLLATE = %s : list = utf8_bin | utf8_general_ci | gbk_bin | gbk_chinese_ci, default = utf8_bin<br/>
![dbms properties](/path/to/6631673596607633152.png)<br/>
第一个：存储引擎<br/> 
第二个：字符集<br/> 
第三个：带bin是区分大小写，ci不区分<br/>
点击ok保存，回到工作区，双击某表，在：<br/> 
Physicial Options中，可以看到刚刚添加的选项，这样就可以按照自己的方式来操作了。<br/>
![Physicial Options](/path/to/6631747263886697576.png)<br/>
打开漏斗选中comment和default value 就可以设置备注和默认值了<br/>
![table properties](/path/to/6631746164375069821.png)<br/>
 