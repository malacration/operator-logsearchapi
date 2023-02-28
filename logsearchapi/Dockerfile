#
# builder image
#
FROM golang:1.19.3-buster as builder
RUN mkdir /build
COPY . /build/

WORKDIR /build

# create module, fetch dependencies, then build
RUN ls -la /build
RUN go build

#
# generate small final image for end users
#
#FROM alpine:3.13.5
# busybox-glibc (versus Alpine's musl) matches Debian, but that is not a techinical issue here. I simply chose to prefer glibc
FROM busybox:1.34.1-glibc

# copy golang binary into container
WORKDIR /root
COPY --from=builder /build/logsearchapi .

# executable
ENTRYPOINT [ "./logsearchapi" ]
