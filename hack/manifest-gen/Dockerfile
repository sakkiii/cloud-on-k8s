FROM docker.elastic.co/wolfi/go:1.23.6@sha256:007151b8fe7cb9a7d5986bdf9b9f7ab0082947894d418e93dd0156d8abf32ec8 as builder
ADD . /manifest-gen
WORKDIR /manifest-gen
ENV GO111MODULE=on CGO_ENABLED=0 GOOS=linux 
RUN go build -a -ldflags '-w -s' -o manifest-gen .

FROM scratch
COPY --from=builder /manifest-gen/manifest-gen /manifest-gen
COPY --from=builder /manifest-gen/assets /assets
ENTRYPOINT ["/manifest-gen"]
