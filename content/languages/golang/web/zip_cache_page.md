---
title: "Zip Cache Page"
date: 2023-10-27T15:03:02+08:00
draft: false
---

Zip Cache Page
===

```go
func router() *http.ServeMux {
	mux := http.NewServeMux()
	fs := http.FileServer(http.FS(assets))
	mux.Handle("/assets/", http.StripPrefix("/", chain(fs, ZipHandler, CacheStatic)))
	mux.HandleFunc("/", homeHandler)
	mux.HandleFunc("/votenum", voteNumHandler)
	mux.HandleFunc("/api/config", sendConfig)
	mux.HandleFunc("/api/polls/new", newPollHandler)
	return mux
}

func ZipPage(d td) string {
	defer bb.Reset()
	tmpl.ExecuteTemplate(&bb, "Home", d)
	w := bytes.Buffer{}
	writer := gzip.NewWriter(&w)
	writer.Write(bb.Bytes())
	writer.Close()
	return w.String()
}

func ZipHandler(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		re, _ := regexp.Compile("[.](js|css|svg)$")
		if re.MatchString(r.URL.Path) {
			w.Header().Add("Content-Encoding", "gzip")
		}
		next.ServeHTTP(w, r)
	})
}

func CacheStatic(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		uri := r.URL.Path
		re, _ := regexp.Compile("[.](js|css|jpg|jpeg|png|json|map)$")
		if re.MatchString(uri) {
			match := r.Header.Get("If-None-Match")
			if len(match) != 0 {
				// if server not restart , check existed etag
				if strings.Contains(match, *ExpireTime) {
					w.WriteHeader(http.StatusNotModified)
					return // old etag
				} else {
					// server restart, set new etag
					w.Header().Set("Etag", *ExpireTime)
					next.ServeHTTP(w, r)
				}
			} else {
				// set etag and continue
				w.Header().Set("Etag", *ExpireTime)
				next.ServeHTTP(w, r)
			}
		} else {
			next.ServeHTTP(w, r)
		}
	})
}

func CachePage(w http.ResponseWriter, r *http.Request) {
	match := r.Header.Get("If-None-Match")
	if len(match) != 0 {
		// if server not restart , check existed etag
		if strings.Contains(match, *ExpireTime) {
			w.WriteHeader(http.StatusNotModified)
			return // old etag
		} else {
			// server restart, set new etag
			w.Header().Set("Etag", *ExpireTime)
		}
	} else {
		// set etag and continue
		w.Header().Set("Etag", *ExpireTime)
	}
}

func chain(f http.Handler, middlewares ...MiddleWare) http.Handler {
	for _, m := range middlewares {
		f = m(f)
	}
	return f
}
```