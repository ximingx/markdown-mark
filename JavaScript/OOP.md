# JavaScript 面向对象

## 1. 面向过程与面向对象

### 面向过程 POP

-  面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。
-  在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。面向对象编程具有灵活、代码可复用、容易维护和开发的优点，适合多人合作的大型软件项目，更符合我们认识事物的规律。

### 面向对象 OOP

- 面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。
- 面向对象的编程思想：对代码和数据进行封装，并以对象调用的方式，对外提供统一的调用接口。
- 比如说，当我们在开车的时候，无需关心汽车的内部构造有多复杂，对于大多数人而言，只需要会开、知道汽车有哪些功能就行了。

面向对象的特性如下：

- **封装性**

- **继承性**

- **多态性**

### POP 与 OOP 对比

|      | 面向过程                                                     | 面向对象                                                     |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 优点 | 性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。 | 易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护 |
| 缺点 | 不易维护、不易复用、不易扩展                                 | 性能比面向过程低                                             |

### JavaScript 中的面向对象

JS 中的面向对象，是基于 **原型 **的面向对象。

另外，在ES6中，新引入了 类（`Class`）和继承（`Extends`）来实现面向对象。

JS 中的对象（Object）是依靠构造器（`constructor`）和原型（`prototype`）构造出来的。

## 2. 构造函数 (ES5)

**构造函数**：是一种特殊的函数，主要用来创建和初始化对象，也就是为对象的成员变量赋初始值。它与 `new` 一起使用才有意义。

我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个构造函数里面。

构造函数的创建方式和普通函数没有区别，**不同的是构造函数习惯上首字母大写。**

构造函数和普通函数的区别就是**调用方式**的不同：普通函数是直接调用，而构造函数需要使用 new 关键字来调用。

```js
// 创建一个构造函数，专门用来创建Person对象
function Person(name, age, gender) {
    this.name = name;
    this.age = age;
    this.gender = gender;
    this.sayName = function () {
        alert(this.name);
    };
}

var per = new Person('ximingx', 18, '男');
var per2 = new Person('luotyue', 16, '女');

// 创建一个构造函数，专门用来创建 Dog 对象
function Dog() {}

var dog = new Dog();
```

### 对象的三种创建方式

1. 字面量方式

   ```js
   var obj = {};
   ```

2. new关键字

   ```js
   var obj = new Object();
   ```

3. 构造函数方式

   ```js
   function Person(name,age){
     this.name = name;
     this.age = age;
   }
   var obj = new Person('zs',12);
   ```

### new 执行流程

new 在执行时，会做下面这四件事：

- 开辟内存空间，在内存中创建一个新的空对象。
- 让 this 指向这个新的对象。
- 执行构造函数里面的代码，给这个新对象添加属性和方法。
- **返回这个新对象（所以构造函数里面不需要 return）。**

### 类、实例

使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个**类**。

通过一个构造函数创建的对象，称为该类的**实例**。

使用 instanceof 可以检查**一个对象是否为一个类的实例**。

**语法如下**：

```javascript
对象 instanceof 构造函数;
```

如果是，则返回 true；否则返回 false。

**代码举例**：

```javascript
function Person() {}

function Dog() {}

var person1 = new Person();

var dog1 = new Dog();

console.log(person1 instanceof Person); // 打印结果： true
console.log(dog1 instanceof Person); // 打印结果：false
console.log(dog1 instanceof Object); // 所有的对象都是Object的后代。因此，打印结果为：true
```

根据上方代码中的最后一行，需要补充一点：**所有的对象都是 Object 的后代，因此 `任何对象 instanceof Object` 的返回结果都是 true**。

### 实例成员

实例成员就是构造函数内部通过 this 添加的成员 如下列代码中uname age sing 就是实例成员,实例成员只能通过实例化的对象来访问

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
     this.sing = function() {
     console.log('我会唱歌');
    }
}
var ldh = new Star('刘德华', 18);
console.log(ldh.uname); //实例成员只能通过实例化的对象来访问, 不可以通过构造函数访问
```

### 静态成员

静态成员 在构造函数本身上添加的成员  如下列代码中 sex 就是静态成员,静态成员只能通过构造函数来访问

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
     this.sing = function() {
     console.log('我会唱歌');
    }
}
// 构造函数上直接添加的成员
Star.sex = '男'; 
var ldh = new Star('刘德华', 18);
console.log(Star.sex); //静态成员只能通过构造函数来访问, 不可以通过对象访问
```

