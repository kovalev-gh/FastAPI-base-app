# FastAPI-base-app 

## 🚀 Установка и запуск проекта

Ниже приведены шаги для локального запуска проекта и работы с ним.

---

## 1. Клонирование репозитория

Склонируйте проект в нужную директорию (например, в папку с вашими проектами).

```bash
# HTTPS
git clone https://github.com/kovalev-gh/FastAPI-base-app.git

# или SSH (предварительно настройте SSH-ключи)
git clone git@github.com:kovalev-gh/FastAPI-base-app.git
```

---

## 2. Установка зависимостей через Poetry

В корне проекта выполните:

```bash
poetry install
```

---

## 3. Узнать путь к виртуальному окружению

```bash
poetry env info --path
```

Пример вывода:

```
/Users/username/Library/Caches/pypoetry/virtualenvs/myproject-abc123-py3.10
```

---

## 4. Подключение интерпретатора в IDE

**Пример для PyCharm**:

1. Откройте: `Settings → Project → Python Interpreter`  
2. Нажмите: `Add Interpreter → Add Local Interpreter`  
3. Выберите **Existing environment** и укажите путь до:  
   - `bin/python` (Linux/Mac)  
   - `Scripts/python.exe` (Windows)  

Путь берём из вывода команды `poetry env info --path`.

---

## 5. Настройка переменных окружения

1. В директории с файлом `.env.template` создайте `.env`  
   Для этого выполните команды:

   ```bash
   cd fastapi-application
   cp .env.template .env
   ```

2. В файле **.env** поменяйте строку подключения к базе на свою, например:  

   ```env
   APP_CONFIG__DB__URL=postgresql+asyncpg://user:password@localhost:5432/shop
   ```

3. В файле **docker-compose.yml** также измените значения на свои.  
   ⚠️ Главное, чтобы они совпадали со значениями в `.env` и строках подключения.

---

## 6. Запуск Docker контейнеров

Убедитесь, что приложение Docker запущено на компьютере, затем в корне проекта выполните:

```bash
docker-compose up --build
```

---

## 7. Активация виртуального окружения Poetry

Выполните команду:

```bash
source $(poetry env info --path)/bin/activate
```

После активации в начале строки появится имя окружения, например:

```
(.venv) user@pc:~/dev/FastAPI-base-app$
```

---

## 8. Маркировка директории `fastapi-application` как Sources Root

В PyCharm:

- Найдите папку `fastapi-application`  
- ПКМ → **Mark Directory as → Sources Root**  
- Папка должна стать синей (в отличие от серых обычных папок).  

---

## ⚠️ Важно
Дальнейшие команды выполняются **внутри активированного виртуального окружения**.

---

## 9. Создание и применение миграций Alembic

Перейдите в директорию приложения:

```bash
cd fastapi-application
```

Создайте новую ревизию (если миграций ещё нет):

```bash
alembic revision --autogenerate -m "create tables"
```

Проверьте созданный файл в `alembic/versions/`.  
Если всё корректно — примените миграции:

```bash
alembic upgrade head
```

Теперь можно подключиться к БД через PyCharm или pgAdmin и проверить наличие таблиц.

---

## 10. Запуск приложения

```bash
cd fastapi-application
uvicorn main:main_app --reload
```

Приложение будет доступно по одному из адресов:

- http://localhost:8000/docs  
- http://127.0.0.1:8000/docs  
- http://0.0.0.0:8000/docs  

---

✅ Готово! Теперь вы можете пользоваться приложением.
