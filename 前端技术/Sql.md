# MongoDB

## 1.1 基本介绍

**MongoDB是一种非关系型数据库,MySQL是一种关系型数据库**

**特点: 不需要设计表的结构,可以任意的存放数据,文档结构没有任何限制**

**在MongoDB中不需要显式创建数据库，如果正在使用的数据库不存在，MongoDB会自动创建。**

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

## 1.2 基本命令

### 1.2.1 查看所有数据库

**show dbs**

```bash
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
```

### 1.2.2 切换到指定的数据库

如果没有,会先切换,在添加数据后新建 **use `数据库名称`**

```bash
> use itcast
switched to db itcast
```

### 1.2.3 查看当前操作的数据库

**db**

```bash
> db
itcast
```

### 1.2.4 插入数据

 db.`集合名`.insertOne()

```bash
> db.students.insertOne({"name":"ximingx查看当前操作的数据库 **db**"})
{
        "acknowledged" : true,
        "insertedId" : ObjectId("618a5089fe5d81bd4404a9a1")
}
```

### 1.2.5  查看数据

db.`集合名`.find()

```bash
> show collections
students
> db.students.find()
{ "_id" : ObjectId("618a5089fe5d81bd4404a9a1"), "name" : "ximingx查看当前操作的数据库 **db**" }
```

### 1.2.6 用户的增删

```bash
> use admin
# 创建 root 用户
> db.createUser({user:"root用户名",pwd:"root密码",roles:["root"] })
# 验证
> db.auth("root用户名","root密码")
# 创建一般用户
# 先到要创建用户使用的数据库
> use test
# <role> admin 库添加用户和读写权限 
# 1.数据库用户角色：read、readWrite;
# 2.数据库管理角色：dbAdmin、dbOwner、userAdmin；
# 3.集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager；
# 4.备份恢复角色：backup、restore
# 5.所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase
# 6.超级用户角色：root
> db.createUser({user:"users",pwd:"users",roles[{role:"readWrite",db:"users"}]})
db.createUser({user:'user',pwd:'user',roles:[{role:'readWrite',db:'u'}]})
# 删除用户
> db.system.users.remove({user:"user"})
```

### 常用操作

```bash
# 连接MongoDB数据库
> mongo
# 显示数据库
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
test    0.000GB
# 切换使用的数据库
> use admin
switched to db admin
# 创建超级管理员
> db.createUser({user: 'root', pwd: 'root', roles: ['root']})
Successfully added user: { "user" : "root", "roles" : [ "root" ] }
# 退出
> exit
# 关闭数据库服务
> net stop mongodb
MongoDB Server (MongoDB) 服务正在停止.
MongoDB Server (MongoDB) 服务已成功停止。
# 卸载服务
> mongod --remove
{"t":{"$date":"2022-04-18T14:45:08.562+08:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"-","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"}
{"t":{"$date":"2022-04-18T14:45:08.562+08:00"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"-","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":13},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":13},"outgoing":{"minWireVersion":0,"maxWireVersion":13},"isInternalClient":true}}}
{"t":{"$date":"2022-04-18T14:45:09.015+08:00"},"s":"W",  "c":"ASIO",     "id":22601,   "ctx":"main","msg":"No TransportLayer configured during NetworkInterface startup"}
{"t":{"$date":"2022-04-18T14:45:09.015+08:00"},"s":"I",  "c":"NETWORK",  "id":4648602, "ctx":"main","msg":"Implicit TCP FastOpen in use."}
{"t":{"$date":"2022-04-18T14:45:09.018+08:00"},"s":"W",  "c":"ASIO",     "id":22601,   "ctx":"main","msg":"No TransportLayer configured during NetworkInterface startup"}
{"t":{"$date":"2022-04-18T14:45:09.018+08:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationDonorService","ns":"config.tenantMigrationDonors"}}
{"t":{"$date":"2022-04-18T14:45:09.018+08:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationRecipientService","ns":"config.tenantMigrationRecipients"}}
{"t":{"$date":"2022-04-18T14:45:09.018+08:00"},"s":"I",  "c":"CONTROL",  "id":23307,   "ctx":"main","msg":"Trying to remove Windows service","attr":{"name":"MongoDB"}}
{"t":{"$date":"2022-04-18T14:45:09.020+08:00"},"s":"I",  "c":"CONTROL",  "id":23312,   "ctx":"main","msg":"Service removed","attr":{"serviceName":"MongoDB"}}
# 安装服务
> mongod --logpath="F:\environment\mongodb\mongod.log" --dbpath="F:\environment\mongodb\data" --install –-auth
# c
> net start mongod
```