### 构造函数原型 prototype

**构造函数方法很好用，但是存在浪费内存的问题。例如创建实例对象方法的重复会占用内存**

**构造函数通过原型分配的函数是所有对象所共享的。**

**JavaScript 规定，每一个构造函数都有一个prototype 属性，指向另一个对象。注意这个prototype就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。**

**我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法。**

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
Star.prototype.sing = function() {
	console.log('我会唱歌');
}
```

### 对象原型  `__proto__`

对象都会有一个属性 `__proto__` 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 原型对象的属性和方法，就是因为对象有 `__proto__` 原型的存在。

**`__proto__` 对象原型和原型对象 prototype 是等价的**

`__proto__` 对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个非标准属性，**因此实际开发中，不可以使用这个属性，它只是内部指向原型对象 prototype**

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204201412866.png)

### constructor 函数

**对象原型（`__proto__` ）和构造函数（prototype）原型对象里面都有一个属性 constructor 属性 ，constructor 我们称为构造函数，因为它指回构造函数本身。**

constructor 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。

一般情况下，对象的方法都在构造函数的原型对象中设置。**如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor  就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。**

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
 }
 // 很多情况下,我们需要手动的利用constructor 这个属性指回 原来的构造函数
 Star.prototype = {
   // 如果我们修改了原来的原型对象,给原型对象赋值的是一个对象,则必须手动的利用constructor指回原来的构造函数
   constructor: Star, // 手动设置指回原来的构造函数
   sing: function() {
     console.log('我会唱歌');
   },
   movie: function() {
     console.log('我会演电影');
   }
}
var zxy = new Star('张学友', 19);
console.log(zxy)
```

### 原型链

每一个实例对象又有一个__proto__属性，指向的构造函数的原型对象，构造函数的原型对象也是一个对象，也有__proto__属性，这样一层一层往上找就形成了原型链。

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204201418663.png)

### js 成员查找机制

- 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
- 如果没有就查找它的原型（也就是 __proto__指向的 prototype 原型对象）。
- 如果还没有就查找原型对象的原型（Object的原型对象）。
- 依此类推一直找到 Object 为止（null）。
- __proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。

### 三角关系

- 构造函数的prototype属性指向了构造函数原型对象
- 实例对象是由构造函数创建的,实例对象的`__proto__`属性指向了构造函数的原型对象
- 构造函数的原型对象的constructor属性指向了构造函数,实例对象的原型的constructor属性也指向了构造函数

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204201418072.png)

### this 指向

**this 的指向也有所不同**：

-   1.以函数的形式调用时，this 永远都是 window。比如`fun();`相当于`window.fun();`

-   2.以方法的形式调用时，this 是调用方法的那个对象

-   **构造函数中的this和原型对象的this,都指向我们 new 出来的实例对象**

 ```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
 }
 
 var that;
 Star.prototype.sing = function() {
     console.log('我会唱歌');
     that = this;
 }
 
 var ldh = new Star('刘德华', 18);
 // 1. 在构造函数中,里面this指向的是对象实例 ldh
 console.log(that === ldh);//true
 // 2.原型对象函数里面的this 指向的是 实例对象 ldh
 ```

### 通过原型为数组扩展内置方法

```js
 Array.prototype.sum = function() {
   var sum = 0;
   for (var i = 0; i < this.length; i++) {
   sum += this[i];
   }
   return sum;
 };

 //此时数组对象中已经存在sum()方法了  可以始终 数组.sum()进行数据的求
```

### function.call()

- call()可以调用函数
- **call()可以修改this的指向,使用call()的时候 参数一是修改后的this指向**,参数2,参数3..使用逗号隔开连接

```js
 function fn(x, y) {
     console.log(this);
     console.log(x + y);
}
  var o = {
  	name: 'andy'
  };

  fn(1,2) // 调用了函数此时的this指向了 window
  fn.call(o, 1, 2); // 调用了函数此时的this指向了对象o,
```

### 组合继承

#### 继承属性

1. 先定义一个父构造函数
2. 再定义一个子构造函数
3. 子构造函数继承父构造函数的属性(使用call方法)

