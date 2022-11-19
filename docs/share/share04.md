# Reactive VS Ref

> 既生瑜何生亮

*****

#### reactive
(1)它的响应式是更加‘深层次’的，底层本质是将传入的数据包装成一个Proxy。

(2)参数必须是对象或者数组，如果要让对象的某个元素实现响应式时比较麻烦。需要使用toRefs 

#### ref

(1)函数参数可以是基本数据类型，也可以接受对象类型 

(2)如果参数是对象类型时，其实底层的本质还是reactive,系统会自动根据我们给ref传入的值转换成： ref(1)->reactive({value:1}) ref函数只能操作浅层次的数据，把基本数据类型当作自己的属性值；深层次依赖于reactive 复制代码 

(3)在template中访问，系统会自动添加.value;在js中需要手动.value 

(4)ref响应式原理是依赖于Object.defineProperty()的get()和set()的。