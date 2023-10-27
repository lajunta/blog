---
title: "Using Grpc Transfer Binary File"
date: 2021-04-29T09:25:49+08:00
draft: false
---


### Proto file
```bash
syntax = "proto3";

message Response {
    bytes fileChunk = 1;
}
message Request {
    string fileName = 1;
}

service TestService {
    rpc Download(Request) returns (stream Response);
}
```


### Server code
```go
func (srv *Server) Download(req *pbgo.Request, responseStream pbgo.TestService_DownloadServer) error {
    bufferSize := 64 *1024 //64KiB, tweak this as desired
    file, err := os.Open(req.GetFileName())
    if err != nil {
        fmt.Println(err)
        return err
    }
    defer file.Close()
    buff := make([]byte, bufferSize)
    for {
        bytesRead, err := file.Read(buff)
        if err != nil {
            if err != io.EOF {
                fmt.Println(err)
            }
            break
        }
        resp := &pbgo.Response{
            FileChunk: buff[:bytesRead],
        }
        err = responseStream.Send(resp)
        if err != nil {
            log.Println("error while sending chunk:", err)
            return err
        }
    }
    return nil
}
```


### client code

```go
conn, err := grpc.Dial("localhost:9090", grpc.WithInsecure())
if err != nil {
    log.Fatal("client could connect to grpc service:", err)
}
c := pbgo.NewTestServiceClient(conn)
fileStreamResponse, err := c.Download(context.TODO(), &pbgo.Request{
    FileName: "test.txt",
})
if err != nil {
    log.Println("error downloading:", err)
    return
}
for {
    chunkResponse, err := fileStreamResponse.Recv()
    if err == io.EOF {
        log.Println("received all chunks")
        break
    }
    if err != nil {
        log.Println("err receiving chunk:", err)
        break
    }
    log.Printf("got new chunk with data: %s \n", chunkResponse.FileChunk)
}
```