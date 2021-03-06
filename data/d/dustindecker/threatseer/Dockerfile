# Build stage  
ARG GO_VERSION=1.10  
ARG PROJECT_PATH=/go/src/github.com/dustin-decker/threatseer  
FROM golang:${GO_VERSION}-alpine AS builder  
WORKDIR /go/src/github.com/dustin-decker/threatseer  
# GCC and libc-dev is only present for gosigar to compile. The result is not
dependent on libc.  
RUN apk --no-cache add git gcc libc-dev  
RUN go get -u github.com/golang/dep/cmd/dep  
COPY ./ ${PROJECT_PATH}  
RUN export PATH=$PATH:`go env GOHOSTOS`-`go env GOHOSTARCH` \  
&& dep ensure \  
&& CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build --ldflags '-extldflags
"-static"' -o bin/server server/main.go \  
&& go test $(go list ./... | grep -v /vendor/)  
  
# Production image  
FROM scratch  
COPY \--from=builder /go/src/github.com/dustin-
decker/threatseer/threatseer.yml /threatseer.yml  
COPY \--from=builder /go/src/github.com/dustin-
decker/threatseer/threatseer.elk.yml /threatseer.elk.yml  
COPY \--from=builder /go/src/github.com/dustin-decker/threatseer/config
/config  
COPY \--from=builder /go/src/github.com/dustin-decker/threatseer/bin/server
/bin/server  
ENTRYPOINT ["/bin/server"]

