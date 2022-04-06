## 基础概念

Android是一个以Linux为基础的开源操作系统

Android系统分为四层：

- linux 内核层
- 系统用行库层
- 应用程序框架层
- 应用程序层

Android 应用程序包含四种组件：

- Activity
- Service
- Broadcast Receiver
- Content Provider

应用程序生命周期

- 前台进程
- 可见进程
- 服务进程
- 后台进程
- 空进程

## 清单文件

***\*设置清单文件的属性时，需要遵守几项规则\****：

◼元素：在所有的元素中只有`<manifest>`和`<application>`是必需的且只能出现一次

◼属性：元素的属性大部分是可选的但有少数属性是必须设置的

◼定义类名：所有的元素名都对应其在SDK中的类名

◼多数值项：如果某个元素有超过一个数值时，必须通过重复的方式来说明该元素的某个属性具有多个数值项，且不能将多个数值项一次性说明在一个属性中

◼资源项说明：需要引用某个资源时，采用“@[package:]type:name”格式进行引用

◼字符串值：类似于其他语言

## Activity

提供可视化用户界面的组件

**分类： 全屏模式、 浮动窗口模式、 嵌入式模式**

### 如何启动主Activity

**当运行我们的Android应用程序时，Android操作系统首先会去找我们的AndroidManifest.xml这个文件，这个文件是我们应用程序的主配置文件，在主配置文件定义了当前这个应用默认所加载的Activity对象，找到这个 Activity 对 象 后 ， 就 会 调 用 其onCreate()方法，这个方法主要就是用来加载我们的布局文件的，通过setContentView()方法可以来加载我们指定的布局文件，最后根据布局文件中的各个控件显示在我们的屏幕上。**

### Activity A如何启动 Activity B？ 

◼ startActivity(Intent intent)； 

◼ startActivity()方法会查找并启动一个与Intent参数相匹配的Activity

◼ startActivityForResult(Intent intent, int requestCode)； 

◼ startActivityForResult()方法启动Activity并跟踪子Activity的反馈

### 从目标Activity中返回数据

◼ 在目标Activity中调用finish()方法之前，通过setResult()方法向原Activity返回一个结果

◼ setResult()方法是一个重载方法，其形式如下：

```java
setResult(int resultCode)——设置传递到上一个界面的数据
setResult(int resultCode, Intent data) ——设置传递到上一个界面的数据
```

◼ setResult(Activity.RESULT_CANCELED);

```java
Intent result = new Intent(Intent.ACTION_PICK, selectedHorse);
setResult(Activity.RESULT_OK, result);
```

### 处理从目标Activity返回的数据

◼ 重写onActivityResult()方法处理从目标Activity返回的结果

```java
onActivityResult(int requestCode， int resultCode， Intent data));
```

### Activity 生命周期

| 方法        | 描述                                                         | 是否 可终止 | 下一个               |
| ----------- | :----------------------------------------------------------: | ----------- | -------------------- |
| onCreate()  | 在Activity第一次被创建的时候调用。可在此处做初始化设置──创建视图、绑定 数据至列表等。如果曾经有状态记录，则调用此 方法时会传入一个表示Activity以前状态的包对 象做为参数，继以onStart() | 否          | onStart()            |
| onRestart() | Activity由停止状态恢复使用， 再次启动前 被调用， 继以onStart() | 否          | onStart()            |
| onStart()   | 当Activity正要变得为用户所见时被调用 。当Activity转向前台时继以onResume(); 当Activity变为隐藏时继以onStop()。 | 否          | onResume()oronStop() |
| onResume() | Activty由暂停状态恢复使用 ，在Activity开始 与用户进行交互之前被调用。此时Activity位于堆栈 顶部，用户可见。继以onPause() | 否   | onPause() |
| onPause()  | 当系统将要启动另一个 Activity 或者弹出对话 框时调用 。 此方法主要用于将所有持久性数据写入 存储之中，这一切动作应该在短时间内完成，因为 下一个Activity必须等到此方法返回后才会继续。当Activity重新回到前台时继以 onResume()； 当Activity变为用户不可见时继以onStop()。 | 是   | onResume()oronStop() |
| onStop()    | 当Activity不再为用户可见时调用此方法 。 这 可能发生在它被销毁或者另一个Activity （可能是现 存的或者是新的）回到运行状态并覆盖它时。 如果 Activity再次回到前台跟用户交互则继以onRestart(); 如果关闭Activity则继以onDestroy()。 | 是   | onRestart()oronDestroy() |
| onDestroy() | 在Activity销毁前调用。可能发生在Activity结束（调用了它的 finish()  方法）或者因为系统需要临时空间而销毁该Activity  实例时。可以用isFinishing()方法来区分这两种情况。 | 是   | 无                       |

### 整个生命周期

第一次调用onCreate()开始 → onDestroy()结束

### 可见生命周期

onStart()开始 → onStop()结束

### 前台生命周期

onResume() 开始 → onPause()结束

### Activity状态 是什么？

 运行状态（可见，可交互）

 暂停状态（可见，不可交互） 

 停止状态（不可见，不可交互） 

 销毁状态（从内存中删除）

![image-20220329162407781](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202203291624845.png)

### Application 类

启动Application时，系统会创建一个PID，即进程ID，所有的Activity都会在此进程上运行。 

Application对象的生命周期是整个程序中最长的，它的生命周期就等于这个程序的生命周期。 

