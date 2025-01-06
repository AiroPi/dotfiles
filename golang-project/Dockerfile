# ! Select the desired version
FROM golang:1.21-alpine AS build
WORKDIR /app
RUN --mount=type=cache,target=/go/pkg/mod/ \
    --mount=type=bind,source=go.sum,target=go.sum \
    --mount=type=bind,source=go.mod,target=go.mod \
    --mount=type=bind,target=. \
    : \
    && go mod download -x \
    && go build -o /app/main \
    && :


FROM scratch
COPY --from=build /app/client /app/
ENTRYPOINT [ "/app/main" ]
