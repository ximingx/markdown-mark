# MongoDB

[MySQL这篇写的很烂,看他的,啊呜](https://blog.csdn.net/weixin_45851945/article/details/114287877)
[要不看这篇也行,也很不错](https://ximingx.blog.csdn.net/article/details/122157925)
## 介绍

**存储结构**

可以拥有多个数据库 local , admin , config ,app

每一个数据库可以有多个集合 user , products

每一个集合可以拥有多个文档(相当于MySQL的表记录)

| **术语**   | **解释说明**                                             |
| ---------- | -------------------------------------------------------- |
| database   | 数据库，mongoDB数据库软件中可以建立多个数据库            |
| collection | 集合，一组数据的集合，可以理解为JavaScript中的数组       |
| document   | 文档，一条具体的数据，可以理解为JavaScript中的对象       |
| field      | 字段，文档中的属性名称，可以理解为JavaScript中的对象属性 |

```json
{
    local: {
        
    },
    admin: {
        
    },
    config: {
        
    },
    app: {
        user: [
            {
                name: ''
            }
        ],
        products: [
            
        ]
    }
}
```

**MongoDB是一种非关系型数据库,MySQL是一种关系型数据库**

特点: **不需要设计表的结构,可以任意的存放数据,文档结构没有任何限制**

**在MongoDB中不需要显式创建数据库，如果正在使用的数据库不存在，MongoDB会自动创建。**

配置环境变量: path 直接添加安装地址的bin目录

安装成功标志

```bash
mongod --version
```

**手动添加地址地址** C:\data\db

开启服务

```bash
mongod 

sudo mongod --dbpath=/Users/ximingx/data (mac)
```

开启服务后 , 连接mongodb数据库,默认连接本地

```bash
mongo
//连接后可以通过exit退出连接
```

## 基本命令

查看显示所有数据库 **show dbs**

```bash
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
```

切换到指定的数据库(如果没有,会先切换,在添加数据后新建) **use `数据库名称`**

```bash
> use itcast
switched to db itcast
> db
itcast
```

查看当前操作的数据库 **db**

```bash
> db
itcast
```

插入数据 db.`集合名`.insertOne()

```bash
> db.students.insertOne({"name":"ximingx查看当前操作的数据库 **db**"})
{
        "acknowledged" : true,
        "insertedId" : ObjectId("618a5089fe5d81bd4404a9a1")
}
```

查看数据 db.`集合名`.find()

```bash
> show collections
students
> db.students.find()
{ "_id" : ObjectId("618a5089fe5d81bd4404a9a1"), "name" : "ximingx查看当前操作的数据库 **db**" }
```

## Node.js 操作MongoDB

安装依赖

```bash
npm install mongoose
```

**简单无约束的使用**

```js
const mongoose = require('mongoose');
// 连接集数据库
mongoose.connect('mongodb://localhost:27017/test');
// 创建一个模型,设计数据库
// 要求 cat 这个表中,name的值是字符串格式
const Cat = mongoose.model('Cat', {name: String});
for (let i = 0; i < 100; i++) {
  // 实例化一个 Cat
  const kitty = new Cat({name: 'mm' + i});
  // 持久化保存实例
  kitty.save().then(() => console.log('meow'));
}
```

```bash
> show dbs
admin   0.000GB
config  0.000GB
itcast  0.000GB
local   0.000GB
test    0.000GB
> db
itcast
> use test
switched to db test
> show collections
cats
> db.cats.find()
{ "_id" : ObjectId("618a55b5c65e76624f7eb9ec"), "name" : "Zildjian", "__v" : 0 }
```

**设计约束**

```js
const mongoose = require('mongoose')
const Schema = mongoose.Schema
// 连接数据库
mongoose.connect('mongodb://localhost/test').then(r => console.log('connect success'))
// 设计约束
const userSchema = new Schema({
  username: {
    type: String,
    required: true
  },
  password: {
    type: String,
    required: true
  },
  email: {
    type: String
  }
})
// 将文档结构发布为模型
// 第一个参数 最后会转化成 小写复数 的集合名称
// 第二个参数 选择架构
// 返回模型构造函数
// 简单地说 , 用这个约束模型 创建一个 users 集合
const User = mongoose.model('User',userSchema)
// 操作数据
```

**增**

```js
User.insertMany([
	{
          username: 'adawdin',
  		  password: '123456',
  		  email: ''
    },
    {
          username: 'adawdin',
  		  password: '123456',
  		  email: ''
    }
]).then((res)=>{
    console.log('添加成功')
}).catch((err)=>{
    console.log('失败了')
})

```

```js
// 需要先 new 一个实例
const admin = new User({
  username: 'admin',
  password: '123456',
  email: ''
})
// 然后才可以增加
admin.save(function (err,result) {
  if (err) {
    console.log("保存失败")
  } else {
    console.log('保存成功')
  }
})
```

**查**

```js
User.find(function (err,result) {
  if (err) {
    console.log("查询失败")
  } else {
    console.log(result)
  }
})
// [
//   {
//     _id: new ObjectId("618a5f40969aa535f8a22f23"),
//     username: 'admin',
//     password: '123456',
//     email: '',
//     __v: 0
//   }
// ]

// 带条件查询
User.find({
  username: 'admin'
},function (err,result) {
  if (err) {
    console.log("查询失败")
  } else {
    console.log(result)
  }
})
// 外层是数组
// [
//   {
//     _id: new ObjectId("618a5f40969aa535f8a22f23"),
//     username: 'admin',
//     password: '123456',
//     email: '',
//     __v: 0
//   }
// ]

// 查询找到的第一条数据
User.findOne(function (err,result) {
  if (err) {
    console.log("查询失败")
  } else {
    console.log(result)
  }
})
// 直接是一个对象
// {
//   _id: new ObjectId("618a5f40969aa535f8a22f23"),
//   username: 'admin',
//   password: '123456',
//   email: '',
//   __v: 0
// }
```

**删**

```js
// 删除数据
User.remove({
  username: 'adawdn'
},function (err,result) {
  if (err) {
    console.log("删除失败")
  } else {
    console.log("删除成功")
  }
})
// 清空当前集合所有数据 remove
User.remove().then((res)=>{
	console.log('删除成功')
})
// 删除满足条件的一条数据 deleteOne
User.deleteOne({name:'lili'}).then((res)=>{
	console.log('删除成功')
})
// 删除满足条件的多条数据 deleteMany
User.deleteMany({sex:'boy'}).then((res)=>{
	console.log('删除成功')
})
```

**改**

```js
User.findByIdAndUpdate('618a5f40969aa535f8a22f23',{
  password: '12345678'
},function (err,result) {
  if (err) {
    console.log("修改失败")
  } else {
    console.log("修改成功")
  }
})
// 更新一条数据 update
User.update({name:'Max'},{age:23}).then((res)=>{
	console.log('update')
})
// 更新满足条件的多条数据 updateMany
User.updateMany({name:'Max'},{age:23}).then((res)=>{
    console.log('update')
})
```



# 	MySQL

## 连接mysql

```sql
//连接数据库
mysql -uroot -p

//修改用户密码
update mysql.user set authentication_string=password('n') 
where user='root' and Host = 'localhost';

//刷新权限
flush privileges

//退出连接
exit;
```

## 操作数据库

```sql
//创建数据库
create database [if not exists] 数据库名

//删除数据库
drop database [if not exists] 数据库名

//使用数据库
use 数据库名

//查看所有的数据库
show databases
```

## 操作表

```sql
//创建表
create table if not exists 表名(
	`id` int(4) not null auto_increment comment '学号',
    `name` varchar(30) not null default '匿名' comment '姓名',
    `pwd` varchar(20) not null default '123456' comment '密码',
    `sex` varchar(3) not null default '女' comment '性别',
    `birthday` datetime default null comment '出生日期',
    `address` varchar(100) default null comment '家庭住址',
    `email` varchar(50) default null comment '邮件',
    primary key (`id`)
)engine=innodb default charset=utf8
 //查看表中信息
 describe 表名;  //简写 desc 
 //显示表的结构
 DESC `表名`   
```

## 修改表的结构

```sql
//更改表名
ALTER TABLE `表名` RENAME `新表名`;
//添加字段名
ALTER TABLE `表名` ADD `字段名` `字段的列属性`;
//修改表的字段
ALTER TABLE `表名` MODIFY `字段名` `约束`   //修改约束
alter table user modify court_id char(16);
ALTER TABLE `表名` CHANGE `字段名` `新字段名` `类型` //重命名字段
alter table user change courtid court_id int;
//删除表的字段
ALTER TABLE `表名` DROP `字段名`;
//删除表
DROP TABLE IF EXISTS `表名`
```

## 索引的分类

*   **主键索引(primary key)**

    唯一的表示,主键不可重复,只能有一个列作为主键

*   **唯一索引(unique key)**

    避免重复列的出现,唯一索引可以重复,多个列都可以标识唯一索引

*   **常规索引(key / index)**

    默认的,index,key关键字修饰

*   **全文索引(fulltext)**

    特定的数据库引擎才有

    快速定位

```sql
//列名   索引名
alter table `数据库名`.`表名` add 索引分类 index `列名`(`索引名称`)

//全文索引
explain select * from `table` where match(studentName) against('aw');
```


## 外键

```sql
ALTER TABLE `表一` ADD CONSTRAINT `FK_引用列` FOREIGN KEY(`作为外键的 列`) REFERENCES `表二`(`那个字段`);
```

## 增删改查

```sql
INSERT INTO `表名`(`属性1`,`属性2`,`属性3`)VALUES(`值1`,`值2`,`值3`),(`值1`,`值2`,`值3`);

DELETE FROM `表名` WHERE 条件;

UPDATE `表名` SET `属性` = ' ' WHERE [条件]

SELECT DISTINCT <select_list>
FROM <left_table>
<join_type> JOIN <right_table>
ON <join_condition>
WHERE <where_condition>
GROUP BY <group_by_list>
HAVING <having_condition>
ORDER BY <order_by_condition>
LIMIT <limit_number>

// 发现重复数据,去重
select distinct `字段名` from `表名`
```

## where 检索数据中符合条件的值,条件子句

>    逻辑运算符
>
>    and    or     not
>

搜索条件

```sql
select `字段名` from `表名` where 条件 
```

模糊查询

| 运算符      | 语法               | 描述                          |
| ----------- | ------------------ | ----------------------------- |
| is null     | a is null          | 如果操作符为null,结果为真     |
| is not null | a is not null      | 如果操作符不为null,结果为真   |
| between     | a between b and c  | 若a在 c 和 b之间.结果为真     |
| like        | a like b           | 如果a匹配到b,结果为真         |
| in          | a in (a1,a2,a3,a4) | 加入a在a1,a2,a3,a4中,结果为真 |

```sql
// like  %(代表0和任意字符)  _(代表一个字符)单条数据内查询

select `字段名` from `表名` 
where `字段名` like '查询的%'   

select `字段名` from `表名` 
where `字段名` like '查询的_'   

select `字段名` from `表名` 
where `字段名` like '%查%'    
```



```sql
// 多条范围内查询
select `字段名` from `表名` where `字段名` in('1','2') 
查询只在1,2范围内

select `字段名` from `表名` where `字段名` in('北京')    
查询只在北京的
```



```sql
select `字段名` from `表名` where `字段名` is null       
查询该数据为null的

select `字段名` from `表名` where `字段名` is null or `字段名` = '';  
查询该数据为null的或者空的
```

## 常用函数

>   abs    绝对值函数

```sql
select abs(-8)                     
//8
```

>ceiling  向上取整

```sql
select ceiling(6.6)                
//7 
```

>   floor   向下取整

```sql
select floor(6.6)                  
//6
```

>   rand 随机数

```sql
select  rand()                    
//返回一个随机数
```

>   sing  判断一个数的符号                                   
>
>   **-1,0,1**

```sql
select sing(0)
```

>   返回字符串长度

```sql
select char_length('啊呜')          
//2
```

>   concat   连接字符串

```sql
select concat('啊','呜')            
//啊呜
```

>   insert  替换字符串

```sql
select insert('啊呜',1,1,'嗯')       
//嗯呜 
```

>   lower   转化为小写
>
>   upper  转化为大写

```sql
select lower('AW')
```

>   current_date 获取当前日期

```sql
select current_date()
```

>   curdate  获取当前日期

```sql
select curdate()
```

>   now 获取当前时间

```sql
select now()
```

>   时间

```sql
select year(now())
select month(now())
select day(now())
select hour(now())
select minute(now())
select second(now())
```

>   系统

```sql
select system_user()    
//获取当前用户
select version()        
//版本
```



## Node.js 操作MySQL

```js
// npm i mysql
const mysql = require('mysql');
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '123456',
  database: 'node'
});

connection.connect(function (err) {
  if (err) {
    console.error('error connecting: ' + err.stack);
    return;
  }
  console.log('connected');
});
// 执行 MySQL 语句
connection.query('SELECT * FROM `sc`', function (error, results, fields) {
  if (error) throw error;
  console.log(results)
});
```



```js
// 关闭连接
connection.end(function(err) {
  // The connection is terminated now
});
```
一个实例
```js
const express = require('express')
const app = express();
// 连接数据库
const mysql = require('mysql');
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '123456',
  database: 'ximingx'
});
connection.connect(function (err) {
  if (err) {
    console.error('error connecting: ' + err.stack);
    return;
  }
  console.log('connected');
});
// 设置允许跨域访问该服务
app.all('*', function (req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  res.header('Access-Control-Allow-Methods', 'PUT, GET, POST, DELETE, OPTIONS');
  res.header("Access-Control-Allow-Headers", "X-Requested-With");
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  res.header('Access-Control-Allow-Headers', 'mytoken');
  next();
});
// login
app.get('/login', function (req, res) {
  connection.query('SELECT name FROM `user`', function (error, results, fields) {
    let index = results.findIndex((item) => {
      return item.name === req.query.username;
    })
    if (index !== -1) {
      connection.query('SELECT password FROM `user` where `name` = ?',[req.query.username], function (error, results, fields) {
        if (results[0].password === req.query.password) {
          res.send("success")
        } else {
          res.send("error")
        }
      });
    } else {
      res.send("error")
    }
  });
});
// show
app.get('/show',function (req, res) {
  connection.query('SELECT * FROM `students`', function (error, results, fields) {
    res.send(results)
  });
})
// add
app.get('/add',function (req, res) {
  console.log(req.query)
  connection.query('INSERT INTO `students` (`id`,`name`,`sex`,`age`) VALUES(?,?,?,?)', [req.query.id,req.query.name,req.query.sex,req.query.age], function (error, results, fields) {
    if (error) {
      res.send(error)
    } else {
      res.send("success")
    }
  });
})
// cha
app.get('/cha',function (req, res) {
  console.log(req.query)
  connection.query('UPDATE `students` SET id=?,name=?,sex=?,age=? WHERE id=?', [req.query.id,req.query.name,req.query.sex,req.query.age,req.query.old], function (error, results, fields) {
    if (error) {
      res.send(error)
    } else {
      res.send("success")
    }
  });
})
// del
app.get('/del',function (req, res) {
  console.log(req.query)
  connection.query('DELETE FROM `students` where id = ?;', [req.query.id], function (error, results, fields) {
    if (error) {
      res.send(error)
    } else {
      res.send("success")
    }
  });
})
// que
app.get('/que',function (req, res) {
  console.log(req.query)
  connection.query('SELECT * FROM `students` where name = ?;', [req.query.name], function (error, results, fields) {
    if (error) {
      res.send(error)
    } else {
      console.log(results)
      res.send(results)
    }
  });
})

// 端口
app.listen(3000,function () {
  console.log("// -----------------------------------------------------------------------")
  console.log("port 3000 is listening")
});
```