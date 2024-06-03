# Stage 1: Builder stage
FROM python:3.11 AS builder

RUN apt update && apt install tk tcl curl cmake -y

WORKDIR /app

COPY . .

RUN pip install langchain-community
RUN pip install --no-cache-dir -e .

# Stage 2: Final stage
FROM python:3.11

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages
COPY --from=builder /usr/local/bin /usr/local/bin
COPY --from=builder /app .

COPY docker/entrypoint.sh .

ENTRYPOINT ["sh", "/app/entrypoint.sh"]