```js
 // 1. 父构造函数
 function Father(uname, age) {
   // this 指向父构造函数的对象实例
   this.uname = uname;
   this.age = age;
 }

  // 2 .子构造函数 
function Son(uname, age, score) {
  // this 指向子构造函数的对象实例
  3.使用call方式实现子继承父的属性
  Father.call(this, uname, age);
  this.score = score;
}

var son = new Son('刘德华', 18, 100);
```

#### 继承方法

```js
 // 1. 父构造函数
 function Father(uname, age) {
   // this 指向父构造函数的对象实例
   this.uname = uname;
   this.age = age;
 }

Father.prototype.money = function() {
  console.log(100000);
 };

  // 2 .子构造函数 
function Son(uname, age, score) {
  // this 指向子构造函数的对象实例
  3.使用call方式实现子继承父的属性
  Father.call(this, uname, age);
  this.score = score;
}

// Son.prototype = Father.prototype;  这样直接赋值会有问题,如果修改了子原型对象,父原型对象也会跟着一起变化
Son.prototype = new Father();
// 如果利用对象的形式修改了原型对象,别忘了利用constructor 指回原来的构造函数
Son.prototype.constructor = Son;
// 这个是子构造函数专门的方法
Son.prototype.exam = function() {
	console.log('孩子要考试');
}

var son = new Son('刘德华', 18, 100);
```













## 3. 对象与类 (ES6)

对象是由属性和方法组成的：是一个无序键值对的集合,指的是一个具体的事物

- 属性：事物的特征，在对象中用属性来表示（常用名词）
- 方法：事物的行为，在对象中用方法来表示（常用动词）

```js
//字面量创建对象
var ldh = {
    name: 'ximingx',
    age: 20
}


//构造函数创建对象
  function Star(name, age) {
    this.name = name;
    this.age = age;
 }


//实例化对象
console.log(ldh);
var ximingx = new Star('ximingx', 20)
console.log(ximingx);	
```

在 ES6 中新增加了类的概念，可以使用 class 关键字声明一个类，之后以这个类来实例化对象。类抽象了对象的公共部分，它泛指某一大类（class）对象特指某一个，通过类实例化一个具体的对象

### 创建实例化类

1. 语法:

```js
//步骤1 使用class关键字
class name {
  // class body
}    

//步骤2使用定义的类创建实例  注意new关键字
var xx = new name();     
```

2. 示例

```js // 1. 创建类 class  创建一个类
class Star {
    
    // 类的共有属性放到 constructor 里面 constructor是 构造器或者构造函数
    constructor(uname, age) {
      this.uname = uname;
      this.age = age;
    }
    
    //-------------------------------------------> 注意,方法与方法之间不需要添加逗号
    
    sing(song) {
      console.log(this.uname + '唱' + song);
    }
    
}
// 2. 利用类创建对象 new
var ldh = new Star('刘德华', 18);
console.log(ldh); // Star {uname: "刘德华", age: 18}
ldh.sing('冰雨'); // 刘德华唱冰雨
```

注意:

1. 通过class 关键字创建类, 类名我们还是习惯性定义首字母大写
2. **类里面有个constructor 函数,可以接受传递过来的参数,同时返回实例对象**
3. **constructor 函数 只要 new 生成实例时,就会自动调用这个函数**, 如果我们不写这个函数,类也会自动生成这个函数
4. 多个函数方法之间不需要添加逗号分隔
5. 生成实例 new 不能省略
6. 语法规范, 创建类 类名后面不要加小括号,生成实例 类名后面加小括号, 构造函数不需要加function
7. **在 ES6 中类没有变量提升，所以必须先定义类，才能通过类实例化对象**

### 类的继承

1. 语法

```js
// 父类
class Father{  
    
} 

// 子类继承父类
class  Son  extends Father {  
    
}       
```

2. 示例

```js
class Father {
    
      constructor(surname) {
        this.surname= surname;
      }
    
      say() {
        console.log('你的姓是' + this.surname);
      }
    
}


// 这样子类就继承了父类的属性和方法
class Son extends Father{}


var damao= new Son('刘');
damao.say();      // 结果为 你的姓是刘
```

子类使用 super 关键字访问父类的方法, 但是要注意 this 的指向

```js
// 定义了父类
class Father {
    
   constructor(x, y) {
   		this.x = x;
   		this.y = y;
   }
    
   sum() {
   		console.log(this.x + this.y);
    }
    
}


	// 子元素继承父类
    class Son extends Father {
        
   		 constructor(x, y) {
             super(x, y); // 使用super调用了父类中的构造函数
             this.x = x;
             this.y = y;
    	 }
        
        // sum() {
        //    super.sum()
        // }
        
    }

	
    var son = new Son(1, 2);
    son.sum(); // 结果为3
```

