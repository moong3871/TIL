> - API SERVER
> - RESTful API
> - Django REST Framework

# RESTful API

- ## REST

  - 우체국 송장처럼, 서버가 정보를 주고 받는 양식 같은 거

- ## REST API

  - ### 3 가지 구성

    - 자원 URI
      - URL + 계층
    - 행위 HTTP Method
    - 표현 Representational
      - 표현은 복잡한 개념, 일단 **JSON**이라고 생각하기

  - ### 2 가지 규칙

    - **URI는 정보의 자원을 표현**
    - **자원에 대한 행위는 HTTP Method로 표현**
      - GET = Read
      - POST = Create
      - PUT = Update
      - DELETE = Delete

# Django REST Framework

- 개발자들은 JSON형태로 정보를 주고 받는데, 직접 변환하면 코드도 길고 힘드니까 DRF 사용
- 즉, J**SON형태로 정보만 넘겨줄거다**. (UI만드는거 X, render X)

- Serialization

  - 어떤 데이터 타입을 JSON, XML로 바꾸는 것

  - 장고의 Form, ModelForm과 비슷

    |       | Django    | DRF             |
    | ----- | --------- | --------------- |
    | 응답  | HTML      | JSON            |
    | Model | ModelForm | ModelSerializer |

-------

# 작성

- ## 준비

  - 랜덤함 데이터 생성

    - django seed
    - `python manage.py seed app이름 --number=15`

  - DRF 설치

    - `pip install djangorestframework`

    - app 등록

    - app에 `serializers.py` 파일 생성

      - ModelForm 처럼 구성 후 `migrate`

        ```python
        from rest_framework import serializers
        from .models import Article
        
        class ArticleSerializer(serializers.ModelSerializer):
            
            class Meta:
                model = Article
                fields = ('id', 'title', 'content', 'created_at', 'updated_at',)
        ```

- ## CRUD

- 여러 개의 객체를 serialize하려면 ManyTrue option 필수

  `serializer = ArticleSerializer(articles, many=True)`

- ### CR

- ### UD

- postman으로 api 서버 테스트

