第二周正式课笔记
========

第一部分 正则
-------

### 一、正则的基础知识


 1. 正则：规则；
 2. 正则的作用：匹配和捕获 字符串---他就是用来操作字符串；
匹配：判断是否符合我们制定好的规则（test） 
	符合-true 不符合-false；
捕获：把符合我们规则的东西拿出来；   
	reg.exec -数组 大正则中的小正则 （）分组  
	match - 数组 只能返回大正则；   
	replace -arguments - 返回什么看我们心情
 3. 正则由两部分构成：元字符和修饰符
元字符：放在//中间有意义的字符，包括有特殊意义的元字符和代表次数的量词元字符   
1)特殊意义的元字符:   
\ 转义 	 |或  （）分组 	 . 代表除了\n以外的其他元字符  
\n 控制台换行  	\b 单词边界 'w1  w2 w3' 开头结尾和空格   
^ 开头   	$ 结尾  
 \d 0-9数字     \D  跟\d正好相反   	\w 字母数字下划线 \W 、、  
 \s 空格（tab制表符 空格键 换页符）	 \S  、、、 
[abc]   a or b or c 三个中的任意一个；	 	[a-z]  a-z中的任意一个；   [^abc] 除了a or b or c 三个中的任意一个；    [^a-z]  除了a-z中的任意一个； 
 2)代表次数的量词元字符  
 * 0到多次  + 1到多次 
 ？ 0 or 1次：当？放在普通元字符或者非量词元字符后面时，代表0 或 1；（可有可无的意思）  
{n} n 次  
{n,} 至少n次 
{n,m} n 到 m 次；

（?:）在分组中？：的意思是只匹配不捕获
 (?=)正向预查
 (?！)负向预查
  ？在量词的后面，表示非贪婪匹配 比如：+？


4.元字符的应用
1）	var reg/\d\d/;//定义了连续出现两个0-9的数字//  
	var reg=/^\d\d$/;//以数字开头，以数字结尾//  
例子2.  
        var reg=/\d?///  
        str="1123"//     
        console.log(reg.exec(str));
        var reg=/1.2/   
       //var name="zhufeng"; 
      // console.log(reg.test('2015zhufeng2016'))
2）[]
//1.在中括号中出现的所有字符都是代表本身的意思的元字符（没有特殊含义）
//2.中括号不识别两位数,在中括号中出现的多位数是每一个数字中的一个，并不是一个多位数/
  var reg=/[\w+]/---数字、字母下划线或者+号中的一个
  var reg=/^[\d.]$/--只能是0-9之间的数字或者.
例子3./var reg=/^[12]$///1或者2中的一个  [xyz]
3）（）
1-）改变、提高默认优先级 re=/^(18|19)$/;
2-）分组的功能
	分组捕获  
	分组引用--规定和某一个分组出现的内容一模一样
3-）(?:) 只匹配，捕获
 var reg=/^18|19$/ 
符合需求的：18/19//189/119/819/1819
 var reg=/^(18|19)$/ 
符合需求的：只能是18或者19

例子3.
var re=/^(?:[+-])?(\d|([1-9]\d+))(\.\d+)?$/   
var str='+324.256';
console.log(re.exec(str))

5.?
1）？ 当？放在普通元字符或者非量词元字符后面时，本身代表一个量词元字符代表0 或 1；（可有可无的意思）
	var reg=/\d+/
2）？如果放在量词后面，是用来解决正则贪婪性
	var reg=/\d+?/
3）（？：）只匹配不捕获，只出现在分组当中
	var reg=/(?:\d+)/
4)?=	正向预查（都是在设定一些条件）
5）？！	负向预查（都是在设定一些条件）
6.修饰符  
g:global  
i:ignoreCase  
m:multiline