**注意:** 

1. 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,如果有就先执行子类的
2. 继承中,如果子类里面没有,就去查找父类有没有这个方法,如果有,就执行父类的这个方法(就近原则)
3. **如果子类想要继承父类的方法,同时在自己内部扩展自己的方法,利用super 调用父类的构造函数,super 必须在子类this之前调用**

### 类中 this 的指向

1. **constructor中的this指向的是new出来的实例对象** 
2. **自定义的方法, 一般也指向的new出来的实例对象**
3. **绑定事件之后this指向的就是触发事件的事件源**

### 案例 (精彩)

```js
var that;
class Tab {
    constructor(id) {
        // 获取元素
        that = this;
        this.main = document.querySelector(id);
        this.add = this.main.querySelector('.tabadd');
        // li的父元素
        this.ul = this.main.querySelector('.fisrstnav ul:first-child');
        // section 父元素
        this.fsection = this.main.querySelector('.tabscon');
        this.init();
    }
    init() {
            this.updateNode();
            // init 初始化操作让相关的元素绑定事件
            this.add.onclick = this.addTab;
            for (var i = 0; i < this.lis.length; i++) {
                this.lis[i].index = i;
                this.lis[i].onclick = this.toggleTab;
                this.remove[i].onclick = this.removeTab;
                this.spans[i].ondblclick = this.editTab;
                this.sections[i].ondblclick = this.editTab;

            }
        }
        // 因为我们动态添加元素 需要从新获取对应的元素
    updateNode() {
            this.lis = this.main.querySelectorAll('li');
            this.sections = this.main.querySelectorAll('section');
            this.remove = this.main.querySelectorAll('.icon-guanbi');
            this.spans = this.main.querySelectorAll('.fisrstnav li span:first-child');
        }
        // 1. 切换功能
    toggleTab() {
            // console.log(this.index);
            that.clearClass();
            this.className = 'liactive';
            that.sections[this.index].className = 'conactive';
        }
        // 清除所有li 和section 的类
    clearClass() {
            for (var i = 0; i < this.lis.length; i++) {
                this.lis[i].className = '';
                this.sections[i].className = '';
            }
        }
        // 2. 添加功能
    addTab() {
            that.clearClass();
            // (1) 创建li元素和section元素 
            var random = Math.random();
            var li = '<li class="liactive"><span>新选项卡</span><span class="iconfont icon-guanbi"></span></li>';
            var section = '<section class="conactive">测试 ' + random + '</section>';
            // (2) 把这两个元素追加到对应的父元素里面
            that.ul.insertAdjacentHTML('beforeend', li);
            that.fsection.insertAdjacentHTML('beforeend', section);
            that.init();
        }
        // 3. 删除功能
    removeTab(e) {
            e.stopPropagation(); // 阻止冒泡 防止触发li 的切换点击事件
            var index = this.parentNode.index;
            console.log(index);
            // 根据索引号删除对应的li 和section   remove()方法可以直接删除指定的元素
            that.lis[index].remove();
            that.sections[index].remove();
            that.init();
            // 当我们删除的不是选中状态的li 的时候,原来的选中状态li保持不变
            if (document.querySelector('.liactive')) return;
            // 当我们删除了选中状态的这个li 的时候, 让它的前一个li 处于选定状态
            index--;
            // 手动调用我们的点击事件  不需要鼠标触发
            that.lis[index] && that.lis[index].click();
        }
        // 4. 修改功能
    editTab() {
        var str = this.innerHTML;
        // 双击禁止选定文字
        window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
        // alert(11);
        this.innerHTML = '<input type="text" />';
        var input = this.children[0];
        input.value = str;
        input.select(); // 文本框里面的文字处于选定状态
        // 当我们离开文本框就把文本框里面的值给span 
        input.onblur = function() {
            this.parentNode.innerHTML = this.value;
        };
        // 按下回车也可以把文本框里面的值给span
        input.onkeyup = function(e) {
            if (e.keyCode === 13) {
                // 手动调用表单失去焦点事件  不需要鼠标离开操作
                this.blur();
            }
        }
    }

}
new Tab('#tab'); 
```























