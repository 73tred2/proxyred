## 🐳 Docker (Locale o Server)

### ✅ Costruzione e Avvio

```bash
git clone https://github.com/73tred2/proxyred.git
cd tvproxy
docker build -t tvproxy .
docker run -d -p 7860:7860 --name tvproxy tvproxy
```

---

## 🐧 ProxyRed (Dockerfile Hug)

### ✅ Costruzione e Avvio

```bash

FROM python:3.12-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    build-essential \
    git \
    ca-certificates \
    curl \
    libcurl4-openssl-dev \
    libssl-dev \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/73tred2/proxyred .

RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 7860

# Comando ottimizzato per avviare il server
CMD ["gunicorn", "app:app", \
     "-w", "4", \
     "--worker-class", "gevent", \
     "--worker-connections", "100", \
     "-b", "0.0.0.0:7860", \
     "--timeout", "120", \
     "--keep-alive", "5", \
     "--max-requests", "1000", \
     "--max-requests-jitter", "100"]
```

---

## 🐍 Avvio con Python (Locale)

### ✅ Setup e Avvio

```bash
# Clona il repository
git clone https://github.com/73tred2/proxyred.git
cd tvproxy

# Installa le dipendenze
pip install -r requirements.txt

# Avvia il server
gunicorn app:app -w 4 --worker-class gevent --worker-connections 100 -b 0.0.0.0:7860 --timeout 120 --keep-alive 5 --max-requests 1000 --max-requests-jitter 100
```

---
