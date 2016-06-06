1.表单排序
![错误][1]
报错信息：
oTbody.appendChild(ary) ;
Uncaught TypeError: Failed to execute 'appendChild' on 'Node': parameter 1 is not of type 'Node'
正确：
![正确][1]
a和b是整个tr标签，不能把整个数组添加到页面中去，得一个tr一个tr的添加到页面中。

2.split和join
3.http状态码
http://www.cnblogs.com/DeasonGuan/articles/Hanami.html


  [1]: https://github.com/bigfoot110614/anjie-recording/anjie-note/img/debug_info_1.png
  [2]: https://github.com/bigfoot110614/anjie-recording/anjie-note/img/debug_info_2.png