## 1.3 Mongoose

- **Mongoose 是一个让我们可以通过Node来操作MongoDB数据库的一个模块**
- Mongoose 是一个对象文档模型（ODM）库，它是对Node原生的MongoDB模块进行了进一步的优化封装
- 大多数情况下，他被用来把结构化的模式应用到一个MongoDB集合，并提供了验证和类型装换等好处
- 基于MongoDB驱动，通过关系型数据库的思想来实现非关系型数据库

### 1.3.1 new Object

1. [Schema](https://so.csdn.net/so/search?q=Schema&spm=1001.2101.3001.7020)（模式对象）
2. **Model**
3. Document

Schema 对象定义[约束](https://so.csdn.net/so/search?q=约束&spm=1001.2101.3001.7020)了数据库中的文档结构

Model 对象作为[集合](https://so.csdn.net/so/search?q=集合&spm=1001.2101.3001.7020)中的所有文档的表示，相当于MongoDB中的collection，它的每一个实例就是一个document文档

Document表示集合中的具体文档，相当于collection中的一个具体文档

### 1.3.2 安装使用

1. 安装依赖

```bash
$ yarn add mongoose
```

2. 项目中引入mongoose

```js
const mongoose = require(‘mongoose’)
```

3. 连接MongoDB数据库

```js
mongoose.connect(‘mongodb://数据库ip地址 : 端口号( 默认端口27017可以省略 )/数据库名’)
```

- connect()返回的是一个待定状态，在mongoose中有一个属性叫 connection 用来表示数据库的连接
- 通过监视该对象可以用来监听数据库的连接与断开

```js
const mongoose = require('mongoose');

// 连接集数据库
// connect()返回的是一个待定状态，
mongoose.connect(‘mongodb://数据库ip地址 : 端口号( 默认端口27017可以省略 )/数据库名’)
// 没有设置权限密码的情况
mongoose.connect('mongodb://localhost/数据库名字')
// 设置密码权限的情况
mongoose.connect('mongodb://用户名:密码@数据库的ip地址:27017/数据库名')

// 数据库连接成功事件

mongoose.connection.once(‘open’ , () => {})

// 数据库断开事件

mongoose.connection.once(‘close’ , () => {})
```

### 1.3.3 设计模式对象

- 通过`Schema`创建`Model`
- Model 代表的是数据库中的集合，通过Model才能对数据库进行操作, Schema 只是集合约束

```js
var stuSchema = new Schema({
    name: String,
    age: Number,
    gender:{
        type: String,
        default:'male'
    },
    addr: String
})

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
```

支持的字段类型

| 类型     | 作用         |
| -------- | ------------ |
| String   | 定义字符串   |
| Number   | 定义数字     |
| Date     | 定义日期     |
| Buffer   | 定义二进制   |
| Boolean  | 定义布尔值   |
| Mixed    | 定义混合类型 |
| ObjectId | 定义对象ID   |
| Array    | 定义数组     |

> 文档验证

```js
// 【required】：数据必填
// 【default】：默认值
// 【min】【max】：最小/大值 只适用于数字
// 【match】：正则匹配 只适用于字符串
// 【enum】：枚举匹配 只适用于字符串
// 【unique】： 唯一不重复
// 【maxlength】： 最大长度
// 【minlength】： 最小长度
// 【trim 】：是否有两边空格
// 【type 】：类型
// 【validate】：自定义匹配
//  validate实际上是一个函数，函数的参数代表当前字段，返回true表示通过验证，返回false表示未通过验证
var Schema =new mongoose.Schema({
  name:{
    type:String,
    required:true
  },
  age:Number
})
// 自定义验证规则 !!!!!!!!!
const courseSchema = new mongoose.Schema({
  id: {
    type: Number,
    validate: {
      validator: v => {
        // 当返回结果为 true, 满足条件
        return v > 0;
      },
      message() {
        return 'Id必须大于0';
      }
    }
  }
})
```



>  **timestamps**

当 schema 中设置timestamps为 true 时，schema映射的文档 document 会自动添加 createdAt 和 updatedA t这两个字段，代表创建时间和更新时间

```js
var stuSchema = new Schema({
    name: String,
    timestamps: true
})
```

> **_id**

当未定义`_id`字段时 mongoose 会为每一个文档自动添加一个不重复的`_id`，类型为ObiectId（在查询语句中需要通过 findById() 才能查询）

### 1.3.4 转换为模型

```js
// 将文档结构发布为模型
// 第一个参数 最后会转化成 小写复数 的集合名称
// 第二个参数 选择需要对应的 Schema
//将stuSchema映射到一个MongoDB collection并定义这个文档的构成

const User = mongoose.model('User',userSchema)

const Student = mongoose.model('Student',stuSchema)

// 然后可以进行操作
// 对数据库进行增、删、改、查
Student.create({
    name: "ximingx",
    age: 20,
    gender: "male",
    addr: "山西省"
})
```

### 1.3.5 断开数据库连接

```js
// 一般不使用
mongoose.disconnect()
```

### 1.3.6 模型的操作

#### 1.3.6.1 插入操作

> **save()**

```js
// 现在仅仅是创建
const course = new Course({
    name: "mongose",
    author: "aw",
    isPublished: true
})

// 将文档插入到数据库
course.save()
```

> **create()**

```js
// 参数: {插入的集合}, 回调函数
Course.create({
  name: 'React Course',
},(err,doc) => {
    // 错误对象
  if(err) console.log(err);
    // 当前插入的文档
  console.log(doc);
})
```

> **insertMany**
>
> - Model.insertMany(doc(s), [options], [callback])

```js
Student.insertMany({name:"小明",grades:68},{name:"小芳",grades:94},(err,docs) => {
    if(err) {
        console.log(err)
    }
    // 返回值为一个数组
    console.log(docs)
})
```

#### 1.3.6.2 查询操作

> **find()**
>
> - Model.find(conditions, [projection], [options], [callback])
>
> - conditions：查询条件
>
>   [projection]：控制返回字段
>
>   [options]：配置查询参数
>
>   [callback]：回调函数–function(err,docs){}

> 1. 条件查询
>
> + 当条件为 null 时, 查询所有的数据
>
> + $or　　　　 或关系
>
>   $nor　　　 或关系取反
>
>   **$gt　　　　 大于**
>
>   **$gte　　　 大于等于**
>
>   **$lt　　　　 小于**
>
>   **$lte　　　 小于等于**
>
>   **$ne　　　　 不等于**
>
>   **$in　　　　 在多个值范围内**
>
>   **$nin　　　 不在多个值范围内**
>
>   $all　　　 匹配数组中多个值
>
>   **$regex　　 正则，用于模糊查询**
>
>   $size　　　 匹配数组大小
>
>   $maxDistance　 范围查询，距离（基于LBS）
>
>   $mod　　　　 取模运算
>
>   $near　　　 邻域查询，查询附近的位置（基于LBS）
>
>   $exists　　 字段是否存在
>
>   $elemMatch　 匹配内数组内的元素
>
>   $within　　　 范围查询（基于LBS）
>
>   $box　　　　 范围查询，矩形范围（基于LBS）
>
>   $center　　　 范围醒询，圆形范围（基于LBS）
>
>   $centerSphere　范围查询，球形范围（基于LBS）
>
>   $slice　　　　 查询字段集合中的元素（比如从第几个之后，第N到第M个元素
>
> + | 方法     | 作用     |
>   | -------- | -------- |
>   | sort     | 排序     |
>   | skip     | 跳过     |
>   | limit    | 限制     |
>   | select   | 显示字段 |
>   | exect    | 执行     |
>   | count    | 计数     |
>   | distinct | 去重     |

```js
// isPublished 为 true 的所有
Course.find({isPublished: true})
// age 大于20 小于 28 的所有
Course.find({age: {$gt: 20, $lt: 28}})
// hobbies 中匹配包含 敲代码 的文档
Course.find({hobbies: {$in: ['敲代码']}})
 //找出跳过前两条数据的其他数据
Course.find(null,null,{skip:2})
// 对查找的结果排序
stuModel.find().sort('test')
// 显示name、grades字段，不显示_id字段
stuModel.find().select('name grades -_id')
// 显示2个
stuModel.find().limit(2)
// 跳过1个，显示其他
stuModel.find().skip(1)
```

> 2. 返回文档中的第一条, 只有一条 ~ !

```js
Course.findOne({name: 'React Course'})
```

> 3. **findById()**

```js
stuModel.findById(id)
```

> 查询文档总数

```js
// 查询文档的总数
Course.countDocument({})
```

#### 1.3.6.3 更新操作

> - Model.update(conditions, doc, [options], [callback])
> - **若设置了查询条件，当数据库不满足时默认什么也不发生**
> - update() 方法中的回调函数不能省略，否则数据不会更新

```js
stuModel.update({name:'小明'},{$set:{test:34}},(err,raw)=>{
   // 查询name为小明的数据，并将其test更改为34
   // 若有多个文档，默认只更新第一个
   console.log(raw)
})
```

> **updateOne()**

```js
// 方法
Course.updateOne({查询条件}, {要修改的值}).then(res => {
  console.log(res)
})

// 更新一条
Course.updateOne({name: 'lisi'}, {name: "aw"}).then(res => {
  console.log(res)
})
```

> updateMany

```js
// 更新多条
Course.updateMany({name: 'lisi'}, {name: "aw"}).then(res => {
  console.log(res)
})
```

#### 1.3.6.4 删除操作

> remove()
>
> - 会删除符合条件的所有数据

```js
stuModel.remove({name:/差生/},function(err){})
    // 回调函数不能省略，但可以使用exec() 简写
    // stuModel.remove({name:/差生/}).exec()
})
```

> findOneAndDelete()

```js
// 删除一个满足条件的文档
Course.findOneAndDelete({ _id: '5c9d8f9c9c9d8f9c9c9d8f9c' })
  .then(result => console.log(result))
  .catch(err => console.log(err));
```

> deleteMany()

```js
// 表演一个删库跑路
Course.deleteMany({})
  .then(result => console.log(result));
// { acknowledged: true, deletedCount: 5 }
// { 成功 删除 5 个文档 }
```

### 1.3.7 关联集合

通常不同集合的数据之间是有关系的，例如文章信息和用户信息存储在不同集合中，但文章是某个用户发表的，要查询文章的所有信息包括发表用户，就需要用到集合关联

- 使用id对集合进行关联
- 使用populate方法进行关联集合查询

| **文章集合** | **用户集合** |
| ------------ | ------------ |
| _id          | _id          |
| title        | name         |
| author       | age          |
| content      | hobbies      |

```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/test')
  .then(() => console.log('Connected to MongoDB...'))
  .catch(err => console.error('Could not connect to MongoDB...', err));

const User = mongoose.model('User', new mongoose.Schema({
  name: String,
  age: Number
}));
const Post = mongoose.model('Post', new mongoose.Schema({
  title: String,
  content: String,
  author: {
    // id 的字段类型
    type: mongoose.Schema.Types.ObjectId,
    // 关联的模型
    ref: 'User'
  }
}));

// 将集合关联
User.create({
  name: 'John Doe',
  age: 32
}).then((result) => {
  return Post.create({
    title: 'My first post',
    content: 'Hello world!',
    author: result._id
  })
})

// 查询
Post.findOne().populate('author').then(post => {
  console.log(post);
})
```





# 	MySQL

[MySQL这篇写的很烂,看他的,啊呜](https://blog.csdn.net/weixin_45851945/article/details/114287877)
[要不看这篇也行,也很不错](https://ximingx.blog.csdn.net/article/details/122157925)

## 2.1 mysql 操作

### 2.1.1 连接mysql

```sql
//连接数据库
mysql -u root -p

//修改用户密码
update mysql.user set authentication_string=password('n') where user='root' and Host = 'localhost';

//刷新权限
flush privileges

//退出连接
exit;
```

### 2.1.2 操作数据库

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

### 2.1.3 操作表

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

### 2.1.4 修改表的结构

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

### 2.1.5 索引的分类

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

### 2.1.6 外键

```sql
ALTER TABLE `表一` ADD CONSTRAINT `FK_引用列` FOREIGN KEY(`作为外键的 列`) REFERENCES `表二`(`那个字段`);
```

### 2.1.7 增删改查

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

### 2.1.8 where 检索数据

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

### 2.1.8 常用函数

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



## 2.2 Node.js 操作

首先需要安装 

```bash
$ yarn add mysql
```

### 2.2.1 基础的使用

```js
var mysql = require('mysql');
var connection = mysql.createConnection({
    host: 'localhost',
    user: 'me',
    password: 'secret',
    database: 'my_db'
});

connection.connect();

connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results[0].solution);
});

connection.end();
// 您在连接上调用的每个方法都会排队并按顺序执行。
// 关闭连接使用end(), 确保在向 mysql 服务器发送退出数据包之前执行所有剩余查询。
```



```js
// 关闭连接
connection.end(function(err) {
  // The connection is terminated now
});

connection.destroy();
// 这将导致底层套接字立即终止。另外destroy()保证不会为连接触发更多事件或回调。
```
### 2.2.2 直接连接数据库进行操作

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

### 2.2.3 池化链接

该模块不是一个接一个地创建和管理连接，而是使用`mysql.createPool(config)`

创建一个池并直接使用它：

```js
var mysql = require('mysql');
var pool = mysql.createPool({
    connectionLimit: 10,
    host: 'localhost',
    user: 'bob',
    password: 'secret',
    database: 'my_db'
});

pool.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results[0].solution);
});
```





# 服务器数据库的配置

在云服务器宝塔面板安装mongodb数据库后，连接有些问题，特此记录一下。

## » 服务器设置 Mongodb

### 1.宝塔安装mongodb

软件商店搜索 mongodb 安装即可

![image-20220422192725423](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204221927538.png)

### 2.修改mongodb配置

`bindIp` 由127.0.0.1改为0.0.0.0，放开ip限制

![image-20220422193002943](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204221930055.png)

### 3.宝塔放开 27017 端口

![image-20220422192910259](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204221929362.png)

### 4.服务器放开 27017 端口

![image-20220422193104327](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204221931436.png)

### 5.验证

浏览器打开 http://公网ip:27017，出现下图表示安装成功了

![image-20220422193227642](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204221932752.png)

### 6.无密码连接

新建远程连接，输入ip和端口即可

![image-20220422193322592](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204221933647.png)

### 7.配置用户名密码

通过宝塔终端或shell执行如下步骤:

1.连接mongo

```bash
> cd /www/server/mongodb/bin/

> ./mongo

# 这里会显示很多, 但是不需要管

Implicit session: session { "id" : UUID("~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~  ~") }
MongoDB server version: 4.4.6
Welcome to the MongoDB shell.
    For interactive help, type "help".
    For more comprehensive documentation, see
https://docs.mongodb.com/
    Questions? Try the MongoDB Developer Community Forums
https://community.mongodb.com
    ---
        The server generated these startup warnings when booting:
    2022-04-22T19:10:34.984+08:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
    2022-04-22T19:10:35.494+08:00: /sys/kernel/mm/transparent_hugepage/enabled is 'always'. We suggest setting it to 'never'
2022-04-22T19:10:35.494+08:00: /sys/kernel/mm/transparent_hugepage/defrag is 'always'. We suggest setting it to 'never'
---
    ---
        Enable MongoDB's free cloud-based monitoring service, which will then receive and display
metrics about your deployment (disk utilization, CPU, operation statistics, etc).

The monitoring data will be available on a MongoDB website with a unique URL accessible to you
and anyone you share the URL with. MongoDB may use this information to make product
improvements and to suggest MongoDB products and deployment options to you.

    To enable free monitoring, run the following command: db.enableFreeMonitoring()
To permanently disable this reminder, run the following command: db.disableFreeMonitoring()
---

# 然后输入
# 切换数据库
> use admin

switched to db admin

# <role> admin 库添加用户和读写权限 
# 1.数据库用户角色：read、readWrite;
# 2.数据库管理角色：dbAdmin、dbOwner、userAdmin；
# 3.集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager；
# 4.备份恢复角色：backup、restore
# 5.所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase
# 6.超级用户角色：root
> db.createUser({user:"用户名",pwd:"密码",roles:["root"] })
Successfully added user: {
  "user" : "用户名",
      "roles" : [
    {
      "role" : "",
      "db" : ""
    }
  ]
}

# 验证
> db.auth("用户名","密码")

Error: Authentication failed.
0

> db.auth("用户名","密码")
1

> ^C
bye
```

### 8. 修改mongodb配置

修改mongodb配置文件中的`authorization` 为 enabled，并重启

![image-20220422193831919](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204221938996.png)

### 9. 重新连接

怎么说, 如果可以麻烦好评 + 1

