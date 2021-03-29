---
layout:     post
title:      Flask_login
subtitle:   登入装饰器
date:       2020-11-31
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - flask
---

## flask -login验证用户身份

### 保证某些路由只有登陆过的用户才可以进行访问。

flask_login模块提供了扩展

1 ,模板继承UserMixin

 2，创建并初始化login_manage添加到flask对象中 ,并设置重定向页面

 3,创建login_manager的load_user函数 用login_manager.user_loader进行装饰，

目的是将获取的用户id（可选如可获取用户电子邮箱等进行判读）写入会话.

4，@login_required 进行保护

- 在模板类中直接继承UserMixin

  - ```python
    from flask_login import UserMixin 
    class User(UserMixin, db.Model):
        #---
    ```

  - 创建用户初始化flask_login

    >```python
    >from flask_login import LoginManager 
    >login_manager.login_view = 'auth.login'
    >login_manager = LoginManager(app)
    >```
    >
    >login_view属性由于设置登录页面的端点，匿名函数尝试访问受保护的页面时 <em>重定向到该端点</em>

  

  - Flask-Login 要求应用指定一个函数，在扩展需要从数据库中获取 指定标识符对应的用户时调用

  ```python
  from . import login_manager
  @login_manager.user_loader 
  def load_user(user_id):
      return User.query.get(int(user_id))
  ```

  > 与login_user(user.id)对应，login_user将用户id写入会话，jinja2渲染时自动查找写入的此id如果找到 自动调用user_loader装饰的函数传入id。
  > 如不想用id作为标准，则login_user()的参数也要进行更改

  login_manager.user_loader 装饰器把这个函数注册给 Flask-Login， 

  在这个扩展需要获取已登录用户的信息时调用。

  - 保护路由

    在需要保护的路有前加@login_required装饰器保护

    ###  实例（登录用户）

    ```python
    from flask import render_template, redirect, request, url_for, flash from flask_login import login_user 
    from . import auth 
    from ..models import User
    from .forms import LoginForm
    @auth.route('/login', methods=['GET', 'POST']) 
    def login():
        form = LoginForm() 
        if form.validate_on_submit(): 
            user = User.query.filter_by(email=form.email.data).first()
            if user is not None and user.verify_password(form.password.data): 
                
                login_user(user, form.remember_me.data)
                
                next =request.args.get('next') 
                if next is None or not next.startswith('/'): 
                    next = url_for('main.index')
                    return redirect(next) 
                flash('Invalid username or password.') 
                return render_template('auth/login.html', form=form)
    ```

    调用 Flask-Login 的 login_user() 函数，在用户会话中把用户标 

    记为已登录。

    login_user() 函数的参数是要登录的用户，以及可选 

    的“记住我”布尔值，“记住我”也在表单中勾选。如果这个字段的值为 

    False ，关闭浏览器后用户会话就过期了，所以下次用户访问时要重新 

    登录。如果值为 True ，那么会在用户浏览器中写入一个长期有效的 

    cookie，使用这个 cookie 可以复现用户会话。

- 为了登出用户，这个视图函数调用 Flask-Login 的 logout_user() 函 

  数，

```python
from flask_login import logout_user, login_required 
@auth.route('/logout') 
@login_required 
def logout():
    logout_user() 
    flash('You have been logged out.') 
    return redirect(url_for('main.index'))
```

- 官方文档解释

  (1) 用户点击 Log In 链接，访问 http://localhost:5000/auth/login。处理这 

  个 URL 的函数返回登录表单模板。 

  (2) 用户输入用户名和密码，然后点击提交按钮。再次调用相同的处理 

  函数，不过这一次处理的是 POST 请求，而非 GET 请求。 

  a. 处理函数验证通过表单提交的凭据，然后调用 Flask-Login 的 

  login_user() 函数，登入用户。 

  b.<a color = 'red'> login_user() 函数把用户的 ID 以字符串的形式写入用户会 

  话。</a>

  c. 视图函数重定向到首页。 

  (3) 浏览器收到重定向响应，请求首页。 

  ​	a. 调用首页的视图函数，渲染主页的 Jinja2 模板。 

  ​	b. 在渲染这个 Jinja2 模板的过程中，首次出现对 Flask-Login 的 

  ​	current_user 的引用。 

  ​	c. 这个请求还没有给上下文变量 current_user 赋值，因此调用 

  ​	Flask-Login 内部的 _get_user() 函数，找出用户是谁。 

  d. _get_user() 函数检查用户会话中有没有用户 ID。

  如果没有， 返回一个 Flask-Login 的 AnonymousUser 实例。

  如果有 ID，调用应用<a color='red'> 中使用 user_loader 装饰器注册的函数，传入用户 ID。</a>

  e. 应用中的 user_loader 处理函数从数据库中读取用户，将其返 

  回。Flask-Login 把返回的用户对象赋值给当前请求的 current_user 

  上下文变量。 

  f. 模板收到新赋值的 current_user 。 

  使用 login_required 装饰器装饰的视图函数将使用 current_user 

  上下文变量判断 current_user.is_authenticated 表达式的结果是 

  否为 True 。

总结：在flask_login 判断用户是否登录的依据就是current_user变量，login_user()将

函数把用户的 ID（可以是别的，但在下面也要做相应更改） 以字符串的形式写入用户会话。

，jinja2进行渲染时，会在用户会话中去查找current-user变量，找到在自动调用user_loader装饰的函数将current_user赋值。