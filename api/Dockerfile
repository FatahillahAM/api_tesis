FROM python:3.11-slim

RUN apt-get update && apt-get install -y \
    libgl1 \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN mkdir -p uploads static

EXPOSE 8000

# Gunakan shell form (bukan array) agar $PORT bisa dibaca Railway
CMD gunicorn index:app --bind 0.0.0.0:${PORT:-8000} --workers 1 --timeout 300 --preload
