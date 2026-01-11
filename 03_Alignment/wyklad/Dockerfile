FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

RUN mkdir -p /data

ENV OUTPUT_DIR=/data

CMD ["python", "script/scraper.py"]