# Build environment
# -----------------
FROM golang:1.15.0 as build-env
WORKDIR /cng

RUN apt-get update && apt-get install gcc git bash

COPY . .

RUN go build -ldflags '-w -s' -a -o ./bin/app ./cmd/app

# Deployment environment
# ----------------------
FROM debian
RUN apt-get update && apt-get install bash

COPY --from=build-env /cng/bin/app /cng/

EXPOSE 8080
CMD [ "/cng/app" ]