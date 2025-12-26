# 🐳 Django + Docker + Nginx + MySQL Setup

This project demonstrates a production-style Django application running with:

Django (Gunicorn)

MySQL

Nginx (reverse proxy + static files)

Docker & Docker Compose

# The same setup works locally and can be deployed to AWS EC2 or any Linux server.

# 📁 Project Structure

project-root/

├── docker/

│   ├── docker-compose.yml

│   ├── Dockerfile

│   ├── nginx.conf

│   └── .env

├── my_app/

│   ├── settings.py

│   ├── urls.py

│   ├── wsgi.py

│   └── asgi.py

├── manage.py

├── requirements.txt

└── README.md


# ⚙️ Tech Stack

* Python 3.11

* Django 4.2 (LTS)

* Gunicorn

* MySQL 8
 
* Nginx
 
* Docker & Docker Compose


# 🔐 Environment Variables

# Create a .env file inside the docker/ folder:

DJANGO_SECRET_KEY=your-secret-

DJANGO_DEBUG=0

DB_NAME=django_db

DB_USER=django_user

DB_PASSWORD=django_pass

DB_HOST=db

DB_PORT=3306


# 🚀 How to Run the Project

# install docker compose
sudo mkdir -p /usr/local/lib/docker/cli-plugins

sudo curl -SL https://github.com/docker/compose/releases/download/v2.29.7/docker-compose-linux-x86_64 \
  -o /usr/local/lib/docker/cli-plugins/docker-compose

sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose

# check version
docker compose version

# 1️⃣ Clone the repository

git clone <repo-url>

cd project-root/docker


# 2️⃣ Build and start containers

docker compose build

docker compose up -d

# 3️⃣ Run database migrations

docker compose exec web python manage.py migrate

# 4️⃣ Create superuser

docker compose exec web python manage.py createsuperuser

# 5️⃣ Collect static files (IMPORTANT)

docker compose exec web python manage.py collectstatic

Type yes when prompted.


# 🌐 Access the Application
Service   	URL
Home	    http://localhost/

Admin     Panel	http://localhost/admin/

MySQL	    localhost:3306


# ⚠️ Note:

Django is NOT exposed directly

Nginx runs on port 80

Gunicorn runs internally on port 8000


# 🛑 Common Commands
# Stop containers

docker compose down

# Stop & remove volumes (reset DB)
docker compose down -v

# View logs
docker compose logs web

docker compose logs nginx

docker compose logs db



# 👨‍💻 Author
Tanmay Kulkarni

Full Stack Developer | Django | Docker | AWS