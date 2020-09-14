# 온라인 코칭 흐름

## web 수업의 목적

WEB? 무언가 만든다

python, javascript, html, css, django, vue 등의 사용법을 익히는게 아니라 

**목표로 하는 걸 스스로 만들어낼 수 있도록**

공식 문서, 구글링을 통해 스스로 문제해결 가능하도록

**전체 흐름을 알고, 내 프로젝트를 위해서 뭐가 필요한지(서버, db, 크롬 익스텐션) 알게 되는 것**

==혼자서 도전해보는 것, 무엇을? 내가 만들 수 있는 것을 직접 만들어보는 것==

ex) 

- 수업자료를 그대로 따라하기
- 에러 발생 시 무턱대고 검색X, 질문X --> **에러코드, 메세지 읽고 이 녀석을 어떻게 해결할 수 있을까? 반드시 고민!**
- 검색의 범위 또한 줄어들고, 질문 또한 명확해진다.

---------



게시판을 가진 웹사이트를 만들거야

- 메인 페이지 = 글 리스트
- 글쓰기
  - 글 쓸 수 있는 페이지를 보여주는 녀석(create)
  - 사용자가 보낸 글을 저장하는 녀석
- 데이터베이스 - 글 정보가 저장됨



- django는 app을 기능별로 만들어서 관리
  - 게시판 - article app
  - 유저관리 - users app

## 1. 가상환경 설정

1. startproject

2. startapp

3. app 등록

4. url (주소 입력시 어떤 페이지를 보여줄건지 결정)

   `path('search/', views.search),` search/라는 주소로 들어오면 view의 search를 보여준다. 즉, path(주소, 어떤 화면을 보여줄 로직)

   `path('articles/', include('articles'),` articles/ 주소 아래에 오는 것들은 articles폴더의 urls.py에 있다. ex) articles/delete

5. view

   5-1. model

   5-2. view

6. template



.gitignore **왜 venv, vscode, db.sqlite 넣지 말라했는지 생각해보기**

## 2. 프로젝트와 app

### urls

- 프로젝트의 urls.py

  ```python
  from django.urls import path, include
  ```

  

  ```python
  urlpatterns = [
      path('articles/', include ('articles.urls')), 
  ]
  ```

- app의 urls.py

  ```python
  from django.urls import path
  from . import views
  ```
  
  
  
  ```python
app_name = 'articles'
   
  urlpatterns = [
      path('', views.index, name = 'index'),
      path('create/', views.create, name='create'),
  ]
  ```
  
  - `path(주소, view)`와 `path(주소, include)` 차이
    - `path('search/', views.search),` search/라는 주소로 들어오면 view의 search를 보여준다. 즉, path(주소, 어떤 화면을 보여줄 로직)
    - `path('articles/', include('articles'),` articles/ 주소 아래에 오는 것들은 articles폴더의 urls.py에 있다. ex) articles/delete

### templates

- app, 프로젝트와 같은 레벨에 `templates 폴더` 생성

  - `base.html`파일 생성 및 기본 양식과 `block content` 

- 경로 추가

  - 프로젝트의 settings.py에 경로 추가

    ```python
    TEMPLATES = [
        'DIRS': [BASE_DIR / 'templates'],
    ]
    ```

- app에 `templates 폴더` 생성, 그 아래에 `appname 폴더`생성

  - `~.html`파일 생성

    ```python
    {% extends 'base.html' %}
    
    {% block content %}
    {% endblock content %}
    ```

### views.py 와 html

```python
from django.shortcuts import render, redirect
from . models import Article
```



- index

  ```python
  def index(request):
      articles = Article.objects.all()
      context = {
          'articles' : articles,
      }
      return render(request, 'articles/index.html', context)
  ```

  ```python
  <a href = {% url 'articles:create'%}> 새글쓰기 </a>
  <hr>
  {% for article in articles %}
    <h1>{{article.title}}</h1>
    <p>{{article.content}}</p>
    <hr>
  {% endfor %}
  ```

  

- create

  ```python
  def create(request): # 글 쓸 수 있는 페이지
      if request.method == 'POST':
          # 글을 쓰는 로직
          title = request.POST.get('title')
          content = request.POST.get('content')
          article = Article()
          article.title = title 
          article.content = content
          article.save()
          return redirect('articles:index') # articles app의 index url을 요청
          
      else:
          return render(request, 'articles/create.html')
  ```

  - `return render` 와 `return redirect` 차이
    - `return render`: 오른쪽 주소의 html 화면을 보여주는 것
    - `return redirect`: 오른쪽 주소로 url 요청을 다시 하는 것

  ```python
  <form action="{% url 'articles:create' %}" method="POST">
    {%csrf_token%}  
    <label for="title">title : </label>
    <input type="text" name="title" id="title">
    <label for="content">content : </label>
    <textarea name="content" id="content" cols="30" rows="10"></textarea>
    <input type="submit" value="제출하기">
  </form>
  ```

  1. 클라이언트가 서버에게 정보를 보낼 떄: form tag
  2. 주소를 한번에 바꿀 때를 대비: action에 `url 'app_name: url_name'`
  3. `POST`방식이므로 **csrf_token 필수**

## 3. git

1. `pip freeze > requirements.txt`를 통해 설치한 프로그램을 알려준다.

2. app, 프로젝트와 같은 레벨에 `.gitignore`파일 생성

   ```python
   venv/
   .vscode/
   db.sqlite3
   ```

   git하지 않을 파일 입력 OR `gitignore.io`에 입력 후 복붙