---
layout: post
title: Flask로 Firstapp 만들기
categories : TIL
tags : flask
---

## Flask로 Firstapp 만들기 


### > flask 설치 및 가상환경 세팅
```
# 가상환경 설정을 위한 virtualenv 설치
$ sudo apt-get install python-virtualenv

# 폴더 생성 및 가상 실행환경 생성
$ mkdir my flaskapp
$ cd myflaskapp
$ virtualenv venv

# 가상환경 활성화
. venv/bin/activate

# 가상환경에서 flask 설치
(venv) pip install flask
```

### > app.py
```python
#-*- coding:utf-8 -*_
from flask import Flask, render_template
from data import Articles

# 플라스크 app 객체 생성
app = Flask(__name__)

# data.py 파일에서 Articles 함수 import 하여 객체 생성
Articles = Articles()

# 생성된 flask app객체에 localhost/ 연결 시 INDEX text 표기되도록 라우팅
@app.route('/')
def index():
    return 'INDEX'

# localhost/home 연결 시 home.html 로 연결
@app.route('/home')
def home():
    return render_template('home.html')

# localhost/about 연결 시 about.html 로 연결
@app.route('/about')
def about():
    return render_template('about.html')

# localhost/articles 연결 시 Articles 객체를 article 변수에 담아서 articles.html 파일에 넘겨줌
@app.route('/articles')
def articles():
    return render_template('articles.html', articles = Articles)

# localhost/article/숫자 연결 시 해당 숫자를 id 변수로 가져와서 article.html 에 넘겨줌
@app.route('/article/<string:id>/')
def article(id):
    return render_template('article.html', id = id)

# 현재 스크립트 파일이 프로그램의 시작점이 맞는지 판단
if __name__ == '__main__':
    #디버그 모드를 실행, 파일 변경 시 서버가 코드변경 감지하여 자동으로 reload
    app.run(debug=True)

```


### > data.py
``` python
def Articles():
    articles = [
        {
            'id': 1,
            'title':'Article One',
            'body':'article one body',
            'author':'Stellar1',
            'create_date':'03-06-2018'
        },

	  {
            'id': 2,
            'title': 'Article two',
            'body': 'article two body',
            'author': 'Stellar2',
            'create_date': '03-07-2018'

        },
        {
            'id': 3,
            'title': 'Article three',
            'body': 'article three body',
            'author': 'Stellar3',
            'create_date': '03-08-2018'

        }
    ]

    return articles
```

   ### > layout.html
   ``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>MYFlaskApp</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">

</head>
<body>
    {% include 'includes/_navbar.html' %}

    <div class="container">

    {% block body %}{% endblock%}

    </div>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js"></script>
</body>
</html>

   ```

### > home.html
``` html
{% extends 'layout.html' %}

<!--layout.html 의 block body endblock 사이에 아래의 내용이 들어감 -->
{% block body %}
    <div class="jumbotron text=center">
        <h1>Welcome To FlaskApp</h1>
        <p class="lead">This application is the Best application</p>

    </div>
{% endblock %}

```

### > _navbar.html
``` html
<nav class="navbar navbar-expand-md navbar-dark bg-dark mb-4">
      <a class="navbar-brand" href="#">Top navbar</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarCollapse" aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarCollapse">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">MyflaskApp <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/home">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="about">About</a>
          </li>
            <li class="nav-item">
            <a class="nav-link disabled" href="/articles">Articles</a>
          </li>
        </ul>
        <form class="form-inline mt-2 mt-md-0">
          <input class="form-control mr-sm-2" type="text" placeholder="Search" aria-label="Search">
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>
```


### > articles.html
``` html
{% extends 'layout.html' %}

<!--layout.html 의 block body endblock 사이에 아래의 내용이 들어감 -->
{% block body %}
    <h1>Articles</h1>
    <ul class="list-group">

        {% for article in articles %}

        <table class="table">
            <tr>
                <th>title</th>
                <th>author</th>
                <th>body</th>
                <th>title</th>
                <th>create_date</th>

            </tr>
            <tr>
                <td><a href="article/{{article.id}}"> {{article.title}}</a></td>

                <td> {{article.author}}</td>
                <td> {{article.body}}</td>
                <td> {{article.title}}</td>
                <td> {{article.create_date}}</td>
            </tr>
        </table>
        {% endfor %}

    </ul>

{% endblock %}
```


### > article.html
``` html
{% extends 'layout.html' %}

{% block body %}
    <h1>{{id}}</h1>

{% endblock %}
```

### > about.html
``` html
{% extends 'layout.html' %}

<!--layout.html 의 block body endblock 사이에 아래의 내용이 들어감 -->
{% block body %}

    <h1>About us</h1>
    <p>something like this</p>

{% endblock %}
```


>  참고 : https://www.youtube.com/watch?v=zRwy8gtgJ1A