# Snippets

## `pip install`

```Dockerfile
RUN --mount=type=cache,target=/root/.cache/pip \
    --mount=type=bind,source=requirements.txt,target=requirements.txt \
    : \
    && pip install -U -r requirements.txt \
    && : \
```

# Examples

## With compiled dependencies

```Dockerfile
FROM python:3.12.0-alpine as build
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN --mount=type=cache,target=/var/cache/apk/ \
    --mount=type=cache,target=/root/.cache/pip \
    --mount=type=bind,source=requirements.txt,target=requirements.txt \
    : \
    && apk add gcc musl-dev linux-headers \
    && pip install -U -r requirements.txt \
    && :


FROM python:3.12.0-alpine
WORKDIR /app
COPY --from=build /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
ENV PYTHONUNBUFFERED=0
CMD ["/bin/sh", "python ./main.py"]
```

## With debug

```Dockerfile
...

FROM python:3.12.0-alpine as base
WORKDIR /app
COPY --from=build /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
ENV PYTHONUNBUFFERED=0

FROM base as prod
CMD ["/bin/sh", "-c", "python ./main.py"]

FROM base as debug
ENV DEBUG=1
ENV LOG_LEVEL=DEBUG
RUN pip install debugpy
CMD ["/bin/sh", "-c", "python -m debugpy --wait-for-client --listen 0.0.0.0:5678 ./main.py"]
```
