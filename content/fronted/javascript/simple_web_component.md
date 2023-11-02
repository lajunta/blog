---
title: "Simple_web_component"
date: 2023-11-02T11:34:51+08:00
draft: false
---

Simple Web Component
===

From [web components](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements)

Prepare two pictures alt.png and default.png

## Html part

```html
  <h2>hello</h2>

  <popup-info img="alt.png" data-text="Your card validation code (CVC)
  is an extra security feature — it is the last 3 or 4 numbers on the
  back of your card."></popup-info>

  <script src="hello.js"></script>
```

## JS part

```js
class PopUpInfo extends HTMLElement{
  constructor(){
    super()
    const shadow = this.attachShadow({mode: 'open'})
    const wrapper = document.createElement('span')
    wrapper.setAttribute('class','wrapper')
    const icon = document.createElement('span')
    icon.setAttribute('class','icon')
    icon.setAttribute('tabindex',0)

    const img = icon.appendChild(document.createElement('img'))
    img.src = this.hasAttribute('img') ? this.getAttribute('img') : 'default.png'
    const info = document.createElement('span')
    info.setAttribute('class','info')
    console.log(this.getAttribute("img"))
    info.textContent = this.getAttribute('data-text')
    const style = document.createElement('style')

    // set style for this web component
    style.textContent = `
    .wrapper {
      position: relative;
    }

    .info {
      font-size: 0.8rem;
      width: 200px;
      display: inline-block;
      border: 1px solid black;
      padding: 10px;
      background: white;
      border-radius: 10px;
      opacity: 0;
      transition: 0.6s all;
      position: absolute;
      bottom: 20px;
      left: 10px;
      z-index: 3;
    }

    img {
      width: 1.2rem;
    }

    .icon:hover + .info, .icon:focus + .info {
      opacity: 1;
    }
    `
    
    // attach the created elements to the shadow DOM
    shadow.appendChild(style)
    shadow.appendChild(wrapper)
    wrapper.appendChild(icon)
    wrapper.appendChild(info)
  }
}
customElements.define("popup-info",PopUpInfo)
```
