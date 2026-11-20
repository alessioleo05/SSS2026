FROM python:3.12-slim

RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Clona il repo del professore e copia tutto in /app
RUN git clone https://github.com/mmenapace/SomeBankingApp.git /tmp/repo \
    && cp -r /tmp/repo/. . \
    && rm -rf /tmp/repo

# main.py si trova in /app/backend
WORKDIR /app/backend

EXPOSE 8000

# --root-path /api fa si' che Swagger cerchi /api/openapi.json
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--root-path", "/api"]