7.创建一个正则：
1)实例创建 var re=new RegExp('\\d');
2）字面量创建 var re=/\d/;3）
区别：   
1.在实例创建的正则中，特殊意义的元字符需要\转义，但字面量方式创建不需要； 
2.在实例创建中，可以进行变量拼接，但是字面量方式不可以；
例子1.
	var reg=/^\d+"+name+"\d+$/ 
 // 以数字开头，并且出现一到多次，字符串出现一到多次，包含nam三个字符，e出现一到多次，出现字符串，包含双引号--不是字符串拼接
	var reg=new RegExp("^\\d+"+name+"\\d+$",'g');
//字符串里的/d识别不了console.log(reg.test('2015zhufeng2016'))

7、正则捕获的特性
1）
 a)懒惰型
   体现：每一次执行exec只捕获第一个匹配的内容，在不进行任何处理的情况下，在执行多次捕获，捕获的还是第一个匹配的内容
   出现懒惰性的原因：lastIndex是正则每一次捕获在字符串中开始查找的位置，默认的值是0

例子4.
  var reg=/\d+/g;  
  var str="zhufeng2015peixun2016";
  var res=reg.exec(str);
  console.log(res)//["2015", index: 7, input: "zhufeng2015peixun2016"]
  我们第二次通过exec捕获的内容还是第一个2015


 b)如何解决懒惰性？
   在正则的末尾加一个修饰符“g”（global）。
   原理：加了全局修饰符，正则每一次捕获结束后，我们的lastIndex值变为了最新的值，下一次捕获从最新的位置开始查找，这样可以获取所有的内容。

例子5.  全局g--lastIndex 
    `var str='aadd22';
    var str1='a34ggg';
	var str2='a34ggg';
	var reg=/\d+/g
	console.log(reg.exec(str))//22
	console.log(reg.exec(str1))//null//捕获不到内容的时候lastIndex`
	值重新归零
	//reg.lastIndex=0;---当有一次查找不到的时候，浏览器会自己把lastIndex值归零从头开始找
	console.log(reg.exec(str2))//34

例子5.利用这个原理封装：找到所有的符合内容

方法一：
 var reg=/\d+/g;//   
 var str="zhufeng2015peixun2016zhufeng2017";
 var res=reg.exec(str)
 var ary=[];
 while(res){
 ary.push(res[0]);
 res=reg.exec(str);}
 console.log(ary)

方法二：
var reg=/\d+/g;
var str="zhufeng2015peixun2016zhufeng2017"
function getExec(reg,str){
  //1.判断下是否加修饰符   
  //2.循环reg.exec的返回值是否为null    
    var ary=[];
    var res=null;
    if(!reg.global){
        return reg.exec(str)
    }
    while(res=reg.exec(str)){
    //[“大正则匹配的内容”，index：匹配字符的起始索引，input：原始字符串]        
   ary[ary.length]=res[0]  }
   return ary}
	console.log(getExec(reg,str))


2）贪婪性：
   正则每一次捕获都是按照匹配最长的结果捕获，2015
   解决贪婪性：只需在量词元字符后面加问号
   ？在正则中有很多的作用：
放在一个普通的元字符后面代表出现0-1次
/\d?/ 数字可能出现也可能不出现
放在一个量词的元字符后面是取消捕获时候的贪婪性

例子6：
var reg=/\d+?/g;//出现1到多个0-9之间的数字// 
var str="zhufeng2015peixun2016zhufeng2017";
var res=reg.exec(str);
console.log(res)//["2",index:7,input:"zhufeng2015peixun2016zhufeng2017"]
ary=[];
while(res){
ary.push(res[0]);
res=reg.exec(str)}
console.log(ary) ;


8.正则的捕获方式
1）exec--正则的捕获
   每一次捕获的时候都是先进行默认的匹配，如果没有匹配成功，捕获的结果是null；只有有匹配的内容我们才能捕获到
a)捕获到的内容是一个数组
b）数组中的第一项是当前大正则捕获的内容
c）index：捕获内容在字符串中开始的索引位置
d）input：捕获的原始字符串

2）字符串中的match方法
   把所有和正则匹配的字符串都获取到   
例子7.
   var reg=/\d+?/g;
   var str="zhufeng2015peixun2016zhufeng2017";
   var ary=str.match(reg);
   console.log(ary)

  //虽然在当前match比exec更简单，但是match中存在一些自己处理不了的问题：在分组获取的情况下，match只能捕获到大正则匹配的内容，而面对小正则捕获的内容是无法获取

