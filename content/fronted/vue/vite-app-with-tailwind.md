---
title: "Vite App With Tailwind"
date: 2021-04-20T08:27:20+08:00
draft: false
---

### Initialize a vitejs app

```bash
  yarn create @vitejs/app
  cd your app
  yarn
  yarn dev
```

### Install tailwindcss

```bash 
  yarn add -D @tailwindcss/jit tailwindcss@latest postcss@latest autoprefixer@latest postcss-cli@latest
  npx tailwindcss init -p
```

###modify postcss.config.js

```bash
  1 module.exports = {
  2   plugins: {
  3     '@tailwindcss/jit': {},
  4     autoprefixer: {},
  5   },
  6 }
```

### modify tailwindcss.config.js remove unused classes

```bash
  purge: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
```

### Include Tailwind in your css

create `./src/index.css` file with content:
```
@tailwind base;
@tailwind component;
@tailwind utilities;
```

### Run your app

```bash
yarn dev
```