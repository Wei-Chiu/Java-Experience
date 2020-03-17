# GET和POST区别

1、get用于获取数据，post用于提交数据

2、get提交参数追加在url后面，post参数可以通过http body提交

3、get的url会有长度上的限制，则post的数据则可以非常大

4、get提交信息明文显示在url上，不够安全，post提交的信息不会在url上显示

5、get提交可以被浏览器缓存，post不会被浏览器缓存