加g和不加g的区别
  //不加g  match和exec一样 可以捕获小分组和大正则，捕获一次
  //加g   match把所有和正则匹配的字符串都获取到,但是不能捕获小分组,exec不能一次全都捕获到，要执行多次
    不加g，结果都一样
var reg=/^[+-]?(\d|[1-9]\d+)(\.\d+)$/
var reg=/\d+/;
var str="zhufeng2015peixun2016zhufeng2017";
var ary=str.match(reg);
console.log(reg.exec(str))
console.log(ary)
//["2015",index:7,input:"zhufeng2015peixun2016zhufeng2017"]

	加g，
var reg=/^[+-]?(\d|[1-9]\d+)(\.\d+)$/
var reg=/\d+/g;
var str="zhufeng2015peixun2016zhufeng2017";
console.log(reg.exec(str))
//["2015", index: 7, input: "zhufeng2015peixun2016zhufeng2017"]
console.log(str.match(reg))//["2015", "2016", "2017"]
例子8：封装模拟match方法
String.prototype.match=function(reg){ 
	 //this--str  我们想操作的那个字符串--原型上的方法，里面的this都是我们要操作的当前的实例  
//        var ary=[];  
//        var res=reg.exec(this);  
//        while(res){  
//            ary.push(res[0])  
 //            res=reg.exec(this);   
//        }   
//        return ary   
//    }    //    str.match(reg)
3）replace 见10 replace专题

9.分组捕获一：
1)正则分组
a).改变优先级
b).分组引用
c).\2代表和第二个分组出现一模一样的内容；\1和第一个分组出现一模一样的内容一模一样：和对应分组中内容值也一样
/var reg=/^(\w)\1(\w)\2$/;
console.log(reg.test("zzff"))//true
console.log(reg.test("z0f_"))false


2).反向引用
var reg=/(\w+)(\w+)/;
var str="bbs.zhufeng.com"reg.exec(str);//["bbs", "bb", "s"]
var str="bbbs.zhufeng.com"reg.exec(str);//["bbbs", "bbb", "s"]


var reg=/(\w+)(\w+)\1\2/;
var str="bbbs.zhufeng.com"reg.exec(str)//null

var reg=/(\w+)(\w+)\1\2/;
var str="bsbs.zhufeng.com"reg.exec(str)//["bsbs", "b", "s"]



   分组捕获二
 正则在捕获时，不仅仅把大正则匹配的内容捕获到，而且可以把小正则捕获到
（?:）在分组中？：的意思是只匹配不捕获

var reg=/^(\d{2})(\d{4})(\d{4})(\d{2})(?:\d{2})(\d{2})(\d)(\d|X)$/;
var str="142727199002020021"
//console.log(reg.exec(str));
//["142727199002020021", "14", "2727", "1990", "02", "02", "00", "2", "1", index: 0, input: "142727199002020021"]
//ary[0]--大正则匹配的内容
//ary[1]--14--第一个分组捕获的内容
//ary[2]--第二个分组捕获的内容//....//
console.log(str.match(reg));//和exec获取结果是一样的
var reg=/zhufeng(\d+)/g;
var str="zhufeng1234zhufeng4333zhufeng83";
//我们用exec执行三次，每一次不仅仅把大正则匹配结果获取到，还可以获取第一个分组匹配的内容  
//console.log(reg.exec(str))//["zhufeng1234", "1234", index: 0, input:                      "zhufeng1234zhufeng4333zhufeng83"]  
//console.log(reg.exec(str))//["zhufeng4333", "4333", index: 11, input:                     "zhufeng1234zhufeng4333zhufeng83"]  
//console.log(reg.exec(str))["zhufeng83","83",index:22,input:"zhufeng1234zhufeng4333zhufeng83"]
而match只能获取大正则匹配的内容    
console.log(str.match(reg))//["zhufeng1234","zhufeng4333","zhufeng83"]


