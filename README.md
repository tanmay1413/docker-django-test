# 🐳 Django + Docker + Nginx + MySQL Setup

This project demonstrates a production-style Django application running with:

Django (Gunicorn)

MySQL

Nginx (reverse proxy + static files)

Docker & Docker Compose

CI/CD using GitHub Actions

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

├── .github/

    └── workflows/

      └── deploy.yml

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

* GitHub Actions (CI/CD)


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


# 🔄 CI/CD Pipeline (GitHub Actions)

This project uses GitHub Actions to automatically deploy changes to an EC2 server whenever code is pushed to the main branch.

# 📌 CI/CD Flow
Local Commit

   ↓ git push

GitHub Actions

   ↓ SSH

AWS EC2 Server

   ↓

docker compose up -d --build

# 🔐 Required GitHub Secrets

Add the following secrets in your repository:

GitHub → Settings → Secrets → Actions

# Secret Name	Value

EC2_HOST	EC2 Public IP or Elastic IP

EC2_USER	ubuntu

EC2_SSH_KEY	Private SSH key (id_ed25519)

# ⚠️ Paste the entire private key, including:

-----BEGIN OPENSSH PRIVATE KEY-----

📄 GitHub Actions Workflow

Create the file:

.github/workflows/deploy.yml



# ✅ Result

git push

→ GitHub Actions

→ SSH to EC2

→ Docker rebuild & restart

→ Application updated 🚀



















# 👨‍💻 Author
Tanmay Kulkarni

Full Stack Developer | Django | Docker | AWS


# output

![terminal code](image.png)
![login page](image-2.png)
![admin dashboard](image-1.png)

<img width="1919" height="1137" alt="image" src="https://github.com/user-attachments/assets/4ddf7220-af9c-4e7a-807b-9cc7689bdbf8" />
