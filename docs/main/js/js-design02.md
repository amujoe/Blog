# 前端代码优化



## 1. 提炼函数

如果在函数中有一段代码可以被独立出来，那我们最好把这些代码放进另外一个独立的函数中. 

优点:	

- 避免出现超大函数。


- 独立出来的函数有助于代码复用。
- 独立出来的函数更容易被覆写
- 独立出来的函数如果拥有一个良好的命名，它本身就起到了注释的作用



## 2.合并重复的条件片段		

如果一个函数体内有一些条件分支语句，而这些条件分支语句内部散布了一些重复的代码，那么就有必要进行合并去重工作

```js
// 原代码
function pagejump(currentpage) {
  if (currentpage <= 0) {
    currentpage = 0
    jump(currentpage)
  } else if (currentpage > totalpage) {
    currentpage = totalpage;
    jump(currentpage)
  } else {
    jump(currentpage)
  }
}


// 优化后
function pagejump(currentpage) {
  if (currentpage <= 0) {
    currentpage = 0
  } else if (currentpage > totalpage) {
    currentpage = totalpage;
  } 
  
  // 把 jump 独立出来
  jump(currentpage)
}

```

​			

## 3.把条件分支语句提炼成函数

复杂的条件分支语句是导致程序难以阅读和理解的重要原因，而且容易导致一个庞大的函数

```js
// 现在有一个需求是编写一个计算商品价格的 getPrice 函数，商品的计算只 有一个规则:如果当前正处于夏季，那么全部商品将以 8 折出售

// 原代码
var getPrice = function( price ){
	var date = new Date();
	if ( date.getMonth() >= 6 && date.getMonth() <= 9 ){
		return price * 0.8; 
    }
  
	return price; 
};

// 优化后

/** 判断是否是夏天 */
var isSummer = function () {
  	var date = new Date();
	return date.getMonth() >= 6 && date.getMonth() <= 9;
}

var getPrice = function( price ){
	if ( isSummer() ){
		return price * 0.8; 
    }
  
	return price; 
};
```

​			

## 4.合理使用对象的键值

在函数体内，如果有些代码通过判断 ABCD 来实现 abcd 的操作,  可以简单的利用对象的 键 和 值,  快速实现准确定位

```js
// 假设为了兼容性, 根据不同的版本, 打印不同的文案; 以四个为例子, 可能会更多

// 原代码
let print = (version) => {
  if (version === "one") {
    console.log("你好, 我是版本一");
  } else if (version === "two") {
     console.log("你好, 我是版本二");
  } else if (version === "three") {
     console.log("你好, 我是版本三");
  } else if (version === "four") {
     console.log("你好, 我是版本四");
  } else {
    console.log("你好, 没找到你的版本");
  }
}

// 优化 
let print = (version) => {
  let versions = {
    "one": "我是版本一",
    "two": "我是版本一",
    "three": "我是版本一",
    "four": "我是版本一",
  }; 
  
  if (version in versions) {
    console.log(versions[version]);
  } else {
    console.log("你好, 没找到你的版本");
  }
}

```



## 5.提前让函数退出代替嵌套条件分支

我们可以挑选一些条件分支，在进入这些条件分支之后，就立即让这个函数退出

```js
var del = function( obj ) { 
  	if ( obj.isReadOnly ) {
		return;
  	}
	if ( obj.isFolder ) {
		return deleteFolder( obj );
	}
	if ( obj.isFile ){
		return deleteFile( obj ); 
    }
};
```

​	

## 6.传递对象参数 - 代替 - 过长的参数列表

有时候一个函数有可能接收多个参数，而参数的数量越多，函数就越难理解和使用。使用该函数的人首先得搞明白全部参数的含义，在使用的时候，还要小心翼翼，**以免少传了某个参数**或者把两个参数搞反了位置

