# fed-e-task-01-01

1.请说出下列最终的执行结果，并解释为什么？
var a = []
for (var i = 0; i < 10; i++) {
    a[i] = function () {
        console.log(i);
    }
}
a[6]();
答：执行结果为10，因为变量i是用var声明的，var声明的变量作用域为全局，
循环结束后变量i的值变为10，故执行a[6]()时打印结果为10.

2.请说出下列最终的执行结果，并解释为什么？
var tmp = 123;
if (true) {
    console.log(tmp);
    let tmp;
}
答：执行结果将会报错。let为块级作用域，当块中存在let定义的变量，不会
出现变量提升，console.log(tmp)执行时，发现tmp在块中存在，但使用时尚未定义，将直接报错。

3.结合ES6新语法，用最简单的方式找出数组中的最小值？
var arr = [12, 34, 32, 89, 4];
答：Math.min(...arr)

4.请详细说明var,let,const 三种声明变量的方式之间的具体差别？
答：var定义的变量作用域在当前函数作用域中，且存在变量提升现象（即先使用后定义不会报错，使用时值为undefined）；
   let和const定义的变量作用域在当前代码块内，且不存在变量提升现象，不同的是let定义的变量可以改变，const定义的
   变量不可改变（对象属性可以修改，因为定义时保存的是当前对象的地址）

5.请说出下列最终的执行结果，并解释为什么？
var a = 10;
var obj = {
    a: 20;
    fn () {
        setTimeout(() => {
            console.log(this.a);
        })
    }
}
obj.fn();
答：20。因为当调用obj.fn()时，执行方法时中的this指向的是obj本身，
而setTimeout的函数使用箭头函数定义，箭头函数不会改变this指向，故当执行
console.log(this.a)时，this依然指向obj，故执行结果为20.

6.简述Symbol类型的用途？
答：Symbol类型是用来表示一个独一无二的值。一般有一下几种用法：
1.可以用来避免对象属性名重复问题；
2.创建对象的私有成员

7.说说什么是浅拷贝，什么是深拷贝？
答：浅拷贝：只拷贝对象的存储地址，不进行值的拷贝，修改对象属性值，会影响拷贝后的结果。
   深拷贝：拷贝对象的值，修改对象属性值，不会影响拷贝后的结果。

8.谈谈你是如何理解JS异步编程的，Event Loop是做什么的，什么是宏任务，什么是微任务？
答：JS最初定义为实现页面动画效果，逻辑比较简单，且操作dom，
故js是单线程语言（不考虑web worker，web worker也不能操作dom），
为了解决单线程带来的无法处理大量耗时任务的问题，因此js实现了js异步编程，
从而不用等待耗时任务执行完成返回结果，直接开启下一个任务，
等耗时任务完成后通过回调函数的形式执行耗时任务后续逻辑。
Event Loop，即事件循环，用来执行js异步编程后续逻辑的回调函数。
宏任务：即回调队列中的任务,如UI渲染，setTimeout等。
微任务：宏任务执行过程中产生的异步任务，在当前宏任务执行完成后直接执行，
如 promise，mutation.observe，process.nextTick

9.将下面异步代码使用Promise改进？
setTimeout(function () {
    var a = "hello";
    setTimeout(function () {
        var b = "lagou";
        setTimeout(function () {
            var c = "I love u";
            console.log(a + b + c);
        }, 10);
    }, 10);
}, 10);
答：
Promise.resolve("hello").then(function (a) {
    return a + ' lagou'
}).then(function (b) {
    console.log(b + ' I love u')
})

10.请简述TypeScript 与 JavaScript 之间的关系？
答：TypeScript是JavaScript的扩展集，是在JavaScript基础上扩展了类型系统以及对ES6+的支持，
最终直接编译为JavaScript。

11.请谈谈你所认为的TypeScript优缺点？
答：优点：
      1.任何一种JavaScript运行环境都支持
      2.功能强大，生态健全完善
      3.属于渐进式的
      4.类型系统添加了强校验，减少出错率
   缺点：
      1.相较JavaScript多了很多概念，提高了学习成本。
      2.对于周期比较短的项目，会增加开发成本
