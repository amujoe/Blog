## 设计模式



从《设计模式》副标题“可复用面向对象软件的基础”可以知道，这本书理应教我们如何编写可复用的面向对象程序。这本书把大多数笔墨都放在如何封装变化上面，这跟编写可复用的面向对象程序是不矛盾的。当我们想办法把程序中变化的部分封装好之后，剩下的即是稳定而可复用的部分了。

设计模式在很多时候其实都体现了语言的不足之处。Peter Norvig 曾说，设计模式是对语言不足的补充，

​			

变量的生存周期除了变量的作用域之外，另外一个跟闭包有关的概念是变量的生存周期。对于全局变量来说，全局变量的生存周期当然是永久的，除非我们主动销毁这个全局变量。

​			
但在 JavaScript 中，函数作为一等对象，本身就可以四处传递，用函数对象而不是普通对象来封装请求显得更加简单和自然。如果需要往函数对象中预先植入命令的接收者，那么闭包可以完成这个工作。在面向对象版本的命令模式中，预先植入的命令接收者被当成对象的属性保存起来;而在闭包版本的命令模式中，命令接收者会被封闭在闭包形成的环境中，

​		

```js
var isType = function( type ){return function( obj ){

return Object.prototype.toString.call( obj ) === '[object '+ type +']';}

};

var isString = isType( 'String' );

var isArray = isType( 'Array' );

var isNumber = isType( 'Number' );

console.log( isArray( [ 1, 2, 3 ] ) );

```

​	
AOP(面向切面编程)的主要作用是把一些跟核心业务逻辑模块无关的功能抽离出来，这些跟业务逻辑无关的功能通常包括日志统计、安全控制、异常处理等。把这些功能抽离出来之后，再通过“动态织入”的方式掺入业务逻辑模块中。这样做的好处首先是可以保持业务逻辑模块的纯净和高内聚性，其次是可以很方便地复用日志统计等功能模块


​			


1. 分时函数 ( 短时间内执行 1W 次,  浏览器可能会垮掉,  转化为 设置500ms 执行 100次, 多次执行)

2. 惰性加载函数

3. ​

   ​

   ### 14 种设计模式**

   ​				

   ### 1. 单例模式		

   保证一个类仅有一个实例，并提供一个访问它的全局访问点

   用一个变量来标志当前是否已经为某个类创建过对象，如果是，则在下一次获取该类的实例时，直接返回之前创建的对象

   ​			
   javascript 中单例模式的核心是确保只有一个实例，并提供全局访问

   **惰性单例**	,  不需要在页面一加载的时候, 就创建个div. 只有在需要创建的时候, 再创建.  并且再第二次调用的时候, 不再重新创建. 



通用的单例模式生成器

```js

/**
写在开始, 其实是总结

创建实例对象的职责和管理单例的职责分别放置在两个方法里，这两 个方法可以独立变化而互不影响，当它们连接在一起的时候，就完成了创建唯一实例对象的功能， 看起来是一件挺奇妙的事情
*/

/** 通用的单例模式生成器 */
var getSingle = function( fn ){
  	var result;
	return function(){
		return result || ( result = fn .apply(this, arguments ) );
	}};
}

// 内容
var createLoginLayer = function(){
	var div = document.createElement( 'div' );
	div.innerHTML = '我是登录浮窗';
	div.style.display = 'none'; 2 document.body.appendChild( div );
	return div;
};

// 创建单例模式
var createSingleLoginLayer = getSingle( createLoginLayer );

// 业务调用
document.getElementById( 'loginBtn' ).onclick = function(){ 
  var loginLayer = createSingleLoginLayer(); loginLayer.style.display = 'block';
};

// 这样创建div的操作只会执行一次

```



### 2.策略模式

策略模式的定义是: 定义一系列的算法，把它们一个个封装起来，并且使它们可以相互替换;

详解: 定义一系列的算法，把它们各自封装成策略类，算法被封装在策略类内部的方法里。在客户对 Context 发起请求的时候，Context 总是把请求委托给这些策略对象中间的某一个进行计算。




1. 去除if else
2. 有弹性, 可扩展
3. 算法的复用性



**将不变的部分和变化的部分隔开是每个设计模式的主题**

​		
**策略模式的目的就是将算法的使用与算法的实现分离开来**

```js

// 很多公司的年终奖是根据员工的工资基数和年底绩效情况来发放的。例如，绩效为 S 的人年 终奖有 4 倍工资，绩效为 A 的人年终奖有 3 倍工资，而绩效为 B 的人年终奖是 2 倍工资。假设财 务部要求我们提供一段代码，来方便他们计算员工的年终奖

/** 策略内容, 年终奖的具体算法 */
var strategies = {
  "S": function( salary ){
  	return salary * 4; 
  },
  "A": function( salary ){ 
  	return salary * 3;
  },
  "B": function( salary ){
  	return salary * 2;
  }
};

/** 策略的实现 */
var calculateBonus = function( level, salary ){ 
  return strategies[ level ]( salary );
};

// 调用
console.log( calculateBonus( 'S', 20000 ) );  // 输出:80000
console.log( calculateBonus( 'A', 10000 ) );  // 输出:30000

```

