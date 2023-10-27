---
title: "Golang read toml file"
date: 2021-04-04T23:56:54+08:00
draft: false
tags: ["golang","web"]
---
Toml Config 
===

从toml格式文件中读取配置

```go
package main
import(
    "fmt"
    "log"
    "github.com/BurnSushi/toml"
)


type Config struct{
    Name string
    Awake bool
    Hungry bool
}

func main(){
    c := Config{}
    _, err := toml.DecodeFile("config.toml", &c)
    if err!= nil{
        log.Fatal(err)
    }

    fmt.Printf("+v\n",c)
}

```