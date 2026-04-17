FROM python:3.11-slim

LABEL maintainer="timnekk"
LABEL version="1.0.0"
LABEL description="Production app"

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        wget \
        vim \
        git \
        build-essential \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN --mount=type=cache,target=/root/.cache/pip \
    --mount=type=bind,source=requirements.txt,target=requirements.txt \
    python -m pip install --no-cache-dir -r requirements.txt

USER 1001

COPY . .

EXPOSE 8080

CMD ["python", "/app/app.py"]

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://localhost:8080')" || exit 1

