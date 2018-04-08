---
layout: post
title: [django] 회원가입 폼 만들기
categories : TIL
tags : django
---


## [django] 회원가입 폼 만들기

>[djangogirls 튜토리얼][https://tutorial.djangogirls.org/ko/]을 따라서 블로그를 만들면 admin 계정으로만 로그인 할 수 있다.
>
>일반 사용자들도 이용할 수 있도록 회원가입 폼을 만들어 보도록 한다.



### 참고 

>https://nomade.kr/vod/django/37/
>
>[user id 가져오는 방법 ](https://stackoverflow.com/questions/12615154/how-to-get-the-currently-logged-in-users-user-id-in-django/12615192)



- accounts 앱 생성

  ```
  python manage.py startapp accounts
  ```

- mysite 폴더 안 settings.py 내의 installed_apps에 새로 생성한 accounts 추가

  ```python
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'blog',
      'accounts', 
  ]
  ```


- accounts/urls.py 추가

  ```python
  from django.conf.urls import url
  urlpatterns = [
      url(r'^signup/$', views.signup, name='signup'),
  ]
  ```

- mysite/urls.py 추가

  ```python
  urlpatterns = [
  	url(r'^accounts/', include('accounts.urls')),
  ]
  ```

- accounts/views.py

  ```python
  from django.shortcuts import render
  from django.contrib.auth.forms import UserCreationForm
  from django.conf import settings

  def signup(request):
      if request.method == 'POST':
          form = UserCreationForm(request.POST)
          if form.is_valid():
              form.save()
              return redirect(settings.LOGIN_URL)
      else:
          form = UserCreationForm()
      return render(request, 'accounts/signup_form.html', {'form': form})
  ```

- accounts/accounts/templates/accounts/signup_form.html

  ```html
  <form action="" method="post">
      {% csrf_token %}
      <table>
          {{ form.as_table}}        
      </table>
      <input type = "submit" />
  </form>
  ```

- 현재 로그인한 User 객체의 id를 가져오는 방법 

  ```
  user = request.user.id
  # request.user에 값이 없으면 AnonymousUser를 반환한다.
  # if request.user.is_authenticated(): 로 로그인 되었는지 아닌지 판별
  ```

  ​