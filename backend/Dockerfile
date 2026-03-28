FROM python:3.12

WORKDIR /app

# Устанавливаем gunicorn через зеркало Aliyun
RUN pip install -i https://mirrors.aliyun.com/pypi/simple/ \
    --default-timeout=100 \
    --retries=5 \
    gunicorn==23.0.0

COPY requirements.txt .

# Устанавливаем зависимости приложения через то же зеркало
RUN pip install -i https://mirrors.aliyun.com/pypi/simple/ \
    --default-timeout=100 \
    --retries=5 \
    -r requirements.txt \
    --no-cache-dir

COPY . .

# Собираем статику (новая строка!)
RUN python manage.py collectstatic --noinput

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "backend.wsgi"]