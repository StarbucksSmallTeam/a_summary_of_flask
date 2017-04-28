flask总结
=============
微框架思想-Flask 旨在保持核心简单而易于扩展。
### 三个依赖库：
* Jinjia2: 默认的模版引擎
* Werkzeug: 一个包含WSGI、路由、调试的工具集
* Itsdangerous: 基于Django签名模块的签名实现

### 基本功能：

* Web服务器
<pre><code>
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run()
</code></pre>

* 路由功能与HTTP方法
<pre><code>
@app.route('/index', methods=['GET','POST'])
</code></pre>

* 视图
<pre><code>
@app.route('/')
def index():
    mes = request.args.get('error')
    #app.logger.debug('index')
    return render_template('index.html', mes=mes)
</code></pre>

* 模版
<pre><code>
<!doctype html>
<title>Hello from Flask</title>
{% if name %}
  Hello {{ name }}!
{% else %}
  Hello World!
{% endif %}
</code></pre>

* 数据库 flask-sqlalchemy
<pre><code>
from flask_sqlalchemy import SQLAlchemy
db = SQLAlchemy()
</code></pre>
定义模型：
<pre><code>
class File(db.Model):
    __tablename__ = 'uploadfile'
    name = db.Column(db.VARCHAR(40), primary_key=True, unique=True, nullable=False)
    path = db.Column(db.VARCHAR(100), unique=True)
    user = db.Column(db.VARCHAR(20))
    time = db.Column(db.DATETIME)

    def __init__(self, name=None, path=None, user=None, time=None):
        self.name = name
        self.path = path
        self.user = user
        self.time = time

    def __repr__(self):
        return '<File %r>' % (self.name)
</code></pre>

* 应用上下文
<p>
暂时没用到
</p>
* 信号机制
<p>
Flask-Login
<br>
登录的时候需要用login信号简化后台代码
<br>
Flask-security
<br>
权限设置会用到
<br>
</p>
