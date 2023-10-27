---
title: "Web Cache"
date: 2023-10-27T14:54:40+08:00
draft: false
---

Web Cache 
===

相关链接: [MDN Cache](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)

# 验证缓存仍然可用的方法 

- If-None-Match
- If-Modified-Since

# If-None-Match and Etag

当max-age 过期后 客户端发送 if-none-match 到服务端

服务端查看 etag 有没有变化，如果没有则返回 304 ， 如果有变化，则返回 200 和新的响应

# max-age  and if-modified-since

max-age 指定在客户端存放的时间, 当过期后，客户端会发送 if-modified-since, 如果没有变化 ，就返回 304

如果有变化，返回 200，和新的响应内容

## 不做缓存  

cache-control: no-store  // 不会删除 以前的缓存,不保证以前的缓存不会被使用
cache-control: no-cache // 每次必须进行验证，删除以前的缓存

- no-store: never store anything
- no-cache: never cache hit
- must-revalidate: never serve stale

# private and public

cache-control: private // 只存在本地浏览器，可带个人信息， 本个使用
cache-control: public  // 可以存放在缓存或代理服务器上， 大家都可以使用。

# Vary 

根据不同的头内容进行 缓存
如 vary: accept-language 对下面不同的语言进行缓存 

accept-language: en
accept-language: ja

# must-revalidate

要求客户端 当响应过期后必须重新 验证 新的响应是否可用


