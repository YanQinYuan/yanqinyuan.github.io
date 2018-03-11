---
layout: post
title: "解决生产测试环境数据库变量问题"
date: 2018-01-28
categories: tech
---

系统环境：ubuntu/macos，python，virtualenv,flask

把以下代码加入 bin/activate 文件中（或者 docker 的 启动文件里），在环境启动的时候加入系统变量

~~~js
export POSTGRES_URL="127.0.0.1:5432"
export POSTGRES_USER="postgres"
export POSTGRES_PW="dbpw"
export POSTGRES_DB="test"
~~~

增加方法获取系统变量：
~~~python
def get_env_variable(name):
    try:
        return os.environ[name]
    except KeyError:
        message = "Expected environment variable '{}' not set.".format(name)
        raise Exception(message)

# the values of those depend on your setup
POSTGRES_URL = get_env_variable("POSTGRES_URL")
POSTGRES_USER = get_env_variable("POSTGRES_USER")
POSTGRES_PW = get_env_variable("POSTGRES_PW")
POSTGRES_DB = get_env_variable("POSTGRES_DB")
~~~

使用 SQLALchemy ：
~~~python
from flask_sqlalchemy import SQLAlchemy

DB_URL = 'postgresql+psycopg2://{user}:{pw}@{url}/{db}'.format(user=POSTGRES_USER,pw=POSTGRES_PW,url=POSTGRES_URL,db=POSTGRES_DB)

app.config['SQLALCHEMY_DATABASE_URI'] = DB_URL
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False # silence the deprecation warning

db = SQLAlchemy(app)
~~~
