# SE-Lab-7

## files description
# Dockerfile
```
FROM python:3
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 8000'''
```
در خط اول گفته ایم که سکوی پایه ای کانتینر ما python3 است. در خط دوم یک فولدر جدید به عنوان app ساخته ایم که درون آن برنامه ها را بریزیم و اجرا کنیم.
در خط سوم محتویات کل پروژه را درون کانتینر کپی میکنیم. سپس در خط چهارم دستور نصب requirement ها را اجرا میکنیم.
در آخر نیز پورت 8000 را باز میکنیم.

# docker-compose.yml
```
services:
  db:
    image: postgres
    volumes:
      - ./data/db:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=123456
  webserver: 
    build: notes
    command: >
      sh -c "python manage.py makemigrations
             python manage.py migrate && 
             python manage.py runserver 0.0.0.0:8000"
    ports: 
      - '8000:8000'
    environment:
      - POSTGRES_NAME=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=123456
    depends_on:
      - db
```
در بخش اول سرویس دیتابیس خود را از روی ایمیج آماده postgres میسازیم. همچنین متغیر های محیطی آن را به طور دلخواه تنظیم میکنیم.
در قسمت webserver دستور لازم برای اجرای سرور جنگو را در command مینویسیم. این دستورات شامل migrate کردن و ران کردن سرور است. همچنین پورت را مشخص میکنیم.
در پایان متغیر های محیطی را برای این سرویس ست میکنیم. بعدا با استفاده از تابع os.environ.get درون کد خود میتوانیم از آنها استفاده کنیم.
در پایان نیز dependency بین دو سرویس را مشخص میکنیم.

## Testing Requests
1.
![2](https://github.com/Software-Engineering-Laboratory-Sharif/SE-Lab-7/assets/39655434/7c84674e-62e8-4c2a-9586-f1e95d4199db)
Login:
![3](https://github.com/Software-Engineering-Laboratory-Sharif/SE-Lab-7/assets/39655434/13dcbd42-9b92-4386-a6f3-7803bf8fa5ab)
2.
![4](https://github.com/Software-Engineering-Laboratory-Sharif/SE-Lab-7/assets/39655434/70f84f8f-e7d0-423b-8f57-a5f5bcd73662)
3.
![5](https://github.com/Software-Engineering-Laboratory-Sharif/SE-Lab-7/assets/39655434/f19a6331-5839-425d-95a1-8783bc4ef1c8)
4.
![6](https://github.com/Software-Engineering-Laboratory-Sharif/SE-Lab-7/assets/39655434/e280c8d8-ffc1-41b0-8c09-6460f0917dfd)
5.
![7](https://github.com/Software-Engineering-Laboratory-Sharif/SE-Lab-7/assets/39655434/b353da63-6bbb-4fe6-aafb-8d6e3695b0ca)
6.
![8](https://github.com/Software-Engineering-Laboratory-Sharif/SE-Lab-7/assets/39655434/981683d9-38bd-4c09-b5ed-6f7f74682bdc)


