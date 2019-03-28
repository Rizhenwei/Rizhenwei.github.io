---
title: 快速建站框架-Flask
date: 2019-03-17 13:51:19
categories: 
    - python
    - web 前端
tags:

    - python

series:
description: python Flask
keywords: web 前端
---

# 快速建站框架-Flask
## Flask 基本要点
- 主要用于微小项目，无需安装其他服务器如:Tomcat 、 Apache
- 提供python单元测试框架unitest接口
- Flask的socket是基于Werkzeug 实现的，模板语言依赖jinja2模板
- 可用插件较多，[插件地址](http://flask.pocoo.org/extensions/)

## 第一个 hello word

```python
from flask import Flask
app=Flask(__name__,template_folder='templates',static_url_path='/static/',static_path='/zhanggen') #创建1个Flask实例
@app.route('/')      #路由系统生成 视图对应url,1. decorator=app.route() 2. decorator(first_flask)
def first_flask():    #视图函数
    return 'Hello World'  #response
if __name__ == '__main__':
    app.run()              #启动socket

```
### 1、 配置文件

`app=Flask(__name__,template_folder='templates',static_url_path='/static/',static_path='/zhanggen')`
* 模板路径： template_folder='templates'
* 静态文件路径：static_url_path='/static/'
* 静态文件引入别名：static_path='/zhanggen'
* 设置为调试环境：app.debug=True （代码修改自动更新）
* 设置json编码格式 如果为False 就不使用ascii编码：app.config['JSON_AS_ASCII']=False
* 设置响应头信息Content-Type   app.config['JSONIFY_MIMETYPE'] ="application/json;charset=utf-8"  

### 2、路由系统
**动态路由（url传参）**
_视图必须有对应接收参数_
```python
1. @app.route('/user/<name>')  #接收输入参数
2. @app.route('/post/<int:age>')  #接收整型数字参数
3. @app.route('/post/<float:salary>') #接收浮点型数字参数
4. @app.route('/post/<path:path>') # 接收URL链接类型参数
```
**指定允许的请求方法**
`@app.route('/login', methods=['GET', 'POST'])`

```python
app=Flask(__name__)
@app.route('/<path:url>/',methods=['get']) #只允许get请求
def first_flask(url):
    print(url)
    return 'Hello World'  #response

if __name__ == '__main__':
    app.run()
```

**通过别名反向生成url**

```python
from flask import Flask,url_for
app=Flask(__name__)
@app.route('/<path:url>',endpoint='name1')
def first_flask(url):
    print(url_for('name1',url=url)) #如果设置了url参数，url_for（别名,加参数）
    return 'Hello World'

if __name__ == '__main__':
    app.run()
```
**通过app.add_url_rule()调用路由**
```python
app=Flask(__name__)

def first_flask():
    return 'Hello World' 

app.add_url_rule(rule='/index/',endpoint='name1',view_func=first_flask,methods=['GET'])
#app.add_url_rule(rule=访问的url,endpoint=路由别名,view_func=视图名称,methods=[允许访问的方法])
if __name__ == '__main__':
    app.run()

```
### 3、视图
**给Flask视图函数加装饰器**
> [python装饰器的作用就是为已经存在的函数或对象添加额外的功能](https://www.cnblogs.com/cicaday/p/python-decorator.html)
```python
#1、定义1个装饰器
def auth(func):
    print('我在上面')
    def inner(*args,**kwargs):
        return func(*args,**kwargs)
    return inner


app=Flask(__name__)

@app.route('/',methods=['GET'])
@auth #注意如果要给视图函数加装饰器，一点要加在路由装饰器下面，才会被路由装饰器装饰
def first_flask():
    print('ffff')
    return 'Hello World'

if __name__ == '__main__':
    app.run()
```
**request和response**
* a.请求相关信息

1. request.method： 获取请求方法

1. request.json

2. request.json.get("json_key")：获取json数据 **较常用      

3. request.argsget('name') ：获取get请求参数   

4. request.form.get('name') ：获取POST请求参数

5. request.form.getlist('name_list')：获取POST请求参数列表（多个）

6. request.values.get('age') ：获取GET和POST请求携带的所有参数（GET/POST通用）

7. request.cookies.get('name')：获取cookies信息

8. request.headers.get('Host')：获取请求头相关信息

9. request.path：获取用户访问的url地址，例如（/，/login/，/ index/）；

10. request.full_path：获取用户访问的完整url地址+参数 例如(/login/?age=18)

11. request.script_root： 抱歉，暂未理解其含义；

12. request.url：获取访问url地址，例如http://127.0.0.1:5000/?age=18；

13. request.base_url：获取访问url地址，例如 http://127.0.0.1:5000/；

14. request.url_root

15. request.host_url

16. request.host：获取主机地址 

17. request.files：获取用户上传的文件

18. obj = request.files['the_file_name']

19. obj.save('/var/www/uploads/' + secure_filename(f.filename))  直接保存

 * b、响应相关信息

1. return "字符串" ：响应字符串

2. return render_template('html模板路径',**{})：响应模板

3. return redirect('/index.html')：跳转页面