FROM python:3.11-alpine

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /app

# Install system dependencies required for mysqlclient 2.2.7
RUN apk add --no-cache \
    gcc \
    musl-dev \
    mariadb-dev \
    mariadb-connector-c-dev \
    pkgconf \
    python3-dev

# Copy and install Python requirements
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy your project files
COPY . .

EXPOSE 8000

# Start Gunicorn
CMD [ "gunicorn", "--workers", "3", "--bind", "0.0.0.0:8000", "my_app.wsgi:application" ]