10.replace专题：
   1）.传递进这个匿名函数执行几次取决于正则和字符串匹配的次数，匹配一次，执行一次
   2）每执行一次匿名函数都会把当前匹配/捕获的内容当做参数传递给这个匿名函数
   3)arguments中存储的值和每一次exec获取的数组是非常的相似的。
   4）每一次执行匿名函数，方法中return后面返回啥，都相当于把当前这一次大正则所匹配的内容替换成啥。

0）replace替换--对原有字符串不产生影响
  varstr="zhufengpeixunzhufengketang";
  str=str.replace("zhufeng","珠峰");
  console.log(str)
str=str.replace(/zhufeng/g, function (content,index,input) {
        console.log(arguments)
        return content.toUpperCase();})
console.log(str)

1).
var re=/(\d+)zhufeng(\d+)/g;
var str='123zhufeng321zhufeng';
console.log(re.exec(str))
console.log(str.match(re))
2)
var str='my name is {0},my age is {1} , i come form {2}';var ary=['zhufeng','8','沧州'];
var str='zhufengzhufeng'var re=/zhufeng/g;
str=str.replace('zhufeng','zhufengpeixun');
str=str.replace(re,'zhufengpeixun');
console.log(str);
3)
var re=/{(\d+)}/g;
str=str.replace(re,function(){   return ary[arguments[1]]})
console.log(str);
4)
var str='20160514';var ary=['零','壹','贰','叁','肆','伍','陆','柒','捌','玖'];
var re=/(\d)/g;
str=str.replace(re,function(){  console.log(arguments)  return ary[arguments[0]]})
console.log(str);


var str=”2016-05-23”
var reg=/^(\d{4})-(\d{1,2})-(\d{1,2})$/g;
str.replace(reg,function(){  
//在匿名函数中使用$1在ie中不兼容,在外边使用不存在兼容问题
return RegExp.$1+”年”+RegExp.$2+”月”+RegExp.$3+”日”
}
//str.replace(reg,$1年$2月$3日)---效果一样。
5)var str='全日制第七期学费:12';
var ary=['零','壹','贰','叁','肆','伍','陆','柒','捌','玖'];
var re=/(\d)/g;
str=str.replace(re,function(){  console.log(arguments)  return ary[arguments[0]];});
console.log(str)
6)统计出现次数最多的单词(可能是多个)，及出现多少次
方法一：

var str='abcAAAABBBB';
var re=/[a-z]/gi;
var obj={};
str.replace(re,function(){
    console.log(arguments);
    var cur=arguments[0].toLowerCase();//拿到每个单词的小写；    if(obj[cur]){//给控对象赋值：把单词当作属性名，出现次数当作属性值；        obj[cur]++;
    }else{
        obj[cur]=1;
    }
})
console.log(obj)
var max=0;
var ary=[];//Object {a: 5, b: 5, c: 1}for(var k in obj){
    if(obj[k]>max){
        max=obj[k];
    }
}
for(var k in obj){//对象中，谁的属性值等于以上我们求出的最大值；那么谁的属性名就是我们要找的；    if(obj[k]==max){
        ary.push(k)
    }
}
console.log(max)
console.log(ary)

方法二：

 //获取一个字符串中出现次数最多的字符和对应的次数 
   var str='zhufengpeixunaaaaaadddddd'    
　　str=str.split('');
    str.sort(function(a,b){
　//        return a-b        
　　return a.localeCompare(b)
    })

    str=str.join('');
    var reg=/(\w)\1+/g;
    var str2='';
    var res='';
    var max=0    console.log(str);
    //aaaaaaddddddeefghinnpuuxz   
　　 str.replace(reg,function(){
        console.log(arguments)
        var len=arguments[0].length;
        if(len>max){
            max=len;
            res=arguments[1]+","+max;
        }
        str2+=arguments[1]+len;
    })
    console.log(str2)
    console.log(res)



