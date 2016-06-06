正式课第一周
--

1.git 操作步骤
git config --global user.name "zfpx" 
git config --global user.email "zfpx@126.com" 
mkdir test  创建文件夹test
ls 查看目录
1. cd test 进入到test的文件夹
pwd 查看路径
git init 初始化本地仓库
git add index.txt 添加到本地仓库的暂存区
git commit -m"注释" 提交到仓库
一.本地仓库和远程仓库关联起来
git remote add origin https://github.com/amgYen/testFactory.git
origin自己可以随便起   https://github.com/amgYen/testFactory.git 是远程仓库的地址
二、查看关联的远程地址
git remote -v
三、解除关联
git remote rm origin
四.远程仓库的内容更新到本地仓库
git pull origin master
五.把本地的内容提交到远程仓库
	git push -u origin master
	-u 把本地的主分支(master)和远程的主分支(master)关联起来 (-u只需要第一次写,下一次就不需要写了)直接 git push origin master就可以了

fork 课件仓库的地址 
1.git clone https://github.com/你自己github的用户名/javascript201604.git 把远程的仓库地址克隆到本地
2.把本地的内容添加到本地仓库去 git add 文件名 git commit -m"注释
3.关联珠峰培训课件仓库地址git remote add amgYen https://github.com/zhufengpeixun/JavaScript201604.git
4.到自己github上的javascript201604这个仓库,点击按钮New pull request ->create pull request
获得每日课件
git clone https://github.com/zhufengpeixun/JavaScript201604.git
git pull origin master 

2.浏览器工作原理
浏览器加载的时候,提供一个供js代码执行的环境->全局作用域函数执行的时候会产生私有作用域(局部作用域) 作用域 -->"栈内存"     1)存储基本类型的数据 
2)提供js代码执行的环境
var ary = [10,34,5,6];
function fn(ary){ 
//	argument[0]=””
    ary[0] = 0;
    ary = [0];
    ary[0] = 100;
    return ary;
}
var res = fn(ary);
console.log(res);//[100]
console.log(ary);//[0,34,5,6]

对象数据类型的工作原理
对象类型在内存空间里的存储步骤//方法的定义和方法的执行步骤 对象存储步骤和方法的定义  
 1.开辟一个内存空间,xxff00  
2.对象(属性名和属性值) 函数(字符串) 
3.xxff00赋值给变量名(方法名)//方法执行  
 1)重新开辟一个私有的空间(私有作用域)  
 2)在代码执行之前,给形参赋值(形参是私有变量,只能方法体内访问的到) 
 3)代码从上往下执行

2. 封装一个方法 取n-m之间的随机数    
function getRandom(n, m) {
        var n = Number(n);
        var m = Number(m);
        //如果n或者m之间任意一个不是有效数则返回一个随机数        	if (isNaN(n) || isNaN(m)) {
            return Math.random();
        }
        //如果n>m时 n和m交换位置//     
	    var temp = null;    
      temp = n; n = m;//      
      m = temp;//    
  		 n = n(10) + m(5);//    
    m = n(15) - m(5);//    
    n = n(15) - m(10);   
    n = n + m;
    m = n - m;
    n = n - m;
     return Math.random() * (m - n) + n;

    }
    getRandom(5, 10);



3.逻辑运算符
     a||b 如果a为真则返回a的值,如果a为假则返回b的值 
	  a&&b  如果a为真则返回b的值,如果a为假则返回a的值       		5 || 3 ->5  
		 false || 0 ->0  
		 true ||1 ->true  
		  false && 0 ->false  
		 优先级  &&>||  
		 0 && 3 ||5 ->0&&3->0  0||5->5 
		  3 || 0 && 5  ->0&&5 ->0 3||0->3



4.预解释：
 预解释(变量提升):在当前作用域下,代码执行之前,对带var或者function关键字的提前声明或定义,带var关键字和带function关键字的预解释是不一样的
    预解释:
        1)var关键字的是提前声明(declare)
        2)function关键字的是定义(声明+赋值)defined
     页面加载的时候,浏览器会提供一个供js代码执行的环境 -->全局作用域 
     函数运行的时候,也会提供一个供js代码执行的环境-->私有的作用域  
var x=y=5//var x=5； y=5  y不预解释
var和不带var的变量有什么区别  
	  var num = 13;
        num = 12;
    //1.var关键字的变量要预解释,不带var关键字的变量不需要预解释 
    //2.var num = 13;在全局作用域下定义了一个变量num= 13 ;    给window增加了一个属性 window.num = 13  //num = 12;仅仅是给window增加了一个属性 window.num = 12;    //3.在私有作用域中,不带var关键字的变量称为非私有变量,去它的上级作用域查找看是否有这个变量,如果有的话,则把值获取到,如果没有找到的话再继续往上级查找....一直找到window为止.如果window下也没有找到,则报错...
