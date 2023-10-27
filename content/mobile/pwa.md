---
title: "Make Webpage Installed In Android"
date: 2023-10-27T15:15:30+08:00
draft: false
---

Make your web app installable in android
===

## 1. Make app.json file and link into your html file header

```json
{
  "lang":"zh-CN",
  "short_name": "App Name",
  "name": "Full App Name",
  "start_url": "/",
  "id": "/",
  "scope": "/",
  "display": "standalone",
  "theme_color": "#ffffff",
  "background_color":"#ffffff",
  "icons": [
    {
      "src": "/assets/static/logos/logo.png",
      "sizes": "48x48",
      "type": "image/png"
    },
    {
      "src": "/assets/static/logos/logo@2x.png",
      "sizes": "96x96",
      "type": "image/png"
    },
    {
      "src": "/assets/static/logos/logo@3x.png",
      "sizes": "144x144",
      "type": "image/png"
    },
    {
      "src": "/assets/static/logos/logo@4x.png",
      "sizes": "192x192",
      "type": "image/png"
    }

  ],

  "description": "App Description",
  "shortcuts" : [
    {
      "name": "Home",
      "url": "/",
      "description": "Page Description",
      "icons":[
        {
        "src": "/assets/static/logos/logo@2x.png",
        "sizes":"96x96",
        "type":"image/png"
      },
      {
        "src": "/assets/static/logos/logo@3x.png",
        "sizes":"144x144",
        "type":"image/png"
      },
      {
        "src": "/assets/static/logos/logo@4x.png",
        "sizes":"192x192",
        "type":"image/png"
      }
    ]
    }
  ]
}
```

## 2. Make a servicework js file called sw.js

```javascript

const addResourcesToCache = async (resources) => {
  const cache = await caches.open("v1");
  await cache.addAll(resources);
};

self.addEventListener("install", (event) => {
  addResourcesToCache([
    "/",
    "/home",
    "/assets/static/app.js",
    "/assets/static/app.js.map",
    "/assets/static/app.css",
    "/assets/static/logo.png",
  ])
});


let deferredPrompt;
self.addEventListener('beforeinstallprompt', (e) => {

  e.preventDefault();

  deferredPrompt = e;

  showInAppInstallPromotion();
});

self.addEventListener('fetch', { redirect: 'follow' }, function (event) {
  event.respondWith(
    caches.match(event.request).then(function (response) {
      return response || fetch(event.request);
    })
  );
});
```

## 3 . load sw.js file at the end of body tag 

```javascript
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register("/assets/static/sw.js", { "scope": "." }).then(function () { });
  }                                                                                                          
</script>
```