# Snippets

## alpine `apk install`

```Dockerfile
RUN --mount=type=cache,target=/var/cache/apk/ \
    : \
    && apk install pkg \
    && :
```