```js
/** 
	假设我们正在编写一个注册的页面，在点击注册按钮之前，有如下几条校验逻辑。
	 用户名不能为空。
	 密码长度不能少于 6 位。 
	 手机号码必须符合格式。
*/

var strategies = {
  // 为空验证
  isNonEmpty: function( value, errorMsg ){
    if ( value === '' ){ 
      return errorMsg ;
    } 
  },
  // 长度验证
  minLength: function( value, length, errorMsg ){ 
    if ( value.length < length ){
  		return errorMsg;
    }
  },
  // 手机号码格式
  isMobile: function( value, errorMsg ){ 
  	if ( !/(^1[3|5|8][0-9]{9}$)/.test( value ) ){ 
      return errorMsg;
  	} 
  }
};


var validataFunc = function(){
	var validator = new Validator(); // 创建一个 validator 对象
	/***************添加一些校验规则****************/
	validator.add(registerForm.userName, 'isNonEmpty', '用户名不能为空' ); 
  	validator.add(registerForm.password, 'minLength:6', '密码长度不能少于 6 位' ); 
  	validator.add(registerForm.phoneNumber, 'isMobile', '手机号码格式不正确' );
	var errorMsg = validator.start(); // 获得校验结果
	return errorMsg; // 返回校验结果 
}


var registerForm = document.getElementById( 'registerForm' ); 
registerForm.onsubmit = function(){
	var errorMsg = validataFunc(); // 如果 errorMsg 有确切的返回值，说明未通过校验 
  	if ( errorMsg ){
		alert ( errorMsg );
		return false; // 阻止表单提交 
    }
};


// validator.js
/**
使用策略模式重构代码之后，我们仅仅通过“配置”的方式就可以完成一个表单的校验， 这些校验规则也可以复用在程序的任何地方，还能作为插件的形式，方便地被移植到其他项 目中
*/

var Validator = function(){
	this.cache = []; // 保存校验规则
};

/** 添加教研规则 */
Validator.prototype.add = function( 
	var ary = rule.split( ':' ); // 把 strategy 和参数分开

	// 把校验的步骤用空函数包装起来，并且放入 cache
	this.cache.push(function(){ 
		var strategy = ary.shift(); //  用户挑选的 strategy
      	ary.unshift( dom.value ); // 把 input 的 value 添加进参数列表
      	ary.push( errorMsg ); // 把 errorMsg 添加进参数列表
      	return strategies[ strategy ].apply( dom, ary )
    }); 
};

/** 执行 */
Validator.prototype.start = function(){
	for ( var i = 0, validatorFunc; validatorFunc = this.cache[ i++ ]; ){
		var msg = validatorFunc(); // 开始校验，并取得校验后的返回信息 
      	if ( msg ){ 
          // 如果有确切的返回值，说明校验没有通过
			return msg; 
        }
     }
};

```

 策略模式的优点:



- 策略模式利用组合、委托和多态等技术和思想，可以有效地避免多重条件选择语句。

- 策略模式提供了对开放—封闭原则的完美支持，将算法封装在独立的 strategy 中，使得它

  们易于切换，易于理解，易于扩展

- 策略模式中的算法也可以复用在系统的其他地方，从而避免许多重复的复制粘贴工作

- 在策略模式中利用组合和委托来让 Context 拥有执行算法的能力，这也是继承的一种更轻

  便的替代方案。



## 代理模式

代理模式是为一个对象提供一个代用品或占位符，以便控制对它的访问

​		
代理模式的关键是，当客户不方便直接访问一个对象或者不满足需要的时候，提供一个替身对象来控制对这个对象的访问，客户实际上访问的是替身对象。替身对象对请求做出一些处理之后，再把请求转交给本体对象




**缓存代理**: 缓存代理可以为一些开销大的运算结果提供暂时的存储，在下次运算时，如果传递进来的参

数跟之前一致，则可以直接返回前面存储的运算结果



```js
// 先创建一个用于求乘积的函数:

var mult = function(){ 
     console.log( '开始计算乘积' ); 
     var a = 1;
     for ( var i = 0, l = arguments.length; i < l; i++) {
         a = a * arguments[i];
     }
); 
mult( 2, 3 );  // 输出:6
mult( 2, 3, 4); // 输出:24
   
  
// 现在加入缓存代理函数:
var proxyMult = (function(){ 
	var cache = {};
	return function(){
		var args = Array.prototype.join.call( arguments, ',' ); 
      	if ( args in cache ){
			return cache[ args ]; 
        }
	return cache[ args ] = mult.apply( this, arguments ); }
})();
  
proxyMult( 1, 2, 3, 4 ); // 输出:24
proxyMult( 1, 2, 3, 4 ); // 输出:24
                                          
```


