# python_web_cmdb
基于django的CMDB之资产管理系统




python manage.py startapp spider

python manage.py makemigrations
python manage.py migrate



使用开发服务器
开发服务器，即开发时使用，一般修改代码后会自动重启，方便调试和开发，但是由于性能问题，建议只用来测试，不要用在生产环境。
python manage.py runserver
 
# 当提示端口被占用的时候，可以用其它端口：
python manage.py runserver 8001
python manage.py runserver 9999
（当然也可以kill掉占用端口的进程，具体后面有讲，此处想知道的同学可查下 lsof 命令用法）
 
# 监听机器所有可用 ip （电脑可能有多个内网ip或多个外网ip）
python manage.py runserver 0.0.0.0:8000
# 如果是外网或者局域网电脑上可以用其它电脑查看开发服务器
# 访问对应的 ip加端口，比如 http://172.16.20.2:8000

清空数据库
python manage.py flush
此命令会询问是 yes 还是 no, 选择 yes 会把数据全部清空掉，只留下空表。


创建超级管理员




# 按照提示输入用户名和对应的密码就好了邮箱可以留空，用户名和密码必填
# 修改 用户密码可以用：
python manage.py changepassword username


Django 更改超级用户密码
在工程文件目录下敲入：
python manage.py shell

from django.contrib.auth.models import User
user = User.objects.get(username = 'admin')
user.set_password('123456')
user.save()
------------------------------------------------
grant usage on schema public to root;
grant create on schema public to root;
------------------------------------------------

Django根据现有数据库建立model
Django引入外部数据库还是比较方便的，步骤如下 
创建一个项目，修改seting文件，在setting里面设置你要连接的数据库类型和连接名称，地址之类，和创建新项目的时候一致 
运行下面代码可以自动生成models模型文件 
python manage.py inspectdb 
这样就可以在命令行看到数据库的模型文件了

把模型文件导入到app中 
创建一个app 
django-admin.py startapp app 
python manage.py inspectdb > spider/models.py 
ok模型文件已经生成好了。下面的工作就和之前一样了
----------------------------------------------------------------------


