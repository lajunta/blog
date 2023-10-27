---
title: "Tainwindcss Setup"
date: 2021-06-30T14:11:51+08:00
draft: false
categories: ["html"]
tags: ["html"]
---

# Tailwindcss Setup

## Init tailwindcss

```bash
# install tailwindcss
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest

# make default config file tailwind.config.js
npx tailwindcss init

```

## tailwind.config.js 

```js
module.exports = { 
  purge: ['./views/*.html', './src/app.scss'],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {}, 
  },  
  variants: {
    extend: {}, 
  },  
  plugins: [], 
}
```

## Include tailwindcss

```css
/* src/app.scss */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

