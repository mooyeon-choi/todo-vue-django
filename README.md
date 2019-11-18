# Vue - DRF

## 1. 기본 설정

1. Django

   1. 가상환경 설정

      ```bash
      $ python -V
      3.7.4
      $ python -m venv venv
      $ source venv/Scripts/activate
      (venv) $
      ```

      

   2. 패키지 설치

      ```bash
      (venv) $ pip install django djangorestframework
      (venv) $ pip freeze > requirements.txt
      ```

   3. django 프로젝트 생성

      ```bash
      $ django-admin startproject {프로젝트명} .
      ```

      

2. Vue

   1. VueCLI 설치

      ```bash
      $ npm install -g @vue/cli
      ```

   2. Vue 프로젝트 생성

      ```bash
      $ vue create {프로젝트 이름}
      ```

3. 프로젝트 폴더 구조

      ```
      todo-django-vue/
      	.git/
      	todo-django/
      		venv/
      		manage.py
      		todo_django/
      	todo-vue/
      		node_modules/
      		public/
      		src/
      		package.json
      ```

      

## 2. DRF 모델링

## 3. Vue

### Vue-router

> about 페이지 / home 페이지로 이동하는 버튼이 생김
>
> 경로를 설정해줌

```bash
$ npm i vue-router
$ vue add router
> y
> y
```