**防火墙代理**:控制网络资源的访问，保护主题不让“坏人”接近。

**远程代理**:为一个对象在不同的地址空间提供局部代表

**保护代理:** 用于对象应该有不同访问权限的情况




**虽然代理模式非常有用，但我们在编写业务代码的时候，往往不需要去预先猜测是否需要使用代理模式。当真正发现不方便直接访问某个对象的时候，再编写代理也不迟。**
​	



## 迭代器模式

迭代器模式是指提供一种方法顺序访问一个聚合对象中的各个元素，而又不需要暴露该对象的内部表示

最好的理解就是:  forEach  map 等循环遍历函数



## 发布—订阅模式

发布—订阅模式又叫观察者模式，它定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都将得到通知。在 JavaScript 开发中，我们一般用事件模型来替代传统的发布—订阅模式

​	

优点: 如 订阅 ajax 请求的 error、succ 等事件发布—订阅模式的优点非常明显，一为时间上的解耦，二为对象之间的解耦。它的应用非常广泛，既可以用在异步编程中，也可以帮助我们完成更松耦合的代码编写


​			
缺点: 创建订阅者本身要消耗一定的时间和内存，而且当你订阅一个消息后，也许此消息最后都未发生，但这个订阅者会始终存在于内存中

​			

## 命令模式



命令模式是最简单和优雅的模式之一，命令模式中的命令(command)指的是一个执行某些特定事情的指令。

命令模式最常见的应用场景是:有时候需要向某些对象发送请求，但是并不知道请求的接收者是谁，也不知道被请求的操作是什么。此时希望用一种松耦合的方式来设计程序,  是的请求发送者和请求接收者能够消除彼此之间的耦合关系

​		

**设计模式的主题总是把不变的事物和变化的事物分离开来**





## 模版模式			

​		

不同的事情, 寻找共同点, 抽离公共方法, 把变数当作参数传递

​	
由于抽象类不能被实例化，如果有人编写了一个抽象类，那么这个抽象类一定是用来被某些具体类继承的

​			
举例:  煮咖啡、煮茶



**“好莱坞原则**


在这一原则的指导下，我们允许底层组件将自己挂钩到高层组件中，而高层组件会决定什么时候、以何种方式去使用这些底层组件，高层组件对待底层组件的方式，跟演艺公司对待新人演员一样，都是“别调用我们，我们会调用你”。

​			

## 享元模式

享元模式的目标是尽量减少共享对象的数量



**对象池**


地图搜索时候, 搜索家附近的饭店,  第一次搜索面馆, 地图出现2个气泡,  再次搜索川菜, 出现6个气泡.  是重新创建6个气泡? 还是只用新增4个气泡?

​		

**享元模式是为解决性能问题而生的模式，这跟大部分模式的诞生原因都不一样。在一个存在大量相似对象的系统中，享元模式可以很好地解决大量对象带来的性能问题**。	

​		

## 状态模式

理解: 有一个电灯，电灯上面只有一个开关。当电灯开着的时候，此时按下开关，电灯会切换到关闭状态;再按一次开关，电灯又将被打开。同一个开关按钮，在不同的状态下，表现出来的行为是不一样的。

​						
**允许一个对象在其内部状态改变时改变它的行为，对象看起来似乎修改了它的类**

```javascript

// 状态机在游戏开发中也有着广泛的用途，特别是游戏 AI 的逻辑编写。在我曾经开发的 HTML5 版街头霸王游戏里，游戏主角 Ryu 有走动、攻击、防御、跌倒、跳跃等多种状态。这些 状态之间既互相联系又互相约束。比如 Ryu 在走动的过程中如果被攻击，就会由走动状态切换为 跌倒状态。在跌倒状态下，Ryu 既不能攻击也不能防御。同样，Ryu 也不能在跳跃的过程中切换 到防御状态，但是可以进行攻击。这种场景就很适合用状态机来描述。代码如下:

var FSM = { 
  walk: {
	attack: function(){ 
      console.log( '攻击' );
	},
     defense: function(){
		console.log( '防御' ); 
     },
	jump: function(){ 
      console.log( '跳跃' );
	}
  },
  attack: {
  	defense: function(){
		console.log( '攻击的时候不能防御' ); 
  	},
	jump: function(){
		console.log( '攻击的时候不能跳跃' );
	} 
  }
}


```



## 适配器模式

适配器模式的作用是解决两个软件实体间的接口不兼容的问题。使用适配器模式之后，原本由于接口不兼容而不能工作的两个软件实体可以一起工作



### 但一职责的原则

### 最少知识原则 

### 开放-封闭原则

软件实体(类、模块、函数)等应该是可以扩展的，但是不可修改