7).模板引擎：
var str="my name is {0},my age is {1},come from {2},i love {3}~~";
var ary=["依文",28,"湖南","js"];
var reg=/{(\d+)}/g;
//var res=reg.exec(str);
console.log(res)//["{0}", "0", index: 11, input: "my name is {0},my age is {1},come from {2},i love {3}~~"] 
str=str.replace(reg,function(larCon,smallCon,index,input){
     //larCon---arguments[0]--大正则  
 //smallCon---arguments[1]--小正则   
//index---arguments[2] console.log(arguments)
     return ary[arguments[1]];
 })
console.log(str)

8）repalce 不改变原有字符串，返回替换后的新的字符串    
var reg=/\w+/g;
varstr='www.zhufengpeixun.cn'   str=str.replace('cn','com').replace('','').replace('','');    str=str.replace(reg,'zf');
console.log(str)

 9)var reg=/(\w+).(\w+).(\w+)/g;
   var	str='www.zhufengpeixun.cn'    　　　　　str=str.replace(reg,'$3.$2.$1');//$3表示第三个分组匹配的内容   //str=str.replace(reg,'\$');//也可以直接替换为$    
console.log(str)



10）单词首字母大写    
　　　var str='my name is zhufeng peixun ';
    　var reg=/\w+/g;
    　str=str.replace(reg,function(){
        console.log(arguments)
       res= arguments[0].charAt(0).toUpperCase();
　　　//console.log(res); 
       return res+arguments[0].substring(1);

    })
    console.log(str);




   

 11）queryURLParameter  获取地址栏中的参数

varstr = "http://kbs.sports.qq.com/kbsweb/game.htm?mid=1467588&age=18";

//->{mid:"1467588",age:18}
var reg = /([^?=&]+)=([^?=&]+)/g;
var obj = {};
str = str.replace(reg,function(){
    obj[arguments[1]] = arguments[2];
})
console.log(obj);



常用正则的实际应用小例子：
1）求年龄介于18-65之间正则表达式：
分组思路：18-19  20-59  60-65
// var reg=/^(1[8-9]|[2-5]\d|6[0-5])$/; 
//console.log(reg.test("18")) 

2）验证邮箱
//左边：数字、字母、下划线 
//1144709265@qq.com 1144709265@qq.com.cn  1282347298@163.com
//var reg=/^[\w.-]+@[0-9a-zA-Z]+(\.[a-zA-Z]{2,4}){1,2}$/; 
//var reg=/^[\w.-]+@[0-9a-zA-Z]+(\.[a-zA-Z]{2,4}){1,2}$/; 

3）中国标准真实姓名 2-4位汉字
 //var reg=/^[\u4e00-\u9fa5]{2,4}$///uniqu编码值

4）.身份证号码
//var reg=/^\d{17}(\d|X)$/; 
//项目中//13 0828 1990 12 04 06 1 7 
var reg=/^(\d{2})(\d{4})(\d{4})(\d{2})(\d{2})(\d{2})(\d)(\d|X)$/

5）有效数：
1.+-可有可无
2.可以使一位数字，如果是多位数字，第一位必须是1-9之间的数
3.小数位可有可无
var reg=/^[+-]?(\d|[1-9]\d+)(\.\d+)$/

6）手机号码
var reg=/^1\d{10}$/

表单验证去掉表情

根据RegExp.prototype,学习正则上的方法和属性
1.test()
2.exec

11.回调函数
把函数A做为实参传给另一个函数B的形参；在B中根据条件执行A函数；A函数可以执行无数次；
1)<script>
    function fn1(v){
        v();
    }
    function fn2(){
        alert('22222');

    }
    //fn1(fn2());fn2千万不能加括号，否则返回值是undefined,但如果fn2返回一个函数除外；   
 fn1(fn2);

</script>

 2)这里函数参数传的是对象；  
var b={name:'zhufeng',fn:fn2};
//JSON数据格式；严格的JSON{“name”:'zhufeng'}; 

 3)setInterval(function(){},300)  

4)
function fn1(v){      
alert(v.name)     
 v.fn();  } 
function fn2(){
      alert(this)  
    alert('我就是那个回调函数')  }
    fn1(b);








 





