---
title: "Worker_pool"
date: 2023-11-02T11:32:06+08:00
draft: false
---

Golang Worker Pool
===

This example is from tutorialedge

```golang
package main

import (
	"log"
	"net/http"
)

type Site struct {
	URL string
}

type Result struct {
	URL    string
	Status int
}

func crawl(wId int, jobs <-chan Site, results chan<- Result) {
	for site := range jobs {
		log.Printf("worker ID %d\n", wId)
		resp, err := http.Get(site.URL)
		if err != nil {
			log.Println(err.Error())
		}
		results <- Result{
			URL:    site.URL,
			Status: resp.StatusCode,
		}
	}
}

func main() {

	jobs := make(chan Site, 3)
	results := make(chan Result, 3)

	for w := 1; w <= 3; w++ {
		go crawl(w, jobs, results)
	}

	urls := []string{
		"http://www.baidu.com",
		"http://www.qq.com",
		"http://cnbeta.com",
		"http://www.hello.net",
	}

	for _, url := range urls {
		jobs <- Site{URL: url}
	}

	close(jobs)

	for a := 1; a <= 4; a++ {
		result := <-results
		log.Println(result)
	}
}
```