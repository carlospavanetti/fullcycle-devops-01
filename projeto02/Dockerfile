FROM golang:alpine AS build-env

ADD . /src

RUN cd /src && go build -o main.out -ldflags "-w"


FROM scratch

WORKDIR /app
COPY --from=build-env /src/main.out /app/

ENTRYPOINT ["/app/main.out"]