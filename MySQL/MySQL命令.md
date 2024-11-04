```
C:\Windows\System32>D:
	手动进入D盘
D:\>cd D:\Program Files\MySQL\MySQL Server 8.1\bin
	进入bin
D:\Program Files\MySQL\MySQL Server 8.1\bin>net start MySQL81
	启动MySQL81服务
D:\Program Files\MySQL\MySQL Server 8.1\bin>mysql -P 3306 -h 127.0.0.1 -u root -p
Enter password: **********
	链接到 MySQL monitor
mysql> show databases;
CREATE DATABASE cateam_db;
use cateam_db;
```

```
CREATE TABLE IF NOT EXISTS cateam_members (
   -> cateam_id INT NOT NULL AUTO_INCREMENT,
   -> cateam_name VARCHAR(100) NOT NULL,
   -> cateam_phone VARCHAR(40) NOT NULL,
   -> submission_date DATE,
   -> PRIMARY KEY ( cateam_id )
   -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

```
desc cateam_members;
	查看这个表
```

```

mysql> INSERT INTO cateam_members
    -> (cateam_name, cateam_phone, submission_date)
    -> VALUES
    -> ("吴伟翔", "电话1234567", NOW());
```

如果数据是字符型，必须使用单引号或者双引号，如："value"。

在以上实例中，我们并没有提供 runoob_id 的数据，因为该字段我们在创建表的时候已经设置它为 AUTO_INCREMENT(自动增加) 属性。 所以，该字段会自动递增而不需要我们去设置。实例中 NOW() 是一个 MySQL 函数，该函数返回日期和时间。

接下来我们可以通过以下语句查看数据表数据：
`select * from cateam_members;`