因 为 Application 对 象 是 全 局 的 单 例 的 ， 所 以 在 在Application 创建的时候初始化全局变量 ， 不同的Activity,Service中获得的对象都是同一个对象。所以可以通过Application来进行一些，如：数据传递、数据共享和数据缓存等操作。

## Service

用于执行一些持续性的、耗时长的并且无需与用户界面交互的操作

Service拥有独立的生命周期

Service 拥有的优先级要比暂停和停止状态的Activity级别更高

Service没有界面（最多只能显示一个通知） 

Android系统中提供了大量可以直接调用的系统Service

### 启动service的两种方法？

Start方式启动Service

Bind方式启动Service

### IntentService

◼IntentService是Service的子类;

◼其内部会自动开始一个新线程执行任务，并在任务执行完毕后停止Service;

◼当有多个任务时，IntentService会将任务加到一个队列中，按照次序依次执行，直到所有任务执行完毕后停止Service。

### 分类

- 按照运行的进程不同

本地Service

远程Service

- 按照运行的形式

前台Service

后台Service

- 按照使用Service的方式

启动方式Service

绑定方式Service

混合方式Service

### Service执行时

◼ **Service运行于UI线程中**

◼ 耗时任务通常都需要新开线程执行

◼ Service不是线程，不是进程

## BroadcastReceiver

◼ **BroadcastReceiver是广播接收器，用于接收系统和应用中的广播**

◼ BroadcastReceiver是一种对广播进行过滤接收并响应的组件

◼ 自身并不提供用户图形界面

◼ 本质上就是一个全局监听器，用于监听系统全局的广播消息

◼ 电池的使用状态、电话的接收和短信的接收等都会产生一个广播

◼常驻广播：使用AndroidManifest.xml注册，接受者不随Activity的销毁而销毁，也就是拥有独立的生命周期。

◼非常驻广播：使用registerReceiver对广播接收者进行注册。同时，需要使用unregisterReceiver注销这个广播接收者。注册时表示创建广播接收者，注销时表示销毁这个广播接收者。生命周期由开发者决定。通常在activity的onCreate方法中创建广播接收者，在onDestroy中销毁广播接收者。生命周期可控。

## ContentProvider

**ContentProvider保存和获取数据并使其对所有应用程序可见。是不同应用程序间共享数据的唯一方式。**

在Android中，没有提供所有应用共同访问的公共存储区域。 

Android每个应用程序的数据是私有的，不能被其他应用访问

## intent

**Intent是一个动作的完整描述， 包含了产生组件、 接收组件和传递数据信息。**

Intent是Android应用内不同组件之间的通讯载体。

换言之， Intent是同一或不同应用程序之间的一种运行时绑定(runtime  binding)机制， 它能在程序运行的过程中连接两个不同的组件。 通过Intent， 你的程序可以向Android表达某种请求或者意愿， Android会根据意愿的内容选择适当的组件来响应。

### intent 用法

Intent启动Activity、 Service和BroadcastReceiverd

◆ 启 动 Activity ：  startActivity(Intent  intent) 或 startActivityForResult(Intent intent,int requestCode)方法

◆ 启 动 Service  ：  startService(Intent  intent) 或 bindService(Intent  intent,ServiceConnection  conn  ,int flags)方法

◆ 触 发 BroadcastReceiver  ：  sendBroadcast(Intent intent)方法

### Intent属性

◆ Component组件

◆ Action动作

◆ Category类别

◆ Data数据

◆ Type数据类型

◆ Extras扩展信息

◆ Flags标志位

### action

| Action | 作用 |
| :--: | :--: |
|➢ ACTION_BOOT_COMPLETED：| 系统启动完成广播|
|➢ ACTION_TIME_CHANGED：|时间改变广播|
|➢ ACTION_DATE_CHANGED：|日期改变广播|
|➢ ACTION_TIME_TICK：|每分钟改变一次时间|
|➢ ACTION_TIMEZONE_CHANGED：|时区改变广播|
|➢ ACTION_BATTERY_LOW：|电量低广播|
|➢ ACTION_PACKAGE_ADDED：|添加包广播|
|➢ ACTION_PACKAGE_REMOVED：|删除包广播|

### **常见的使用Intent来启动内置应用程序：**

◆ 启动浏览器

```java
Intent i=new Intent(Intent.ACTION_VIEW,Uri.parse("http://www.baidu.com"));

startActivity(i);
```

◆ 启动地图

```java
Intent i=new Intent(Intent.ACTION_VIEW,

Uri.parse("geo:25.04692437135412,121.5161783959678"));

startActivity(i);
```

◆ 打电话

```java
Intent i=new Intent(Intent.ACTION_DIAL，Uri.parse("tel:+1234567"));

startActivity(i);
```

◆ 发送电子邮件

```java
Intent i=new Intent(Intent.ACTION_SENDTO，Uri.parse("mailto:qst@163.com"));

startActivity(i);
```

## ui

Android界面元素主要由5部分构成： 

- View 视图 

- ViewGroup 视图容器 

- 布局管理器 

- Activity 活动 

- Fragment 碎片

### 元素

View控件是用户界面的基础元素。

View对象是Android屏幕上一个特定的矩形区域的 布局和内容属性的数据载体。

Android 应用的绝大部分UI组件都放在 android.widget 包及其子包中，所有这些UI组件 都继承了View类。

![image-20220406081836606](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204060818647.png)

View类有一个非常重要的ViewGroup子类，该类 通常作为其他控件的容器使用。

### 布局管理器



### Didget 简单控件

