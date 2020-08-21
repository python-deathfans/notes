## 路由

+ 现代Web框架使用**路由技术**来帮助用户**记住应用程序URL**。可以直接访问所需的页面，而无需从主页导航

+ ```python
  @app.route(‘/hello’)
  def hello_world():
     return ‘hello world’
  ```

+ 在这里，URL **'/ hello'** 规则绑定到**hello_world()**函数。 因此，如果用户访问**http：// localhost：5000 / hello** URL，**hello_world()**函数的输出将在浏览器中呈现。

## 变量规则

+ 通过向规则参数添加变量部分，可以**动态构建URL**。此变量部分标记为<variable-name>。它作为关键字参数传递给与规则相关联的函数。

```python
# 携带数据a
@app.route('/do/<a>')
def do(a):
    return "Hello World " + str(a)
```

+ 当用户访问**/do/123**,页面显示为 **Hello World123**

+ 除了默认字符串，还可以使用以下转换器构建规则

  + | 序号 | 转换器和描述                         |
    | ---- | ------------------------------------ |
    | 1    | **int**    接受整数                  |
    | 2    | **float**    接受浮点数              |
    | 3    | **path**    接受用作目录分隔符的斜杠 |

+ ```python
  from flask import Flask
  app = Flask(__name__)
  
  @app.route('/blog/<int:postID>')
  def show_blog(postID):
     return 'Blog Number %d' % postID
  
  @app.route('/rev/<float:revNo>')
  def revision(revNo):
     return 'Revision Number %f' % revNo
  
  if __name__ == '__main__':
     app.run()
  ```

+ **URL命名规范**

  + ```python
    from flask import Flask
    app = Flask(__name__)
    
    @app.route('/flask')
    def hello_flask():
       return 'Hello Flask'
    
    # 该方法命名规范
    @app.route('/python/')
    def hello_python():
       return 'Hello Python'
    
    if __name__ == '__main__':
       app.run()
    ```

  + 这两个规则看起来类似，但在第二个规则中，使用斜杠**（/）**。因此，它成为一个规范的URL。因此，使用 **/python** 或 **/python/**返回相同的输出。但是，如果是第一个规则，**/flask/ URL**会产生“404 Not Found”页面。

## URL 构建

> **url_for()**函数对于动态构建特定函数的URL非常有用。该函数接受函数的名称作为第一个参数，以及一个或多个关键字参数，每个参数对应于URL的变量部分。

```python
from flask import Flask, redirect, url_for
app = Flask(__name__)
@app.route('/admin')
def hello_admin():
   return 'Hello Admin'


@app.route('/guest/<guest>')

def hello_guest(guest):
   return 'Hello %s as Guest' % guest


@app.route('/user/<name>')
def hello_user(name):
   if name =='admin':
      return redirect(url_for('hello_admin'))
   else:
      return redirect(url_for('hello_guest',guest = name))


if __name__ == '__main__':
   app.run(debug = True)
```

+ **User()**函数检查接收的参数是否与**'admin'**匹配。如果匹配，则使用**url_for()**将应用程序重定向到**hello_admin()**函数，否则重定向到将接收的参数作为guest参数传递给它的**hello_guest()**函数。

## HTTP请求方法

| 序号 | 方法与描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | GET  未加密的形式将数据发送到服务器，最常见                  |
| 2    | HEAD  和GET方法相同，但是没有相应实体                        |
| 3    | POST  用于将HTML表单数据发送到服务器。POST方法接受的数据不由服务器缓存 |
| 4    | PUT  用上传的内容代替目标资源的所有当前表示                  |
| 5    | DELETE 删除由URL给出的目标资源的所有当前表示                 |

默认情况下，Flask路由响应**GET**请求。但是，可以通过为**route()**装饰器提供方法参数来更改此首选项。

## 模板

> 可以以HTML的形式返回绑定到某个URL的函数的输出。例如，在以下脚本中，**hello()**函数将使用
>
> 标签呈现'Hello World'。

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route('/hello/<user>')
def index(user):
    return render_template('hello.html', name=user)


if __name__ == '__main__':
   app.run(debug=True)
```

但是，从Python代码生成HTML内容很麻烦，尤其是在需要放置变量数据和Python语言元素（如条件或循环）时。这需要经常从HTML中转义。

这是可以利用Flask所基于的**Jinja2**模板引擎的地方。而不是从函数返回硬编码HTML，可以通过**render_template()**函数呈现HTML文件。

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route('/score/<int:marks>')    # 如果需要做判断的时候，一定要加上类型声明，不然都会认为是string
def score(marks):
    # score_ = int(input("请输入分数:"))
    return render_template('score.html', score=marks)


@app.route('/')
def hello():
    return 'Hello World'


if __name__ == '__main__':
    app.run(debug=True)

```

## Request对象

来自客户端网页的数据作为全局请求对象发送到服务器。为了处理请求数据，应该从Flask模块导入。

Request对象的重要属性如下所列：

- **Form** - 它是一个字典对象，包含表单参数及其值的键和值对。
- **args** - 解析查询字符串的内容，它是问号（？）之后的URL的一部分。
- **Cookies** - 保存Cookie名称和值的字典对象。
- **files** - 与上传文件有关的数据。
- **method** - 当前请求方法。