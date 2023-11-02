---
title: "Grpc_golang_part1"
date: 2023-11-02T11:15:28+08:00
draft: false
---

Grpc Golang Part 1
===

- [grpc tutorial](https://grpc.io/docs/tutorials/)
- [demo](https://github.com/lajunta/myauthd)


## Prerequisites

### Install protoc

```text
Go to https://github.com/protocolbuffers/protobuf to download protoc
```

```text
export GO111MODULE=on  # Enable module mode
go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway
go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger
go get github.com/golang/protobuf/protoc-gen-go@v1.3
export PATH="$PATH:$(go env GOPATH)/bin"
```

### Make a proto file

```text
syntax = "proto3";

package grpcd;

import "google/api/annotations.proto";

service Grpcd {
    rpc Auth(AuthRequest) returns (AuthReply) {
        option (google.api.http) = {
        post: "/v1/auth"
        body: "*"
        };
    }    
}

message AuthRequest{
    string Login = 1; 
    string Password = 2; 
}

message AuthReply{
    bool Logined = 1; 
    string Login = 2; 
    string RealName = 3; 
    string Tags = 4; 
}
```

## Make service file and reverse-proxy gateway file

```text
echo "Make Grpcd Service File"
protoc -I /usr/local/include -I. -I $GOPATH/src -I $GOPATH/src/github.com/grpc-ecosystem/grpc-gateway/third_party/googleapis \
 -I grpcd --go_out=plugins=grpc:. grpcd/grpcd.proto 

echo "Generate reverse-proxy gateway file"
protoc -I/usr/local/include -I. \
  -I$GOPATH/src \
  -I$GOPATH/src/github.com/grpc-ecosystem/grpc-gateway/third_party/googleapis \
  --grpc-gateway_out=logtostderr=true:. \
  grpcd/grpcd.proto

```