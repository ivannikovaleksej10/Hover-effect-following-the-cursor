# Hover effect following the cursor

Underline link when hovering over a menu item

## html

```HTML
<nav>
    <a href="#">Features</a>
    <a href="#">PressKit</a>
    <a href="#">Download</a>
</nav>
```

## scss

```scss
body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #f8f8f8;
  font: normal 400 130%/1.5 -apple-system, BlinkMacSystemFont, Helvetica, Arial,
    sans-serif;
}

nav {
  display: grid;
  grid-auto-flow: column;
  grid-gap: 1em;
}

a {
  position: relative;
  font-weight: 600;
  text-decoration: none;
  color: rgba(0, 0, 0, 0.4);
  transition: color 0.3s ease;

  &::after {
    --scale: 0;

    content: "";
    position: absolute;
    left: 0;
    right: 0;
    top: 100%;
    height: 3px;
    background: rgb(76, 129, 201);
    transform: scaleX(var(--scale));
    transform-origin: var(--x) 50%;
    transition: transform 0.3s cubic-bezier(0.535, 0.05, 0.355, 1);
  }

  &:hover {
    color: rgb(76, 129, 201);
  }

  &:hover::after {
    --scale: 1;
  }
}
```

## JS

```js
document.querySelectorAll("a").forEach((elem) => {
  elem.onmouseenter = elem.onmouseleave = (e) => {
    const tolerance = 5;

    const left = 0;
    const right = elem.clientWidth;

    let x = e.pageX - elem.offsetLeft;

    if (x - tolerance < left) x = left;
    if (x + tolerance > right) x = right;

    elem.style.setProperty("--x", `${x}px`);
  };
});
```
