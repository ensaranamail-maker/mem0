FROM python:3.12-slim

RUN apt-get update && apt-get install -y \
    libpq-dev \
    gcc \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN mkdir -p /app/history && chmod 777 /app/history

EXPOSE 8000

ENV PYTHONUNBUFFERED=1

CMD ["sh", "-c", "python -c 'from db import engine; from models import Base; Base.metadata.create_all(engine); print(\"DB tables ready\")' && uvicorn main:app --host 0.0.0.0 --port 8000"]