定义一个变量的过程
var str = "珠峰培训";//定义一个变量Str  
var str;//声明了一个变量str   
//执行步骤 ：1.在代码执行之前,声明一个变量str (预解释)       2.在代码执行时,开辟一个内存空间,保存珠峰培训这个数值       3.把珠峰培训这个数据赋值给变量str,变量和值之间就关联起来的,这时才定义了一个变量str  
 console.log(num);//undefined  
1.预解释时已经声明了一个变量 
在全局作用域下,声明了一个变量也相当于给window增加了一个属性 window.num但是没有值,undefined  
var num = 12;   console.log(num);  
 //方法分为两步(方法定义和方法的执行)   
//fn();//在预解释时是定义  
 //function fn(){ 方法的定义 (当代码执行到这边时,由于在预解释时已经定义过了,所以这边就不再理会了)     
   console.log("在预解释时是定义")}   //fn();   //function(){} //函数的声明   //var  fn1 = function(){} //函数表达式//    fn1(); //   (function(){})(); 自执行函数   //预解释也是发生在私有作用域中    var num = 13;
    function fn(num){ //当形参和私有变量名一样时,可以当成一直是对形参的赋值过程       //console.log(num);        var num =12;
        console.log(num);//12    }
    fn(num);
    console.log(num);
    //函数里私有变量:形参,私有变量(var 申明的变量)  
	 //方法运行的时候,代码执行之前:1.形参赋值 2.预解释 3.代码从上往下执行  
	  var num = 13;
     function fn(){
        console.log(num);//全局下的num的值获得到13        			var num = 12;//把全局作用域下的num的值改成12        12    }
    fn();

    
作用域链
1）怎么查找上级作用域?
.当前的这个函数是在哪个作用域下定义的,上一级作用域就是谁 ,跟函数在哪儿执行的是没有关系（见例子）
.作用域链(为了保证执行环境里的函数或者变量之间有序访问)
.window作用域是最外层的作用域链 
.当前执行的函数是最前端的作用域链
例子1：function fn(){
    //console.log(num);  
	 num = 12; //给查找不到的变量直接赋值,就相当于给window增加了个属性num ->window.num = 12;  
	  console.log(num);
}
fn();
console.log(num);

例子2：var windowColor = "blue";
function fn(){
    var oneColor = "red";
    function fn1(){
        var otherColor = "yellow"      
	  console.log(oneColor);
    }
    //console.log(otherColor);    fn1();
}
fn();
//证明查找上级作用域和方法在哪里执行没有关系,和方法在哪里定义有关系
例1：
unction fn1() {
    var num = 13;
    function f() {
        console.log(num);
        }
        return f;
    }
  var num = 12;  
 var aa = fn1();  
var aa = function f(){console.log(num)};
aa();//num的值->是否是私有的->不是->往上级查找(这个方法是在哪定义的)
例二：
function fn1() {
        var num = 13;
        function f() {
            console.log(num);
        }
        return f;
    }
	function fn2() {
    	var num = 14;
   	var bb = fn1();//var bb = function f(){console.log(num)}    	bb();
	}
	fn2();
例三：var num = 18;
var str = "lily";
function fn2(){
    console.log(str,num);   num = 19;
    str = "wyz";
    var num = 14;
    console.log(str,num);}
fn2();
console.log(str,num);
//lily undefiend    wyz 14   wyz 18
例4.
var num = 12;
function fn() {
    var num = 100;
    return function () {
        console.log(num);
    }
}
var f = fn();
f();
预解释之无节操特点

1。in用来检测对象里是否有这个属性
2.不管条件成立与否，都会预解释
例：
if(!("a" in window)){//在预解释时声明了变量a,就表示在window下有个属性a  
var a = "珠峰培训"; 
} 
alert(a); //undefined 

例：fn();
if( 9 == 8 ){   
 function fn(){alert("坑爹的预解释")} }
fn();//
3.方法当值存在时，是不预解释的，以下情况都不预解释
var fn = function f(){alert("here~~~")};
fn();
oDiv.onclick=function(){console.log(111)};
window.setTimeout(function(){},1000);
4.自执行函数，定义+执行一起做了
;(function (){console.log(111)})();
~function (){console.log(222)}();
!function (){console.log(333)}();

;(function(){
    console.log(num);//undefined    var num = 12;
    //形参赋值   //预解释   //代码从上往下执行})()
5.函数的return
return "下面"的代码不再执行,但是要预解释  
return "后面" 的函数不进行预解释
 function sum(){
  console.log(aa);//undefined
   b();//报错
  return function b(){alert("fn1")};
  var aa = 12; }
  sum();
6.重名变量
	var b =  12; var b = 13; 
	console.log(b);*///变量名重复只会声明一次,但是会赋值多次
var b = 13;
function b(){//方法预解释的时候已经定义过了,代码执行到这边时就忽视了(跳过这一步)    console.log("111");
}
console.log(b);
例1.
fn();
function fn(){console.log(1);};
fn();var fn=12;
fn();报错 Uncaught TypeError: fn is not a function
function fn(){console.log(2);};
fn();




