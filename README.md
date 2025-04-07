<h2>Инструкция по запуску</h2>

<h3>1. Подготовка окружения</h3>

<h4>1.1. Установите Docker и Docker Compose</h4>
  Убедитесь, что на вашей машине установлены:

  Docker: https://docs.docker.com/get-docker/
  Docker Compose: https://docs.docker.com/compose/install/

  Проверьте установку
  ```ruby
    docker --version
    docker-compose --version
  ```

<h3>2. Клонирования репозитория</h3>
  Склонируйте репозиторий на локальную машину:
  
  ```ruby
    git clone https://github.com/ivanT1625/gitlab_ci_cd
  ```
      
<h3>3. Настройка GitLab и GitLab Runner</h3>
  Запустите GitLab и GitLab Runner:
    
   ```ruby
      docker-compose up -d
   ```
    
  GitLab будет доступен по адресу "http://localhost". Войдите как администратор:
       - Логин: root
       - Пароль: admin
       
<h3>4. Регистрация GitLab Runner</h3>
  <h4>4.1. Получите токен для регистрации раннера</h4>
  
    1. Перейдите в GitLab через браузер
    2. Войдите как администратор (root)
    3. Перейдите в Settings > CI/CD > Runners
    4. Скопируйте токен для регистрации нового раннера

  <h4>4.2 Зарегистрируйте раннер</h4>
    Выполните команду для регистрации раннера:
    
  ```ruby
    docker exec -it gitlab-runner gitlab-runner register
  ```
  Ответьте на вопросы:
      - URL GitLab : http://gitlab.local/
      - Registration token : вставьте токен из GitLab.
      - Description : devops-test-runner
      - Tags : devops-test
      - Executor : docker
      - Default Docker image : python:3.9
      
<h3>5. Настройка проекта в GitLab</h3>
  <h4>5.1 Создайте новый проект в GitLab</h4>
  
      1. Войдите в GitLab.
      2. Создайте новый проект (например, ci-cd-demo).
      3. Выберите Blank project .
      
  <h4>5.2. Добавьте удаленный репозиторий GitLab</h4>
      Добавьте GitLab как удаленный репозиторий:
      
  ```ruby
    git remote add gitlab http://localhost/root/ci-cd-demo.git
  ```
      
  Проверьте, что удаленный репозиторий добавлен:
    
  ```ruby
    git remote -v
  ```

  <h4>5.3 Загрузите файлы в GitLab</h4>
      Загрузите файлы из вашего локального репозитория в GitLab:
      
  ```ruby
      git push gitlab main
  ```
<h3>6. Проверка работы пайплайна</h3>

  1. Перейдите в раздел CI/CD > Pipelines в GitLab.
  2. Убедитесь, что пайплайн запускается и проходит все этапы (lint, build, test).
  

