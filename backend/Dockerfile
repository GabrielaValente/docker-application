FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh

COPY . .

EXPOSE 5000

ENV DB_HOST=db_host
ENV DB_USER=db_user
ENV mysql_password=db_password
ENV DB_NAME=db_name

CMD ["/wait-for-it.sh", "$DB_HOST:3306", "--", "python", "app.py"]

# docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=very_secure_root_password -e MYSQL_DATABASE=myapp_db -e MYSQL_USER=myapp_user -e MYSQL_PASSWORD=securepass -p 3306:3306 -v mysql-data:/var/lib/mysql mysql:8.0
# docker run -p 5000:5000 -e DB_HOST=localhost:3306 -e DB_USER=myapp_user -e mysql_password=securepass -e DB_NAME=myapp_db  ap-backend