```js
// 优化前
var setUserInfo = function( id, name, address, sex, mobile, qq ){ console.log( 'id= ' + id );
	console.log( 'name= ' +name );
	console.log( 'address= ' + address );
	console.log( 'sex= ' + sex ); console.log( 'mobile= ' + mobile ); console.log( 'qq= ' + qq );
};
setUserInfo( 1314, 'sven', 'shenzhen', 'male', '137********', 377876679 )


// 优化后
var setUserInfo = function( obj ){ 2 console.log( 'id= ' + obj.id );
	console.log( 'name= ' + obj.name );
	console.log( 'address= ' + obj.address );
    console.log( 'sex= ' + obj.sex ); 
    console.log( 'mobile= ' + obj.mobile ); 
    console.log( 'qq= ' + obj.qq );
};
setUserInfo({ 
 	id: 1314,
	name: 'sven',
	address: 'shenzhen', sex: 'male',
	mobile: '137********', qq: 377876679
});
```



## 7.少用三目运算符


三目运算符性能高，代码量少。不过，这两个理由其实都很难站得住脚

同样，相比损失的代码可读性和可维护性

```js
// 看到这样的代码, 想骂街嘛? 

function deom () {
  
	const tempvalue  = a === doc ? -1 :
		b === doc ? 1 : aup ? -1 :
		bup ? 1 : sortInput ?
		( indexOf.call( sortInput, a ) - indexOf.call( sortInput, b ) ) :
		0;
  
	return tempvalue
}

```

如果条件分支逻辑简单且清晰，这无碍我们使用三目运算符:

```js
var global = typeof window !== "undefined" ? window : this;
```

但如果条件分支逻辑非常复杂. 那后面维护的同学要骂街了



## 8.合理使用链式调用

使用链式调用的方式并不会造成太多阅读上的困难，也确实能省下一些字符和中间变量，但节省下来的字符数量同样是微不足道的, 链式调用带来的坏处就是在调试的时候非常不方便，如果我们知道一条链中有错误出现，必须得先把这条链拆开才能加上一些调试 log 或者增加断点，这样才能定位错误出现的地方

如果该链条很容易发生变化，导致调试和维护困难，那么还是建议使用普通调用的形式

```js
// 在 JavaScript 中，可以很容易地实现方法的链式调用，即让方法调用结束后返回对象自身


var User = { id: null,
	name: null,
	setId: function( id ){
		this.id = id;
		return this; 
    },
	setName: function( name ){ 
      	this.name = name; 
      	return this;
	} 
};


// 原代码
console.log( User.setId( 1314 ).setName( 'sven' ) );

// 优化
var user = new User();
user.setId( 1314 );
user.setName( 'sven' );

```

​			

## 9.分解大型类	

```js

// 原代码 spirit.js
var Spirit = function( name ){ 
  this.name = name;
};

Spirit.prototype.attack = function ( type ) {
 	if (type === "waveBoxing")
  		console.log(this.name + ': 使用波动拳')
	} else if( type === 'whirlKick' ){
 		console.log(this.name + ': 使用旋风腿')
    }
}


var spirit = new Spirit( 'RYU' );
spirit.attack( 'waveBoxing' ); // 输出:RYU: 使用波动拳
spirit.attack( 'whirlKick' ); // 输出:RYU: 使用旋风腿

// ------------------------- 看不到我 我是分割线-------------------------------

// 优化

// attack.js
var Attack = function( spirit ){ 
  this.spirit = spirit;
};
Attack.prototype.start = function( type ){ 
  	return this.list[ type ].call( this );
};
Attack.prototype.list = { 
  	waveBoxing: function(){
		console.log( this.spirit.name + ': 使用波动拳' ); 
  	},
	whirlKick: function(){
		console.log( this.spirit.name + ': 使用旋风腿' );
	} 
};


// spirit.js
var Spirit = function( name ){
	this.name = name;
	this.attackObj = new Attack( this );
};
Spirit.prototype.attack = function( type ){ 
  this.attackObj.start( type );
};

// 调用
var spirit = new Spirit( 'RYU' );
// 攻击
spirit.attack( 'waveBoxing' ); // 输出:RYU: 使用波动拳 
spirit.attack( 'whirlKick' ); // 输出:RYU: 使用旋风腿
```



​			
​		
​		
​	
​		
​	

​			