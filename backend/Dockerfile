FROM python:3.11-slim

WORKDIR /app

# Installiere system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    curl \
    ffmpeg \
    eyed3 \
    && rm -rf /var/lib/apt/lists/*

# Kopiere requirements und installiere Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Kopiere den ganzen App code
COPY . .

# Erstelle notwendige Verzeichnisse
RUN mkdir -p /app/data /app/uploads /app/instance && \
    chmod -R 777 /app/data /app/uploads /app/instance

# Kopiere das Entrypoint skript
COPY docker-entrypoint.sh /app/
RUN chmod +x /app/docker-entrypoint.sh

EXPOSE 10000

CMD ["python", "-c", "import os; os.environ.setdefault('PORT', '10000'); exec(open('app.py').read())"]