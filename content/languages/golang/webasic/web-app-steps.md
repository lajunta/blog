---
title: "Web App Steps"
date: 2021-06-30T08:34:10+08:00
draft: false
---

# Golang web app steps



## First make a web server

```go
  func home(w http.ResponseWriter, r *http.Request) {
    tmpl.ExecuteTemplate(w, "Home", nil)
  }

  http.HandleFunc("/",home)
  http.ListenAndServe(":8080",nil)
```

## Second make assets dir and path

```go
//go:embed static/* views/*
var assets embed.FS

// add assets path
http.Handle("/assets/", http.StripPrefix("/assets/", http.FileServer(http.FS(assets))))

```

## Make template file and code

```go

var (
  tmpl        *template.Template
)

tmpl = template.Must(template.ParseFS(assets, "views/*.html"))
```

## Modify your views/home.html 

```html
  {{ define "Home" }}
  ...
  
  <link rel="stylesheet" href="/assets/static/app.css">
  <script src="/assets/static/app.js" defer></script>
  
  ...
  {{ end }}
```

## Make json output

```go
  w.Header().Set("Content-Type", "application/json")
  json.NewEncoder(w).Encode(solua())
```

## Make query from client js

```js
    const url = new URL("http://127.0.0.1:8080/solu")
    const params = { term: this.term, num: this.num }
    url.search = new URLSearchParams(params).toString()
    fetch(url)
      .then(response => response.json())
      .then(data => this.data = data);
```

## Make makefile

```bash
css:
  NODE_ENV=production npx tailwindcss -i ./src/app.scss  -c ./tailwind.config.js -o ./static/app.css --jit --minify
  esbuild --bundle ./src/app.js --outdir=./static/ --minify --sourcemap

linux: css 
  go build -ldflags="-w -s" -o bin/app
  upx bin/app

win: css 
  GOOS=windows GOARCH=amd64 go build -ldflags="-w -s" -o bin/app.exe
  upx bin/app.exe
```