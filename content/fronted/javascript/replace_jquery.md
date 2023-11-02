---
title: "Replace Jquery With Vanilla Javascript"
date: 2023-11-02T18:30:21+08:00
draft: false
---

使用原生javascript取代jquery
===


## Selectors 


### Finding html by ID

```js
myElement = document.getElementById("id01");
```

### Finding html elements by TagName

return all p element

```js
myElements = document.getElementsByTagName("p");
```

### Finding html elements by class name

return all elements with class intro
```js
myElements = document.getElementsByClassName("intro");
```


### Finding html elements by css selectors

return a list of all p elements with class intro

```js
myElements = document.querySelectorAll("p.intro");
```


## Get Set content 

### Set text content

```js
myElement.textContent = "Hello CMS!";
```

### Get text content

```js
myText = document.getElementById("content").textContent;
```

### Set html content

```js
myElement.innerHTML = "<p>Hello World</p>";
```