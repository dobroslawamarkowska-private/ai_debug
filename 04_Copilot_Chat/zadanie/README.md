### ZADANIE 1 — Minimalna aplikacja FastAPI: Hello World + Docker

W tym uproszczonym wariancie budujemy minimalne API FastAPI bez bazy i predykcji.

Struktura projektu
project/
  main.py
  requirements.txt
  Dockerfile

Plik main.py
from fastapi import FastAPI

app = FastAPI(title="Hello API")

@app.get("/")
def root():
    return {"message": "Hello World"}

Plik requirements.txt
fastapi
uvicorn[standard]

Plik Dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

Część 1: Zbuduj obraz Dockera

W katalogu projektu uruchom:

docker build -t hello-api:latest .

przygotuj testy z pytest. 

▶ Część 2: Uruchom kontener lokalnie
docker run -p 8000:8000 hello-api:latest


Otwórz w przeglądarce:

http://localhost:8000


Powinieneś zobaczyć:

{ "message": "Hello World" }

Część 3: Wypchnięcie obrazu do rejestru (przez github-actions) skryptem z .github/ci-cd.yml i zbudowanie obrazu. 

