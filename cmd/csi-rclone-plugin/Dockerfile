FROM golang:1.15 as build
COPY . /app
RUN cd /app/cmd/csi-rclone-plugin && go build -o csi-rclone-plugin .

FROM alpine:3.9
RUN apk add --no-cache ca-certificates bash fuse curl unzip

RUN curl https://rclone.org/install.sh | bash

COPY --from=build /app/cmd/csi-rclone-plugin/csi-rclone-plugin /bin/csi-rclone-plugin
ENTRYPOINT ["/bin/csi-rclone-plugin"]
