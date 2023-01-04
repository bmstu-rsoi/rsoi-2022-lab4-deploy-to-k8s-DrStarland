# FROM golang:1.19 AS builder

# ENV GO111MODULE=on

# WORKDIR /app

# COPY . .

# RUN go mod tidy
# RUN go build -o app ./cmd/gateway

# EXPOSE 8080

# ENTRYPOINT ["./app"]

# # 1 шаг
FROM golang:1.19 AS build_stage
WORKDIR /app
COPY . .
RUN go mod tidy
RUN go build -o app.x ./cmd/gateway

# 2 шаг
FROM alpine AS run_stage
WORKDIR /app
COPY --from=build_stage /app/app.x /app/app.x
RUN chmod +x ./app.x

EXPOSE 8080

ENTRYPOINT ["./app.x"]
