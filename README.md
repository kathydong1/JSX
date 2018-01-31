JSX简介
JSX(JavaScript XML)是js内定义的一套XML语法，可以解析出目标js代码,颠覆传统js写法。实质上HTML也是xml协议，有由浏览器解析，而JSX是由js解析。当让也可以通过构建工具先解析生成，如grunt、webpack,这样可以减少代码这行中js解析JSX的时间，这个后面会专题讲诉。JSX原本是使用官方自己提供的方法处理，2015-7-12日官方博客文章声明其自身用于JSX语法解析的编译器JSTransform已经过期，不再维护，React JS和React Native已经全部采用第三方Babel的JSX编译器实现。

基本语法
JSX必须严格闭合。
<div></div> 
可以把JSX标签当做一个变量，可以在任何位置使用和使用变量装起来。

var div = <div>ddd</div>
ReactDOM.render(div);
JSX一个标签就是一个组件，当存在两个组件在同一级是，必须使用一个标签（组件）包起来

<span>
    <div></div>
    <div></div>
</span>
自定义组件使用是必须首字母大写，数字母不大写直接解析为同名html标签。

<Test />//自定义
<div></div>//直接解析为<div></div>
<test />//直接解析为<test></test>,在浏览器是不识别的，无法显示
JSX使用JavaScipt
上面代码体现了 JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。不是什么JavaScript语法都可以用的，像if语句就不可以用，下面列举一些用法。其实会用最基本的用法就够了，其他的了解下。

在JSX中使用变量
var name = "test";
<div>{name + "666"}</div>
在JSX中使用Array（特殊的变量）
这个方式，很方便

var arr = [
  <h1>Hello world!</h1>,
  <h2>React is awesome</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);
在JSX中使用函数
因为上面可以直接使用数组，就方便了下面map方法的使用。其实就是相当于函数返回了一个结果，这个结果没有绑在变量上，直接使用了。

var names = ['Alice', 'Emily', 'Kate'];
<div>
    { 
        names.map(function (name) { 
            return <div>Hello, {name}!</div>
        }) 
    }
</div>
条件判断
直接使用if语句目前是不支持的。

<div className={if(isComplete){ 'is-complete' }}></div>
而解决办法是使用以下方法：

使用三目运算符

<div className={this.state.isComplete ? 'is-complete' : ''}></div>
设置一个变量并在属性中引用它

将逻辑转化到函数中

使用&&运算符

<div className={this.state.isComplete && 'is-complete'}></div>
在JSX中使用...操作符
...操作符是ES6新语法，JSX使用了它的特点，但并不是真正的ES6语法。

var props = {};
props.foo = x;
props.bar = y;
var component = <Component {...props} />;
相当于

var component = <Component foo={props.foo} bar={props.bar} />;
如果override，该怎么做呢？也很简单：

var component = <Component {...props} foo="override"/>;
console.log(this.props.foo) //输出 override
JSX注释
JSX的注释，实话说不方便。下面的注释是错误的，只要把JSX关键部分注释是没效果的。

//<div></div>
<div> //</div>
下面有两种方式可以生效

或括号注释,跟javascript差不多

<div>
    {
        /*
            dddd
        */
    }
</div>
内联属性注释

//多行注释
<input
    /*
        dddd
    */
    name="email"/>
// 单行注释
<input 
    name="email"  //ddd
    placeholder="ddd"/>
所以像注释某个或多个JSX整个标签，要在花括号中注释

{
    //必须有空字符串，要不会包语法错误。
    ""//<div>ddd</div>
}
JSX优点和特点
更加熟悉，语法跟HTML非常相似（90以上相似度）

更加语义化，允许自定义标签及组件。

更加直观，标签处理方式，更加可读。

抽象化，React的升级，不需要改动任何JSX代码。

关注点分离,模块化，JSX以干净且简洁的方式保证了组件中的标签与所有业务逻辑的互相分离。

JSX与HTML有何不同
JSX跟HTML很像，但却不是HTML语法的完美复制。实际上，JSX规范中这样声明：

这个规范（JSX）并不尝试去遵循任何XML或HTML规范。JSX是作为一种ECMAScript特性来设计的，至于大家觉得JSX像XML这一事实，那仅仅是因为大家比较熟悉XML。详细

下面我们探索下JSX与HTML语法上的几点关键区别。

JSX可以使用变量属性
首先看看HTML的例子

JSX以同样的方式实现了属性的设置，同时还提供了将属性设置为动态JavaScript变量的便利。要设置动态属性，你只需要包原本的引号括起来的文本替换为花括号包囊的JavaScript变量或函数。看例子：

var id = this.props.id;
function getId(){
    return "test";
}
<div id={id} ></div>//变量
<div id={this.getId()} ></div>//函数也可以
其中使用到HTML的class在JSX中是className

//在js中写css属性当然要遵守语法，就像写js对象一样。
<div className="test"></div>
事件要使用驼峰式写法。

var add =  funtion(){}
<div className="test" onClick={add} style={style}></div>
sytle的css属性要使用驼峰式写法。

//在js中写css属性当然要遵守语法，就像写js对象一样。
var style= {
    fontSize: 13,
    bold: normal,
}
<div style={style}></div>
